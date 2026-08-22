# Crossplane (crossplane)

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

Crossplane is a graduated CNCF open-source Kubernetes add-on that transforms a cluster into a universal control plane for cloud infrastructure, services, and applications. Crossplane introduces custom resources including CompositeResourceDefinitions (XRDs), Compositions, Claims, Providers, ProviderConfigs, Configurations, Functions, and EnvironmentConfigs, allowing platform teams to author self-service platform APIs that compose managed resources across AWS, GCP, Azure, and other providers using Kubernetes-style declarative configuration.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/crossplane/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/crossplane/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Provider
- **Access:** Public

## Tags

- Apache 2.0
- CNCF
- Cloud Native
- Composition
- Control Plane
- Custom Resource Definitions
- Graduated
- Infrastructure as Code
- Kubernetes
- Multi-Cloud
- Open Source
- Platform Engineering
- Providers

## Timestamps

- **Created:** 2025-01-01
- **Modified:** 2026-05-19

## APIs

### Crossplane Kubernetes API

The Crossplane Kubernetes API extends the Kubernetes API server with custom resources for managing cloud infrastructure declaratively. Resources are organized into two main API groups: apiextensions.crossplane.io for composition primitives (Compositions, CompositeResourceDefinitions, EnvironmentConfigs, DeploymentRuntimeConfigs) and pkg.crossplane.io for package management (Providers, Functions, Configurations and their revisions). All operations use standard Kubernetes REST conventions and are authenticated through the Kubernetes API server's authentication mechanisms.

- **Human URL:** [https://docs.crossplane.io/latest/api/](https://docs.crossplane.io/latest/api/)
- **Base URL:** `https://kubernetes.default.svc`

#### Tags

- Composition
- Control Plane
- Custom Resources
- Infrastructure as Code
- Kubernetes
- Multi-Cloud
- Platform Engineering

#### Properties

- [Documentation](https://docs.crossplane.io/latest/)
- [Reference](https://docs.crossplane.io/latest/api/)
- [Getting Started](https://docs.crossplane.io/latest/get-started/get-started-with-composition/)
- [OpenAPI](openapi/crossplane-kubernetes-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/crossplane-kubernetes-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/crossplane-kubernetes-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Rules](rules/crossplane-kubernetes-api-rules.yml)
- [Capabilities](capabilities/crossplane-kubernetes-api-capabilities.yml)
- [JSON Schema](json-schema/crossplane-composition-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/crossplane-xrd-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/crossplane-provider-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/crossplane-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Changelog](https://github.com/crossplane/crossplane/releases)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/crossplane)
- [JSON Schema](json-schema/crossplane-composition-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/crossplane-xrd-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/crossplane-provider-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON-LD](json-ld/crossplane-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](vocabulary/crossplane-vocabulary.yml)
- [Website](https://www.crossplane.io/)
- [Documentation](https://docs.crossplane.io/latest/)
- [Getting Started](https://docs.crossplane.io/latest/get-started/get-started-with-composition/)
- [Reference](https://docs.crossplane.io/latest/api/)
- [Blog](https://blog.crossplane.io/)
- [GitHub Organization](https://github.com/crossplane)
- [GitHub Repository](https://github.com/crossplane/crossplane)
- [Changelog](https://github.com/crossplane/crossplane/releases)
- [Community](https://docs.crossplane.io/latest/learn/)
- [Contributing](https://docs.crossplane.io/contribute/contribute/)
- [License](https://github.com/crossplane/crossplane/blob/main/LICENSE)
- [C N C F](https://www.cncf.io/projects/crossplane/)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
