# Hybrid Infrastructure Homelab

## Project Goal

Build a production-inspired hybrid cloud platform that combines cloud infrastructure with an on-prem virtualization cluster. All infrastructure should be reproducible, version-controlled, and deployed through Infrastructure as Code (IaC).

This project serves as a long-term learning lab and platform for cloud engineering, DevOps, networking, systems administration, and automation.

## Project Milestones

* [x] Install Proxmox and setup Ubuntu Template
* [] Use Terraform + Cloud Init to clone that template into a new VM
* [] Configure VM with Ansible
* [] Deploy first Docker stack (Pi-Hole, or Gitea, or similar)
* [] Refactor and add CI/CD to repo

## Guiding Principles

### 1. Infrastructure as Code First

Infrastructure should never be manually created if it can be provisioned using Terraform or other automation.

### 2. Reproducibility

The entire environment should be recoverable from source control.

Given replacement hardware and valid credentials, another engineer should be able to recreate the environment by following the documentation.

### 3. Git as the Source of Truth

Infrastructure definitions, configuration, documentation, diagrams, and automation scripts all live in the repository.

### 4. Modular Design

Each service should be independent and reusable.

Examples:

* Networking
* Monitoring
* VPN
* Storage
* Media

should all be deployable without affecting unrelated services.

### 5. Incremental Growth

The platform should evolve through small, self-contained **iterations** rather than large rewrites.

Each iteration should leave the platform in a functional state.

### 6. Documentation as Code

Every major component should include:

* Architecture diagram
* Purpose
* Deployment instructions
* Disaster recovery notes
* Networking information

### 7. Production Mindset

Whenever practical, configure the lab similarly to real production environments rather than taking shortcuts for a home lab.

The goal is to learn professional engineering practices rather than simply host applications.


## Wishlist

* S3 blob to store Terraform State (& other configs? Ansible?) remotely and securely
* Backup and redundancy tools
* SysAdmin Lab which includes the following VMs:
  * Windows 11
  * Rocky Linux (to practice RHEL sysadmin)
  * Ubuntu Linux
* Security lab which includes (multiple?) Kali Linux VM(s)
* Cluster for networking lab (could be combo of on-prem and cloud nodes)

## On-Prem Devices (Hardware)

* Lenovo ThinkCentre M720 (Mini PC)
* Raspberry Pi 5
* Windows PC (Main Workstation)
