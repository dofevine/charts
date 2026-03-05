# FileRise Helm Chart

Unofficial Helm Chart for deploying FileRise on Kubernetes.

FileRise is a self-hosted web file manager with WebDAV, sharing, and per-folder ACLs.
Drag & drop uploads, OnlyOffice integration, and optional folder-level encryption at rest — all in one PHP app you control.
Built for homelabs, teams, and client portals that need fast browsing, strict ACLs, and zero-database simplicity.

Official project repository:  
<https://github.com/error311/FileRise>

## Installation

### Prerequisites

- Kubernetes 1.19+
- Helm 3+
- (Optional) Ingress Controller or Gateway API configured
- A configured StorageClass in the cluster

### Basic Installation

```bash
helm install filerise ./filerise
```

## Configuration

Below are the main configurable parameters available in `values.yaml`.

| Parameter | Description | Default |
| ------------ | ------------ | ---------- |
| `replicaCount` | Number of Deployment replicas | `1` |
| `image.repository` | Container image repository | `error311/filerise-docker` |
| `image.tag` | Image tag | `v3.5.2` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `imagePullSecrets` | Secrets for private repository | `[]` |
| `serviceAccount.create` | Create a ServiceAccount | `false` |
| `serviceAccount.name` | Custom name | `""` |
| `serviceAccount.automount` | Automount API credentials | `true` |
| `podAnnotations` | Extra pod annotations | `{}` |
| `podLabels` | Extra pod labels | `{}` |
| `service.type` | Kubernetes Service type | `ClusterIP` |
| `service.port` | Service port | `8080` |
| `ingress.enabled` | Enable Ingress | `false` |
| `ingress.className` | Ingress class | `""` |
| `ingress.hosts` | Configured hosts | `""` |
| `ingress.tls` | TLS configuration | `[]` |
| `httpRoute.enabled` | Enable HTTPRoute | `false` |
| `httpRoute.annotations` | Annotations | `{}` |
| `httpRoute.parentRefs` | Target Gateway | `{}` |
| `httpRoute.hostnames` | Hostnames | `[]` |
| `httpRoute.rules` | Routing rules | `{}` |
| `autoscaling.enabled` | Enable HPA | `false` |
| `autoscaling.minReplicas` | Minimum replicas | `1` |
| `autoscaling.maxReplicas` | Maximum replicas | `10` |
| `autoscaling.targetCPUUtilizationPercentage` | CPU utilization target | `80` |
| `autoscaling.targetMemoryUtilizationPercentage` | Memory utilization target | `2Gi` |
| `volumes` | list of volumes. See values.yaml | [] |
| `storage.keep` | Enable helm resource policy keep | `true` |
| `storage.storageClass` | Storage Class name. If empty will use cluster default | "" |
| `storage.metadata.size` | Size of pvc used for metadata | [] |
| `storage.users.size` | Size of pvc used for metadata | [] |
| `storage.uploads.size` | Size of pvc used for metadata | [] |
| `nodeselector` | Definition of the node that the pod will run. See [k8s docs](https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes/) | `{}` |
| `affinity` | Definition of pod affinity and anti-affity. See [k8s docs](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) | `{}` |

## Environment Variables

| Variable | Description | Default |
| ----------- | ------------ | ---------- |
| `TIMEZONE` | Application timezone | `America/New_York` |
| `TOTAL_UPLOAD_SIZE` | Total upload size limit | `1G` |
| `SECURE` | Enable secure mode | `false` |
| `PERSISTENT_TOKENS_KEY` | Key for persistent tokens | `change_me` |
| `SCAN_ON_START` | Scan files on startup | `true` |
| `CHOWN_ON_START` | Adjust permissions on startup | `true` |
| `HTTP_PORT` | Internal HTTP port | `8080` |
| `FR_BASE_PATH` | Subpath deployment | (optional) |
| `FR_PUBLISHED_URL` | Public URL of the application | (optional) |
| `FR_TRUSTED_PROXIES` | Trusted proxy list | (optional) |

## Recommendations

- Change `PERSISTENT_TOKENS_KEY`

- Define resource limits and requests
- Use a reliable StorageClass
- Configure proper backups for persistent volumes

## Using https

- Enable TLS in Ingress
- Set `SECURE=true`

## Next Steps of this chart

- Configure HTTPRoute via Gateway API
- Configure subpath deployment using `FR_BASE_PATH`
- Publish the chart to a public Helm repository
- Enable use of existing pvc for uploads
- Configure probe

## License

Refer to the original FileRise project repository for licensing information.

## Maintainers

- **[Domingos](https://github.com/dofevine/)** — Initial development and maintenance of this chart
