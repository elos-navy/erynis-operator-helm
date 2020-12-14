# Erynis Monitoring Stack Parameters

This document contains all available parameters used in Erynis monitoring stack for different components. Parameters are used in custom resources as input for Erynis monitoring operator, which processes them and creates target resources with desired configuration on OpenShift / K8s cluster.

## Thanos Parameters

Custom resource type: Thanos

The following tables lists the configurable parameters of the Thanos component and their default values per section/component:

### Global parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`                               | Global Docker image registry                                                                           | `nil`                                                   |
| `global.imagePullSecrets`                            | Global Docker registry secret names as an array                                                        | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`                                | Global storage class for dynamic provisioning                                                          | `nil`                                                   |

### Common parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `image.registry`                                     | Thanos image registry                                                                                  | `docker.io`                                             |
| `image.repository`                                   | Thanos image name                                                                                      | `bitnami/thanos`                                        |
| `image.tag`                                          | Thanos image tag                                                                                       | `{TAG_NAME}`                                            |
| `image.pullPolicy`                                   | Thanos image pull policy                                                                               | `IfNotPresent`                                          |
| `image.pullSecrets`                                  | Specify docker-registry secret names as an array                                                       | `[]` (does not add image pull secrets to deployed pods) |
| `nameOverride`                                       | String to partially override thanos.fullname                                                           | `nil`                                                   |
| `fullnameOverride`                                   | String to fully override thanos.fullname                                                               | `nil`                                                   |
| `clusterDomain`                                      | Default Kubernetes cluster domain                                                                      | `cluster.local`                                         |
| `objstoreConfig`                                     | [Objstore configuration](https://thanos.io/storage.md/#configuration)                                  | `nil`                                                   |
| `indexCacheConfig`                                   | [Index cache configuration](https://thanos.io/components/store.md/#memcached-index-cache)              | `nil`                                                   |
| `bucketCacheConfig`                                  | [Bucket cache configuration](https://thanos.io/components/store.md/#caching-bucket)                    | `nil`                                                   |
| `existingObjstoreSecret`                             | Name of existing secret with Objstore configuration                                                    | `nil`                                                   |
| `existingObjstoreSecretItems`                        | List of Secret Keys and Paths                                                                          | `[]`                                                    |
| `existingServiceAccount`                             | Name for the existing service account to be shared between the components                              | `nil`                                                   |

### Thanos Querier parameters

| Parameter                                       | Description                                                                                            | Default                                                 |
|-------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `querier.enabled`                               | Enable/disable Thanos Querier component                                                                | `true`                                                  |
| `querier.logLevel`                              | Thanos Querier log level                                                                               | `info`                                                  |
| `querier.replicaLabel`                          | Replica indicator(s) along which data is deduplicated                                                  | `replica`                                               |
| `querier.dnsDiscovery.enabled`                  | Enable store APIs discovery via DNS                                                                    | `true`                                                  |
| `querier.dnsDiscovery.sidecarsService`          | Sidecars service name to discover them using DNS discovery                                             | `nil` (evaluated as a template)                         |
| `querier.dnsDiscovery.sidecarsNamespace`        | Sidecars namespace to discover them using DNS discovery                                                | `nil` (evaluated as a template)                         |
| `querier.stores`                                | Store APIs to connect with Thanos Querier                                                              | `[]`                                                    |
| `querier.sdConfig`                              | Service Discovery configuration                                                                        | `nil`                                                   |
| `querier.existingSDConfigmap`                   | Name of existing ConfigMap with Ruler configuration                                                    | `nil`                                                   |
| `querier.extraFlags`                            | Extra Flags to passed to Thanos Querier                                                                | `[]`                                                    |
| `querier.replicaCount`                          | Number of Thanos Querier replicas to deploy                                                            | `1`                                                     |
| `querier.strategyType`                          | Deployment Strategy Type                                                                               | `RollingUpdate`                                         |
| `querier.affinity`                              | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `querier.nodeSelector`                          | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `querier.tolerations`                           | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `querier.priorityClassName`                     | Controller priorityClassName                                                                           | `nil`                                                   |
| `querier.securityContext.enabled`               | Enable security context for Thanos Querier pods                                                        | `true`                                                  |
| `querier.securityContext.fsGroup`               | Group ID for the Thanos Querier filesystem                                                             | `1001`                                                  |
| `querier.securityContext.runAsUser`             | User ID for the Thanos Querier container                                                               | `1001`                                                  |
| `querier.resources.limits`                      | The resources limits for the Thanos Querier container                                                  | `{}`                                                    |
| `querier.resources.requests`                    | The requested resources for the Thanos Querier container                                               | `{}`                                                    |
| `querier.podAnnotations`                        | Annotations for Thanos Querier pods                                                                    | `{}`                                                    |
| `querier.livenessProbe`                         | Liveness probe configuration for Thanos Querier                                                        | `Check values.yaml file`                                |
| `querier.readinessProbe`                        | Readiness probe configuration for Thanos Querier                                                       | `Check values.yaml file`                                |
| `querier.grpcTLS.server.secure`                 | Enable TLS for GRPC server                                                                             | `false`                                                 |
| `querier.grpcTLS.server.cert`                   | TLS Certificate for gRPC server                                                                        | `nil`                                                   |
| `querier.grpcTLS.server.key`                    | TLS Key for gRPC server                                                                                | `nil`                                                   |
| `querier.grpcTLS.server.ca`                     | TLS client CA for gRPC server used for client verification purposes on the server                      | `nil`                                                   |
| `querier.grpcTLS.client.secure`                 | Use TLS when talking to the gRPC server                                                                | `false`                                                 |
| `querier.grpcTLS.client.cert`                   | TLS Certificates to use to identify this client to the server                                          | `nil`                                                   |
| `querier.grpcTLS.client.key`                    | TLS Key for the client's certificate                                                                   | `nil`                                                   |
| `querier.grpcTLS.client.ca`                     | TLS CA Certificates to use to verify gRPC servers                                                      | `nil`                                                   |
| `querier.grpcTLS.client.servername`             | Server name to verify the hostname on the returned gRPC certificates.                                  | `nil`                                                   |
| `querier.service.type`                          | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `querier.service.clusterIP`                     | Thanos Querier service clusterIP IP                                                                    | `None`                                                  |
| `querier.service.http.port`                     | Service HTTP port                                                                                      | `9090`                                                  |
| `querier.service.http.nodePort`                 | Service HTTP node port                                                                                 | `nil`                                                   |
| `querier.service.grpc.port`                     | Service GRPC port                                                                                      | `10901`                                                 |
| `querier.service.grpc.nodePort`                 | Service GRPC node port                                                                                 | `nil`                                                   |
| `querier.service.loadBalancerIP`                | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `querier.service.loadBalancerSourceRanges`      | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `querier.service.annotations`                   | Annotations for Thanos Querier service                                                                 | `{}`                                                    |
| `querier.serviceAccount.annotations`            | Annotations for Thanos Querier Service Account                                                         | `{}`                                                    |
| `querier.autoscaling.enabled`                   | Enable autoscaling for Thanos Querier                                                                  | `false`                                                 |
| `querier.autoscaling.minReplicas`               | Minimum number of Thanos Querier replicas                                                              | `nil`                                                   |
| `querier.autoscaling.maxReplicas`               | Maximum number of Thanos Querier replicas                                                              | `nil`                                                   |
| `querier.autoscaling.targetCPU`                 | Target CPU utilization percentage                                                                      | `nil`                                                   |
| `querier.autoscaling.targetMemory`              | Target Memory utilization percentage                                                                   | `nil`                                                   |
| `querier.pdb.create`                            | Enable/disable a Pod Disruption Budget creation                                                        | `false`                                                 |
| `querier.pdb.minAvailable`                      | Minimum number/percentage of pods that should remain scheduled                                         | `1`                                                     |
| `querier.pdb.maxUnavailable`                    | Maximum number/percentage of pods that may be made unavailable                                         | `nil`                                                   |
| `querier.ingress.enabled`                       | Enable ingress controller resource                                                                     | `false`                                                 |
| `querier.ingress.certManager`                   | Add annotations for cert-manager                                                                       | `false`                                                 |
| `querier.ingress.hostname`                      | Default host for the ingress resource                                                                  | `thanos.local`                                          |
| `querier.ingress.annotations`                   | Ingress annotations                                                                                    | `[]`                                                    |
| `querier.ingress.extraHosts[0].name`            | Additional hostnames to be covered                                                                     | `nil`                                                   |
| `querier.ingress.extraHosts[0].path`            | Additional hostnames to be covered                                                                     | `nil`                                                   |
| `querier.ingress.extraTls[0].hosts[0]`          | TLS configuration for additional hostnames to be covered                                               | `nil`                                                   |
| `querier.ingress.extraTls[0].secretName`        | TLS configuration for additional hostnames to be covered                                               | `nil`                                                   |
| `querier.ingress.secrets[0].name`               | TLS Secret Name                                                                                        | `nil`                                                   |
| `querier.ingress.secrets[0].certificate`        | TLS Secret Certificate                                                                                 | `nil`                                                   |
| `querier.ingress.secrets[0].key`                | TLS Secret Key                                                                                         | `nil`                                                   |
| `querier.ingress.grpc.enabled`                  | Enable ingress controller resource (GRPC)                                                              | `false`                                                 |
| `querier.ingress.grpc.certManager`              | Add annotations for cert-manager (GRPC)                                                                | `false`                                                 |
| `querier.ingress.grpc.hostname`                 | Default host for the ingress resource (GRPC)                                                           | `thanos.local`                                          |
| `querier.ingress.grpc.annotations`              | Ingress annotations (GRPC)                                                                             | `[]`                                                    |
| `querier.ingress.grpc.extraHosts[0].name`       | Additional hostnames to be covered (GRPC)                                                              | `nil`                                                   |
| `querier.ingress.grpc.extraHosts[0].path`       | Additional hostnames to be covered (GRPC)                                                              | `nil`                                                   |
| `querier.ingress.grpc.extraTls[0].hosts[0]`     | TLS configuration for additional hostnames to be covered (GRPC)                                        | `nil`                                                   |
| `querier.ingress.grpc.extraTls[0].secretName`   | TLS configuration for additional hostnames to be covered (GRPC)                                        | `nil`                                                   |
| `querier.ingress.grpc.secrets[0].name`          | TLS Secret Name (GRPC)                                                                                 | `nil`                                                   |
| `querier.ingress.grpc.secrets[0].certificate`   | TLS Secret Certificate (GRPC)                                                                          | `nil`                                                   |
| `querier.ingress.grpc.secrets[0].key`           | TLS Secret Key (GRPC)                                                                                  | `nil`                                                   |

### Thanos Bucket Web parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `bucketweb.enabled`                                  | Enable/disable Thanos Bucket Web component                                                             | `false`                                                 |
| `bucketweb.logLevel`                                 | Thanos Bucket Web log level                                                                            | `info`                                                  |
| `bucketweb.refresh`                                  | Refresh interval to download metadata from remote storage                                              | `30m`                                                   |
| `bucketweb.timeout`                                  | Timeout to download metadata from remote storage                                                       | `5m`                                                    |
| `bucketweb.extraFlags`                               | Extra Flags to passed to Thanos Bucket Web                                                             | `[]`                                                    |
| `bucketweb.replicaCount`                             | Number of Thanos Bucket Web replicas to deploy                                                         | `1`                                                     |
| `bucketweb.strategyType`                             | Deployment Strategy Type                                                                               | `RollingUpdate`                                         |
| `bucketweb.affinity`                                 | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `bucketweb.nodeSelector`                             | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `bucketweb.tolerations`                              | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `bucketweb.priorityClassName`                        | Controller priorityClassName                                                                           | `nil`                                                   |
| `bucketweb.securityContext.enabled`                  | Enable security context for Thanos Bucket Web pods                                                     | `true`                                                  |
| `bucketweb.securityContext.fsGroup`                  | Group ID for the Thanos Bucket Web filesystem                                                          | `1001`                                                  |
| `bucketweb.securityContext.runAsUser`                | User ID for the Thanos Bucket Web container                                                            | `1001`                                                  |
| `bucketweb.resources.limits`                         | The resources limits for the Thanos Bucket Web container                                               | `{}`                                                    |
| `bucketweb.resources.requests`                       | The requested resources for the Thanos Bucket Web container                                            | `{}`                                                    |
| `bucketweb.podAnnotations`                           | Annotations for Thanos Bucket Web pods                                                                 | `{}`                                                    |
| `bucketweb.livenessProbe`                            | Liveness probe configuration for Thanos Compactor                                                      | `Check values.yaml file`                                |
| `bucketweb.readinessProbe`                           | Readiness probe configuration for Thanos Compactor                                                     | `Check values.yaml file`                                |
| `bucketweb.service.type`                             | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `bucketweb.service.clusterIP`                        | Thanos Bucket Web service clusterIP IP                                                                 | `None`                                                  |
| `bucketweb.service.http.port`                        | Service HTTP port                                                                                      | `8080`                                                  |
| `bucketweb.service.http.nodePort`                    | Service HTTP node port                                                                                 | `nil`                                                   |
| `bucketweb.service.loadBalancerIP`                   | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `bucketweb.service.loadBalancerSourceRanges`         | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `bucketweb.service.annotations`                      | Annotations for Thanos Bucket Web service                                                              | `{}`                                                    |
| `bucketweb.serviceAccount.annotations`               | Annotations for Thanos Bucket Web Service Account                                                      | `{}`                                                    |
| `bucketweb.serviceAccount.existingServiceAccount`    | Name for an existing Thanos Bucket Web Service Account                                                 | `nil`                                                   |
| `bucketweb.pdb.create`                               | Enable/disable a Pod Disruption Budget creation                                                        | `false`                                                 |
| `bucketweb.pdb.minAvailable`                         | Minimum number/percentage of pods that should remain scheduled                                         | `1`                                                     |
| `bucketweb.pdb.maxUnavailable`                       | Maximum number/percentage of pods that may be made unavailable                                         | `nil`                                                   |
| `bucketweb.ingress.enabled`                          | Enable ingress controller resource                                                                     | `false`                                                 |
| `bucketweb.ingress.certManager`                      | Add annotations for cert-manager                                                                       | `false`                                                 |
| `bucketweb.ingress.hostname`                         | Default host for the ingress resource                                                                  | `thanos-bucketweb.local`                                |
| `bucketweb.ingress.annotations`                      | Ingress annotations                                                                                    | `[]`                                                    |
| `bucketweb.ingress.extraHosts[0].name`               | Additional hostnames to be covered                                                                     | `nil`                                                   |
| `bucketweb.ingress.extraHosts[0].path`               | Additional hostnames to be covered                                                                     | `nil`                                                   |
| `bucketweb.ingress.extraTls[0].hosts[0]`             | TLS configuration for additional hostnames to be covered                                               | `nil`                                                   |
| `bucketweb.ingress.extraTls[0].secretName`           | TLS configuration for additional hostnames to be covered                                               | `nil`                                                   |
| `bucketweb.ingress.secrets[0].name`                  | TLS Secret Name                                                                                        | `nil`                                                   |
| `bucketweb.ingress.secrets[0].certificate`           | TLS Secret Certificate                                                                                 | `nil`                                                   |
| `bucketweb.ingress.secrets[0].key`                   | TLS Secret Key                                                                                         | `nil`                                                   |

### Thanos Compactor parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `compactor.enabled`                                  | Enable/disable Thanos Compactor component                                                              | `false`                                                 |
| `compactor.logLevel`                                 | Thanos Compactor log level                                                                             | `info`                                                  |
| `compactor.retentionResolutionRaw`                   | Resolution and Retention flag                                                                          | `30d`                                                   |
| `compactor.retentionResolution5m`                    | Resolution and Retention flag                                                                          | `30d`                                                   |
| `compactor.retentionResolution1h`                    | Resolution and Retention flag                                                                          | `10y`                                                   |
| `compactor.consistencyDelay`                         | Minimum age of fresh blocks before they are being processed                                            | `30m`                                                   |
| `compactor.extraFlags`                               | Extra Flags to passed to Thanos Compactor                                                              | `[]`                                                    |
| `compactor.strategyType`                             | Deployment Strategy Type                                                                               | `RollingUpdate`                                         |
| `compactor.affinity`                                 | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `compactor.nodeSelector`                             | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `compactor.tolerations`                              | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `compactor.priorityClassName`                        | Controller priorityClassName                                                                           | `nil`                                                   |
| `compactor.securityContext.enabled`                  | Enable security context for Thanos Compactor pods                                                      | `true`                                                  |
| `compactor.securityContext.fsGroup`                  | Group ID for the Thanos Compactor filesystem                                                           | `1001`                                                  |
| `compactor.securityContext.runAsUser`                | User ID for the Thanos Compactor container                                                             | `1001`                                                  |
| `compactor.resources.limits`                         | The resources limits for the Thanos Compactor container                                                | `{}`                                                    |
| `compactor.resources.requests`                       | The requested resources for the Thanos Compactor container                                             | `{}`                                                    |
| `compactor.podAnnotations`                           | Annotations for Thanos Compactor pods                                                                  | `{}`                                                    |
| `compactor.livenessProbe`                            | Liveness probe configuration for Thanos Compactor                                                      | `Check values.yaml file`                                |
| `compactor.readinessProbe`                           | Readiness probe configuration for Thanos Compactor                                                     | `Check values.yaml file`                                |
| `compactor.service.type`                             | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `compactor.service.clusterIP`                        | Thanos Compactor service clusterIP IP                                                                  | `None`                                                  |
| `compactor.service.http.port`                        | Service HTTP port                                                                                      | `9090`                                                  |
| `compactor.service.http.nodePort`                    | Service HTTP node port                                                                                 | `nil`                                                   |
| `compactor.service.loadBalancerIP`                   | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `compactor.service.loadBalancerSourceRanges`         | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `compactor.service.annotations`                      | Annotations for Thanos Compactor service                                                               | `{}`                                                    |
| `compactor.serviceAccount.annotations`               | Annotations for Thanos Compactor Service Account                                                       | `{}`                                                    |
| `compactor.serviceAccount.existingServiceAccount`    | Name for an existing Thanos Compactor Service Account                                                  | `nil`                                                   |
| `compactor.persistence.enabled`                      | Enable data persistence                                                                                | `true`                                                  |
| `compactor.persistence.existingClaim`                | Use a existing PVC which must be created manually before bound                                         | `nil`                                                   |
| `compactor.persistence.storageClass`                 | Specify the `storageClass` used to provision the volume                                                | `nil`                                                   |
| `compactor.persistence.accessModes`                  | Access modes of data volume                                                                            | `["ReadWriteOnce"]`                                     |
| `compactor.persistence.size`                         | Size of data volume                                                                                    | `8Gi`                                                   |

### Thanos Store Gateway parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `storegateway.enabled`                               | Enable/disable Thanos Store Gateway component                                                          | `false`                                                 |
| `storegateway.logLevel`                              | Thanos Store Gateway log level                                                                         | `info`                                                  |
| `storegateway.extraFlags`                            | Extra Flags to passed to Thanos Store Gateway                                                          | `[]`                                                    |
| `storegateway.config`                                | Thanos Store Gateway cache configuration                                                               | `nil`                                                   |
| `storegateway.existingConfigmap`                     | Name of existing ConfigMap with Thanos Store Gateway cache configuration                               | `nil`                                                   |
| `storegateway.updateStrategyType`                    | Statefulset Update Strategy Type                                                                       | `RollingUpdate`                                         |
| `storegateway.replicaCount`                          | Number of Thanos Store Gateway replicas to deploy                                                      | `1`                                                     |
| `storegateway.affinity`                              | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `storegateway.nodeSelector`                          | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `storegateway.tolerations`                           | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `storegateway.priorityClassName`                     | Controller priorityClassName                                                                           | `nil`                                                   |
| `storegateway.securityContext.enabled`               | Enable security context for Thanos Store Gateway pods                                                  | `true`                                                  |
| `storegateway.securityContext.fsGroup`               | Group ID for the Thanos Store Gateway filesystem                                                       | `1001`                                                  |
| `storegateway.securityContext.runAsUser`             | User ID for the Thanos Store Gateway container                                                         | `1001`                                                  |
| `storegateway.resources.limits`                      | The resources limits for the Thanos Store Gateway container                                            | `{}`                                                    |
| `storegateway.resources.requests`                    | The requested resources for the Thanos Store Gateway container                                         | `{}`                                                    |
| `storegateway.podAnnotations`                        | Annotations for Thanos Store Gateway pods                                                              | `{}`                                                    |
| `storegateway.livenessProbe`                         | Liveness probe configuration for Thanos Store Gateway                                                  | `Check values.yaml file`                                |
| `storegateway.readinessProbe`                        | Readiness probe configuration for Thanos Store Gateway                                                 | `Check values.yaml file`                                |
| `storegateway.service.type`                          | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `storegateway.service.clusterIP`                     | Thanos Store Gateway service clusterIP IP                                                              | `None`                                                  |
| `storegateway.service.http.port`                     | Service HTTP port                                                                                      | `9090`                                                  |
| `storegateway.service.http.nodePort`                 | Service HTTP node port                                                                                 | `nil`                                                   |
| `storegateway.service.grpc.port`                     | Service GRPC port                                                                                      | `10901`                                                 |
| `storegateway.service.grpc.nodePort`                 | Service GRPC node port                                                                                 | `nil`                                                   |
| `storegateway.service.loadBalancerIP`                | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `storegateway.service.loadBalancerSourceRanges`      | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `storegateway.service.annotations`                   | Annotations for Thanos Store Gateway service                                                           | `{}`                                                    |
| `storegateway.service.additionalHeadless`            | Additional Headless service                                                                            | `false`                                                 |
| `storegateway.serviceAccount.annotations`            | Annotations for Thanos Store Gateway Service Account                                                   | `{}`                                                    |
| `storegateway.serviceAccount.existingServiceAccount` | Name for an existing Thanos Store Gateway Service Account                                              | `nil`                                                   |
| `storegateway.persistence.enabled`                   | Enable data persistence                                                                                | `true`                                                  |
| `storegateway.persistence.existingClaim`             | Use a existing PVC which must be created manually before bound                                         | `nil`                                                   |
| `storegateway.persistence.storageClass`              | Specify the `storageClass` used to provision the volume                                                | `nil`                                                   |
| `storegateway.persistence.accessModes`               | Access modes of data volume                                                                            | `["ReadWriteOnce"]`                                     |
| `storegateway.persistence.size`                      | Size of data volume                                                                                    | `8Gi`                                                   |
| `storegateway.autoscaling.enabled`                   | Enable autoscaling for Thanos Store Gateway                                                            | `false`                                                 |
| `storegateway.autoscaling.minReplicas`               | Minimum number of Thanos Store Gateway replicas                                                        | `nil`                                                   |
| `storegategay.autoscaling.maxReplicas`               | Maximum number of Thanos Store Gateway replicas                                                        | `nil`                                                   |
| `storegateway.autoscaling.targetCPU`                 | Target CPU utilization percentage                                                                      | `nil`                                                   |
| `storegateway.autoscaling.targetMemory`              | Target Memory utilization percentage                                                                   | `nil`                                                   |
| `storegateway.pdb.create`                            | Enable/disable a Pod Disruption Budget creation                                                        | `false`                                                 |
| `storegateway.pdb.minAvailable`                      | Minimum number/percentage of pods that should remain scheduled                                         | `1`                                                     |
| `storegateway.pdb.maxUnavailable`                    | Maximum number/percentage of pods that may be made unavailable                                         | `nil`                                                   |

### Thanos Ruler parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `ruler.enabled`                                      | Enable/disable Thanos Ruler component                                                                  | `false`                                                 |
| `ruler.logLevel`                                     | Thanos Ruler log level                                                                                 | `info`                                                  |
| `ruler.dnsDiscovery.enabled`                         | Enable Querier APIs discovery via DNS                                                                  | `true`                                                  |
| `ruler.alertmanagers`                                | Alermanager URLs array                                                                                 | `[]`                                                    |
| `ruler.evalInterval`                                 | The default evaluation interval to use                                                                 | `1m`                                                    |
| `ruler.clusterName`                                  | Used to set the 'ruler_cluster' label                                                                  | `nil`                                                   |
| `ruler.extraFlags`                                   | Extra Flags to passed to Thanos Ruler                                                                  | `[]`                                                    |
| `ruler.config`                                       | Ruler configuration                                                                                    | `nil`                                                   |
| `ruler.existingConfigmap`                            | Name of existing ConfigMap with Ruler configuration                                                    | `nil`                                                   |
| `ruler.updateStrategyType`                           | Statefulset Update Strategy Type                                                                       | `RollingUpdate`                                         |
| `ruler.replicaCount`                                 | Number of Thanos Ruler replicas to deploy                                                              | `1`                                                     |
| `ruler.affinity`                                     | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `ruler.nodeSelector`                                 | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `ruler.tolerations`                                  | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `ruler.priorityClassName`                            | Controller priorityClassName                                                                           | `nil`                                                   |
| `ruler.securityContext.enabled`                      | Enable security context for Thanos Ruler pods                                                          | `true`                                                  |
| `ruler.securityContext.fsGroup`                      | Group ID for the Thanos Ruler filesystem                                                               | `1001`                                                  |
| `ruler.securityContext.runAsUser`                    | User ID for the Thanos Ruler container                                                                 | `1001`                                                  |
| `ruler.resources.limits`                             | The resources limits for the Thanos Ruler container                                                    | `{}`                                                    |
| `ruler.resources.requests`                           | The requested resources for the Thanos Ruler container                                                 | `{}`                                                    |
| `ruler.podAnnotations`                               | Annotations for Thanos Ruler pods                                                                      | `{}`                                                    |
| `ruler.livenessProbe`                                | Liveness probe configuration for Thanos Ruler                                                          | `Check values.yaml file`                                |
| `ruler.readinessProbe`                               | Readiness probe configuration for Thanos Ruler                                                         | `Check values.yaml file`                                |
| `ruler.service.type`                                 | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `ruler.service.clusterIP`                            | Thanos Ruler service clusterIP IP                                                                      | `None`                                                  |
| `ruler.service.http.port`                            | Service HTTP port                                                                                      | `9090`                                                  |
| `ruler.service.http.nodePort`                        | Service HTTP node port                                                                                 | `nil`                                                   |
| `ruler.service.grpc.port`                            | Service GRPC port                                                                                      | `10901`                                                 |
| `ruler.service.grpc.nodePort`                        | Service GRPC node port                                                                                 | `nil`                                                   |
| `ruler.service.loadBalancerIP`                       | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `ruler.service.loadBalancerSourceRanges`             | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `ruler.service.annotations`                          | Annotations for Thanos Ruler service                                                                   | `{}`                                                    |
| `ruler.service.additionalHeadless`                   | Additional Headless service                                                                            | `false`                                                 |
| `ruler.serviceAccount.annotations`                   | Annotations for Thanos Ruler Service Account                                                           | `{}`                                                    |
| `ruler.serviceAccount.existingServiceAccount`        | Name for an existing Thanos Ruler Service Account                                                      | `nil`                                                   |
| `ruler.persistence.enabled`                          | Enable data persistence                                                                                | `true`                                                  |
| `ruler.persistence.existingClaim`                    | Use a existing PVC which must be created manually before bound                                         | `nil`                                                   |
| `ruler.persistence.storageClass`                     | Specify the `storageClass` used to provision the volume                                                | `nil`                                                   |
| `ruler.persistence.accessModes`                      | Access modes of data volume                                                                            | `["ReadWriteOnce"]`                                     |
| `ruler.persistence.size`                             | Size of data volume                                                                                    | `8Gi`                                                   |
| `ruler.pdb.create`                                   | Enable/disable a Pod Disruption Budget creation                                                        | `false`                                                 |
| `ruler.pdb.minAvailable`                             | Minimum number/percentage of pods that should remain scheduled                                         | `1`                                                     |
| `ruler.pdb.maxUnavailable`                           | Maximum number/percentage of pods that may be made unavailable                                         | `nil`                                                   |

### Metrics parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `metrics.enabled`                                    | Enable the export of Prometheus metrics                                                                | `false`                                                 |
| `metrics.serviceMonitor.enabled`                     | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false`                                                 |
| `metrics.serviceMonitor.namespace`                   | Namespace in which Prometheus is running                                                               | `nil`                                                   |
| `metrics.serviceMonitor.labels`                      | Additional labels for ServiceMonitor                                                                   | `{}`                                                    |
| `metrics.serviceMonitor.interval`                    | Interval at which metrics should be scraped.                                                           | `nil` (Prometheus Operator default value)               |
| `metrics.serviceMonitor.scrapeTimeout`               | Timeout after which the scrape is ended                                                                | `nil` (Prometheus Operator default value)               |

### Volume Permissions parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `volumePermissions.enabled`           | Enable init container that changes the owner and group of the persistent volume(s) mountpoint to `runAsUser:fsGroup` | `false`                                                 |
| `volumePermissions.image.registry`    | Init container volume-permissions image registry                                                                     | `docker.io`                                             |
| `volumePermissions.image.repository`  | Init container volume-permissions image name                                                                         | `bitnami/minideb`                                       |
| `volumePermissions.image.tag`         | Init container volume-permissions image tag                                                                          | `buster`                                                |
| `volumePermissions.image.pullPolicy`  | Init container volume-permissions image pull policy                                                                  | `Always`                                                |
| `volumePermissions.image.pullSecrets` | Specify docker-registry secret names as an array                                                                     | `[]` (does not add image pull secrets to deployed pods) |

### MinIO chart parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `minio.enabled`                                      | Enable/disable Minio chart installation                                                                | `false`                                                 |
| `minio.accessKey.password`                           | MinIO Access Key                                                                                       | _random 10 character alphanumeric string_               |
| `minio.secretKey.password`                           | MinIO Secret Key                                                                                       | _random 40 character alphanumeric string_               |
| `minio.defaultBuckets`                               | Comma, semi-colon or space separated list of buckets to create                                         | `nil`                                                   |



### Thanos Querier Frontend parameters


| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `querierfrontend.enabled`                            | Enable/disable Thanos Querier Frontend component                                                       | `true`                                                  |
| `querierfrontend.logLevel`                           | Thanos Querier Frontend log level                                                                      | `info`                                                  |
| `querierfrontend.extraFlags`                         | Extra Flags to passed to Thanos Querier Frontend                                                       | `[]`                                                    |
| `querierfrontend.replicaCount`                       | Number of Thanos Querier Frontend replicas to deploy                                                   | `1`                                                     |
| `querierfrontend.strategyType`                       | Deployment Strategy Type                                                                               | `RollingUpdate`                                         |
| `querierfrontend.affinity`                           | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `querierfrontend.nodeSelector`                       | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `querierfrontend.tolerations`                        | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `querierfrontend.resources.limits`                   | The resources limits for the Thanos Querier Frontend container                                         | `{}`                                                    |
| `querierfrontend.resources.requests`                 | The requested resources for the Thanos Querier Frontend container                                      | `{}`                                                    |
| `querierfrontend.securityContext.enabled`            | Enable security context for Thanos Querier Frontend pods                                               | `false`                                                 |
| `querierfrontend.securityContext.fsGroup`            | Group ID for the Thanos Querier Frontend filesystem                                                    | `1001`                                                  |
| `querierfrontend.securityContext.runAsUser`          | User ID for the Thanos Querier Frontend container                                                      | `1001`                                                  |
| `querierfrontend.service.type`                       | Kubernetes service type                                                                                | `ClusterIP`                                             |
| `querierfrontend.service.clusterIP`                  | Thanos Querier Frontend service clusterIP IP                                                           | `None`                                                  |
| `querierfrontend.service.http.port`                  | Service HTTP port                                                                                      | `9090`                                                  |
| `querierfrontend.service.loadBalancerIP`             | loadBalancerIP if service type is `LoadBalancer`                                                       | `nil`                                                   |
| `querierfrontend.service.loadBalancerSourceRanges`   | Address that are allowed when service is LoadBalancer                                                  | `[]`                                                    |
| `querierfrontend.service.annotations`                | Annotations for Thanos Querier Frontend service                                                        | `{}`                                                    |
| `querierfrontend.openshiftRoute.enabled`             | Specifies whether to create an OpenShift route object                                                  | `false`                                                 |
| `querierfrontend.openshiftRoute.host`                | URL for OpenShift route object                                                                         | ``                                                      |
| `querierfrontend.oauthProxy.enabled`                 | Enable oAuth proxy                                                                                     | `true`                                                  |
| `querierfrontend.oauthProxy.image.registry`          | Registry for oAuth proxy image                                                                         | `quay.io`                                               |
| `querierfrontend.oauthProxy.image.repository`        | Repository for oAuth proxy image                                                                       | `openshift-release-dev/ocp-v4.0-art-dev@sha256`         |
| `querierfrontend.oauthProxy.image.tag`               | Tag for oAuth proxy image                                                                              | ``                                                      |




## Thanos Receive Parameters

Custom resource type: ThanosReceive

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `nodeSelector`                                       | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `tolerations`                                        | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `replicaCount`                                       | Number of replicas to deploy                                                                           | `1`                                                     |
| `image.repository`                                   | Thanos image name                                                                                      | `quay.io/thanos/thanos`                                 |
| `image.tag`                                          | Thanos image tag                                                                                       | `{TAG_NAME}`                                            |
| `image.pullPolicy`                                   | Thanos image pull policy                                                                               | `IfNotPresent`                                          |
| `persistence.enabled`                                | Enable data persistence                                                                                | `true`                                                  |
| `persistence.existingClaim`                          | Use a existing PVC which must be created manually before bound                                         | `nil`                                                   |
| `persistence.storageClass`                           | Specify the `storageClass` used to provision the volume                                                | `nil`                                                   |
| `persistence.accessModes`                            | Access modes of data volume                                                                            | `["ReadWriteOnce"]`                                     |
| `persistence.size`                                   | Size of data volume                                                                                    | `8Gi`                                                   |
| `resources.limits`                                   | The resources limits for the Thanos Receive container                                                  | `{}`                                                    |
| `resources.requests`                                 | The requested resources for the Thanos Receive container                                               | `{}`                                                    |
| `tsdb.retention`                                     | Retention period for Thanos Receive                                                                    | `5d`                                                    |
| `objectStoreSecret.name`                             | Object store configuration secret name                                                                 | ``                                                      |
| `objectStoreSecret.key`                              | Object Store key where object storage configuration is available                                       | `objstore.yml`                                          |
| `openshiftRoute.enabled`                             | Specifies whether to create an OpenShift route object                                                  | `false`                                                 |
| `openshiftRoute.host`                                | URL for OpenShift route object                                                                         | ``                                                      |
| `oauthProxy.enabled`                                 | Enable oAuth proxy                                                                                     | `true`                                                  |
| `oauthProxy.image.registry`                          | Registry for oAuth proxy image                                                                         | `quay.io`                                               |
| `oauthProxy.image.repository`                        | Repository for oAuth proxy image                                                                       | `openshift-release-dev/ocp-v4.0-art-dev@sha256`         |
| `oauthProxy.image.tag`                               | Tag for oAuth proxy image                                                                              | ``                                                      |
| `serviceAccount.create`                              | Specifies whether a service account should be created                                                  | `true`                                                  |
| `serviceAccount.name`                                | The name of the service account to use.                                                                | ``                                                      |
| `serviceAccount.annotations`                         | Annotations for Thanos Receive Service Account                                                         | `{}`                                                    |
| `serviceAccount.existingServiceAccount`              | Name for an existing Thanos Receive Service Account                                                    | `nil`                                                   |
| `podAnnotations`                                     | Annotations for Thanos Receive pods                                                                    | `{}`                                                    |
| `securityContext.enabled`                            | Enable security context for pods                                                                       | `true`                                                  |
| `securityContext.fsGroup`                            | Group ID for filesystem                                                                                | `1001`                                                  |
| `securityContext.runAsUser`                          | User ID for container                                                                                  | `1001`                                                  |


## Prometheus PushGateway Parameters

Custom resource type: PushGateway

|        Parameter                  |                                                          Description                                                          |      Default                      |
| --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------------------------------- |
| `affinity`                        | Affinity settings for pod assignment                                                                                          | `{}`                              |
| `extraArgs`                       | Optional flags for pushgateway                                                                                                | `[]`                              |
| `extraVars`                       | Optional environment variables for pushgateway                                                                                | `[]`                              |
| `image.repository`                | Image repository                                                                                                              | `prom/pushgateway`                |
| `image.tag`                       | Image tag                                                                                                                     | `v1.2.0`                          |
| `image.pullPolicy`                | Image pull policy                                                                                                             | `IfNotPresent`                    |
| `ingress.enabled`                 | Enables Ingress for pushgateway                                                                                               | `false`                           |
| `ingress.annotations`             | Ingress annotations                                                                                                           | `{}`                              |
| `ingress.hosts`                   | Ingress accepted hostnames                                                                                                    | `nil`                             |
| `ingress.tls`                     | Ingress TLS configuration                                                                                                     | `[]`                              |
| `resources`                       | CPU/Memory resource requests/limits                                                                                           | `{}`                              |
| `replicaCount`                    | Number of replicas                                                                                                            | `1`                               |
| `strategy`                        | Deployment strategy                                                                                                           | `{ "type": "Recreate" }`          |
| `service.type`                    | Service type                                                                                                                  | `ClusterIP`                       |
| `service.port`                    | The service port                                                                                                              | `9091`                            |
| `service.nodePort`                | The optional service node port when `service.type` is `NodePort`                                                              | ``                                |
| `service.targetPort`              | The target port of the container                                                                                              | `9091`                            |
| `serviceAnnotations`              | Annotations for the service                                                                                                   | `{}`                              |
| `serviceLabels`                   | Labels for service                                                                                                            | `{}`                              |
| `serviceAccount.create`           | Specifies whether a service account should be created.                                                                        | `true`                            |
| `serviceAccount.name`             | Service account to be used. If not set and `serviceAccount.create` is `true`, a name is generated using the fullname template |                                   |
| `tolerations`                     | List of node taints to tolerate                                                                                               | `{}`                              |
| `nodeSelector`                    | Node labels for pod assignment                                                                                                | `{}`                              |
| `podAnnotations`                  | Annotations for pod                                                                                                           | `{}`                              |
| `podLabels`                       | Labels for pod                                                                                                                | `{}`                              |
| `serviceAccountLabels`            | Labels for service account                                                                                                    | `{}`                              |
| `persistentVolumeLabels`          | Labels for persistent volume                                                                                                  | `{}`                              |
| `serviceMonitor.enabled`          | if `true`, creates a Prometheus Operator ServiceMonitor                                                                       | `false`                           |
| `serviceMonitor.namespace`        | Namespace which Prometheus is running in                                                                                      | `monitoring`                      |
| `serviceMonitor.interval`         | How frequently to scrape metrics (use by default, falling back to Prometheus' default)                                        | `nil`                             |
| `serviceMonitor.scrapeTimeout`    | How long to scrape metrics before timing out. (use by default, falling back to Prometheus' default)                           | `nil`                             |
| `serviceMonitor.additionalLables` | Used to pass Labels that are required by the Installed Prometheus Operator                                                    | `{}`                              |
| `serviceMonitor.honorLabels`      | if `true`, label conflicts are resolved by keeping label values from the scraped data                                         | `true`                            |
| `podDisruptionBudget`             | If set, create a PodDisruptionBudget with the items in this map set in the spec                                               | ``                                |
| `networkPolicy.allowAll`          | Allow connectivity from all pods in the cluster                                                                               | ``                                |
| `networkPolicy.customSelectors`   | Allow connectivity from pods that match a list of podSelectors and namespaceSelectors                                         | ``                                |


## Grafana Parameters

Custom resource type: Grafana

The following tables lists the configurable parameters of the grafana component and their default values.

### Global parameters

| Parameter                 | Description                                     | Default                                                 |
|---------------------------|-------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`    | Global Docker image registry                    | `nil`                                                   |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`     | Global storage class for dynamic provisioning   | `nil`                                                   |

### Common parameters

| Parameter           | Description                                   | Default         |
|---------------------|-----------------------------------------------|-----------------|
| `nameOverride`      | String to partially override grafana.fullname | `nil`           |
| `fullnameOverride`  | String to fully override grafana.fullname     | `nil`           |
| `clusterDomain`     | Default Kubernetes cluster domain             | `cluster.local` |

### Grafana parameters

| Parameter                              | Description                                                                 | Default                                                 |
|----------------------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------|
| `image.registry`                       | Grafana image registry                                                      | `docker.io`                                             |
| `image.repository`                     | Grafana image name                                                          | `bitnami/grafana`                                       |
| `image.tag`                            | Grafana image tag                                                           | `{TAG_NAME}`                                            |
| `image.pullPolicy`                     | Grafana image pull policy                                                   | `IfNotPresent`                                          |
| `image.pullSecrets`                    | Specify docker-registry secret names as an array                            | `[]` (does not add image pull secrets to deployed pods) |
| `admin.user`                           | Grafana admin username                                                      | `admin`                                                 |
| `admin.password`                       | Grafana admin password                                                      | Randomly generated                                      |
| `admin.existingSecret`                 | Name of the existing secret containing admin password                       | `nil`                                                   |
| `admin.existingSecretPasswordKey`      | Password key on the existing secret                                         | `password`                                              |
| `smtp.enabled`                         | Enable SMTP configuration                                                   | `false`                                                 |
| `smtp.user`                            | SMTP user                                                                   | `user`                                                  |
| `smtp.password`                        | SMTP password                                                               | `password`                                              |
| `smtp.existingSecret`                  | Name of the existing secret with SMTP credentials                           | `nil`                                                   |
| `smtp.existingSecretUserKey`           | User key on the existing secret                                             | `user`                                                  |
| `smtp.existingSecretPasswordKey`       | Password key on the existing secret                                         | `password`                                              |
| `plugins`                              | Grafana plugins to be installed in deployment time separated by commas      | `nil`                                                   |
| `ldap.enabled`                         | Enable LDAP for Grafana                                                     | `false`                                                 |
| `ldap.allowSignUp`                     | Allows LDAP sign up for Grafana                                             | `false`                                                 |
| `ldap.configMapName`                   | Name of the ConfigMap with the LDAP configuration file for Grafana          | `nil`                                                   |
| `extraEnvVars`                         | Array containing extra env vars to configure Grafana                        | `{}`                                                    |
| `extraConfigmaps`                      | Array to mount extra ConfigMaps to configure Grafana                        | `{}`                                                    |
| `config.useGrafanaIniFile`             | Allows to load a `grafana.ini` file                                         | `false`                                                 |
| `config.grafanaIniConfigMap`           | Name of the ConfigMap containing the `grafana.ini` file                     | `nil`                                                   |
| `config.grafanaIniSecret`              | Name of the Secret containing the `grafana.ini` file                        | `nil`                                                   |
| `dashboardsProvider.enabled`           | Enable the use of a Grafana dashboard provider                              | `false`                                                 |
| `dashboardsProvider.configMapName`     | Name of a ConfigMap containing a custom dashboard provider                  | `nil` (evaluated as a template)                         |
| `dashboardsConfigMaps`                 | Array with the names of a series of ConfigMaps containing dashboards files  | `nil`                                                   |
| `datasources.secretName`               | Secret name containing custom datasource files                              | `nil`                                                   |
| `AzureADOauth.enabled`                 | Enable Grafana AzureADOauth authentization, disable Oauth proxy             | `false`                                                 |
| `AzureADOauth.clientId`                | Azure client id                                                             | `nil` 
| `AzureADOauth.clientSecret`            | Azure client secret                                                         | `nil`
| `AzureADOauth.tenantId`                | Azure tenant id                                                             | `nil`



### Deployment parameters

| Parameter                      | Description                                              | Default                        |
|--------------------------------|----------------------------------------------------------|--------------------------------|
| `replicaCount`                 | Number of Grafana nodes                                  | `1`                            |
| `updateStrategy`               | Update strategy for the deployment                       | `{type: "RollingUpdate"}`      |
| `schedulerName`                | Alternative scheduler                                    | `nil`                          |
| `podLabels`                    | Grafana pod labels                                       | `{}` (evaluated as a template) |
| `podAnnotations`               | Grafana Pod annotations                                  | `{}` (evaluated as a template) |
| `affinity`                     | Affinity for pod assignment                              | `{}` (evaluated as a template) |
| `nodeSelector`                 | Node labels for pod assignment                           | `{}` (evaluated as a template) |
| `tolerations`                  | Tolerations for pod assignment                           | `[]` (evaluated as a template) |
| `livenessProbe`                | Liveness probe configuration for Grafana                 | `Check values.yaml file`       |
| `readinessProbe`               | Readiness probe configuration for Grafana                | `Check values.yaml file`       |
| `securityContext.enabled`      | Enable securityContext on for Grafana deployment         | `true`                         |
| `securityContext.runAsUser`    | User for the security context                            | `1001`                         |
| `securityContext.fsGroup`      | Group to configure permissions for volumes               | `1001`                         |
| `securityContext.runAsNonRoot` | Run containers as non-root users                         | `true`                         |
| `resources.limits`             | The resources limits for Grafana containers              | `{}`                           |
| `resources.requests`           | The requested resources for Grafana containers           | `{}`                           |
| `sidecars`                     | Attach additional sidecar containers to the Grafana pod  | `{}`                           |
| `extraVolumes`                 | Additional volumes for the Grafana pod                   | `[]`                           |
| `extraVolumeMounts`            | Additional volume mounts for the Grafana container       | `[]`                           |

### Persistence parameters

| Parameter                   | Description                       | Default         |
|-----------------------------|-----------------------------------|-----------------|
| `persistence.enabled`       | Enable persistence                | `true`          |
| `presistence.storageClass`  | Storage class to use with the PVC | `nil`           |
| `persistence.accessMode`    | Access mode to the PV             | `ReadWriteOnce` |
| `persistence.size`          | Size for the PV                   | `10Gi`          |

### RBAC parameters

| Parameter                    | Description                                        | Default                                         |
|------------------------------|----------------------------------------------------|-------------------------------------------------|
| `serviceAccount.create`      | Enable creation of ServiceAccount for Grafana pods | `true`                                          |
| `serviceAccount.name`        | Name of the created serviceAccount                 | Generated using the `grafana.fullname` template |
| `serviceAccount.annotations` | ServiceAccount Annotations                         | `{}`                                            |

### Exposure parameters

| Parameter                           | Description                                                                                                                                                                                                                           | Default             |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| `service.type`                      | Kubernetes Service type                                                                                                                                                                                                               | `ClusterIP`         |
| `service.port`                      | Grafana service port                                                                                                                                                                                                                  | `3000`              |
| `service.nodePort`                  | Port to bind to for NodePort service type (client port)                                                                                                                                                                               | `nil`               |
| `service.annotations`               | Annotations for Grafana service                                                                                                                                                                                                       | `{}`                |
| `service.loadBalancerIP`            | loadBalancerIP if Grafana service type is `LoadBalancer`                                                                                                                                                                              | `nil`               |
| `service.loadBalancerSourceRanges`  | loadBalancerSourceRanges if Grafana service type is `LoadBalancer`                                                                                                                                                                    | `nil`               |
| `ingress.enabled`                   | Enable the use of the ingress controller to access the web UI                                                                                                                                                                         | `false`             |
| `ingress.certManager`               | Add annotations for cert-manager                                                                                                                                                                                                      | `false`             |
| `ingress.annotations`               | Annotations for the Grafana Ingress                                                                                                                                                                                                   | `{}`                |
| `ingress.hosts[0].name`             | Hostname to your Grafana installation                                                                                                                                                                                                 | `grafana.local`     |
| `ingress.hosts[0].paths`            | Path within the url structure                                                                                                                                                                                                         | `["/"]`             |
| `ingress.hosts[0].extraPaths`       | Ingress extra paths to prepend to every host configuration. Useful when configuring [custom actions with AWS ALB Ingress Controller](https://kubernetes-sigs.github.io/aws-alb-ingress-controller/guide/ingress/annotation/#actions). | `[]`                |
| `ingress.hosts[0].tls`              | Utilize TLS backend in ingress                                                                                                                                                                                                        | `false`             |
| `ingress.hosts[0].tlsHosts`         | Array of TLS hosts for ingress record (defaults to `ingress.hosts[0].name` if `nil`)                                                                                                                                                  | `nil`               |
| `ingress.hosts[0].tlsSecret`        | TLS Secret (certificates)                                                                                                                                                                                                             | `grafana.local-tls` |

### Metrics parameters

| Parameter                              | Description                                                                                            | Default                                                 |
|----------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `metrics.enabled`                      | Enable the export of Prometheus metrics                                                                | `false`                                                 |
| `metrics.service.annotations`          | Annotations for Prometheus metrics service                                                             | `Check values.yaml file`                                |
| `metrics.serviceMonitor.enabled`       | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false`                                                 |
| `metrics.serviceMonitor.namespace`     | Namespace in which Prometheus is running                                                               | `nil`                                                   |
| `metrics.serviceMonitor.interval`      | Interval at which metrics should be scraped.                                                           | `nil` (Prometheus Operator default value)               |
| `metrics.serviceMonitor.scrapeTimeout` | Timeout after which the scrape is ended                                                                | `nil` (Prometheus Operator default value)               |
| `metrics.serviceMonitor.selector`      | Prometheus instance selector labels                                                                    | `nil`                                                   |

### Grafana Image Renderer parameters

| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `imageRenderer.enabled`                              | Enable using a remote rendering service to render PNG images                                           | `false`                                                 |
| `imageRenderer.image.registry`                       | Grafana Image Renderer image registry                                                                  | `docker.io`                                             |
| `imageRenderer.image.repository`                     | Grafana Image Renderer image name                                                                      | `bitnami/grafana-image-renderer`                        |
| `imageRenderer.image.tag`                            | Grafana Image Renderer image tag                                                                       | `{TAG_NAME}`                                            |
| `imageRenderer.image.pullPolicy`                     | Grafana Image Renderer image pull policy                                                               | `IfNotPresent`                                          |
| `imageRenderer.image.pullSecrets`                    | Specify docker-registry secret names as an array                                                       | `[]` (does not add image pull secrets to deployed pods) |
| `imageRenderer.replicaCount`                         | Number of Grafana Image Renderer nodes                                                                 | `1`                                                     |
| `imageRenderer.podAnnotations`                       | Grafana Image Renderer Pod annotations                                                                 | `{}` (evaluated as a template)                          |
| `imageRenderer.affinity`                             | Affinity for pod assignment                                                                            | `{}` (evaluated as a template)                          |
| `imageRenderer.nodeSelector`                         | Node labels for pod assignment                                                                         | `{}` (evaluated as a template)                          |
| `imageRenderer.tolerations`                          | Tolerations for pod assignment                                                                         | `[]` (evaluated as a template)                          |
| `imageRenderer.securityContext.enabled`              | Enable securityContext on for Grafana Image Renderer deployment                                        | `true`                                                  |
| `imageRenderer.securityContext.runAsUser`            | User for the security context                                                                          | `1001`                                                  |
| `imageRenderer.securityContext.fsGroup`              | Group to configure permissions for volumes                                                             | `1001`                                                  |
| `imageRenderer.securityContext.runAsNonRoot`         | Run containers as non-root users                                                                       | `true`                                                  |
| `imageRenderer.service.port`                         | Grafana Image Renderer service port                                                                    | `8080`                                                  |
| `imageRenderer.metrics.enabled`                      | Enable the export of Prometheus metrics                                                                | `false`                                                 |
| `imageRenderer.metrics.annotations`                  | Annotations for Prometheus metrics service                                                             | `Check values.yaml file`                                |
| `imageRenderer.metrics.serviceMonitor.enabled`       | if `true`, creates a Prometheus Operator ServiceMonitor (also requires `metrics.enabled` to be `true`) | `false`                                                 |
| `imageRenderer.metrics.serviceMonitor.namespace`     | Namespace in which Prometheus is running                                                               | `nil`                                                   |
| `imageRenderer.metrics.serviceMonitor.interval`      | Interval at which metrics should be scraped.                                                           | `nil` (Prometheus Operator default value)               |
| `imageRenderer.metrics.serviceMonitor.scrapeTimeout` | Timeout after which the scrape is ended                                                                | `nil` (Prometheus Operator default value)               |
| `imageRenderer.metrics.serviceMonitor.selector`      | Prometheus instance selector labels                                                                    | `nil`                                                   |

### Grafana injector parameters
| Parameter                                            | Description                                                                                            | Default                                                 |
|------------------------------------------------------|--------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `injector.enabled`                                   | Enable Grafana injector side container to run                                                          | `false`
| `injector.image.registry`                            | Grafana injector image registry                                                                        | `quay.io`
| `injector.image.repository`                          | Grafana injector image name                                                                            | `elostech/grafana-injector`
| `injector.image.tag`                                 | Grafana injector image tag                                                                             | `v0.1`
| `injector.resources.limits.cpu`                      | Grafana injector container cpu limit                                                                   | `100m`
| `injector.resources.limits.memory`                   | Grafana injector container memory limit                                                                | `128Mi`
| `injector.resources.requests.cpu`                    | Grafana injector container cpu request                                                                 | `100m`
| `injector.resources.requests.memory`                 | Grafana injector container memory request                                                              | `128Mi`
| `injector.apiEndpoints.openshift.url`                | Openshift API url to read project, users, bindings etc.                                                | `nil`
| `injector.apiEndpoints.openshift.port`               | Openshift API port to read project, users, bindings etc.                                               | `nil`
| `injector.apiEndpoints.grafana.url`                  | Grafana API url                                                                                        | `http://localhost`
| `injector.apiEndpoints.grafana.port`                 | Grafana API port                                                                                       | `3000`
| `injector.apiEndpoints.git.url`                      | Dashboards Git url                                                                                     | `nil`
| `injector.apiEndpoints.git.port`                     | Dashboards Git port                                                                                    | `nil`
| `injector.credentials.grafana.user`                  | Used for Grafana API authentication                                                                    | `nil`
| `injector.credentials.grafana.pass`                  | Used for Grafana API authentication                                                                    | `nil`
| `injector.credentials.git.user`                      | Used for GIT authentication                                                                            | `nil`
| `injector.credentials.git.pass`                      | Used for GIT authentication                                                                            | `nil`
| `injector.timing.startDelay`                         | Wait for others containers to start before first start in seconds                                      | `60`
| `injector.timing.interval`                           | Wait interval between each round in seconds                                                            | `120`
| `injector.projects_labels_selector`                  | This label marks Openshift project for processing by injector                                          | `monitoring.elostech.cz/create-grafana-folder=true`
| `injector.pruneFolders`                              | If 'true' injector deletes folders in Grafana (project not exist in Openshift or bad/missing label)    | `false`
