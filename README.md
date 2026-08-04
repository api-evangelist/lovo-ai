# LOVO AI (lovo-ai)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

LOVO AI is an AI text-to-speech and voice generation platform. Its flagship product, Genny, turns text into natural-sounding speech across a large library of speakers, locales, and speaker styles, and adds AI voice cloning and voiceover tooling. The **Genny API** is a REST API (base `https://api.genny.lovo.ai`) authenticated with an `X-API-KEY` header carrying a key generated in the Genny app at [https://genny.lovo.ai](https://genny.lovo.ai). It exposes synchronous and asynchronous text-to-speech conversions, a speakers/voices catalog with styles, per-conversion pronunciation/pause/emphasis controls, and a team billing/usage endpoint.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/lovo-ai/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/lovo-ai/refs/heads/main/apis.yml)

## Access Model

- **Authentication:** `X-API-KEY` header. Generate an API key in the Genny app (profile tab) at [https://genny.lovo.ai](https://genny.lovo.ai).
- **Subscription required:** API access requires an active LOVO AI subscription. Keys without one receive a `402 No active subscription`. TTS credits are deducted from the account associated with the API key.
- **Rate limit:** 20 requests per minute.
- **Input limit:** Up to 500 characters of text per TTS conversion.
- **Audio URLs:** Generated audio URLs are valid for 24 hours; download the result for further use.
- **Async model:** Long-running TTS uses a job model - submit a job, then poll `GET /api/v1/tts/{jobId}` or register up to 4 `callbackUrls` that receive a single HTTP POST webhook on completion. There is **no** public WebSocket API.

## Tags

- AI
- Text to Speech
- TTS
- Voice Generation
- Voice Cloning
- Speech Synthesis
- Voiceover

## Timestamps

- **Created:** 2026-07-11
- **Modified:** 2026-07-11

## APIs

### LOVO AI Text-to-Speech API

Convert text into natural-sounding speech. Submit an asynchronous job (`POST /tts`) and poll or receive a callback, or run a synchronous conversion (`POST /tts/sync`) with a 90-second timeout, then retrieve results and audio URLs by job id (`GET /tts/{jobId}`). Requests take `text` (up to 500 chars), a `speaker` id, an optional `speakerStyle`, and `speed`.

- **Human URL:** [https://docs.genny.lovo.ai/reference/async-tts](https://docs.genny.lovo.ai/reference/async-tts)
- **Base URL:** `https://api.genny.lovo.ai/api/v1`

#### Tags

- Text to Speech
- Conversions
- TTS

#### Properties

- [Documentation](https://docs.genny.lovo.ai/reference/intro/getting-started)
- [API Reference](https://docs.genny.lovo.ai/reference/async-tts)
- [OpenAPI](openapi/lovo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/lovo-ai.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/lovo-ai.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LOVO AI Speakers API

Browse the Genny voice catalog. Retrieve speakers (`GET /speakers`) with pagination and sorting by displayName, locale, gender, speakerType, and ageRange. Each speaker exposes its id, locale, gender, avatar, age range, and available speaker styles with sample audio URLs - the speaker ids used when requesting a TTS conversion.

- **Human URL:** [https://docs.genny.lovo.ai/reference/retrieve-speakers](https://docs.genny.lovo.ai/reference/retrieve-speakers)
- **Base URL:** `https://api.genny.lovo.ai/api/v1`

#### Tags

- Speakers
- Voices
- Catalog

#### Properties

- [API Reference](https://docs.genny.lovo.ai/reference/retrieve-speakers)
- [OpenAPI](openapi/lovo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/lovo-ai.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/lovo-ai.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LOVO AI Pronunciation and Prosody

Pronunciation, pause, and emphasis controls applied to a TTS conversion. These are modeled honestly as data structures on the TTS output (word-level pronunciation replacements, timed pauses of 0-2 seconds, and emphasis markers), not as a standalone endpoint - they are carried within the text-to-speech job payload rather than a dedicated `/pronunciations` resource.

- **Human URL:** [https://docs.genny.lovo.ai/reference/sync-tts](https://docs.genny.lovo.ai/reference/sync-tts)
- **Base URL:** `https://api.genny.lovo.ai/api/v1`

#### Tags

- Pronunciation
- Pause
- Emphasis

#### Properties

- [Documentation](https://docs.genny.lovo.ai/reference/sync-tts)
- [OpenAPI](openapi/lovo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### LOVO AI Teams and Billing API

Read team billing and usage information for the account tied to the API key (`GET /teams/status`). Returns the team name, subscription status and billing interval, current period start/end, and metered usage entries - useful for tracking API credit consumption.

- **Human URL:** [https://docs.genny.lovo.ai/reference/intro/getting-started](https://docs.genny.lovo.ai/reference/intro/getting-started)
- **Base URL:** `https://api.genny.lovo.ai/api/v1`

#### Tags

- Billing
- Usage
- Teams

#### Properties

- [Documentation](https://docs.genny.lovo.ai/reference/intro/getting-started)
- [OpenAPI](openapi/lovo-ai-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/lovo-ai)
- [Website](https://lovo.ai)
- [Documentation](https://docs.genny.lovo.ai)
- [Plans](plans/lovo-ai-plans-pricing.yml)
- [Rate Limits](rate-limits/lovo-ai-rate-limits.yml)
- [Fin Ops](finops/lovo-ai-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
