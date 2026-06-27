# ADR-0001: Infrastructure Provisioning Guidance

**Status:** Accepted
**Date:** 2026-06-27

## Context

The Hybrid Infrastructure Platform combines cloud resources in AWS with on-premises infrastructure hosted on a Proxmox virtualization server. As the platform grows, multiple tools could potentially provision and configure infrastructure, including Terraform, cloud-init, Ansible, and manual administration.

Without clearly defining the responsibility of each tool, the project risks configuration drift, duplicated effort, and inconsistent deployment practices.

One of the primary goals of this project is that the entire environment should be reproducible from source control with minimal manual intervention.

## Decision

Terraform will provision **everything it reasonably can**.

Infrastructure resources that can be declaratively managed by Terraform should always be provisioned through Terraform rather than created manually.

Configuration management and application deployment are explicitly outside Terraform's responsibility and will be delegated to other tools.

The responsibilities of each tool are defined as follows:

| Tool                      | Responsibility                                                                                                                    |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **Terraform**             | Provision infrastructure resources (AWS, Proxmox, networking, storage, IAM, virtual machines, cloud-init configuration)           |
| **Cloud-init**            | Perform first-boot initialization of virtual machines (users, SSH keys, package updates, bootstrap configuration)                 |
| **Ansible**               | Configure operating systems, install software, apply security hardening, deploy services, and manage ongoing system configuration |
| **GitHub Actions**        | Validate infrastructure, execute CI workflows, and automate deployment pipelines                                                  |
| **Manual Administration** | Limited to initial hardware installation, firmware updates, or tasks that cannot reasonably be automated                          |

## Consequences

### Positive

* Infrastructure is reproducible from source control.
* Reduces configuration drift.
* Encourages Infrastructure as Code best practices.
* Supports automated disaster recovery.
* Keeps infrastructure definitions version-controlled and reviewable.
* Mirrors common practices used by cloud and platform engineering teams.

### Trade-offs

* Initial setup may require additional effort to automate.
* Some Proxmox features or hardware-specific tasks may not be supported by Terraform providers.
* Not every administrative task can or should be automated.

## Guiding Principle

When introducing new infrastructure, ask the following questions in order:

1. Can Terraform provision this resource?
2. If not, can it be initialized with cloud-init?
3. If not, can Ansible configure it after provisioning?
4. Only if all of the above are impractical should the task require manual intervention.

## Examples

### Appropriate Terraform Responsibilities

* AWS VPCs
* Security Groups
* EC2 instances
* IAM resources
* S3 buckets
* Proxmox virtual machines
* Virtual machine networking
* Storage configuration
* Cloud-init configuration

### Appropriate Ansible Responsibilities

* Installing Docker
* Installing Kubernetes
* Configuring NGINX
* Deploying Prometheus and Grafana
* Applying SSH hardening
* Managing system packages
* Configuring application services

### Manual Tasks

* Installing Proxmox on bare metal
* BIOS and firmware updates
* Physical hardware replacement
* Network cabling
* Initial router configuration (until automation is feasible)

## Future Considerations

This decision should be revisited if additional provisioning tools are introduced (e.g., Kubernetes operators, Crossplane, or OpenTofu), or if Terraform providers gain support for infrastructure that currently requires manual configuration.

However, the underlying principle should remain unchanged:

> Infrastructure should be provisioned through declarative Infrastructure as Code whenever it is practical to do so.
