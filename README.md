# Allo-Media

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

Allo-Media, which now trades as **uh!ive**, is a French conversational-voice-AI company that
transcribes and analyses telephone conversations in real time and in batch — speech-to-text tuned for
8kHz telephony, named entity recognition and redaction, speech analytics, and call tracking.

`www.allo-media.net` now 301s to `https://uh.live/en/`, and every runtime API host has moved to the
`uh.live` domain, but the developer documentation still lives at
[docs.allo-media.net](https://docs.allo-media.net/) under the old brand.

## API surface

| API | Base | Docs |
|---|---|---|
| Activate API (REST, read-only over processed calls) | `https://activate.uh.live` | [docs](https://docs.allo-media.net/activate-api/rest/) |
| Stream API for humans (WebSocket, real-time transcription) | `wss://api.uh.live/socket/websocket` | [docs](https://docs.allo-media.net/stream-h2h/) |
| Stream API for voicebots (MRCP / WebSocket) | `https://api.uh.live` | [docs](https://docs.allo-media.net/stream-h2b/) |
| Hermes (browser call-tracking script) | `https://hermes.allo-media.net` | [docs](https://docs.allo-media.net/hermes/) |

Plus JUpload (SFTP batch ingestion) and an HMAC-SHA256-signed webhook. Authentication is OAuth 2.0
`client_credentials` against a Keycloak realm; credentials come from an account manager, not
self-service.

## What this profile found

- **No OpenAPI, AsyncAPI, GraphQL, MCP server or A2A agent card.** `/.well-known/agent-card.json` and
  `/.well-known/agent.json` return 404 on every host. The docs link a Swagger UI for the pre-v3 API at
  `api.allo-media.net/swagger`, but that host refused every probe.
- **The only machine-readable contract the company serves is its identity layer** — a full Keycloak
  OIDC discovery document, captured verbatim in `well-known/`. It exposes a per-product scope model
  (`activate`, `stream-h2h`, `stream-h2h-v2`, `stream-h2b`, `scribr`, and an undocumented
  `voip-callapi`) that the developer documentation never mentions, plus mTLS-bound access tokens, DPoP
  and dynamic client registration.
- A valid RFC 9116 `security.txt`, a public dated product roadmap, a public status page, eight separate
  release-note streams, and two official SDKs (`uhlive` on PyPI, `@uhlive/javascript-sdk` on npm).
- No published pricing or plans; enterprise sales-led, with self-service API onboarding sitting on the
  company's own public roadmap under "Later".

Source: portfolio company of [serena](https://github.com/api-evangelist/serena) — https://uh.live/en/
