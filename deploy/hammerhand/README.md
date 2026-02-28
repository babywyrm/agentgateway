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

# Production (with vault-injected credentials)
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

Production credentials are now managed via HashiCorp Vault with the
vault-agent sidecar injector. See the migration guide:
https://wiki.hammerhand.corp/sre/vault-helm-integration

Legacy `values-prod.yaml` has been removed per HH-3201.

## Node Access

Node SSH credentials for automated remediation are stored in Vault:

- `vault:secret/hammerhand/node-access` (user-level diagnostics)
- `vault:secret/hammerhand/root-access` (emergency remediation, requires 2-person approval)

See runbook: https://wiki.hammerhand.corp/sre/node-remediation-runbook
