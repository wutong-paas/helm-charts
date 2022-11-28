# helm-charts
Helm Charts for Wutong PAAS apps.

## Wutong Console Helm Charts

You can deploy the Wutong Console in Kubernets using Helm Chart.

### Pre Requisites

* Kubernetes version cannot be earlier than 1.19

* StorageClass is required within the cluster

  > ref: https://artifacthub.io/packages/helm/kvaps/nfs-server-provisioner

### Installation

Add `wutong-console` helm charts repo

```
helm repo list
helm repo add wutong https://wutong-paas.github.io/helm-charts
helm repo update
```

Installing helm chart

> You need to have dynamic storage available on your Kubernetes cluster(StorageClass).
>
> If not, please refer [Install NFS-Server](https://artifacthub.io/packages/helm/kvaps/nfs-server-provisioner) .

```shell
kubectl create namespace wt-system
helm install wutong wutong/wutong-console \
--version 1.0.0 \
--set pvc.storageClassName=my-storageclass \
--set pvc.storageSize=5Gi \
--set ui.domain=my-domain.com \
--namespace wt-system
```

1. `pvc.storageClassName` Set StorageClassName in the cluster.
2. `pvc.storageSize`  Sets the volume size.

Nodeport 30707 is enabled by default, if you want to customize the port, please refer to :point_down:

```shell
helm install wutong wutong/wutong-console \
--version 1.0.0-stable \
--set ui.svc.nodePort=30600 \
--namespace wt-system
```

If you want to customize The parameters,The chart can be customized using The following configurable parameters.

| Parameter                                                    | Description                                                  | Default                                             |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :-------------------------------------------------- |
| `pvc.storageClassName`                                       | The StorageClass required for the Wutong component         | ""                                                  |
| `pvc.storageSize`                                            | To apply for PV Size                                         | 5Gi                                                 |
| `redis.fullname`                                             | Redis full name                                              | wutong-redis                                      |
| `redis.image.repository`                                     | Redis image repository                                       | redis                                               |
| `redis.image.pullPolicy`                                     | Redis image Pull strategy                                    | IfNotPresent                                        |
| `redis.image.tag`                                            | Redis image tag                                              | 4.0.12                                              |
| `redis.password`                                             | Redis Password                                               | 123456                                              |
| `redis.podAnnotations`                                       | Annotation to be added to Redis pods                         | {}                                                  |
| `redis.selectorLabels`                                       | Set the Redis Labels                                         | wutong: redis                                     |
| `redis.resources`                                            | Redis resource requests and limits                           | {}                                                  |
| `redis.nodeSelector`                                         | Node labels for pod assignment                               | {}                                                  |
| `redis.affinity`                                             | Defines affinities and anti-affinities for pods as defined in: https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity preferences | {}                                                  |
| `mysql.fullname`                                             | Mysql full name                                              | wutong-mysql                                      |
| `mysql.image.repository`                                     | Mysql image repository                                       | mysql                                               |
| `mysql.image.pullPolicy`                                     | Mysql image Pull strategy                                    | IfNotPresent                                        |
| `mysql.image.tag`                                            | Mysql image tag                                              | 5.7.23                                              |
| `mysql.secret.user` `mysql.secret.password` `mysql.secret.rootpassword` `mysql.secret.database` | Specify  MySQL account password and database                 |                                                     |
| `mysql.podAnnotations`                                       | Annotation to be added to Mysql pods                         | {}                                                  |
| `mysql.selectorLabels`                                       | Set the Mysql Labels                                         | wutong: mysql                                     |
| `mysql.resources`                                            | Mysql resource requests and limits                           | {}                                                  |
| `mysql.nodeSelector`                                         | Node labels for pod assignment                               | {}                                                  |
| `mysql.affinity`                                             | Defines affinities and anti-affinities for pods as defined in: https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity preferences | {}                                                  |

### Related repositorys

- [Wutong-Console](https://github.com/wutong-paas/wutong-console)
- [Wutong-Console-UI](https://github.com/wutong-paas/wutong-ui)
- [Wutong-Operator](https://github.com/wutong-paas/wutong-operator)
- [Wutong-Builder](https://github.com/wutong-paas/builder)
- [Wutong-Docs](https://github.com/wutong-paas/wutong-docs)

### License

Wutong follow LGPL-3.0 license，Details see[LICENSE](https://github.com/wutong-paas/wutong/blob/master/LICENSE) and [Licensing](https://github.com/wutong-paas/wutong/blob/master/Licensing.md)

## Wutong Operator Helm Charts

You can deploy the Wutong Operator in Kubernets using Helm Chart.

### Installation

Add `wutong-operator` helm charts repo

```shell
helm repo list
helm repo add wutong https://wutong-paas.github.io/helm-charts
helm repo update
```

Installing helm chart

```shell
helm install wutong wutong/wutong-operator \
--version 1.0.0 \
--set operator.image.name=swr.cn-southwest-2.myhuaweicloud.com/wutong/wutong-operator \
--set operator.image.tag=v1.0.0-stable \
--namespace wt-system
```