# MySQL

This helm chart was customization by Poseidom Team.

## Prerequisites

- Kubernetes 1.6+ with Beta APIs enabled
- PV provisioner support in the underlying infrastructure

## Parameters

The following table lists the configurable parameters of the MySQL chart and their default values.

### - Simple create service parameters

| Parameter                                    | Description                                                                                  | Default                                              |
| -------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `global.imageRegistry`                       | Global Docker Image registry                                                                 | By Poseidon Service Setting                          |
| `mysqlDatabase`                              | Name for new database to create.                                                             | `nil`                                                |
| `mysqlRootPassword`                          | Password for the `root` user. Ignored if existing secret is provided                         | Random 10 characters                                 |
| `mysqlUser`                                  | Username of new user to create.                                                              | `nil`                                                |
| `mysqlPassword`                              | Password for the new user. Ignored if existing secret is provided                            | Random 10 characters                                 |

### - Other parameters

| Parameter                                    | Description                                                                                  | Default                                              |
| -------------------------------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| `args`                                       | Additional arguments to pass to the MySQL container.                                         | `[]`                                                 |
| `initContainer.resources`                    | initContainer resource requests/limits                                                       | Memory: `10Mi`, CPU: `10m`                           |
| `image`                                      | `mysql` image repository.                                                                    | `mysql`                                              |
| `imageTag`                                   | `mysql` image tag.                                                                           | `5.7.14`                                             |
| `busybox.image`                              | `busybox` image repository.                                                                  | `busybox`                                            |
| `busybox.tag`                                | `busybox` image tag.                                                                         | `latest`                                             |
| `testFramework.image`                        | `test-framework` image repository.                                                           | `dduportal/bats`                                     |
| `testFramework.tag`                          | `test-framework` image tag.                                                                  | `0.4.0`                                              |
| `imagePullPolicy`                            | Image pull policy                                                                            | `IfNotPresent`                                       |
| `existingSecret`                             | Use Existing secret for Password details                                                     | `nil`                                                |
| `extraVolumes`                               | Additional volumes as a string to be passed to the `tpl` function                            |                                                      |
| `extraVolumeMounts`                          | Additional volumeMounts as a string to be passed to the `tpl` function                       |                                                      |
| `extraInitContainers`                        | Additional init containers as a string to be passed to the `tpl` function                    |                                                      |
| `livenessProbe.initialDelaySeconds`          | Delay before liveness probe is initiated                                                     | 30                                                   |
| `livenessProbe.periodSeconds`                | How often to perform the probe                                                               | 10                                                   |
| `livenessProbe.timeoutSeconds`               | When the probe times out                                                                     | 5                                                    |
| `livenessProbe.successThreshold`             | Minimum consecutive successes for the probe to be considered successful after having failed. | 1                                                    |
| `livenessProbe.failureThreshold`             | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | 3                                                    |
| `readinessProbe.initialDelaySeconds`         | Delay before readiness probe is initiated                                                    | 5                                                    |
| `readinessProbe.periodSeconds`               | How often to perform the probe                                                               | 10                                                   |
| `readinessProbe.timeoutSeconds`              | When the probe times out                                                                     | 1                                                    |
| `readinessProbe.successThreshold`            | Minimum consecutive successes for the probe to be considered successful after having failed. | 1                                                    |
| `readinessProbe.failureThreshold`            | Minimum consecutive failures for the probe to be considered failed after having succeeded.   | 3                                                    |
| `schedulerName`                              | Name of the k8s scheduler (other than default)                                               | `nil`                                                |
| `persistence.enabled`                        | Create a volume to store data                                                                | true                                                 |
| `persistence.size`                           | Size of persistent volume claim                                                              | 8Gi RW                                               |
| `persistence.storageClass`                   | Type of persistent volume claim                                                              | nil                                                  |
| `persistence.accessMode`                     | ReadWriteOnce or ReadOnly                                                                    | ReadWriteOnce                                        |
| `persistence.existingClaim`                  | Name of existing persistent volume                                                           | `nil`                                                |
| `persistence.subPath`                        | Subdirectory of the volume to mount                                                          | `nil`                                                |
| `persistence.annotations`                    | Persistent Volume annotations                                                                | {}                                                   |
| `nodeSelector`                               | Node labels for pod assignment                                                               | {}                                                   |
| `tolerations`                                | Pod taint tolerations for deployment                                                         | {}                                                   |
| `metrics.enabled`                            | Start a side-car prometheus exporter                                                         | `false`                                              |
| `metrics.image`                              | Exporter image                                                                               | `prom/mysqld-exporter`                               |
| `metrics.imageTag`                           | Exporter image                                                                               | `v0.10.0`                                            |
| `metrics.imagePullPolicy`                    | Exporter image pull policy                                                                   | `IfNotPresent`                                       |
| `metrics.resources`                          | Exporter resource requests/limit                                                             | `nil`                                                |
| `metrics.livenessProbe.initialDelaySeconds`  | Delay before metrics liveness probe is initiated                                             | 15                                                   |
| `metrics.livenessProbe.timeoutSeconds`       | When the probe times out                                                                     | 5                                                    |
| `metrics.readinessProbe.initialDelaySeconds` | Delay before metrics readiness probe is initiated                                            | 5                                                    |
| `metrics.readinessProbe.timeoutSeconds`      | When the probe times out                                                                     | 1                                                    |
| `metrics.flags`                              | Additional flags for the mysql exporter to use                                               | `[]`                                                 |
| `metrics.serviceMonitor.enabled`             | Set this to `true` to create ServiceMonitor for Prometheus operator                          | `false`                                              |
| `metrics.serviceMonitor.additionalLabels`    | Additional labels that can be used so ServiceMonitor will be discovered by Prometheus        | `{}`                                                 |
| `resources`                                  | CPU/Memory resource requests/limits                                                          | Memory: `256Mi`, CPU: `100m`                         |
| `configurationFiles`                         | List of mysql configuration files                                                            | `nil`                                                |
| `configurationFilesPath`                     | Path of mysql configuration files                                                            | `/etc/mysql/conf.d/`                                 |
| `securityContext.enabled`                    | Enable security context (mysql pod)                                                          | `false`                                              |
| `securityContext.fsGroup`                    | Group ID for the container (mysql pod)                                                       | 999                                                  |
| `securityContext.runAsUser`                  | User ID for the container (mysql pod)                                                        | 999                                                  |
| `service.annotations`                        | Kubernetes annotations for mysql                                                             | {}                                                   |
| `service.type`                               | Kubernetes service type                                                                      | ClusterIP                                            |
| `service.loadBalancerIP`                     | LoadBalancer service IP                                                                      | `""`                                                 |
| `ssl.enabled`                                | Setup and use SSL for MySQL connections                                                      | `false`                                              |
| `ssl.secret`                                 | Name of the secret containing the SSL certificates                                           | mysql-ssl-certs                                      |
| `ssl.certificates[0].name`                   | Name of the secret containing the SSL certificates                                           | `nil`                                                |
| `ssl.certificates[0].ca`                     | CA certificate                                                                               | `nil`                                                |
| `ssl.certificates[0].cert`                   | Server certificate (public key)                                                              | `nil`                                                |
| `ssl.certificates[0].key`                    | Server key (private key)                                                                     | `nil`                                                |
| `imagePullSecrets`                           | Name of Secret resource containing private registry credentials                              | `nil`                                                |
| `initializationFiles`                        | List of SQL files which are run after the container started                                  | `nil`                                                |
| `timezone`                                   | Container and mysqld timezone (TZ env)                                                       | `nil` (UTC depending on image)                       |
| `podAnnotations`                             | Map of annotations to add to the pods                                                        | `{}`                                                 |
| `podLabels`                                  | Map of labels to add to the pods                                                             | `{}`                                                 |
| `priorityClassName`                          | Set pod priorityClassName                                                                    | `{}`                                                 |
| `deploymentAnnotations`		       | Map of annotations for deployment							      | `{}`						     |

## Persistence

The [MySQL](https://hub.docker.com/_/mysql/) image stores the MySQL data and configurations at the `/var/lib/mysql` path of the container.

By default a PersistentVolumeClaim is created and mounted into that directory. In order to disable this functionality
you can change the values.yaml to disable persistence and use an emptyDir instead.

> *"An emptyDir volume is first created when a Pod is assigned to a Node, and exists as long as that Pod is running on that node. When a Pod is removed from a node for any reason, the data in the emptyDir is deleted forever."*

**Notice**: You may need to increase the value of `livenessProbe.initialDelaySeconds` when enabling persistence by using PersistentVolumeClaim from PersistentVolume with varying properties. Since its IO performance has impact on the database initialization performance. The default limit for database initialization is `60` seconds (`livenessProbe.initialDelaySeconds` + `livenessProbe.periodSeconds` * `livenessProbe.failureThreshold`). Once such initialization process takes more time than this limit, kubelet will restart the database container, which will interrupt database initialization then causing persisent data in an unusable state.

## Custom MySQL configuration files

The [MySQL](https://hub.docker.com/_/mysql/) image accepts custom configuration files at the path `/etc/mysql/conf.d`. If you want to use a customized MySQL configuration, you can create your alternative configuration files by passing the file contents on the `configurationFiles` attribute. Note that according to the MySQL documentation only files ending with `.cnf` are loaded.

```yaml
configurationFiles:
  mysql.cnf: |-
    [mysqld]
    skip-host-cache
    skip-name-resolve
    sql-mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
  mysql_custom.cnf: |-
    [mysqld]
```

## MySQL initialization files

The [MySQL](https://hub.docker.com/_/mysql/) image accepts *.sh, *.sql and *.sql.gz files at the path `/docker-entrypoint-initdb.d`.
These files are being run exactly once for container initialization and ignored on following container restarts.
If you want to use initialization scripts, you can create initialization files by passing the file contents on the `initializationFiles` attribute.


```yaml
initializationFiles:
  first-db.sql: |-
    CREATE DATABASE IF NOT EXISTS first DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
  second-db.sql: |-
    CREATE DATABASE IF NOT EXISTS second DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;
```

## SSL

This chart supports configuring MySQL to use [encrypted connections](https://dev.mysql.com/doc/refman/5.7/en/encrypted-connections.html) with TLS/SSL certificates provided by the user. This is accomplished by storing the required Certificate Authority file, the server public key certificate, and the server private key as a Kubernetes secret. The SSL options for this chart support the following use cases:

* Manage certificate secrets with helm
* Manage certificate secrets outside of helm

## Manage certificate secrets with helm

Include your certificate data in the `ssl.certificates` section. For example:

```
ssl:
  enabled: false
  secret: mysql-ssl-certs
  certificates:
  - name: mysql-ssl-certs
    ca: |-
      -----BEGIN CERTIFICATE-----
      ...
      -----END CERTIFICATE-----
    cert: |-
      -----BEGIN CERTIFICATE-----
      ...
      -----END CERTIFICATE-----
    key: |-
      -----BEGIN RSA PRIVATE KEY-----
      ...
      -----END RSA PRIVATE KEY-----
```

> **Note**: Make sure your certificate data has the correct formatting in the values file.

## Manage certificate secrets outside of helm

1. Ensure the certificate secret exist before installation of this chart.
2. Set the name of the certificate secret in `ssl.secret`.
3. Make sure there are no entries underneath `ssl.certificates`.

To manually create the certificate secret from local files you can execute:
```
kubectl create secret generic mysql-ssl-certs \
  --from-file=ca.pem=./ssl/certificate-authority.pem \
  --from-file=server-cert.pem=./ssl/server-public-key.pem \
  --from-file=server-key.pem=./ssl/server-private-key.pem
```
> **Note**: `ca.pem`, `server-cert.pem`, and `server-key.pem` **must** be used as the key names in this generic secret.

If you are using a certificate your configurationFiles must include the three ssl lines under [mysqld]

```
[mysqld]
    ssl-ca=/ssl/ca.pem
    ssl-cert=/ssl/server-cert.pem
    ssl-key=/ssl/server-key.pem
```
