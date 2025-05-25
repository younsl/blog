# Squid Helm Chart

A Helm chart for running [Squid](http://www.squid-cache.org/) proxy server on Kubernetes.

## Background

## What is Squid?

Squid is a web proxy that caches HTTP, HTTPS, and FTP requests. It helps speed up web browsing and reduce bandwidth usage.

## Requirements

- Kubernetes 1.21+
- Helm 3.2.0+

## Installation

### Helm Chart

First of all, add the helm repository:

```bash
helm repo add younsl https://younsl.xyz/charts
helm repo update
```

Write your values.yaml and install the chart with your values file:

```bash
# Install with dedicated namespace
helm install squid younsl/squid \
  --namespace squid \
  --create-namespace

# Install with custom values file
helm install squid younsl/squid \
  --namespace squid \
  --create-namespace \
  --values your-values.yaml
```

## Configuration

### Basic Settings

| Parameter | Description | Default |
|-----------|-------------|---------|
| **General** | | |
| `replicaCount` | Number of pods | `2` |
| `revisionHistoryLimit` | Number of old deployments to keep | `10` |
| `nameOverride` | Override chart name | `""` |
| `fullnameOverride` | Override full name | `""` |
| **Image** | | |
| `image.repository` | Squid image repository | `ubuntu/squid` |
| `image.tag` | Image tag | `5.2-22.04_beta` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `imagePullSecrets` | Image pull secrets | `[]` |
| **Service** | | |
| `service.type` | Service type | `ClusterIP` |
| `service.port` | Service port | `3128` |
| `service.targetPort` | Container port | `3128` |
| `service.nodePort` | NodePort (if type is NodePort) | `""` |
| **Resources** | | |
| `resources.limits.memory` | Memory limit | `256Mi` |
| `resources.requests.cpu` | CPU request | `50m` |
| `resources.requests.memory` | Memory request | `128Mi` |
| **Security** | | |
| `serviceAccount.create` | Create service account | `true` |
| `serviceAccount.automountServiceAccountToken` | Auto-mount SA token | `false` |
| `securityContext.runAsUser` | Run as user ID | `0` |
| `securityContext.runAsNonRoot` | Run as non-root user | `false` |
| **High Availability** | | |
| `podDisruptionBudget.enabled` | Enable PDB | `true` |
| `podDisruptionBudget.minAvailable` | Minimum available pods | `1` |
| `topologySpreadConstraints` | Pod distribution rules | `[]` |
| **Storage** | | |
| `persistence.enabled` | Enable persistent storage | `false` |
| `persistence.size` | Storage size | `1Gi` |
| `persistence.accessMode` | Access mode | `ReadWriteOnce` |
| **Network** | | |
| `config.allowedNetworks.extra` | Additional allowed networks | `[]` |
| `dnsPolicy` | DNS policy | `ClusterFirst` |

### Squid Configuration

#### Network Access

Add allowed networks:

```yaml
config:
  allowedNetworks:
    extra:
      - name: "office"
        cidr: "10.1.0.0/24"
        description: "office network"
```

#### Domain Filtering

Enable domain whitelist in `values.yaml`:

```yaml
config:
  squid.conf: |
    # Uncomment these lines:
    acl allowed_domains dstdomain .example.com
    acl allowed_domains dstdomain .google.com
    
    # Change access rule from:
    # http_access allow allowed_nets
    # To:
    http_access allow allowed_nets allowed_domains
```

## Usage

### Test Connection

```bash
# Port forward to local machine
kubectl port-forward svc/my-squid 3128:3128

# Test proxy connection
export http_proxy=http://localhost:3128
curl -v https://www.google.com
```

This creates a tunnel from your local machine to the Squid proxy running in Kubernetes. The `curl` command will route through the proxy. You should see proxy-related headers in the output if it's working correctly.

Expected output:

- Connection to proxy established
- HTTP headers showing the request went through Squid
- Successful response from the target website

### Use in Applications

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-app
spec:
  containers:
  - name: app
    image: curlimages/curl
    env:
    - name: http_proxy
      value: "http://squid.squid.svc.cluster.local:3128"
    - name: https_proxy
      value: "http://squid.squid.svc.cluster.local:3128"
```

## Monitoring

Check logs:

```bash
kubectl logs deployment/squid --namespace squid
```

Check squid configuration file:

```bash
kubectl exec deployment/squid --namespace squid -- cat /etc/squid/squid.conf
```

## Upgrade

```bash
helm upgrade squid younsl/squid \
  --install \
  --namespace squid \
  --values your-modified-values.yaml
```

## Uninstall

Uninstall helm chart:

```bash
helm uninstall squid --namespace squid
```

Delete dedicated namespace:

```bash
kubectl get namespace squid
kubectl delete namespace squid
```

## License

MIT License