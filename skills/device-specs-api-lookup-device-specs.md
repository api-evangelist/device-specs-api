---
name: Look up the full specification for one phone
description: Resolve a manufacturer + model into the complete Device Specs API record, including the parsed normalized_specs subtree, and recover cleanly when the model name does not match.
api: openapi/device-specs-api-openapi-original.json
operations:
  - "GET /api/values/clean/getspecs/{manufacturer}/{model}"
  - "GET /api/values/clean/getdevices/{manufacturer}"
generated: '2026-08-09'
method: generated
---

# Look up the full specification for one phone

Use this when you have a device name in hand ("Pixel 9 Pro", "Galaxy S24 Ultra") and need its
hardware facts as typed values rather than marketing prose.

## Authentication

Every request needs two headers. There is no OAuth, no bearer token and no scope model.

```
x-rapidapi-key:  <your RapidAPI subscription key>
x-rapidapi-host: <the gateway host you are calling>
```

The gateway host that answers on probe is `gsmarenaparser.p.rapidapi.com`. The provider's docs name
`deviceultraparser.p.rapidapi.com`; that host currently returns `{"message":"API doesn't exists"}`.
If one host 404s, try the other before concluding the device is missing — see
`conventions/device-specs-api-conventions.yml`.

## Steps

1. **Fetch the device.**
   `GET /api/values/clean/getspecs/{manufacturer}/{model}`
   (proposed operationId `getDeviceSpecs`). Both path segments are URL-encoded free text and are
   matched case-insensitively. Spaces are legal once encoded — `Pixel%209%20Pro`.

   ```
   GET https://gsmarenaparser.p.rapidapi.com/api/values/clean/getspecs/Google/Pixel%209%20Pro
   ```

2. **Read the typed values, not the raw strings.** The response carries both. Fields suffixed
   `_raw` (`battery_raw`, `cpu_raw`, `displayType_raw`, `internal_raw`, `charging_raw`) are the
   unparsed source strings — do not regex them. Use `normalized_specs` instead:

   | You want | Read |
   |---|---|
   | Screen size / refresh rate / peak nits | `normalized_specs.display.size_inches`, `.refresh_rate_hz`, `.peak_brightness_nits` |
   | Core count and peak clock | `normalized_specs.processor.total_cores`, `.max_clock_speed_ghz` |
   | RAM and storage options | `normalized_specs.memory_options.available_ram_gb[]`, `.available_storage_gb[]` |
   | Battery and charging | `normalized_specs.battery_and_charging.capacities_mah[]`, `.max_wired_charging_w`, `.has_wireless_charging` |
   | Weight, dimensions, IP rating | `normalized_specs.physical.*` |
   | EU energy label | `normalized_specs.eu_label.energy_class`, `.repairability_class` |

   `available_ram_gb` and `available_storage_gb` are **arrays** — a device has variants. `variants[]`
   carries the regional model numbers.

3. **On 404, do not guess a new spelling.** A 404 means the brand or model was not matched. Call
   `GET /api/values/clean/getdevices/{manufacturer}` (proposed operationId
   `getDevicesByManufacturer`) to list every tracked device for that brand, then pick the exact
   `model` string from that list and retry step 1 with it.

## Rules

- **Read-only.** All four operations are `GET`. There is nothing to create, update or retry unsafely,
  and the provider publishes no idempotency contract because it needs none.
- **Errors carry no schema.** Failures return `{"message": "..."}` with no type URI and no error code
  — this API is not RFC 9457. Branch on the HTTP status: `400` bad filter syntax, `401` missing or
  invalid key, `404` device not found, `429` tier rate limit exceeded. See
  `errors/device-specs-api-problem-types.yml`.
- **Budget your calls.** The free BASIC tier is **15 requests per day** at 20/min. Cache device
  records — the provider states data changes only when a device is announced (claimed 24-hour
  freshness). Do not poll.
- **No pagination on this operation.** `getspecs` returns one object. `getdevices` accepts `limit`
  (default 50, max 500) and `offset` per the provider's llms.txt, though neither parameter appears in
  the published OpenAPI.
