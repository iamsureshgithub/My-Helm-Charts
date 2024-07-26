# nvidia-device-plugin

A Helm chart for deploying NVIDIA Device Plugin DaemonSet to allow scheduling of GPU workloads on nodes with NVIDIA GPUs.

![Version: 0.2.2](https://img.shields.io/badge/Version-0.2.2-informational?style=flat-square)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)
![AppVersion: v0.16.0](https://img.shields.io/badge/AppVersion-v0.16.0-informational?style=flat-square)

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| la-cc | <artem@lajko.dev> | <https://github.com/la-cc> |

## Installing the Chart

To install the chart with the release name `nvidia-device-plugin`:

```console
$ helm repo add nvidia-device-plugin https://la-cc.github.io/nvidia-device-plugin-helm-chart
$ helm repo update
$ helm install nvidia-device-plugin nvidia-device-plugin/nvidia-device-plugin
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env | list | `[{"name":"FAIL_ON_INIT_ERROR","value":"false"}]` | Environment variables to set in the container. |
| env[0] | object | `{"name":"FAIL_ON_INIT_ERROR","value":"false"}` | Name of the environment variable. |
| env[0].value | string | `"false"` | Value of the environment variable. |
| image | object | `{"pullPolicy":"IfNotPresent","repository":"nvcr.io/nvidia/k8s-device-plugin","tag":"v0.16.1"}` | Configuration for the Docker image used by the pod. |
| image.pullPolicy | string | `"IfNotPresent"` | The pull policy for the image. IfNotPresent means the image will only be pulled if it is not already present locally. |
| image.repository | string | `"nvcr.io/nvidia/k8s-device-plugin"` | The Docker repository to pull the image from. |
| image.tag | string | `"v0.16.1"` | The specific tag of the image to use. |
| nodeSelector | object | `{"node.kubernetes.io/instance-type":"Standard_NC6s_v3"}` | Constraints to ensure pods are scheduled on nodes with specific attributes. |
| nodeSelector."node.kubernetes.io/instance-type" | string | `"Standard_NC6s_v3"` | Only schedule pods on nodes with this instance type. |
| priorityClassName | string | `"system-node-critical"` | Priority class name for the pod, indicating its scheduling priority. |
| replicaCount | int | `1` | Number of pod replicas to deploy. |
| securityContext | object | `{"allowPrivilegeEscalation":false,"capabilities":{"drop":["ALL"]}}` | Security options for the pod. |
| securityContext.allowPrivilegeEscalation | bool | `false` | Prevent privilege escalation within the container. |
| securityContext.capabilities | object | `{"drop":["ALL"]}` | Capabilities to add or drop from the default set. |
| securityContext.capabilities.drop | list | `["ALL"]` | Drop all capabilities for the container. |
| tolerations | list | `[{"effect":"NoSchedule","key":"ai","operator":"Equal","value":"true"}]` | Tolerations for taints on nodes, allowing pods to be scheduled on tainted nodes. |
| tolerations[0] | object | `{"effect":"NoSchedule","key":"ai","operator":"Equal","value":"true"}` | The taint key that the toleration applies to. |
| tolerations[0].effect | string | `"NoSchedule"` | The effect of the taint; pods with this toleration can be scheduled on nodes with the taint. |
| tolerations[0].operator | string | `"Equal"` | The operator to use for the toleration. |
| tolerations[0].value | string | `"true"` | The value of the taint to tolerate. |
| volumeMounts | list | `[{"mountPath":"/var/lib/kubelet/device-plugins","name":"device-plugin"}]` | Volumes to mount into the container. |
| volumeMounts[0] | object | `{"mountPath":"/var/lib/kubelet/device-plugins","name":"device-plugin"}` | Name of the volume. |
| volumeMounts[0].mountPath | string | `"/var/lib/kubelet/device-plugins"` | Path inside the container where the volume should be mounted. |
| volumes | list | `[{"hostPath":{"path":"/var/lib/kubelet/device-plugins"},"name":"device-plugin"}]` | Volumes to be used by the pod. |
| volumes[0] | object | `{"hostPath":{"path":"/var/lib/kubelet/device-plugins"},"name":"device-plugin"}` | Name of the volume. |
| volumes[0].hostPath | object | `{"path":"/var/lib/kubelet/device-plugins"}` | Use a directory from the host node's filesystem. |
| volumes[0].hostPath.path | string | `"/var/lib/kubelet/device-plugins"` | Path on the host node to use as the volume. |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.14.2](https://github.com/norwoodj/helm-docs/releases/v1.14.2)
