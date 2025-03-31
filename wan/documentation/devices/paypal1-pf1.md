# paypal1-pf1

## Table of Contents

- [Management](#management)
  - [Agents](#agents)
  - [Management Interfaces](#management-interfaces)
  - [DNS Domain](#dns-domain)
  - [IP Name Servers](#ip-name-servers)
  - [NTP](#ntp)
  - [Management SSH](#management-ssh)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
  - [AAA Authorization](#aaa-authorization)
- [Aliases Device Configuration](#aliases-device-configuration)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
  - [Logging](#logging)
  - [Flow Tracking](#flow-tracking)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [IP Security](#ip-security)
  - [IKE policies](#ike-policies)
  - [Security Association policies](#security-association-policies)
  - [IPSec profiles](#ipsec-profiles)
  - [IP Security Device Configuration](#ip-security-device-configuration)
- [Interfaces](#interfaces)
  - [Switchport Default](#switchport-default)
  - [DPS Interfaces](#dps-interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router Adaptive Virtual Topology](#router-adaptive-virtual-topology)
  - [Router Traffic-Engineering](#router-traffic-engineering)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
  - [IP Extended Community Lists](#ip-extended-community-lists)
- [ACL](#acl)
  - [IP Access-lists](#ip-access-lists)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Platform](#platform)
  - [Platform Summary](#platform-summary)
  - [Platform Device Configuration](#platform-device-configuration)
- [System L1](#system-l1)
  - [Unsupported Interface Configurations](#unsupported-interface-configurations)
  - [System L1 Device Configuration](#system-l1-device-configuration)
- [Application Traffic Recognition](#application-traffic-recognition)
  - [Applications](#applications)
  - [Application Profiles](#application-profiles)
  - [Field Sets](#field-sets)
  - [Router Application-Traffic-Recognition Device Configuration](#router-application-traffic-recognition-device-configuration)
  - [Router Path-selection](#router-path-selection)
- [Quality Of Service](#quality-of-service)
  - [QOS](#qos)
  - [QOS Class Maps](#qos-class-maps)
  - [QOS Policy Maps](#qos-policy-maps)
- [STUN](#stun)
  - [STUN Server](#stun-server)
  - [STUN Device Configuration](#stun-device-configuration)
- [EOS CLI Device Configuration](#eos-cli-device-configuration)

## Management

### Agents

#### Agent KernelFib

##### Environment Variables

| Name | Value |
| ---- | ----- |
| KERNELFIB_PROGRAM_ALL_ECMP | 'true' |

#### Agents Device Configuration

```eos
!
agent KernelFib environment KERNELFIB_PROGRAM_ALL_ECMP='true'
```

### Management Interfaces

#### Management Interfaces Summary

##### IPv4

| Management Interface | Description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | default | 192.168.1.5/24 | - |

##### IPv6

| Management Interface | Description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | oob_management | oob | default | - | - |

#### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   no shutdown
   ip address 192.168.1.5/24
```

### DNS Domain

DNS domain: sjc.aristanetworks.com

#### DNS Domain Device Configuration

```eos
dns domain sjc.aristanetworks.com
!
```

### IP Name Servers

#### IP Name Servers Summary

| Name Server | VRF | Priority |
| ----------- | --- | -------- |
| 169.254.169.254 | default | - |
| 8.8.4.4 | default | 4 |
| 8.8.8.8 | default | 4 |

#### IP Name Servers Device Configuration

```eos
ip name-server vrf default 8.8.4.4 priority 4
ip name-server vrf default 8.8.8.8 priority 4
ip name-server vrf default 169.254.169.254
```

### NTP

#### NTP Summary

##### NTP Servers

| Server | VRF | Preferred | Burst | iBurst | Version | Min Poll | Max Poll | Local-interface | Key |
| ------ | --- | --------- | ----- | ------ | ------- | -------- | -------- | --------------- | --- |
| 0.us.pool.ntp.org | default | True | - | - | - | - | - | - | - |

#### NTP Device Configuration

```eos
!
ntp server 0.us.pool.ntp.org prefer
```

### Management SSH

#### SSH Timeout and Management

| Idle Timeout | SSH Management |
| ------------ | -------------- |
| default | Enabled |

#### Max number of SSH sessions limit and per-host limit

| Connection Limit | Max from a single Host |
| ---------------- | ---------------------- |
| - | - |

#### Ciphers and Algorithms

| Ciphers | Key-exchange methods | MAC algorithms | Hostkey server algorithms |
|---------|----------------------|----------------|---------------------------|
| default | default | default | default |


#### Management SSH Device Configuration

```eos
!
management ssh
   client-alive interval 180
```

### Management API HTTP

#### Management API HTTP Summary

| HTTP | HTTPS | Default Services |
| ---- | ----- | ---------------- |
| False | True | - |

#### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| default | - | - |

#### Management API HTTP Device Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf default
      no shutdown
```

## Authentication

### Local Users

#### Local Users Summary

| User | Privilege | Role | Disabled | Shell |
| ---- | --------- | ---- | -------- | ----- |
| admin | 15 | network-admin | False | - |
| arastra | 15 | network-admin | False | - |
| avd | 15 | network-admin | False | - |
| cvpadmin | 15 | network-admin | False | - |

#### Local Users Device Configuration

```eos
!
username admin privilege 15 role network-admin secret sha512 <removed>
username arastra privilege 15 role network-admin secret sha512 <removed>
username avd privilege 15 role network-admin secret sha512 <removed>
username cvpadmin privilege 15 role network-admin secret sha512 <removed>
```

### AAA Authorization

#### AAA Authorization Summary

| Type | User Stores |
| ---- | ----------- |
| Exec | local |

Authorization for configuration commands is disabled.

#### AAA Authorization Device Configuration

```eos
aaa authorization exec default local
!
```

## Aliases Device Configuration

```eos
alias cc clear counters
alias senz show interface counter error | nz
alias shin show interface status
alias shmc show int | awk '/^[A-Z]/ { intf = $1 } /, address is/ { print intf, $6 }'
alias snz show interface counter | nz
alias spc show port-channel %1 detail all
alias sqnz show interface counter queue | nz
alias srnz show interface counter rate | n

!
```

## Monitoring

### TerminAttr Daemon

#### TerminAttr Daemon Summary

| CV Compression | CloudVision Servers | VRF | Authentication | Smash Excludes | Ingest Exclude | Bypass AAA |
| -------------- | ------------------- | --- | -------------- | -------------- | -------------- | ---------- |
| gzip | apiserver.cv-staging.corp.arista.io:443 | default | token-secure,/tmp/cv-onboarding-token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | True |

#### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=apiserver.cv-staging.corp.arista.io:443 -cvauth=token-secure,/tmp/cv-onboarding-token -cvvrf=default -disableaaa -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

### Logging

#### Logging Servers and Features Summary

| Type | Level |
| -----| ----- |
| Console | debugging |
| Monitor | debugging |

#### Logging Servers and Features Device Configuration

```eos
!
logging console debugging
logging monitor debugging
```

### Flow Tracking

#### Flow Tracking Hardware

##### Trackers Summary

| Tracker Name | Record Export On Inactive Timeout | Record Export On Interval | Number of Exporters | Applied On |
| ------------ | --------------------------------- | ------------------------- | ------------------- | ---------- |
| FLOW-TRACKER | 70000 | 5000 | 1 | Dps1<br>Ethernet1<br>Ethernet2 |

##### Exporters Summary

| Tracker Name | Exporter Name | Collector IP/Host | Collector Port | Local Interface |
| ------------ | ------------- | ----------------- | -------------- | --------------- |
| FLOW-TRACKER | CV-TELEMETRY | - | - | Loopback0 |

#### Flow Tracking Device Configuration

```eos
!
flow tracking hardware
   tracker FLOW-TRACKER
      record export on inactive timeout 70000
      record export on interval 5000
      exporter CV-TELEMETRY
         collector 127.0.0.1
         local interface Loopback0
         template interval 30000
   no shutdown
```

## Spanning Tree

### Spanning Tree Summary

STP mode: **none**

### Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
```

## IP Security

### IKE policies

| Policy name | IKE lifetime | Encryption | DH group | Local ID |
| ----------- | ------------ | ---------- | -------- | -------- |
| CP-IKE-POLICY | - | - | - | 192.168.99.1 |

### Security Association policies

| Policy name | ESP Integrity | ESP Encryption | Lifetime | PFS DH Group |
| ----------- | ------------- | -------------- | -------- | ------------ |
| CP-SA-POLICY | - | aes256gcm128 | - | 14 |

### IPSec profiles

| Profile name | IKE policy | SA policy | Connection | DPD Interval | DPD Time | DPD action | Mode | Flow Parallelization |
| ------------ | ---------- | ----------| ---------- | ------------ | -------- | ---------- | ---- | -------------------- |
| CP-PROFILE | CP-IKE-POLICY | CP-SA-POLICY | start | - | - | - | transport | - |

### IP Security Device Configuration

```eos
!
ip security
   !
   ike policy CP-IKE-POLICY
      local-id 192.168.99.1
   !
   sa policy CP-SA-POLICY
      esp encryption aes256gcm128
      pfs dh-group 14
   !
   profile CP-PROFILE
      ike-policy CP-IKE-POLICY
      sa-policy CP-SA-POLICY
      connection start
      shared-key 7 <removed>
      dpd 10 50 clear
      mode transport
```

## Interfaces

### Switchport Default

#### Switchport Defaults Summary

- Default Switchport Mode: routed

#### Switchport Default Device Configuration

```eos
!
switchport default mode routed
```

### DPS Interfaces

#### DPS Interfaces Summary

| Interface | IP address | Shutdown | MTU | Flow tracker(s) | TCP MSS Ceiling |
| --------- | ---------- | -------- | --- | --------------- | --------------- |
| Dps1 | 192.168.99.1/32 | - | 9214 | Hardware: FLOW-TRACKER |  |

#### DPS Interfaces Device Configuration

```eos
!
interface Dps1
   description DPS Interface
   mtu 9214
   flow tracker hardware FLOW-TRACKER
   ip address 192.168.99.1/32
```

### Ethernet Interfaces

#### Ethernet Interfaces Summary

##### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet2 |  - | access | - | - | - | - |

*Inherited from Port-Channel Interface

##### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | AT & T_ATTI-CKT-PF-1-172.16.99.1 | routed | - | 172.16.99.1/28 | default | - | False | - | - |

#### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description AT & T_ATTI-CKT-PF-1-172.16.99.1
   no shutdown
   no switchport
   flow tracker hardware FLOW-TRACKER
   ip address 172.16.99.1/28
!
interface Ethernet2
   switchport
   flow tracker hardware FLOW-TRACKER
```

### Loopback Interfaces

#### Loopback Interfaces Summary

##### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | Router_ID | default | 10.254.99.1/32 |

##### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | Router_ID | default | - |

#### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description Router_ID
   no shutdown
   ip address 10.254.99.1/32
```

### VXLAN Interface

#### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Dps1 |
| UDP port | 4789 |

##### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| default | 101 | - |
| prod | 1 | - |

#### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description paypal1-pf1_VTEP
   vxlan source-interface Dps1
   vxlan udp-port 4789
   vxlan vrf default vni 101
   vxlan vrf prod vni 1
```

## Routing

### Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

### IP Routing

#### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | True |
| prod | True |

#### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf prod
```

### IPv6 Routing

#### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | False |
| default | false |
| prod | false |

### Static Routes

#### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP | Exit interface | Administrative Distance | Tag | Route Name | Metric |
| --- | ------------------ | ----------- | -------------- | ----------------------- | --- | ---------- | ------ |
| default | 0.0.0.0/0 | 172.16.99.2 | - | 1 | - | - | - |

#### Static Routes Device Configuration

```eos
!
ip route 0.0.0.0/0 172.16.99.2
```

### Router Adaptive Virtual Topology

#### Router Adaptive Virtual Topology Summary

Topology role: pathfinder

#### AVT Profiles

| Profile name | Load balance policy | Internet exit policy |
| ------------ | ------------------- | -------------------- |
| DEFAULT-AVT-POLICY-CONTROL-PLANE | LB-DEFAULT-AVT-POLICY-CONTROL-PLANE | - |
| DEFAULT-AVT-POLICY-DEFAULT | LB-DEFAULT-AVT-POLICY-DEFAULT | - |
| PROD-AVT-POLICY-DEFAULT | LB-PROD-AVT-POLICY-DEFAULT | - |
| PROD-AVT-POLICY-IT-APP | LB-PROD-AVT-POLICY-IT-APP | - |
| PROD-AVT-POLICY-Voice | LB-PROD-AVT-POLICY-Voice | - |

#### AVT Policies

##### AVT policy DEFAULT-AVT-POLICY-WITH-CP

| Application profile | AVT Profile | Traffic Class | DSCP |
| ------------------- | ----------- | ------------- | ---- |
| APP-PROFILE-CONTROL-PLANE | DEFAULT-AVT-POLICY-CONTROL-PLANE | - | - |
| default | DEFAULT-AVT-POLICY-DEFAULT | - | - |

##### AVT policy PROD-AVT-POLICY

| Application profile | AVT Profile | Traffic Class | DSCP |
| ------------------- | ----------- | ------------- | ---- |
| IT-APP | PROD-AVT-POLICY-IT-APP | 3 | 26 |
| Voice | PROD-AVT-POLICY-Voice | 5 | 46 |
| default | PROD-AVT-POLICY-DEFAULT | - | - |

#### VRFs configuration

##### VRF default

| AVT policy |
| ---------- |
| DEFAULT-AVT-POLICY-WITH-CP |

| AVT Profile | AVT ID |
| ----------- | ------ |
| DEFAULT-AVT-POLICY-DEFAULT | 1 |
| DEFAULT-AVT-POLICY-CONTROL-PLANE | 254 |

##### VRF prod

| AVT policy |
| ---------- |
| PROD-AVT-POLICY |

| AVT Profile | AVT ID |
| ----------- | ------ |
| PROD-AVT-POLICY-DEFAULT | 1 |
| PROD-AVT-POLICY-Voice | 4 |
| PROD-AVT-POLICY-IT-APP | 6 |

#### Router Adaptive Virtual Topology Configuration

```eos
!
router adaptive-virtual-topology
   topology role pathfinder
   !
   policy DEFAULT-AVT-POLICY-WITH-CP
      !
      match application-profile APP-PROFILE-CONTROL-PLANE
         avt profile DEFAULT-AVT-POLICY-CONTROL-PLANE
      !
      match application-profile default
         avt profile DEFAULT-AVT-POLICY-DEFAULT
   !
   policy PROD-AVT-POLICY
      !
      match application-profile IT-APP
         avt profile PROD-AVT-POLICY-IT-APP
         traffic-class 3
         dscp 26
      !
      match application-profile Voice
         avt profile PROD-AVT-POLICY-Voice
         traffic-class 5
         dscp 46
      !
      match application-profile default
         avt profile PROD-AVT-POLICY-DEFAULT
   !
   profile DEFAULT-AVT-POLICY-CONTROL-PLANE
      path-selection load-balance LB-DEFAULT-AVT-POLICY-CONTROL-PLANE
   !
   profile DEFAULT-AVT-POLICY-DEFAULT
      path-selection load-balance LB-DEFAULT-AVT-POLICY-DEFAULT
   !
   profile PROD-AVT-POLICY-DEFAULT
      path-selection load-balance LB-PROD-AVT-POLICY-DEFAULT
   !
   profile PROD-AVT-POLICY-IT-APP
      path-selection load-balance LB-PROD-AVT-POLICY-IT-APP
   !
   profile PROD-AVT-POLICY-Voice
      path-selection load-balance LB-PROD-AVT-POLICY-Voice
   !
   vrf default
      avt policy DEFAULT-AVT-POLICY-WITH-CP
      avt profile DEFAULT-AVT-POLICY-DEFAULT id 1
      avt profile DEFAULT-AVT-POLICY-CONTROL-PLANE id 254
   !
   vrf prod
      avt policy PROD-AVT-POLICY
      avt profile PROD-AVT-POLICY-DEFAULT id 1
      avt profile PROD-AVT-POLICY-Voice id 4
      avt profile PROD-AVT-POLICY-IT-APP id 6
```

### Router Traffic-Engineering

- Traffic Engineering is enabled.

#### Router Traffic Engineering Device Configuration

```eos
!
router traffic-engineering
```

### Router BGP

ASN Notation: asplain

#### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65199 | 192.168.99.1 |

| BGP AS | Cluster ID |
| ------ | --------- |
| 65199 | 10.254.99.1 |

| BGP Tuning |
| ---------- |
| no bgp default ipv4-unicast |
| maximum-paths 16 |

#### Router BGP Listen Ranges

| Prefix | Peer-ID Include Router ID | Peer Group | Peer-Filter | Remote-AS | VRF |
| ------ | ------------------------- | ---------- | ----------- | --------- | --- |
| 192.168.110.0/30 | - | WAN-OVERLAY-PEERS | - | 65199 | default |
| 192.168.100.0/30 | - | WAN-OVERLAY-PEERS | - | 65199 | default |

#### Router BGP Peer Groups

##### WAN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | wan |
| Remote AS | 65199 |
| Route Reflector Client | Yes |
| Source | Dps1 |
| BFD | True |
| BFD Timers | interval: 1000, min_rx: 1000, multiplier: 10 |
| TTL Max Hops | 1 |
| Send community | all |
| Maximum routes | 0 (no limit) |

##### WAN-RR-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | wan |
| Remote AS | 65199 |
| Route Reflector Client | Yes |
| Source | Dps1 |
| BFD | True |
| BFD Timers | interval: 1000, min_rx: 1000, multiplier: 10 |
| TTL Max Hops | 1 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD | RIB Pre-Policy Retain | Route-Reflector Client | Passive | TTL Max Hops |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- | --------------------- | ---------------------- | ------- | ------------ |
| 192.168.99.2 | Inherited from peer group WAN-RR-OVERLAY-PEERS | default | - | Inherited from peer group WAN-RR-OVERLAY-PEERS | Inherited from peer group WAN-RR-OVERLAY-PEERS | - | Inherited from peer group WAN-RR-OVERLAY-PEERS(interval: 1000, min_rx: 1000, multiplier: 10) | - | Inherited from peer group WAN-RR-OVERLAY-PEERS | - | Inherited from peer group WAN-RR-OVERLAY-PEERS |

#### Router BGP EVPN Address Family

- Next-hop resolution is **disabled**

##### EVPN Peer Groups

| Peer Group | Activate | Encapsulation |
| ---------- | -------- | ------------- |
| WAN-OVERLAY-PEERS | True | default |
| WAN-RR-OVERLAY-PEERS | True | default |

#### Router BGP IPv4 SR-TE Address Family

##### IPv4 SR-TE Peer Groups

| Peer Group | Activate | Route-map In | Route-map Out |
| ---------- | -------- | ------------ | ------------- |
| WAN-OVERLAY-PEERS | True | - | - |
| WAN-RR-OVERLAY-PEERS | True | - | - |

#### Router BGP Link-State Address Family

##### Link-State Peer Groups

| Peer Group | Activate | Missing policy In action | Missing policy Out action |
| ---------- | -------- | ------------------------ | ------------------------- |
| WAN-OVERLAY-PEERS | True | - | deny |
| WAN-RR-OVERLAY-PEERS | True | - | - |

##### Link-State Path Selection Configuration

| Settings | Value |
| -------- | ----- |
| Role(s) | consumer<br>propagator |

#### Router BGP Path-Selection Address Family

##### Path-Selection Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| WAN-OVERLAY-PEERS | True |
| WAN-RR-OVERLAY-PEERS | True |

#### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| default | 192.168.99.1:101 | - |
| prod | 192.168.99.1:1 | connected |

#### Router BGP Device Configuration

```eos
!
router bgp 65199
   router-id 192.168.99.1
   maximum-paths 16
   no bgp default ipv4-unicast
   bgp cluster-id 10.254.99.1
   bgp listen range 192.168.110.0/30 peer-group WAN-OVERLAY-PEERS remote-as 65199
   bgp listen range 192.168.100.0/30 peer-group WAN-OVERLAY-PEERS remote-as 65199
   neighbor WAN-OVERLAY-PEERS peer group
   neighbor WAN-OVERLAY-PEERS remote-as 65199
   neighbor WAN-OVERLAY-PEERS update-source Dps1
   neighbor WAN-OVERLAY-PEERS route-reflector-client
   neighbor WAN-OVERLAY-PEERS bfd
   neighbor WAN-OVERLAY-PEERS bfd interval 1000 min-rx 1000 multiplier 10
   neighbor WAN-OVERLAY-PEERS ttl maximum-hops 1
   neighbor WAN-OVERLAY-PEERS password 7 <removed>
   neighbor WAN-OVERLAY-PEERS send-community
   neighbor WAN-OVERLAY-PEERS maximum-routes 0
   neighbor WAN-RR-OVERLAY-PEERS peer group
   neighbor WAN-RR-OVERLAY-PEERS remote-as 65199
   neighbor WAN-RR-OVERLAY-PEERS update-source Dps1
   neighbor WAN-RR-OVERLAY-PEERS route-reflector-client
   neighbor WAN-RR-OVERLAY-PEERS bfd
   neighbor WAN-RR-OVERLAY-PEERS bfd interval 1000 min-rx 1000 multiplier 10
   neighbor WAN-RR-OVERLAY-PEERS ttl maximum-hops 1
   neighbor WAN-RR-OVERLAY-PEERS send-community
   neighbor WAN-RR-OVERLAY-PEERS maximum-routes 0
   neighbor 192.168.99.2 peer group WAN-RR-OVERLAY-PEERS
   neighbor 192.168.99.2 description paypal1-pf2
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor WAN-OVERLAY-PEERS activate
      neighbor WAN-RR-OVERLAY-PEERS activate
      next-hop resolution disabled
   !
   address-family ipv4
      no neighbor WAN-OVERLAY-PEERS activate
      no neighbor WAN-RR-OVERLAY-PEERS activate
   !
   address-family ipv4 sr-te
      neighbor WAN-OVERLAY-PEERS activate
      neighbor WAN-RR-OVERLAY-PEERS activate
   !
   address-family link-state
      neighbor WAN-OVERLAY-PEERS activate
      neighbor WAN-OVERLAY-PEERS missing-policy direction out action deny
      neighbor WAN-RR-OVERLAY-PEERS activate
      path-selection role consumer propagator
   !
   address-family path-selection
      bgp additional-paths receive
      bgp additional-paths send any
      neighbor WAN-OVERLAY-PEERS activate
      neighbor WAN-RR-OVERLAY-PEERS activate
   !
   vrf default
      rd 192.168.99.1:101
      route-target import evpn 65199:101
      route-target export evpn 65199:101
      route-target export evpn route-map RM-EVPN-EXPORT-VRF-DEFAULT
      router-id 192.168.99.1
   !
   vrf prod
      rd 192.168.99.1:1
      route-target import evpn 65199:1
      route-target export evpn 65199:1
      router-id 192.168.99.1
      redistribute connected
```

## BFD

### Router BFD

#### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 300 | 300 | 3 |

#### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 300 min-rx 300 multiplier 3
```

## Filters

### Prefix-lists

#### Prefix-lists Summary

##### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 10.254.99.0/30 eq 32 |

#### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 10.254.99.0/30 eq 32
```

### Route-maps

#### Route-maps Summary

##### RM-CONN-2-BGP

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY | extcommunity soo 10.254.99.1:0 additive | - | - |

##### RM-EVPN-EXPORT-VRF-DEFAULT

| Sequence | Type | Match | Set | Sub-Route-Map | Continue |
| -------- | ---- | ----- | --- | ------------- | -------- |
| 10 | permit | extcommunity ECL-EVPN-SOO | - | - | - |

#### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   set extcommunity soo 10.254.99.1:0 additive
!
route-map RM-EVPN-EXPORT-VRF-DEFAULT permit 10
   match extcommunity ECL-EVPN-SOO
```

### IP Extended Community Lists

#### IP Extended Community Lists Summary

| List Name | Type | Extended Communities |
| --------- | ---- | -------------------- |
| ECL-EVPN-SOO | permit | soo 10.254.99.1:0 |

#### IP Extended Community Lists Device Configuration

```eos
!
ip extcommunity-list ECL-EVPN-SOO permit soo 10.254.99.1:0
```

## ACL

### IP Access-lists

#### IP Access-lists Device Configuration

```eos
!
ip access-list sshACL1
   10 permit tcp 10.1.210.0/24 eq 22 10.1.220.0/24
```

## VRF Instances

### VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| prod | enabled |

### VRF Instances Device Configuration

```eos
!
vrf instance prod
```

## Platform

### Platform Summary

#### Platform Software Forwarding Engine Summary

| Settings | Value |
| -------- | ----- |
| Maximum CPU Allocation | 1 |

### Platform Device Configuration

```eos
!
platform sfe data-plane cpu allocation maximum 1
```

## System L1

### Unsupported Interface Configurations

| Unsupported Configuration | action |
| ---------------- | -------|
| Speed | error |
| Error correction | error |

### System L1 Device Configuration

```eos
!
system l1
   unsupported speed action error
   unsupported error-correction action error
```

## Application Traffic Recognition

### Applications

#### IPv4 Applications

| Name | Source Prefix | Destination Prefix | Protocols | Protocol Ranges | TCP Source Port Set | TCP Destination Port Set | UDP Source Port Set | UDP Destination Port Set | DSCP |
| ---- | ------------- | ------------------ | --------- | --------------- | ------------------- | ------------------------ | ------------------- | ------------------------ | ---- |
| APP-CONTROL-PLANE | PFX-LOCAL-VTEP-IP | - | - | - | - | - | - | - | - |
| IT-App | - | IT-AppDstPrefixes | udp | - | - | - | - | IT-AppDstPorts | - |
| Voice | VoiceHostsSrcPrefixes | VoiceHostsDstPrefixes | - | - | - | - | - | - | - |

### Application Profiles

#### Application Profile Name APP-PROFILE-CONTROL-PLANE

| Type | Name | Service |
| ---- | ---- | ------- |
| application | APP-CONTROL-PLANE | - |

#### Application Profile Name IT-APP

| Type | Name | Service |
| ---- | ---- | ------- |
| application | IT-App | - |

#### Application Profile Name Voice

| Type | Name | Service |
| ---- | ---- | ------- |
| application | Voice | - |

### Field Sets

#### L4 Port Sets

| Name | Ports |
| ---- | ----- |
| IT-AppDstPorts | 5003 |

#### IPv4 Prefix Sets

| Name | Prefixes |
| ---- | -------- |
| IT-AppDstPrefixes | 172.29.3.2/32 |
| PFX-LOCAL-VTEP-IP | 192.168.99.1/32 |
| VoiceHostsDstPrefixes | 172.29.2.2/32<br>172.29.5.2/32 |
| VoiceHostsSrcPrefixes | 172.29.2.2/32<br>172.29.5.2/32 |

### Router Application-Traffic-Recognition Device Configuration

```eos
!
application traffic recognition
   !
   application ipv4 APP-CONTROL-PLANE
      source prefix field-set PFX-LOCAL-VTEP-IP
   !
   application ipv4 IT-App
      destination prefix field-set IT-AppDstPrefixes
      protocol udp destination port field-set IT-AppDstPorts
   !
   application ipv4 Voice
      source prefix field-set VoiceHostsSrcPrefixes
      destination prefix field-set VoiceHostsDstPrefixes
   !
   application-profile APP-PROFILE-CONTROL-PLANE
      application APP-CONTROL-PLANE
   !
   application-profile IT-APP
      application IT-App
   !
   application-profile Voice
      application Voice
   !
   field-set ipv4 prefix IT-AppDstPrefixes
      172.29.3.2/32
   !
   field-set ipv4 prefix PFX-LOCAL-VTEP-IP
      192.168.99.1/32
   !
   field-set ipv4 prefix VoiceHostsDstPrefixes
      172.29.2.2/32 172.29.5.2/32
   !
   field-set ipv4 prefix VoiceHostsSrcPrefixes
      172.29.2.2/32 172.29.5.2/32
   !
   field-set l4-port IT-AppDstPorts
      5003
```

### Router Path-selection

#### Router Path-selection Summary

| Setting | Value |
| ------  | ----- |
| Dynamic peers source | STUN |

#### TCP MSS Ceiling Configuration

| IPV4 segment size | Direction |
| ----------------- | --------- |
| auto | ingress |

#### Path Groups

##### Path Group internet

| Setting | Value |
| ------  | ----- |
| Path Group ID | 101 |
| IPSec profile | CP-PROFILE |

###### Local Interfaces

| Interface name | Public address | STUN server profile(s) |
| -------------- | -------------- | ---------------------- |
| Ethernet1 | - |  |

###### Static Peers

| Router IP | Name | IPv4 address(es) |
| --------- | ---- | ---------------- |
| 192.168.99.2 | paypal1-pf2 | 172.16.99.17 |

##### Path Group LAN_HA

| Setting | Value |
| ------  | ----- |
| Path Group ID | 65535 |
| Flow assignment | LAN |

#### Load-balance Policies

| Policy Name | Jitter (ms) | Latency (ms) | Loss Rate (%) | Path Groups (priority) | Lowest Hop Count |
| ----------- | ----------- | ------------ | ------------- | ---------------------- | ---------------- |
| LB-DEFAULT-AVT-POLICY-CONTROL-PLANE | - | - | - | internet (1)<br>LAN_HA (1) | False |
| LB-DEFAULT-AVT-POLICY-DEFAULT | - | - | - | internet (1)<br>LAN_HA (1) | False |
| LB-PROD-AVT-POLICY-DEFAULT | - | - | - | internet (1)<br>LAN_HA (1) | False |
| LB-PROD-AVT-POLICY-IT-APP | - | - | - | internet (1)<br>LAN_HA (1) | False |
| LB-PROD-AVT-POLICY-Voice | - | - | - | internet (1)<br>LAN_HA (1) | False |

#### Router Path-selection Device Configuration

```eos
!
router path-selection
   peer dynamic source stun
   tcp mss ceiling ipv4 ingress
   !
   path-group internet id 101
      ipsec profile CP-PROFILE
      !
      local interface Ethernet1
      !
      peer static router-ip 192.168.99.2
         name paypal1-pf2
         ipv4 address 172.16.99.17
   !
   path-group LAN_HA id 65535
      flow assignment lan
   !
   load-balance policy LB-DEFAULT-AVT-POLICY-CONTROL-PLANE
      path-group internet
      path-group LAN_HA
   !
   load-balance policy LB-DEFAULT-AVT-POLICY-DEFAULT
      path-group internet
      path-group LAN_HA
   !
   load-balance policy LB-PROD-AVT-POLICY-DEFAULT
      path-group internet
      path-group LAN_HA
   !
   load-balance policy LB-PROD-AVT-POLICY-IT-APP
      path-group internet
      path-group LAN_HA
   !
   load-balance policy LB-PROD-AVT-POLICY-Voice
      path-group internet
      path-group LAN_HA
```

## Quality Of Service

### QOS

#### QOS Summary

QOS rewrite DSCP: **disabled**

#### QOS Device Configuration

```eos
!
```

### QOS Class Maps

#### QOS Class Maps Summary

| Name | Field | Value |
| ---- | ----- | ----- |
| class1 | acl | sshACL1 |

#### Class-maps Device Configuration

```eos
!
class-map type qos match-any class1
   match ip access-group sshACL1
```

### QOS Policy Maps

#### QOS Policy Maps Summary

##### policy1

| Class Name | COS | DSCP | Traffic Class | Drop Precedence | Police Rate (Burst) -> Action |
| ---------- | --- | -----| ------------- | --------------- | ----------------------------- |
| class1 | - | 32 | - | - | - |

#### QOS Policy Maps Device Configuration

```eos
!
policy-map type quality-of-service policy1
   class class1
      set dscp 32
```

## STUN

### STUN Server

| Server Local Interfaces | Bindings Timeout (s) | SSL Profile | SSL Connection Lifetime | Port |
| ----------------------- | -------------------- | ----------- | ----------------------- | ---- |
| Ethernet1 | - | - | - | 3478 |

### STUN Device Configuration

```eos
!
stun
   server
      local-interface Ethernet1
```

## EOS CLI Device Configuration

```eos
!
username cwomble secret *
username cwomble ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDOZFQIhHNghkuJryYiNyFUbkVPyGH2tU1gFuoJ/wDDg420VY9tb1OQn7k+XoDaVWWoEoOek07sJzns0Yy7WYUhgHP3T8Q3qW2DRjRDCUgUXnt9iW9N/axh4U4OP71UbWJNw3D6b5JE4EWt56okFcR6eSAyyKoYZvUAiCX1oUGVbRDz0cTNTbbnYHXp8DFBM/3fLNrO7Ntif+1ZtY8IQoZoDaOZpQLqTt40QGBAJgyXy0xP3urSaSJP2alSZP0g2IY9WebHaJAKnzP+SCuU4pMpcWYE3EoevYB6RLy12WylXq7Ht8sy2cjB9HH19BM4lNvRJ7ArjsL8enBP4OdqdyCH/SfLy6YrQ2EFidNpxnGBNVxIA7lkK82jLGFiqKJJNapZW4nRljT+KVMFEh/NTDP61wYmUPCR331+e3TiKsapwcIN/Q1+20WBVf11RseChjLqZzu54y9PDw/MA8ra8mPbuenhNJ6Xw8nkZbeUr+o/jZHwTP0sTLFyv4uJKvOACBc=
username ec2-user shell /bin/bash nopassword
username ec2-user ssh-key ssh-rsa ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQD0NRhYoVfQZwawep5MxXnhjHw+LQJEwvgukdY6MjXlx59Na18F1hRNLKaIBTBEKKIbKELFRRdZlynz9qmo7RP+68Wjd1RVPNk5rBoK1xf4GrbmPrLz7TkWYnfhOLG1wkX2h6KcAn6vtiqNrzltpsSYM94ja9kB65SFDc6Pz/3klMSuUnupo37fDPmV/L7fgTIxv79tOW6sf/1LU+cSWlkIlL2plu/YohAYydqFDTV7tEp9BCdV72BEhYRdzdMP3ZCzb68uMfVxNe4sOtQcu3t2uc/OwYTfDVDKpRkbUot5Td0wuLNYn7Jezssmsd8ImDv+TZE90NeW/r5EvPhpQ4KDDFwyOzKXuaUUlV98Xe8e6qnXSJSFpXkS4M/RPjYvc91uJxjAbwmouMtqn11ox5Jvoc9G+rTtlRezND949B6bEo74woVDL6RzlXt8/o/8KAHEiligrZZikOhCBD7kp9AE2DKecgFqGEF7lV2Vgipan1Dnceb2gjcZ0vIeWO8xzIc= nonroot@buildkitsandbox
username gcp-user secret *
username gcp-user ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGPEoZ2l67eEEwrlGfBAHPMx44IoqhyfjqXj2Ka4PxLuHgi1mv131VuCRlyWjOjddccyFUilfR1Bprdmd1Tj7o4Q11YQ138LOqFWJT3h0pxgHFdIHo70y4rI8aL15ixukZYa+g9KX8qTN+ZpFfea2d3CEFzMp+Y3xVPiWwLKzalq1JwT5J4MK2VHCbcnpN3zRON+gca/iZH9upA0WaXWJXNBnYXrgXFVGCJFk6Yl1ZXIGnEcKGe44c77zWgF4C66VhltsW999XD5vF31f6TTs25qxGScsiKMDg2uM1AzVg5KfxxhVy5HKd23YJJMytvUXL9h5Wq1HEEluSCcFtNI81
username mircea secret *
username mircea ssh-key ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQDw26o1dbfin+wgiYhiHybYebcYlS1EpucVdzfZASTkaMnCiaGy61mLtCaiZA82MEMNbkHLr9WgO2f9pHN2fiIiJc2gmlZPAUvSDzOHQapGuWzoPbeoKTaPyEzkDD5IzerV8wgMooaJOIWU9dWRjVPpUyj2GJ3JirC3HiLRnhkHFh3F+vUkEL81lMzJ/0HdnW3WrIjU6JnuOnpjiJ+np1OEPSbBdANT89tzaEm87QUioPQF7hHknKFUYK2Zqh5SXR6vQaLEcIhRqlAvZyjc95vDtYFWzqrdrHTdznyr8Hs/R2OeLmPGArGm6V8sGC9Q1bGfbhwjxvoWH9igUO6d82HKL2h8PJ1gXJU4XCb6Dkft7y0M4CDx6tIOo9jDxwFRtim9oC0uwxsRoXL4xCDYGH+jO4RAQSVxP6MQsJBEOvXez6whUev1lR91CiXmtUwQfzfmol03U8xMsBkdZ+Y4B7AkBUIpi/+8aEbMwRACyDZJB0+FzkYuWIYpiqoQ4pwUVw8=
username service shell /bin/bash secret sha512 $6$dCspVgQvOaoW3uL8$mj41FoMt981jOgBeNKNVW74q5gt.QExNr0gv7IbwAETzSps5nXUQyAzO96Ii787aJN4DX.zoRQYArzsnwztvl/
```
