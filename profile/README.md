# Welcome to Aggrik8s-net
## Purpose
This organization hosts several repositories which collectively provision a mesh of [Talos clusters](https://www.talos.dev/) ready to host application development.

The key repositories and their purpose are:
- [Aggrik8s-net/aggrik8s-fabric](https://github.com/Aggrik8s-net/aggrik8s-fabric) provisions VLAN based resources to support the cluster mesh,
- [Aggrik8s-net/aggrik8s-cluster](https://github.com/Aggrik8s-net/aggrik8s-cluster) spins up two (or more) clusters and automates the following tasks:
  - [Deploying Cilium on Talos](https://www.talos.dev/v1.11/kubernetes-guides/network/deploying-cilium/) is automated using both Terraform and BASH scripts,
  - [Ceph with Rook on Talos](https://www.talos.dev/v1.11/kubernetes-guides/configuration/ceph-with-rook/) is automated using Terraform and HELM,

### Talos
Using these repos we provision a Mikrotik & Proxmox based fabric which uses OSPF to route traffic between our VLANs. 
For development purposes we use Proxmox to spin up the following clusters:
  - `talos-east` on VLAN1500 which uses `192.168.15.0/24`,
  - `talos-west` on VLAN2000 which uses `192.168.20.0/24`.

Talos is our current development platform to deliver immutable clusters for the IoT Edge.
### Rancher Government RKE2
We also have a [Rancher Government RKE2](https://ranchergovernment.com/rke2) cluster running on Raspberry Pi 5 nodes.
  - `piCluster` on VLAN10 which uses `192.168.10.0/24`.

`piCluster` is our original Raspberry Pi 5 based cluster which will eventually be added as the third cluster in our mesh.
We use [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) to provision on the Pi5 nodes.
Several Ansible Playbooks developed on this platform have been verified to work on our Talos clusters. 
These playbooks will be added to this organization in the near future (after tidying up).

At this time, Talos does not run on Raspberry Pi 5 (only 4) and having a hybrid mesh seems like a noble goal (given time).
## Architecture
[Topology Aware Routing and Service Mesh across Clusters with Cluster Mesh](https://isovalent.com/blog/post/t://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/) includes the following high level view of our Talos Mesh.
<p align="center">
  <img src="https://cdn.sanity.io/images/xinsvxfu/production/d167e95632e405b09a6711e7d310067d9786db9a-1200x630.png?auto=format&q=80&fit=clip&w=1080" title="Aggrik8s Cluster Mesh - Cross Cluster Deployments" style="style=width:100%;height:100%;">
</p>
The Cluster Mesh allows both `Frontend` and `Backend` applications to have policy based access accross clusters.
An example `Canary Load Balancing` 
- [https://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/#using-ingress-for-multi-cluster-load-balancing(https://isovalent.com/blog/post/topology-aware-routing-and-service-mesh-across-clusters-with-cluster-mesh/#using-ingress-for-multi-cluster-load-balancing) B


Talos is a version of Linux purpose built to run Kubernetes. 
A single YAML file configures a machine as either a `controlplane` or `worker` node. 
`talosctl` is used to administer Linux on individual nodes and `kubectl` is used to administer the Kubernetes cluster.
As Talos does not include `sshd` all administration of the cluwster is done using declarative tooling.
Traditional OSF based administration tooling is not part of the Talos experience.

with  CNI functionality and [ROOK](https://rook.io/) to provide CSI services to the Kubernetes clusters. `Cilium` uses [eBPF](https://ebpf.io/) so observability and scalability features are essentially built in.  Future enhancements will use [CozyStack](https://github.com/cozystack/cozystack) to provide out of the box multi-tennancy and virtualizaion as a service.

[Top 20 Cilium Use Cases](https://isovalent.com/blog/post/top-20-cilium-use-cases/) describes the benefits of using Cilium as our platform `CNI`. [Isovalent Hubble](https://docs.cilium.io/en/stable/overview/intro/) gives deep observability into network traffic and []() the  us to mesh our which n  and support research into platform observability, security, scalability, and repeatability. [Cilium](https://www.cncf.io/projects/cilium/) uses [eBPF](https://ebpf.io/) to provide Kubernetes CNI services for our based clusters.[Isovalent Tetragon](https://github.com/cilium/tetragon) enables powerful real-time, eBPF-based Security Observability and Runtime Enforcement.

We will use the declarative provisioning mofdel to reduce the complexity of maintaining our IoT platform. Infrastructure provisioning will be done using Terraform and some shell and Ansible. Day-2 provisioning will typically use Ansible or Helm. All platform services will be able to be created, destroyed, and rebuilt to ensure data persistence is built into the services deployed on ephemeral resources. 

After reviewing several alternatives, the current focus is to build BareMetal Kubernetes clusters using:
- [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) on Raspberry Pi 5 SoC (ARM64),
- [siderolabs/talos](https://github.com/siderolabs/talos) on Proxmox (X864) based VMs,
- **TBD** an Apple Silicon based Automation toolchain to deploy both of the above on a MacBook.



Examples of businesses that have successfully monetized a Kubernetes based Edge strategy include:
- [Chick-fil-A - Enterprise Restaurant Compute](https://medium.com/chick-fil-atech/enterprise-restaurant-compute-f5e2fd63d20f),
- [ROCHE - 10,000 Kubernetes clusters](https://www.youtube.com/watch?v=H1mtCFNgK7k).

Alas, no good deed goes unpunished ... 

[Why Kubernetes Isn’t Always the Right Choice](https://www.youtube.com/watch?v=auPcq0460Ok) discusses the anti-pattern of deploying Kubernetes at the Edge. Their conclusions seem to be that the proper Automation and Orchestration strategy can make an Enterprise Edge look and work like a Cloud based environment.
