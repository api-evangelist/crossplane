# Crossplane (crossplane)

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
