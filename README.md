# FreeSWITCH + CSTA Inside

This chart provides ability to extend applications with VoIP using FreeSWITCH Software Defined Telecom Stack and CSTA Inside CTI extension

### Requirements:
- Helm 3.7+
- Kubernetes 1.21+ with Windows node(s), 2 vCore, 4 GiB RAM
- Optional: persistent storage for configuration and data

-----

### Get Repo Info
```bash
helm repo add cstainside https://<chart-repo-for-cstainside>
helm repo update
```
-----

### Install Chart
```bash
helm install freeswitch cstainside/freeswitch
```
-----

### Configuration
The following table lists the configurable parameters of the carol chart and their default values:

| Parameter  |      Description      |  Default |
|----------|---------------|-------|
| replicaCount |  Number of pods | 1 |
| probes.enabled |  Using liveness and readyness probes | true |
| image.repository |  Container image repository | cstainside/freeswitch |
| image.tag |    Container image tag  | using the chart app version |
| service.csta.serviceType |  Type of CSTA service (ClusterIP or LoadBalancer)  | ClusterIP |
| service.csta.LoadBalancerIP |  Load Balancer IP for CSTA service  | "" |
| service.csta.port |    Port for CSTA service  | 3000 |
| service.sip.serviceType |  Type of SIP and RTP services (ClusterIP or LoadBalancer)  | LoadBalancer |
| service.sip.LoadBalancerIP |  Load Balancer IP for SIP and RTP service  | "" |
| service.sip.port |  Port for SIP service (both TCP and UDP).  | 5060 |
| service.sip.ports |  List of ports for SIP service in case of multiple profile (both TCP and UDP). If specified, *service.sip.port* is ignored. E.g. *--set "service.sip.ports={5060, 5080}"* | \{\} |
| service.rtp.rtp-start-port |  Lowest port for RTP traffic  | 64535 |
| service.sip.rtp-end-port |  Highest port for RTP traffic  | 65535 |
| service.annotations |  Annotations used for services, e.g  *--set service.annotations.metallb\\.universe\\.tf\\/allow-shared-ip=shared-ip-name*  | "" |
| conf.persistence.enabled |  Configure a Persistent Volume as the configuration location. If enabled, telephony configuration options via deployment are ignored, otherwise chart deploys configmaps for FreeSWITCH. It accepts an existing PVC to use. The Persistent Volume is mounted at `c:/Program Files (x86)/FreeSWITCH/conf` in the switch pod. If volume is empty, it will be initialized with demo config | false |
| conf.persistence.pvcName |  Persistent Volume Claim to use for storing configuration | "" |
| conf.persistence.subPath |  Subdirectory for configuration files on persistent volume | "" |
| conf.profiles.external.enable-3pcc |    Enables 3rd party call control on external SIP profile (required for gateways connecting to OpenScape Business PBX)  | false |
| data.persistence.enabled |  Add extra persistent volume for the container for extra data (e.g. for soundfiles). | false |
| data.persistence.mountPath |  Path to mount the data volume into the FreeSWITCH container | "" |
| data.persistence.pvcName |  Persistent Volume Claim to bind the data volume. It is allowed to use the same pvc for config and data volumes. | "" |
| data.persistence.subPath |  Subdirectory for data files on persistent volume | "" |
|||

-----
### Upgrading Chart
```bash
helm upgrade freeswitch
```

-----
### Uninstall Chart

```bash
helm uninstall freeswitch
```

http://cstainside.com
