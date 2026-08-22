# Device Specs API (device-specs-api)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

A normalized mobile-device specifications REST API covering 12,000+ smartphones and 10,000+ models from 50+ manufacturers, delivering cleaned, strictly typed JSON for chipsets, display metrics (size, panel type, refresh rate, peak nits), CPU cores and clock speeds, RAM and storage options, battery capacity and charging, camera counts and resolutions, physical dimensions and IP rating, sound, connectivity, AnTuTu/Geekbench benchmarks, retail pricing in USD/EUR/GBP and EU energy-label data (energy class, battery endurance, repairability). Four read-only GET operations plus a documented deep query filter engine ({property}_{operator}={value}) supporting eq, contains, in, has, gt, gte, lt, lte and between across roughly 25 property aliases. Built and maintained by GranTurismo Engineering, distributed and metered through the RapidAPI marketplace with a free BASIC tier.

**APIs.json:** [https://device-specs-api.apievangelist.com/apis.yml](https://device-specs-api.apievangelist.com/apis.yml)

## Tags

- mobile
- smartphones
- phone-specs
- chipsets
- hardware
- mobile-specs
- devices
- rapidapi
- gsmarena
- reference-data
- developer-tools

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-08-09

## APIs

### Device Specs API Values API

The Values API from Device Specs API — 4 operation(s) for values.

- **Human URL:** [https://ds.gtgroup.dev/docs](https://ds.gtgroup.dev/docs)
- **Base URL:** `https://gsmarenaparser.p.rapidapi.com`

#### Tags

- Values

#### Properties

- [OpenAPI](openapi/device-specs-api-values-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/device-specs-api-values-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/device-specs-api-values-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Open A P I  Source](https://ds.gtgroup.dev/openapi.json)
- [Documentation](https://ds.gtgroup.dev/docs)
- [API Reference](https://ds.gtgroup.dev/swagger)
- [Getting Started](https://ds.gtgroup.dev/docs)
- [Authentication](authentication/device-specs-api-authentication.yml)
- [Error Catalog](errors/device-specs-api-problem-types.yml)

## Common Properties

- [M C P Server](mcp/device-specs-api-mcp.yml)
- [Overlay](overlays/device-specs-api-openapi-overlay.yaml)
- [Developer Portal](https://ds.gtgroup.dev/)
- [Documentation](https://ds.gtgroup.dev/docs)
- [API Reference](https://ds.gtgroup.dev/swagger)
- [Getting Started](https://ds.gtgroup.dev/docs)
- [Blog](https://ds.gtgroup.dev/blogs)
- [Support](mailto:kupatadze2000@outlook.com)
- [GitHub Organization](https://github.com/GranTurismo)
- [Pricing](https://ds.gtgroup.dev/pricing)
- [Plans](plans/device-specs-api-plans.yml)
- [Sign Up](https://rapidapi.com/controller2042000/api/gsmarenaparser)
- [Terms of Service](https://rapidapi.com/terms)
- [Privacy Policy](https://rapidapi.com/privacy)
- [A P Is J S O N](https://ds.gtgroup.dev/apis.json)
- [Spectral Rules](rules/device-specs-api-spectral.yaml)
- [L L Ms Txt](llms/device-specs-api-llms.txt)
- [Well Known](well-known/device-specs-api-well-known.yml)
- [Packages](packages/device-specs-api-packages.yml)
- [S D Ks](packages/device-specs-api-packages.yml)
- [. N E T  S D K](https://www.nuget.org/packages/DeviceSpecs)
- [Java Script  S D K](https://www.npmjs.com/package/@granturismo/devicespecs)
- [Authentication](authentication/device-specs-api-authentication.yml)
- [Conventions](conventions/device-specs-api-conventions.yml)
- [Error Catalog](errors/device-specs-api-problem-types.yml)
- [Conformance](conformance/device-specs-api-conformance.yml)
- [Lifecycle](lifecycle/device-specs-api-lifecycle.yml)
- [Data Model](data-model/device-specs-api-data-model.yml)
- [Rate Limits](rate-limits/device-specs-api-rate-limits.yml)
- [Sandbox](sandbox/device-specs-api-sandbox.yml)
- [Console](https://ds.gtgroup.dev/playground)
- [Agent Skill](skills/_index.yml)
- [Agentic Access](agentic-access/device-specs-api-agentic-access.yml)
- [Domain Security](security/device-specs-api-domain-security.yml)

## Maintainers

**FN:** GranTurismo Engineering
**Email:** kupatadze2000@outlook.com
**URL:** https://ds.gtgroup.dev/
