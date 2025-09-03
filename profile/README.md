# .github
Aggrik8s.net is a project to develop an MVC to develop Edge based Kubernetes applications. Edge based Kubernetes adds some complexity compared to cloud based offerings where the vendor provides most of the required platform engineering and operations tasks.  Edge based platform services can be provided in a Hybrid model using both a combination of onsite BareMetal and Cloud based services. We will rely on the declarative provisioning model to reduce the complexity of maintaining our MVC.

After reviewing several alternatives, the current focus is to build BareMetal Kubernetes clusters using:
- [rancherfederal/rke2-ansible](https://github.com/rancherfederal/rke2-ansible) on Raspberry Pi 5 SoC (ARM64),
- [siderolabs/talos](https://github.com/siderolabs/talos) on Proxmox (X864) based VMs,
- **TBD** an Apple Silicon based Automation toolchain to deploy both of the above on a MacBook.
Theese tools allow deployment of Kubernetes clusters to support research into security, scalability, and repeatability. 

Examples of businesses that have successfully monetized a Kubernetes based Edge strategy include:
- [Chick-fil-A - Enterprise Restaurant Compute](https://www.youtube.com/watch?v=H1mtCFNgK7k),
- [ROCHE - 10,000 Kubernetes clusters](https://www.youtube.com/watch?v=H1mtCFNgK7k).
Alas, no good deed goes unpunished. [Why Kubernetes Isn’t Always the Right Choice](https://www.youtube.com/watch?v=auPcq0460Ok) discusses the anti-pattern of deploying Kubernetes at the Edge. Their conclusions seem to be that the proper Automation and Orchestration strategy can make an Enterprise Edge look and work like a Cloud based environment.
