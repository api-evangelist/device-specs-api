---
name: Compare every device on one chipset
description: Pull the cohort of devices sharing a System-on-Chip and assemble a comparison table from the normalized metrics, without exhausting the request quota.
api: openapi/device-specs-api-openapi-original.json
operations:
  - "GET /api/values/clean/devicesbychipset/{chipset}"
  - "GET /api/values/clean/getspecs/{manufacturer}/{model}"
generated: '2026-08-09'
method: generated
---

# Compare every device on one chipset

Use this for "which phones run the Snapdragon 8 Gen 3, and how do they differ?" — the shape behind
comparison engines, buying guides and silicon-adoption analysis.

## Steps

1. **Pull the cohort in one call.**
   `GET /api/values/clean/devicesbychipset/{chipset}` (proposed operationId `getDevicesByChipset`).
   The path segment is the URL-friendly chipset name — the docs use hyphenated forms:

   ```
   GET https://gsmarenaparser.p.rapidapi.com/api/values/clean/devicesbychipset/Snapdragon-8-Gen-3
   GET https://gsmarenaparser.p.rapidapi.com/api/values/clean/devicesbychipset/Tensor-G4
   GET https://gsmarenaparser.p.rapidapi.com/api/values/clean/devicesbychipset/A18-Pro
   ```

   The response is an array of full `DeviceSpecsResponse` objects — the same shape the single-device
   lookup returns. **You already have every field you need. Do not loop the cohort through
   `getspecs`.**

2. **If the chipset name does not resolve,** fall back to the filter engine, which does substring
   matching instead of exact path matching:

   ```
   GET /api/values/clean/devices?chipset_contains=Snapdragon%208%20Gen%203
   ```

3. **Build the comparison from `normalized_specs`.** Useful axes that are already typed:
   `display.refresh_rate_hz`, `display.peak_brightness_nits`, `memory_options.available_ram_gb[]`,
   `battery_and_charging.capacities_mah[]`, `battery_and_charging.max_wired_charging_w`,
   `physical.weight_g`, `benchmarks.antutu_score`, `benchmarks.geekbench_score`, `price_usd`.

4. **Only call `getspecs` for a device the cohort call did not return** — e.g. a specific variant
   named by the user. That is
   `GET /api/values/clean/getspecs/{manufacturer}/{model}` (proposed operationId `getDeviceSpecs`).

## Rules

- **`benchmarks.antutu_score` and `geekbench_score` are strings, not numbers** (`"1150000 (v10)"`,
  `"1950 (single-core), 4700 (multi-core)"`). Parse them before sorting, and say so if you present a
  ranking — the provider does not give you a comparable numeric.
- **`chipset` on the device record is free text** (`"Google Tensor G4 (4 nm)"`). There is no chipset
  entity, no chipset list operation and no chipset id. Two devices on the same silicon can carry
  differently-worded chipset strings.
- **One cohort call, not N device calls.** The free BASIC tier allows 15 requests per day at 20 per
  minute; a 30-device cohort fetched one device at a time exceeds two days of quota and will start
  returning `429 {"message":"Too many requests"}`.
- Cache the cohort. The provider claims data changes only when a device is announced.
