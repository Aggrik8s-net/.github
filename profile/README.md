# Welcome to Aggrik8s-net
## Organization Purpose
Host repositories to provision a mesh of [Talos clusters](https://www.talos.dev/) ready to use for application development.
## Repositories
The key repositories and their purpose:
1. [Aggrik8s-net/aggrik8s-fabric](https://github.com/Aggrik8s-net/aggrik8s-fabric) provision network resources to host our mesh,
2. [Aggrik8s-net/aggrik8s-cluster](https://github.com/Aggrik8s-net/aggrik8s-cluster) spin up two clusters with task automation for:
   - [Deploying Cilium on Talos](https://www.talos.dev/v1.11/kubernetes-guides/network/deploying-cilium/) using Terraform and BASH,
   - [Ceph with Rook on Talos](https://www.talos.dev/v1.11/kubernetes-guides/configuration/ceph-with-rook/) using Terraform and HELM.

We can reliably create and destroy Talos clusters but care needs to be taken with our network fabric.
## Architecture
[Canary Example 1: 25% / 75% Traffic Split Across Clusters with Failover](https://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/#canary-example-1-25-75-traffic-split-across-clusters-with-failover) describes a multi-cluster application rollout as shown below.

Cilium cluster mesh allows declarative policy to be deployed on `Frontend` and `Backend` applications for all meshed clusters.

This dramatically simplifies operations workflows such as HA Failover and Canary Deployments. 
<p align="center">
  <img src="https://cdn.sanity.io/images/xinsvxfu/production/c3c3ffc5e3706a0f9b8bb99a6f1387838f2d7211-1600x780.png?auto=format&q=80&fit=clip&w=2560" title="Aggrik8s Cluster Mesh - Cross Cluster Deployments" style="style=width:100%;height:100%;">
</p>

## Cluster Details
All of our Kubernetes clusters use [Aggrik8s-net/aggrik8s-fabric](https://github.com/Aggrik8s-net/aggrik8s-fabric) to provision all of our network resources.

We have two code bases with current development focused on Talos.
1. a Legacy Raspberry Pi 5 and Latte Panda Mu based RAW METAL cluster,
2. the Proxmox based Talos clusters provisioned using [Aggrik8s-net/aggrik8s-cluster](https://github.com/Aggrik8s-net/aggrik8s-cluster).

Only our Talos implementation is currently published in this organization.
### Talos
For development purposes, we are using Proxmox to spin up the following clusters:
- `talos-east` on VLAN1500 which uses `192.168.15.0/24`,
- `talos-west` on VLAN2000 which uses `192.168.20.0/24`.

Talos is our current development platform to deliver immutable clusters for the IoT Edge.
### Rancher Government RKE2
We also have a [Rancher Government RKE2](https://ranchergovernment.com/rke2) cluster running on Raspberry Pi 5 nodes mounted in a 6U travel rack.
- `piCluster` on VLAN10 which uses `192.168.10.0/24`.

`piCluster` is our original Raspberry Pi 5 based cluster which will eventually be added as the third cluster in our mesh.

We use [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) to provision the Pi5 nodes.

At this time, Talos does not run on Raspberry Pi 5 and having a hybrid mesh seems like a noble goal.
### Ansible Playbooks
Several Ansible Playbooks initially developed on `piNet` have been verified to work on our Talos mesh.
We will (eventually) publish a `Aggrik8s-net Day-2 repo` with a collection of Ansible Pplaybooks for replaybooks will be added to this organization in the near future (after tidying up).

