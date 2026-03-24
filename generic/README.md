# Generic Helm Chart

Generic chart used to deploy _almost_ any desired app.

## Resources Available

- Service
- Deployment (with container and init container)
- Persistent Volume Claim
- Configmap
- Secret Provider Class
- Horizontal Pod Autoscaler
- Ingress (with the possibility to deploy multiple)
- Service Account

## Requirements

- [Helm](https://helm.sh/)
- [Kubernetes](https://kubernetes.io/pt-br/docs/home/)
- [Secret store csi driver](https://secrets-store-csi-driver.sigs.k8s.io/) (If using a secret provider class)
- An app that you want to deploy

## Configuration

List of values used. Examples for objects are in values.yaml.

| Parameter | Description | Default |
| --- | --- | --- |
| replicaCount | Desired number of pods to run | 1 |
| resources | Memory and cpu resource definition | {} |
| autoscaling.enabled | Enable HorizontalPodAutoscaler | false |
| autoscaling.minReplicas | HPA min replicas | 1 |
| autoscaling.maxReplicas | HPA max replicas | 4 |
| autoscaling.targetCPUUtilizationPercentage | Target cpu utilization for HPA | 80 |
| autoscaling.targetMemoryUtilizationPercentage | Target memory utilization for HPA | 80 |
| command | command to run when the pod's container starts | {} |
| args | args to use when the pod's container starts | {} |
| image.repository | Image repository | "" |
| image.tag | Image tag | "" |
| image.pullPolicy | Image pull policy | "IfNotPresent" |
| imagePullSecrets | list of registry secrets to pull images | - name: "container-registry-secrets" |
| env | environment variables definition. see values.yaml | {} |
| podAnnotations | extra pod annotations | {} |
| podLabels | extra pod labels | {} |
| serviceAccount.create | whether to create or not service account | false |
| serviceAccount.automount | whether to mount or not service account | true |
| serviceAccount.annotations | extra service account annotations | {} |
| serviceAccount.name | service account name | "" |
| podSecurityContext.runAsGroup | user group definition for pod | 3000 |
| podSecurityContext.fsGroup | file system group definition for pod | 3000 |
| securityContext.readOnlyRootFilesystem | wheter or not to define read only file system | true |
| securityContext.allowPrivilegeEscalation | whether or not allow privilege escalation | false |
| securityContext.runAsNonRoot | whether or not run as root user | true |
| securityContext.runAsUser | user definition | 1010 |
| service.type | kubernetes service [type](https://kubernetes.io/docs/concepts/services-networking/service/) | ClusterIP |
| service.ports | list of ports exposed in the service. see values.yaml | [] |
| ports | list of ports exposed in the pod. see values.yaml | [] |
| ingress.enabled | enable or disable ingress | false |
| ingress.className | ingress class name (kong, nginx etc) | "" |
| ingress.ingressList | definition of one or more ingresses. see values.yaml | [] |
| configmap.enabled | enable or disable configmap | false |
| configmap.data | configmap data | {} |
| spc.enabled | enable or disable spc | false |
| spc.provider | name of the vault provider. see [secret store csi driver](https://secrets-store-csi-driver.sigs.k8s.io/) | "" |
| spc.parameters | parameters used to connect to vault. changes for each provider | {} |
| persistence.enabled | enable or disable pvc | false |
| persistence.storage | pvc size | 500Mi |
| volumes | list of volumes. see values.yaml | [] |
| volumemounts | list of volume mounts. see values.yaml | [] |
| nodeselector | definition of the node that the pod will run. see values.yaml | {} |
| affinity | definition of pod affinity and anti-affity. see values.yaml and [k8s docs](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) | {} |
