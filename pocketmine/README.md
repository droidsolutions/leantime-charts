# Gissilabs Helm Charts

## Pocketmine

Pocketmine is a highly customisable, open source server software for Minecraft: Bedrock Edition written in PHP. For more information, check their website at <https://www.pocketmine.net/>.

## Helm Chart

The default installation will deploy one Pocketmine instance without persistence. All data will be lost if the pod is deleted or rescheduled. The default service used is "NodePort", the IP and port will change as the Pod gets rescheduled or upgraded. For stable IPs and ports, use LoadBalancer service type if supported by the cluster.

```bash
helm install mypocketmine gissilabs/pocketmine
```

See options below to customize the deployment.

## **Plugins**

Option | Description | Format | Default
------ | ----------- | ------ | -------
plugins | List of plugins to enable | Array | Empty

## **Network**

Option | Description | Format | Default
------ | ----------- | ------ | -------
service.type | Service Type. [More Information](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types) | Type | NodePort
service.port | Service port | Number | 19132
service.externalTrafficPolicy | External Traffic Policy. [More Information](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) | Local / Cluster | Cluster
service.loadBalancerIP | Manually select IP when type is LoadBalancer | IP address | Not defined
service.nodePorts.port | Manually select node port | Number | Empty

## **Storage**

Option | Description | Format | Default
------ | ----------- | ------ | -------
persistence.enabled | Create persistent volume (PVC). Read-write data including config files, player data, worlds and plugin config files/data. | true / false | false
persistence.size | Size of volume | Size | 5Gi
persistence.accessMode | Volume access mode | Text | ReadWriteOnce
persistence.storageClass | Storage Class | Text | Not defined. Use "-" for default class
persistence.existingClaim | Use existing PVC | Name of PVC | Not defined

## **Image**

Option | Description | Format | Default
------ | ----------- | ------ | -------
image.tag | Docker image tag | Text | Chart appVersion (Chart.yaml)
image.repository | Docker image | Text | pmmp/pocketmine-mp
imagePullSecrets | Image pull secrets | Array | Empty

## **General Kubernetes/Helm**

Option | Description | Format | Default
------ | ----------- | ------ | -------
strategy | Deployment Strategy options | sub-tree | Empty
replicaCount | Number of pod replicas | Number | 1
nameOverride | Name override | Text | Empty
fullnameOverride | Full name override | Text | Empty
serviceAccount.create | Create Service Account | true / false | false
serviceAccount.annotations | Annotations service account | Map | Empty
serviceAccount.name | Service Account name | Text | Generated from template
podAnnotations | Pod Annotations | Map | Empty
podSecurityContext | Pod-level Security Context. Matches Pocketmine User ID in container. | Map | {fsGroup:1000}
securityContext | Container-level Security Context. Matches Pocketmine User ID in container. | Map | {runAsUser:1000, runAsGroup:1000}
resources | Deployment Resources | Map | Empty
nodeSelector | Node selector | Map | Empty
tolerations | Tolerations | Array | Empty
affinity | Affinity | Map | Empty
