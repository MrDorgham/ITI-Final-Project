# ITI Final Project

## Overview:

The ITI Final Project involves the creation of a private cluster, deployment of Jenkins, and application deployment using a Jenkins pipeline. Google Cloud Platform (GCP) serves as the cloud provider, with infrastructure provisioned through Terraform and Jenkins deployed on Google Kubernetes Engine (GKE) using Ansible.

- [Project Infrastructure](https://github.com/MrDorgham/ITI-Final-Project-Infrastructer)
- [Application](https://github.com/MrDorgham/ITI-Final-Project-App)

## Terraform Components:

The Terraform scripts include the setup of various components:

- Virtual Private Cloud (VPC)
- Two subnets (one for GKE and the other for private-bastion)
- GKE cluster
- Identity-Aware Proxy (IAP)
- NAT Gateway and Router
- Service Account
- Automation for private-bastion

https://documents.lucid.app/documents/aa5c849b-13e7-4c67-8bc4-3cf784fd1c3f/pages/0_0?a=1443&x=1&y=2490&w=1541&h=1305&store=1&accept=image%2F*&auth=LCA%20bc7f12573cba7cfbb94136313e5d82e1006e36d86ea013cad1d2e0a1b4528084-ts%3D1700739157

### Commands to run Terraform:

```bash
terraform init
terraform plan
terraform apply
```

To connect the private-bastion to GKE, obtain the "ProxyCommand" by running:

```bash
gcloud compute ssh private-bastion --dry-run private-bastion
```

Generate a key pair:

```bash
ssh-keygen -t rsa
```

SSH into the private-bastion and paste the public key in "/home/user/.ssh/authorized_keys".

### Commands to connect private-bastion to GKE:

```bash
gcloud auth login
gcloud container clusters get-credentials <cluster_name> --zone <zone> --project <project_name>
```

### Jenkins Slave Pod Commands:

- Reset Jenkins password: `passwd jenkins`
- Allow Docker access: `chmod 777 /var/run/docker.sock`
- Start SSH service: `service ssh start`
- Authenticate with GCP and GKE:

```bash
gcloud auth login
gcloud container clusters get-credentials <cluster_name> --zone <zone> --project <project_name>
```

Explore the project repositories for further details and documentation.

- [Project Infrastructure](https://github.com/MrDorgham/ITI-Final-Project-Infrastructer)
- [Application](https://github.com/MrDorgham/ITI-Final-Project-App)
