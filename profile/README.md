# Aggrik8s-net
Aggrik8s-net provisions a `Kubernetes Edge Platform` ready to host IoT applications. The platform is a mesh of [Talos Kubernetes clusters](https://www.talos.dev/) ready to host applications (minus the CI/CD which is the next phase of the project).  Our clusters use [Cilium](https://www.cncf.io/projects/cilium/) to provide CNI functionality and [ROOK](https://rook.io/) to provide CSI services to the Kubernetes clusters. `Cilium` uses [eBPF](https://ebpf.io/) so observability and scalability features are essentially built in.  Future enhancements will use [CozyStack](https://github.com/cozystack/cozystack) to provide out of the box multi-tennancy and virtualizaion as a service.

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
