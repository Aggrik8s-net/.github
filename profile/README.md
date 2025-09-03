# Aggrik8s-net
Aggrik8s-net hosts an Edge based Kubernetes IoT platform. The various repositories in this organization allow the deployment of meshed Kubernetes clusters to host applications and support research into platform observability, security, scalability, and repeatability. 

Edge based Kubernetes strategies trade off infrastructure complexity against scalability and repeatability.  Cloud based offerings shift some of the platform engineering and operations tasks back to the vendor.  Edge based applications can be composed in a Hybrid model using a mix of onsite BareMetal and Cloud based services.  Automating the platform administration allows us to focus on the application layer "sizzle".

We will rely on the declarative provisioning model to reduce the complexity of maintaining our IoT platform. Infrastructure provisioning will be done using Terraform and some shell and Ansible. Day-2 provisioning will typically use Ansible or Helm. All platform services will be able to be created, destroyed, and rebuilt to ensure data persistence is built into the services deployed on ephemeral resources. 

After reviewing several alternatives, the current focus is to build BareMetal Kubernetes clusters using:
- [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) on Raspberry Pi 5 SoC (ARM64),
- [siderolabs/talos](https://github.com/siderolabs/talos) on Proxmox (X864) based VMs,
- **TBD** an Apple Silicon based Automation toolchain to deploy both of the above on a MacBook.



Examples of businesses that have successfully monetized a Kubernetes based Edge strategy include:
- [Chick-fil-A - Enterprise Restaurant Compute](https://medium.com/chick-fil-atech/enterprise-restaurant-compute-f5e2fd63d20f),
- [ROCHE - 10,000 Kubernetes clusters](https://www.youtube.com/watch?v=H1mtCFNgK7k).

Alas, no good deed goes unpunished ... 

[Why Kubernetes Isn’t Always the Right Choice](https://www.youtube.com/watch?v=auPcq0460Ok) discusses the anti-pattern of deploying Kubernetes at the Edge. Their conclusions seem to be that the proper Automation and Orchestration strategy can make an Enterprise Edge look and work like a Cloud based environment.
