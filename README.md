# helm-charts

A collection of reusable Helm charts for Kubernetes deployments.

## Usage

### Option 1: Helm Repository

```bash
helm repo add nikmmd https://nikmmd.github.io/helm-charts
helm repo update
helm search repo nikmmd
helm install myapp nikmmd/webapp --version 0.1.0
```

### Option 2: OCI Registry

```bash
helm install myapp oci://ghcr.io/nikmmd/helm-charts/webapp --version 0.1.0
```

## Available Charts

| Chart | Description |
|-------|-------------|
| [webapp](./charts/webapp) | Production-ready chart for web applications |

## Chart Features (webapp)

- **Core**: Deployment, Service, ServiceAccount, ConfigMap, Secret
- **Routing**: Ingress, HTTPRoute (Gateway API)
- **Autoscaling**: HPA, KEDA ScaledObject
- **Reliability**: PodDisruptionBudget
- **Observability**: ServiceMonitor, PrometheusRule
- **Security**: Certificate (cert-manager), NetworkPolicy, CiliumNetworkPolicy
- **Secrets**: ExternalSecret (external-secrets operator)

## Releasing Charts

### GitHub Pages (helm repo add)

Triggered automatically on push to `main` with changes in `charts/**`.

- Creates a GitHub Release with packaged chart
- Updates `index.yaml` on `gh-pages` branch

### OCI Registry (ghcr.io)

Triggered by pushing a tag or manual workflow dispatch.

```bash
# Tag format: <chart-name>-v<version>
git tag webapp-v0.2.0
git push origin webapp-v0.2.0
```

Or via GitHub Actions UI: Actions → Release Charts → Run workflow

### Typical Release Workflow

1. Make changes to chart
2. Bump `version` in `charts/<chart>/Chart.yaml`
3. Push to `main` → Pages release automatic
4. (Optional) Tag for OCI: `git tag <chart>-v<version> && git push origin <chart>-v<version>`
