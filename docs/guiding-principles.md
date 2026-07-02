# Guiding Principles

## 1. Infrastructure as Code First

Infrastructure should never be manually created if it can be provisioned using Terraform or other automation.

## 2. Reproducibility

The entire environment should be recoverable from source control.

Given replacement hardware and valid credentials, another engineer should be able to recreate the environment by following the documentation.

## 3. Git as the Source of Truth

Infrastructure definitions, configuration, documentation, diagrams, and automation scripts all live in the repository.

## 4. Modular Design

Each service should be independent and reusable.

Examples:

* Networking
* Monitoring
* VPN
* Storage
* Media

should all be deployable without affecting unrelated services.

## 5. Incremental Growth

The platform should evolve through small, self-contained **iterations** rather than large rewrites.

Each iteration should leave the platform in a functional state.

## 6. Documentation as Code

Every major component should include:

* Architecture diagram
* Purpose
* Deployment instructions
* Disaster recovery notes
* Networking information

## 7. Production Mindset

Whenever practical, configure the lab similarly to real production environments rather than taking shortcuts for a home lab.

The goal is to learn professional engineering practices rather than simply host applications.