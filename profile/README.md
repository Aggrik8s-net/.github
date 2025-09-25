# Welcome to Aggrik8s-net
## Organization Purpose
Host several repositories which collectively provision a mesh of [Talos clusters](https://www.talos.dev/) ready to support application development.
## Repositories
The key repositories and their purpose:
- [Aggrik8s-net/aggrik8s-fabric](https://github.com/Aggrik8s-net/aggrik8s-fabric) provision VLAN based resources to support our cluster mesh,
- [Aggrik8s-net/aggrik8s-cluster](https://github.com/Aggrik8s-net/aggrik8s-cluster) spins up two clusters with automation for these tasks:
  - [Deploying Cilium on Talos](https://www.talos.dev/v1.11/kubernetes-guides/network/deploying-cilium/) using both Terraform and BASH scripts,
  - [Ceph with Rook on Talos](https://www.talos.dev/v1.11/kubernetes-guides/configuration/ceph-with-rook/) using Terraform and HELM.
### Talos
We use these repos to provision our Mikrotik & Proxmox based network fabric. 

For development purposes, we are using Proxmox to spin up the following clusters:
  - `talos-east` on VLAN1500 which uses `192.168.15.0/24`,
  - `talos-west` on VLAN2000 which uses `192.168.20.0/24`.

Talos is our current development platform to deliver immutable clusters for the IoT Edge.
### Rancher Government RKE2
We also have a [Rancher Government RKE2](https://ranchergovernment.com/rke2) cluster running on Raspberry Pi 5 nodes mounted in a 6U travel rack.
  - `piCluster` on VLAN10 which uses `192.168.10.0/24`.

`piCluster` is our original Raspberry Pi 5 based cluster which will eventually be added as the third cluster in our mesh.

We use [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) to provision the Pi5 nodes.
Several Ansible Playbooks developed on this platform have been verified to work on our Talos clusters. 
Several of these playbooks will be added to this organization in the near future (after tidying up).

At this time, Talos does not run on Raspberry Pi 5 (only 4) and having a hybrid mesh seems like a noble goal (given time).
## Architecture
[Topology Aware Routing and Service Mesh across Clusters with Cluster Mesh](https://isovalent.com/blog/post/t://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/) provides a reference view of a Talos Mesh which we show below.
The mesh allows both `Frontend` and `Backend` applications to have policy based access across clusters. 
This dramatically simplifies operations workflows such as HA Failover and Canary Deployments. 
<p align="center">
  <img src="https://cdn.sanity.io/images/xinsvxfu/production/d167e95632e405b09a6711e7d310067d9786db9a-1200x630.png?auto=format&q=80&fit=clip&w=1080" title="Aggrik8s Cluster Mesh - Cross Cluster Deployments" style="style=width:100%;height:100%;">
</p>

[Canary Example 1: 25% / 75% Traffic Split Across Clusters with Failover](https://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/#canary-example-1-25-75-traffic-split-across-clusters-with-failover) describes the type of policy based traffic routing we can do across our mesh.