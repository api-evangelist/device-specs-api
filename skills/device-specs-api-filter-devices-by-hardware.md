---
name: Find devices matching hardware criteria with the deep filter engine
description: Translate a natural-language hardware requirement ("5000mAh Snapdragon phones with 120Hz and NFC under $800") into Device Specs API deep-filter query parameters on the list operation.
api: openapi/device-specs-api-openapi-original.json
operations:
  - "GET /api/values/clean/devices"
generated: '2026-08-09'
method: generated
---

# Find devices matching hardware criteria

Use this when the request is a set of constraints rather than a named device.

## The one operation

`GET /api/values/clean/devices` (proposed operationId `listDevices`). Send the two auth headers
(`x-rapidapi-key`, `x-rapidapi-host`) as in every other call.

## The filter grammar

Every filter is one query parameter of the form:

```
{property}_{operator}={value}
```

Omit the operator for equality. Commas delimit list and range values.

| Operator | Applies to | Example |
|---|---|---|
| *(none)* / `eq` | string, numeric, boolean | `manufacturer=Samsung` |
| `contains` | string, list of strings | `chipset_contains=Snapdragon` |
| `in` | string, numeric, list | `manufacturer_in=Apple,Samsung` |
| `has` | boolean | `nfc_has=true` |
| `gt` / `gte` | numeric | `battery_gte=5000` |
| `lt` / `lte` | numeric | `price_lte=800` |
| `between` | numeric | `ram_between=8,12` |

Property aliases resolve to nested `normalized_specs` paths so you never spell a JSON path:

- Root and pricing — `id`, `manufacturer`, `model`, `chipset`, `price` / `price_usd`
- Display — `displaysize`, `panel_type`, `refreshrate`, `brightness`
- Memory and power — `ram`, `storage`, `battery`, `charging`, `wireless_charging`
- Hardware and sound — `nfc`, `water_resistant`, `jack_35mm`, `stereo_speakers`

## Steps

1. **Decompose the ask into (property, operator, value) triples.** "At least 8GB but no more than
   16GB of RAM" is `ram_between=8,16`, not two parameters.
2. **Compose one request.** Filters AND together:

   ```
   GET /api/values/clean/devices?chipset_contains=Snapdragon&battery_gte=5000&ram_between=8,16
   GET /api/values/clean/devices?manufacturer_in=Samsung,Xiaomi,Oppo&nfc_has=true&refreshrate_gte=120
   ```

3. **Never fan out into one request per candidate device.** The deep filter runs server-side; issuing
   N lookups instead of one filtered list will burn a whole day's free-tier quota (15 requests).
4. **Read results from `normalized_specs`,** not from the `_raw` strings — the raw fields are exactly
   the unparsed text this API exists to normalize away.

## Rules

- Only `battery_gte`, `chipset_contains` and `ram_between` are declared in the published OpenAPI; the
  rest of the grammar is documented at <https://ds.gtgroup.dev/docs> only. A spec-driven client will
  not know about them — build the query string yourself.
- A malformed filter returns **400**, not an empty list. If you get a 400, the operator or the
  comma-delimited value shape is wrong, not the data.
- There is no total count, no next-page link and no cursor in the response. `limit` / `offset` are
  documented for the manufacturer listing, not for this operation.
- Filters are AND-only. There is no OR across different properties and no negation; use `in` for
  multi-value matching on a single property.
