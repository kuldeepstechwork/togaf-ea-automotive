# Technology Standards

## Purpose

This catalogue defines the approved technology stack for the modernization program, binding under Principle 8 (Cloud-Native by Default) and Principle 9 (Interoperate Through Standards). It is maintained by the Director, Cloud Platform Engineering, and ratified by the ARB. Standards here are deliberately expressed as capability categories with approved options rather than a single mandated product per category, to preserve flexibility for Phase E vendor evaluation while still bounding architectural sprawl.

## Approved Stack by Category

| Category | Approved Standard(s) | Notes |
|---|---|---|
| Cloud Platform | Single primary public cloud provider (selected in Phase E), multi-region within that provider | On-premises is exception-only per Principle 8 |
| Event Streaming Platform | Managed, partitioned, durable log-based streaming service (cloud-provider-managed preferred over self-hosted) | Selected specifically to support the reference architecture's replay requirement |
| API Gateway | Cloud-managed API gateway with OpenAPI 3.x contract enforcement | All dealer/supplier-facing APIs must publish an OpenAPI spec |
| Container Orchestration | Managed Kubernetes service | Self-managed control planes not approved except for the legacy DMS during transition |
| Data Storage — Transactional | Managed relational database service (per-domain instances, no shared schemas across domains) | Aligned to Principle 2 |
| Data Storage — Analytics | Cloud-managed data warehouse/lakehouse | Serves Phase C analytics consumers; not a system of record |
| Identity & Access | Centralized identity provider with OAuth 2.0 / OIDC; SAML retained only for legacy dealer SSO during transition | CISO-mandated; no service-specific credential stores |
| Observability | Unified logging, metrics, and distributed tracing stack, standardized across all services | Mandatory for every new service prior to production cutover |
| Infrastructure as Code | Declarative IaC tooling, version-controlled, applied via CI/CD pipeline | Manual infrastructure changes in production are prohibited outside declared emergency change process |
| Secrets Management | Centralized managed secrets store; no secrets in source control or environment files checked into version control | Zero-tolerance standard, enforced by pipeline scanning |
| Messaging Contracts | Schema registry with enforced backward-compatibility rules (see [reference-architecture.md](./reference-architecture.md)) | Applies to all event backbone producers |
| EDI (Legacy Compatibility) | Retained for the ~15% of suppliers unable to consume modern APIs, via the EDI translation layer only | Explicit sunset review at 18 and 30 months into the program |

## Exceptions Process

A technology exception is any proposed use of a technology, pattern, or vendor not on this catalogue, or use of an on-premises deployment for a new workload. Exceptions are handled as follows:

1. **Request submission** — the requesting team submits a short exception request to the Director, Cloud Platform Engineering, including the business or technical justification, the specific standard being deviated from, and the proposed alternative.
2. **Technical review** — Cloud Platform Engineering reviews for technical feasibility and operational supportability within 5 business days.
3. **ARB ratification** — any exception with cost, security, or cross-domain impact is escalated to the ARB for ratification at its next standing session (see [governance-framework-setup.md](../00-preliminary/governance-framework-setup.md)); low-impact exceptions (e.g., a temporary tooling choice scoped to a single team's internal development environment) may be approved directly by the Director without full ARB review.
4. **Time-bound approval** — every exception is granted for a maximum of 12 months and must be re-justified or resolved into standard compliance at expiry, tracked in the same architecture decision log used for principle waivers.

## Known Current Exceptions

| Exception | Reason | Expiry |
|---|---|---|
| On-premises DMS core (legacy) remains during transition | Cannot cut over all 600 dealers simultaneously; retained until final migration wave completes | End of Phase F, Wave 6 |
| SAML-based dealer SSO for legacy DMS modules | Legacy DMS does not support OIDC; replacing SSO independently of DMS replacement was assessed as not worth the standalone effort | Same as DMS retirement |
| Self-hosted EDI VAN connectivity | Required for continued support of the ~15% EDI-only supplier segment | 30-month program checkpoint review |

*Fictional case study — see [README](../README.md) for full disclaimer.*
