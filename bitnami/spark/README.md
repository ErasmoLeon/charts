# Apache Spark

[Apache Spark](https://spark.apache.org/) is an open-source distributed general-purpose cluster-computing framework. Spark provides an interface for programming entire clusters with implicit data parallelism and fault tolerance.

## TL;DR;

```console
$ helm install bitnami/spark
```

## Introduction

This chart bootstraps a [spark](https://github.com/bitnami/bitnami-docker-spark) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This Helm chart has been tested on top of [Bitnami Kubernetes Production Runtime](https://kubeprod.io/) (BKPR). Deploy BKPR to get automated TLS certificates, logging and monitoring for your applications.

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release bitnami/spark
```

The command deploys spark on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release. Use the option `--purge` to delete all persistent volumes too.

## Configuration

The following tables lists the configurable parameters of the spark chart and their default values.

| Parameter                                   | Description                                                                                 | Default                                                 |
| ------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| `global.imageRegistry`                      | Global Docker image registry                                                                | `nil`                                                   |
| `global.imagePullSecrets`                   | Global Docker registry secret names as an array                                             | `[]` (does not add image pull secrets to deployed pods) |
| `image.registry`                            | spark image registry                                                                        | `docker.io`                                             |
| `image.repository`                          | spark Image name                                                                            | `bitnami/spark`                                         |
| `image.tag`                                 | spark Image tag                                                                             | `{TAG_NAME}`                                            |
| `image.pullPolicy`                          | spark image pull policy                                                                     | `IfNotPresent`                                          |
| `image.pullSecrets`                         | Specify docker-registry secret names as an array                                            | `[]` (does not add image pull secrets to deployed pods) |
| `master.debug`                              | Specify if debug values should be set on the master                                         | `false`                                                 |
| `worker.debug`                              | Specify if debug values should be set on workers                                            | `false`                                                 |
| `master.webPort`                            | Specify the port where the web interface will listen on the master                          | `8080`                                                  |
| `master.clusterPort`                        | Specify the port where the master listens to communicate with workers                       | `7077`                                                  |
| `master.daemonMemoryLimit`                  | Set the memory limit for the master daemon                                                  | No default                                              |
| `master.configOptions`                      | Optional configuration if the form `-Dx=y`                                                  | No default                                              |
| `master.updateStrategy`                     | Update strategy for the deployment                                                          | `RollingUpdate`                                         |
| `master.replicaCount`                       | Number of master replicas                                                                   | `1`                                                     |
| `master.securityContext.enabled`            | Enable security context                                                                     | `true`                                                  |
| `master.securityContext.fsGroup`            | Group ID for the container                                                                  | `1001`                                                  |
| `master.securityContext.runAsUser`          | User ID for the container                                                                   | `1001`                                                  |
| `master.nodeSelector`                       | Node labels for pod assignment                                                              | `{}`                                                    |
| `master.tolerations`                        | Toleration labels for pod assignment                                                        | `[]`                                                    |
| `master.affinity`                           | Affinity and AntiAffinity rules for pod assignment                                          | `{}`                                                    |
| `master.resources`                          | CPU/Memory resource requests/limits                                                         | Memory: `256Mi`, CPU: `250m`                            |
| `master.livenessProbe.enabled`              | Turn on and off liveness probe                                                              | `true`                                                  |
| `master.livenessProbe.initialDelaySeconds`  | Delay before liveness probe is initiated                                                    | 10                                                      |
| `master.livenessProbe.periodSeconds`        | How often to perform the probe                                                              | 10                                                      |
| `master.livenessProbe.timeoutSeconds`       | When the probe times out                                                                    | 5                                                       |
| `master.livenessProbe.failureThreshold`     | Minimum consecutive failures for the probe to be considered failed after having succeeded.  | 2                                                       |
| `master.livenessProbe.successThreshold`     | Minimum consecutive successes for the probe to be considered successful after having failed | 1                                                       |
| `master.readinessProbe.enabled`             | Turn on and off readiness probe                                                             | `true`                                                  |
| `master.readinessProbe.initialDelaySeconds` | Delay before liveness probe is initiated                                                    | 5                                                       |
| `master.readinessProbe.periodSeconds`       | How often to perform the probe                                                              | 10                                                      |
| `master.readinessProbe.timeoutSeconds`      | When the probe times out                                                                    | 5                                                       |
| `master.readinessProbe.failureThreshold`    | Minimum consecutive failures for the probe to be considered failed after having succeeded.  | 6                                                       |
| `master.readinessProbe.successThreshold`    | Minimum consecutive successes for the probe to be considered successful after having failed | 1                                                       |
| `worker.webPort`                            | Specify the port where the web interface will listen on the worker                          | `8080`                                                  |
| `worker.clusterPort`                        | Specify the port where the worker listens to communicate with the master                    | `7077`                                                  |
| `worker.daemonMemoryLimit`                  | Set the memory limit for the worker daemon                                                  | No default                                              |
| `worker.memoryLimit`                        | Set the maximum memory the worker is allowed to use                                         | No default                                              |
| `worker.coreLimit`                          | Se the maximum number of cores that the worker can use                                      | No default                                              |
| `worker.dir`                                | Set a custom working directory for the application                                          | No default                                              |
| `worker.javaOptions`                        | Set options for the JVM in the form `-Dx=y`                                                 | No default                                              |
| `worker.configOptions`                      | Set extra options to configure the worker in the form `-Dx=y`                               | No default                                              |
| `worker.replicaCount`                       | Set the number of workers                                                                   | `2`                                                     |
| `worker.enableAutoscaling`                  | Enable autoscaling depending on CPU                                                         | `false`                                                 |
| `worker.replicasMax`                        | Maximum number of workers when using autoscaling                                            | `false`                                                 |
| `worker.updateStrategy`                     | Update strategy for the deployment                                                          | `RollingUpdate`                                         |
| `worker.replicaCount`                       | Number of worker replicas                                                                   | `1`                                                     |
| `worker.securityContext.enabled`            | Enable security context                                                                     | `true`                                                  |
| `worker.securityContext.fsGroup`            | Group ID for the container                                                                  | `1001`                                                  |
| `worker.securityContext.runAsUser`          | User ID for the container                                                                   | `1001`                                                  |
| `worker.nodeSelector`                       | Node labels for pod assignment                                                              | `{}`                                                    |
| `worker.tolerations`                        | Toleration labels for pod assignment                                                        | `[]`                                                    |
| `worker.affinity`                           | Affinity and AntiAffinity rules for pod assignment                                          | `{}`                                                    |
| `worker.resources`                          | CPU/Memory resource requests/limits                                                         | Memory: `256Mi`, CPU: `250m`                            |
| `worker.livenessProbe.enabled`              | Turn on and off liveness probe                                                              | `true`                                                  |
| `worker.livenessProbe.initialDelaySeconds`  | Delay before liveness probe is initiated                                                    | 10                                                      |
| `worker.livenessProbe.periodSeconds`        | How often to perform the probe                                                              | 10                                                      |
| `worker.livenessProbe.timeoutSeconds`       | When the probe times out                                                                    | 5                                                       |
| `worker.livenessProbe.failureThreshold`     | Minimum consecutive failures for the probe to be considered failed after having succeeded.  | 2                                                       |
| `worker.livenessProbe.successThreshold`     | Minimum consecutive successes for the probe to be considered successful after having failed | 1                                                       |
| `worker.readinessProbe.enabled`             | Turn on and off readiness probe                                                             | `true`                                                  |
| `worker.readinessProbe.initialDelaySeconds` | Delay before liveness probe is initiated                                                    | 5                                                       |
| `worker.readinessProbe.periodSeconds`       | How often to perform the probe                                                              | 10                                                      |
| `worker.readinessProbe.timeoutSeconds`      | When the probe times out                                                                    | 5                                                       |
| `worker.readinessProbe.failureThreshold`    | Minimum consecutive failures for the probe to be considered failed after having succeeded.  | 6                                                       |
| `worker.readinessProbe.successThreshold`    | Minimum consecutive successes for the probe to be considered successful after having failed | 1                                                       |
| `security.passwordsSecretName`              | Secret to use when using security configuration to set custom passwords                     | No default                                              |
| `security.rpc.authenticationEnabled`        | Enable the RPC authentication                                                               | `no`                                                    |
| `security.rpc.encryptionEnabled`            | Enable the encryption for RPC                                                               | `no`                                                    |
| `security.storageEncryptionEnabled`         | Enable the encryption of the storage                                                        | `no`                                                    |
| `security.ssl.enabled`                      | Enable the SSL configuration                                                                | `no`                                                    |
| `security.ssl.needClientAuth`               | Enable the client authentication                                                            | `no`                                                    |
| `security.ssl.protocol`                     | Set the SSL protocol                                                                        | `TLSv1.2`                                               |
| `security.certificatesSecretName`           | Set the name of the secret that contains the certificates                                   | No default                                              |
| `service.type`                              | Kubernetes Service type                                                                     | `ClusterIP`                                             |
| `service.port`                              | spark client port                                                                           | `2379`                                                  |
| `service.nodePort`                          | Port to bind to for NodePort service type (client port)                                     | `nil`                                                   |
| `service.annotations`                       | Annotations for spark service                                                               | {}                                                      |
| `service.loadBalancerIP`                    | loadBalancerIP if spark service type is `LoadBalancer`                                      | `nil`                                                   |
| `ingress.enabled`                           | Enable the use of the ingress controller to access the web UI                               | `true`                                                  |
| `ingress.hosts`                             | Add hosts to the ingress controller with name and path                                      | `name: spark.local`, `path: /`                          |



Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
$ helm install --name my-release \
  --set master.webPort=8081 bitnami/spark
```

The above command sets the spark master web port to `8081`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
$ helm install --name my-release -f values.yaml bitnami/spark
```

> **Tip**: You can use the default [values.yaml](values.yaml)

### Production configuration and horizontal scaling

This chart includes a `values-production.yaml` file where you can find some parameters oriented to production configuration in comparison to the regular `values.yaml`.

```console
$ helm install --name my-release -f ./values-production.yaml bitnami/spark
```

- Enable RPC authentication:
```diff
- security.rpc.authenticationEnabled: no
+ security.rpc.authenticationEnabled: yes
```

- Enable RPC encryption:
```diff
- security.rpc.encryptionEnabled: no
+ security.rpc.encryptionEnabled: yes
```

- Enable storage encryption:
```diff
- security.storageEncryptionEnabled: no
+ security.storageEncryptionEnabled: no
```

- Configure SSL parameters:
```diff
- security.ssl.enabled: no
- security.ssl.needClientAuth: no
+ security.ssl.enabled: yes
+ security.ssl.needClientAuth: yes
```

- Set a secret name for passwords:
```diff
+ security.passwordsSecretName: my-passwords-secret
```

- Set a secret name for certificates:
```diff
+ security.certificatesSecretName: my-certificates-secret
```

- Enable authentication between master and workers:
```diff
- auth.enabled: false
+ auth.enabled: true
```

- Enable SSL communication:
```diff
- ssl.enabled: false
+ ssl.enabled: true
```

- Enable local storage encryption:
```diff
- storageEncription.enabled: false
+ storageEncription.enabled: true
```

### How to create the certificates secret
It is needed to create two secrets to set the passwords and certificates. The name of the two secrets should be configured on `security.passwordsSecretName` and `security.certificatesSecretName`.
Into the certificates secret, the keys must be `spark-keystore.jks` and `spark-truststore.jks`, and the content must be text on JKS format.
To generate the certificates secret, first it is needed to generate the two certificates and rename them as `spark-keystore.jks` and `spark-truststore.jks`.
Once the certificates are created, to create the secret having the file names as keys, execute a command like the following:
```bash
$ kubectl create secret generic my-secret --from-file=./keystore/spark-keystore.jks --from-file=./truststore/spark-truststore.jks
```

The second secret, the secret for passwords should have four keys: `rpc-authentication-secret`, `ssl-key-password`, `ssl-keystore-password` and `ssl-truststore-password`.
To create this secret, execute a command like the following:
```bash
$ kubectl create secret generic my-passwords-secret --from-literal=rpc-authentication-secret=myRPCSecret --from-literal=ssl-key-password=mySSLKeyPassword --from-literal=ssl-keystore-password=password --from-literal=ssl-truststore-password=password
```

Now that the two secrets are created, deploy the chart enabling security configuration and setting the name for the certificates secret (`my-secret` in this case) at the `security.certificatesSecretName` and setting the name for the passwords secret (`my-passwords-secret` in this case) at `security.passwordsSecretName`.

To deploy execute the following:
```bash
$ helm install . --set security.certificatesSecretName=my-secret,security.passwordsSecretName=my-passwords-secret,security.rpc.authenticationEnabled=yes,security.rpc.encryptionEnabled=yes,security.storageEncrytionEnabled=yes,security.ssl.enabled=yes,security.ssl.needClientAuth=yes
```

> Be aware that currently is not possible to submit an application to a standalone cluster if RPC authentication is configured. More info about the issue [here](https://issues.apache.org/jira/browse/SPARK-25078).

### Submit an application
To submit an application to the cluster use the `spark-submit` script. For example, to deploy one of the example applications:
```bash
$ ./bin/spark-submit   --class org.apache.spark.examples.SparkPi   --master spark://172.17.0.3:7077   --deploy-mode cluster  ./examples/jars/spark-examples_2.11-2.4.3.jar   1000
```

Where the master IP must be changed by you master IP address.
> Be aware that currently is not possible to submit an application to a standalone cluster if RPC authentication is configured. More info about the issue [here](https://issues.apache.org/jira/browse/SPARK-25078).

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

## Enable security for spark

### Configure ssl communication

In order to enable secure transport between workers and master deploy the helm chart with these options:

```console
$ helm install --name my-release --set ssl.enabled=true  bitnami/spark

```
