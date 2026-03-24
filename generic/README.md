# Generic Helm Chart

Generic chart used to deploy _almost_ any desired app.

## Requirements

- [Helm](https://helm.sh/)
- [Kubernetes](https://kubernetes.io/pt-br/docs/home/)
- [Secret store csi driver](https://secrets-store-csi-driver.sigs.k8s.io/) (If using a secret provider class)
- An app that you want to deploy

## Configuration

List of values used. Examples for objects are in values.yaml.

| Parameter | Default | Description |
| --- | --- | --- |
| replicaCount | 1 | Desired number of pods to run |
| resources | {} | Memory and cpu resource definition |
| autoscaling.enabled | false | Enable HorizontalPodAutoscaler |
| autoscaling.minReplicas | 1 | HPA min replicas |
| autoscaling.maxReplicas | 4 | HPA max replicas |
| autoscaling.targetCPUUtilizationPercentage | 80 | Target cpu utilization for HPA |
| autoscaling.targetMemoryUtilizationPercentage | 80 | Target memory utilization for HPA |
| command | {} | command to run when the pod's container starts |
| args | {} | args to use when the pod's container starts |
| image.repository | "" | Image repository |
| image.tag | "" | Image tag |
| image.pullPolicy | "IfNotPresent" | Image pull policy |
| imagePullSecrets | - name: "container-registry-secrets" | list of registry secrets to pull images |
| env | {} | environment variables definition. see values.yaml |
| podAnnotations | {} | extra pod annotations |
| podLabels | {} | extra pod labels |
| serviceAccount.create | false | whether to create or not service account |
| serviceAccount.automount | true | whether to mount or not service account |
| serviceAccount.annotations | {} | extra service account annotations |
| serviceAccount.name | "" | service account name |
| podSecurityContext.runAsGroup | 3000 | user group definition for pod |
| podSecurityContext.fsGroup | 3000 | file system group definition for pod |
| securityContext.readOnlyRootFilesystem | true | wheter or not to define read only file system |
| securityContext.allowPrivilegeEscalation | false | whether or not allow privilege escalation |
| securityContext.runAsNonRoot | true | whether or not run as root user |
| securityContext.runAsUser | 1010 | user definition |
| service.type | ClusterIP | kubernetes service [type](https://kubernetes.io/docs/concepts/services-networking/service/) |
| service.ports | [] | list of ports exposed in the service. see values.yaml |
| ports | [] | list of ports exposed in the pod. see values.yaml |
| ingress.enabled | false | enable or disable ingress |
| ingress.className | "" | ingress class name (kong, nginx etc) |
| ingress.ingressList | [] | definition of one or more ingresses. see values.yaml |
| configmap.enabled | false | enable or disable configmap |
| configmap.data | {} | configmap data |
| spc.enabled | false | enable or disable spc |
| spc.provider | "" | name of the vault provider. see [secret store csi driver](https://secrets-store-csi-driver.sigs.k8s.io/) |
| spc.parameters | {} | parameters used to connect to vault. changes for each provider |
| persistence.enabled | false | enable or disable pvc |
| persistence.storage | 500Mi | pvc size |
| volumes | [] | list of volumes. see values.yaml |
| volumemounts | [] | list of volume mounts. see values.yaml |
| nodeselector | {} | definition of the node that the pod will run. see values.yaml |
| affinity | {} | definition of pod affinity and anti-affity. see values.yaml and [k8s docs](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/) |
