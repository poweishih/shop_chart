# MongoDB

This helm chart was customization by Poseidom Team.

## Prerequisites

- Kubernetes 1.4+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Parameters

The following table lists the configurable parameters of the MongoDB chart and their default values.

### - Simple create service parameters

| Parameter                               | Description                                                                                  | Default                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `global.imageRegistry`                  | Global Docker image registry                                                                 | By Poseidon Service Setting                 |
| `mongodbDatabase`                       | Database to create                                                                           | `nil`                                       |
| `usePassword`                           | Enable password authentication                                                               | `true`                                      |
| `mongodbRootPassword`                   | MongoDB admin password                                                                       | `random alhpanumeric string (10)`           |
| `mongodbUsername`                       | MongoDB custom user                                                                          | `nil`                                       |
| `mongodbPassword`                       | MongoDB custom user password                                                                 | `random alhpanumeric string (10)`           |
| `replicaSet.enabled`                    | Switch to enable/disable replica set configuration                                           | `false`                                     |
| `replicaSet.name`                       | Name of the replica set                                                                      | `rs0`                                       |
| `replicaSet.key`                        | Key used for authentication in the replica set                                               | `nil`                                       |
| `replicaSet.replicas.secondary`         | Number of secondary nodes in the replica set                                                 | `2`                                         |
| `replicaSet.replicas.arbiter`           | Number of arbiter nodes in the replica set                                                   | `0`                                         |
| `replicaSet.pdb.minAvailable.primary`   | PDB for the MongoDB Primary nodes                                                            | `1`                                         |
| `replicaSet.pdb.minAvailable.secondary` | PDB for the MongoDB Secondary nodes                                                          | `2`                                         |
| `replicaSet.pdb.minAvailable.arbiter`   | PDB for the MongoDB Arbiter nodes                                                            | `0`                                         |

### - Other parameters

| Parameter                               | Description                                                                                  | Default                                     |
| --------------------------------------- | -------------------------------------------------------------------------------------------- | ------------------------------------------- |
| `image.repository`                      | MongoDB Image name                                                                           | `bitnami-mongodb-f`                         |
| `image.tag`                             | MongoDB Image tag                                                                            | `v20200217`                                 |
| `image.pullPolicy`                      | Image pull policy                                                                            | `Always`                                    |
| `image.pullSecrets`                     | Specify image pull secrets                                                                   | `nil`                                       |
| `existingSecret`                        | Existing secret with MongoDB credentials                                                     | `nil`                                       |
| `mongodbEnableIPv6`                     | Switch to enable/disable IPv6 on MongoDB                                                     | `true`                                      |
| `mongodbExtraFlags`                     | MongoDB additional command line flags                                                        | []                                          |
| `service.annotations`                   | Kubernetes service annotations                                                               | `{}`                                        |
| `service.type`                          | Kubernetes Service type                                                                      | `ClusterIP`                                 |
| `service.clusterIP`                     | Static clusterIP or None for headless services                                               | `nil`                                       |
| `service.nodePort`                      | Port to bind to for NodePort service type                                                    | `nil`                                       |
| `port`                                  | MongoDB service port                                                                         | `27017`                                     |
| `replicaSet.useHostnames`               | Enable DNS hostnames in the replica set config                                               | `true`                                      |
| `podAnnotations`                        | Annotations to be added to pods                                                              | {}                                          |
| `podLabels`                             | Additional labels for the pod(s).                                                            | {}                                          |
| `resources`                             | Pod resources                                                                                | {}                                          |
| `nodeSelector`                          | Node labels for pod assignment                                                               | {}                                          |
| `affinity`                              | Affinity for pod assignment                                                                  | {}                                          |
| `tolerations`                           | Toleration labels for pod assignment                                                         | {}                                          |
| `securityContext.enabled`               | Enable security context                                                                      | `true`                                      |
| `securityContext.fsGroup`               | Group ID for the container                                                                   | `1001`                                      |
| `securityContext.runAsUser`             | User ID for the container                                                                    | `1001`                                      |
| `persistence.enabled`                   | Use a PVC to persist data                                                                    | `true`                                      |
| `persistence.storageClass`              | Storage class of backing PVC                                                                 | `nil` (uses alpha storage class annotation) |
| `persistence.accessMode`                | Use volume as ReadOnly or ReadWrite                                                          | `ReadWriteOnce`                             |
| `persistence.size`                      | Size of data volume                                                                          | `8Gi`                                       |
| `persistence.annotations`               | Persistent Volume annotations                                                                | `{}`                                        |
| `persistence.existingClaim`             | Name of an existing PVC to use (avoids creating one if this is given)                        | `nil`                                       |
| `livenessProbe.initialDelaySeconds`     | Delay before liveness probe is initiated                                                     | `30`                                        |
| `livenessProbe.periodSeconds`           | How often to perform the probe                                                               | `10`                                        |
| `livenessProbe.timeoutSeconds`          | When the probe times out                                                                     | `5`                                         |
| `livenessProbe.successThreshold`        | Minimum consecutive successes for the probe to be considered successful after having failed. | `1`                                         |
| `livenessProbe.failureThreshold`        | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | `6`                                         |
| `readinessProbe.initialDelaySeconds`    | Delay before readiness probe is initiated                                                    | `5`                                         |
| `readinessProbe.periodSeconds`          | How often to perform the probe                                                               | `10`                                        |
| `readinessProbe.timeoutSeconds`         | When the probe times out                                                                     | `5`                                         |
| `readinessProbe.failureThreshold`       | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | `6`                                         |
| `readinessProbe.successThreshold`       | Minimum consecutive successes for the probe to be considered successful after having failed. | `1`                                         |
| `configmap`                             | MongoDB configuration file to be used                                                        | `nil`                                       |
| `metrics.enabled`                       | Start a side-car prometheus exporter                                                         | `false`                                     |
| `metrics.image.repository`              | MongoDB exporter image name                                                                  | `bitnami-mongodb-exporter`                  |
| `metrics.image.tag`                     | MongoDB exporter image tag                                                                   | `v20200630`                                 |
| `metrics.image.pullPolicy`              | Image pull policy                                                                            | `IfNotPresent`                              |
| `metrics.image.pullSecrets`             | Specify docker-registry secret names as an array                                             | `nil`                                       |
| `metrics.podAnnotations`                | Additional annotations for Metrics exporter pod                                              | {}                                          |
| `metrics.resources`                     | Exporter resource requests/limit                                                             | Memory: `256Mi`, CPU: `100m`                |
| `metrics.serviceMonitor.enabled`        | Create ServiceMonitor Resource for scraping metrics using PrometheusOperator                 | `false`                                     |
| `metrics.serviceMonitor.additionalLabels`          | Used to pass Labels that are required by the Installed Prometheus Operator        | {}                                          |
| `metrics.serviceMonitor.relabellings`              | Specify Metric Relabellings to add to the scrape endpoint                         | `nil`                                       |
| `metrics.serviceMonitor.alerting.rules`            | Define individual alerting rules as required                                      | {}                                          |
| `metrics.serviceMonitor.alerting.additionalLabels` | Used to pass Labels that are required by the Installed Prometheus Operator        | {}                                          |


## Replication

You can start the MongoDB chart in replica set mode with the following command:

```bash
$ helm install --name my-release stable/mongodb --set replication.enabled=true
```

## Production settings and horizontal scaling

The [values-production.yaml](values-production.yaml) file consists a configuration to deploy a scalable and high-available MongoDB deployment for production environments. We recommend that you base your production configuration on this template and adjust the parameters appropriately.

```console
$ curl -O https://raw.githubusercontent.com/kubernetes/charts/master/stable/mongodb/values-production.yaml
$ helm install --name my-release -f ./values-production.yaml stable/mongodb
```

To horizontally scale this chart, run the following command to scale the number of secondary nodes in your MongoDB replica set.

```console
$ kubectl scale statefulset my-release-mongodb-secondary --replicas=3
```

Some characteristics of this chart are:

- Each of the participants in the replication has a fixed stateful set so you always know where to find the primary, secondary or arbiter nodes.
- The number of secondary and arbiter nodes can be scaled out independently.
- Easy to move an application from using a standalone MongoDB server to use a replica set.

## Initialize a fresh instance

The [Bitnami MongoDB](https://github.com/bitnami/bitnami-docker-mongodb) image allows you to use your custom scripts to initialize a fresh instance. In order to execute the scripts, they must be located inside the chart folder `files/docker-entrypoint-initdb.d` so they can be consumed as a ConfigMap.

The allowed extensions are `.sh`, and `.js`.

## Persistence

The [Bitnami MongoDB](https://github.com/bitnami/bitnami-docker-mongodb) image stores the MongoDB data and configurations at the `/bitnami/mongodb` path of the container.

The chart mounts a [Persistent Volume](http://kubernetes.io/docs/user-guide/persistent-volumes/) at this location. The volume is created using dynamic volume provisioning.

## Upgrading

### To 5.0.0

When enabling replicaset configuration, backwards compatibility is not guaranteed unless you modify the labels used on the chart's statefulsets.
Use the workaround below to upgrade from versions previous to 5.0.0. The following example assumes that the release name is `my-release`:

```consoloe
$ kubectl delete statefulset my-release-mongodb-arbiter my-release-mongodb-primary my-release-mongodb-secondary --cascade=false
```
