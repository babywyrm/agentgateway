# Hammerhand Gateway Deployment

Production deployment overlays for the Hammerhand Corp AI-Ops agent gateway.

## Prerequisites

- `helm` v3.12+
- Access to `oci://registry.hammerhand.corp/charts` (VPN required)
- `kubectl` configured for the target cluster
- Namespace `hammerhand` exists

## Quick Start

```bash
# Dev/staging (default values only)
make deploy

# Production (with node management overrides)
make deploy-prod
```

## Chart Source

The gateway chart is published to our internal OCI registry:

```
oci://registry.hammerhand.corp/charts/agentgateway
```

Chart source is maintained internally. See the SRE wiki for development:
https://wiki.hammerhand.corp/sre/agentgateway-chart

## Production Values

Production overrides are managed via `values-prod.yaml`. This file contains
environment-specific configuration for node management and access credentials.

**Security**: Ensure production values are never committed with plaintext
credentials. Use `helm-secrets` or Vault injection for sensitive fields.
