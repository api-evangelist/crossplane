# Crossplane

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

**Areas:** Apache 2.0 · CNCF · Cloud-Native · COMPOSITION · Control Plane · Custom Resource Definitions · Graduated · Infrastructure as Code · Kubernetes · Multi-Cloud · Open Source · Platform Engineering

## Crossplane on APIs.io

Everything profiled for Crossplane is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/crossplane/](https://apis.io/providers/crossplane/)** — or go straight to one of the APIs or properties below.

### APIs (7)

- [Crossplane CompositeResourceDefinitions API](https://apis.io/apis/crossplane/crossplane-compositeresourcedefinitions-api/) — CompositeResourceDefinitions (XRDs) extend the Kubernetes API with new custom resource types. An XRD defines the schema and API surface for a composite…
- [Crossplane Compositions API](https://apis.io/apis/crossplane/crossplane-compositions-api/) — Compositions define how to compose a set of managed resources or Composition Functions into a higher-level composite resource. A Composition acts as a…
- [Crossplane Configurations API](https://apis.io/apis/crossplane/crossplane-configurations-api/) — Configurations are Crossplane packages that bundle Compositions and CompositeResourceDefinitions together into a distributable unit that can be installed…
- [Crossplane DeploymentRuntimeConfigs API](https://apis.io/apis/crossplane/crossplane-deploymentruntimeconfigs-api/) — DeploymentRuntimeConfigs customize the runtime behavior of Provider and Function deployments, including replica counts, resource limits, service account…
- [Crossplane EnvironmentConfigs API](https://apis.io/apis/crossplane/crossplane-environmentconfigs-api/) — EnvironmentConfigs provide shared configuration data that can be referenced by Compositions via environment patches, enabling reusable configuration across…
- [Crossplane Functions API](https://apis.io/apis/crossplane/crossplane-functions-api/) — Functions are Crossplane packages that contain Composition Functions, which are OCI container images invoked during composition to perform advanced resource…
- [Crossplane Providers API](https://apis.io/apis/crossplane/crossplane-providers-api/) — Providers are Crossplane packages that install controllers and CRDs for managing resources on a specific infrastructure platform such as AWS, GCP, or Azure.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Crossplane Agentic Access](https://apis.io/agentic-access/crossplane/crossplane-agentic-access/)

#### JSON Schema (3)

The data models the API reads and writes.

- [Crossplane Composition](https://apis.io/schemas/crossplane/crossplane-composition/)
- [Crossplane Provider Configuration](https://apis.io/schemas/crossplane/crossplane-provider/)
- [Crossplane CompositeResourceDefinition (XRD)](https://apis.io/schemas/crossplane/crossplane-xrd/)

#### JSON-LD (1)

Linked-data contexts for the provider's vocabulary.

- [Crossplane Context](https://apis.io/jsonld/crossplane/crossplane-context/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Crossplane Vocabulary](https://apis.io/vocabularies/crossplane/crossplane-vocabulary/)

#### Collections (15)

Postman and Open Collection request collections.

- [Crossplane Kubernetes CompositeResourceDefinitions API](https://apis.io/collections/crossplane/open-crossplane-compositeresourcedefinitions-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Compositions API](https://apis.io/collections/crossplane/open-crossplane-compositions-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Configurations API](https://apis.io/collections/crossplane/open-crossplane-configurations-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions DeploymentRuntimeConfigs API](https://apis.io/collections/crossplane/open-crossplane-deploymentruntimeconfigs-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions EnvironmentConfigs API](https://apis.io/collections/crossplane/open-crossplane-environmentconfigs-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Functions API](https://apis.io/collections/crossplane/open-crossplane-functions-api/)
- [Crossplane Kubernetes API](https://apis.io/collections/crossplane/open-crossplane-kubernetes-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Providers API](https://apis.io/collections/crossplane/open-crossplane-providers-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions API](https://apis.io/collections/crossplane/postman-crossplane-compositeresourcedefinitions-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Compositions API](https://apis.io/collections/crossplane/postman-crossplane-compositions-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Configurations API](https://apis.io/collections/crossplane/postman-crossplane-configurations-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions DeploymentRuntimeConfigs API](https://apis.io/collections/crossplane/postman-crossplane-deploymentruntimeconfigs-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions EnvironmentConfigs API](https://apis.io/collections/crossplane/postman-crossplane-environmentconfigs-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Functions API](https://apis.io/collections/crossplane/postman-crossplane-functions-api/)
- [Crossplane Kubernetes CompositeResourceDefinitions Providers API](https://apis.io/collections/crossplane/postman-crossplane-providers-api/)

#### Governance rules (2)

Spectral rulesets for the provider's contracts.

- [Crossplane — jsonschema rules](https://apis.io/rules/crossplane/crossplane-jsonschema-spectral-rules/)
- [Crossplane — kubernetes api rules](https://apis.io/rules/crossplane/crossplane-kubernetes-api-rules/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Crossplane Authentication](https://apis.io/security/crossplane/crossplane-authentication/)
- [Crossplane Domain Security](https://apis.io/security/crossplane/crossplane-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Crossplane Plans Pricing](https://apis.io/plans/crossplane/crossplane-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Crossplane Rate Limits](https://apis.io/rate-limits/crossplane/crossplane-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Crossplane Finops](https://apis.io/finops/crossplane/crossplane-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.crossplane.io/)
- [Documentation](https://docs.crossplane.io/latest/)
- [Getting started](https://docs.crossplane.io/latest/get-started/get-started-with-composition/)
- [Changelog](https://github.com/crossplane/crossplane/releases)
- [Blog](https://blog.crossplane.io/)
- [GitHub](https://github.com/crossplane)

## API Evangelist rating

**Kin Score 45.8** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 66.1 |
| Contract quality | 66.7 |
| Contract governance | 27.3 |
| Operational transparency | 36.8 |
| Developer ergonomics | 36.9 |
| Access clarity | 7.9 |

**Agent readiness 22.4** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | — |
| OpenAPI Examples | — |
| Rate Limit Signal | derived (partial credit) |
| Event Surface Described | — |
| Agent Skills | — |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 16.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/crossplane/](https://apis.io/providers/crossplane/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Crossplane: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/crossplane/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
