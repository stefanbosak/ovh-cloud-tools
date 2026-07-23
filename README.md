<div align="center">

# ☁️ OVH Cloud Tools

**OVHcloud ecosystem CLI tools (Hardened)**

[![build_status_badge](../../actions/workflows/docker-image-native-multiplatform-pipeline.yaml/badge.svg?branch=main)](.github/workflows/docker-image-native-multiplatform-pipeline.yaml)
[![OVHcloud](https://img.shields.io/badge/OVHcloud-000E9C?style=flat-square)](https://www.ovhcloud.com/)

</div>

---

## 📦 Latest Build

<!-- VERSION_INFO_START -->
| Component | Version |
|-----------|---------|
| **Ansible** | [`v2.21.2`](https://github.com/ansible/ansible/releases/tag/v2.21.2) |
| **cert-manager CLI** | [`v2.5.0`](https://github.com/cert-manager/cmctl/releases/tag/v2.5.0) |
| **Helm** | [`v4.2.3`](https://github.com/helm/helm/releases/tag/v4.2.3) |
| **K9s** | [`v0.51.0`](https://github.com/derailed/k9s/releases/tag/v0.51.0) |
| **Kops** | [`v1.36.0`](https://github.com/kubernetes/kops/releases/tag/v1.36.0) |
| **Kubectl** | [`v1.36.3`](https://github.com/kubernetes/kubernetes/releases/tag/v1.36.3) |
| **Kustomize** | [`5.8.1`](https://github.com/kubernetes-sigs/kustomize/releases/tag/kustomize/v5.8.1) |
| **OVHcloud CLI** | [`v0.12.0`](https://github.com/ovh/ovhcloud-cli/releases/tag/v0.12.0) |
| **SwarmCLI** | [`v1.13.0-rc4`](https://github.com/Eldara-Tech/swarmcli/releases/tag/v1.13.0-rc4) |
| **Terraform** | [`1.16.0-beta1`](https://github.com/hashicorp/terraform/releases/tag/v1.16.0-beta1) |
| **Terragrunt** | [`v1.1.1`](https://github.com/gruntwork-io/terragrunt/releases/tag/v1.1.1) |

> 🔄 Last updated: 2026-07-23T20:41:48+02:00 · [Build #18](https://github.com/stefanbosak/ovh-cloud-tools/actions/runs/30042526904)
<!-- VERSION_INFO_END -->

---

## 📋 Overview

This repository provides a fully automated preparation of <span style="color: #0969da;">**containerized**</span> [OVHcloud](https://www.ovhcloud.com/) environment.

### Covered CLI tools

| Tool | Description |
|------|-------------|
| [Ansible CLI](https://docs.ansible.com/ansible/latest/command_guide/command_line_tools.html) | <span style="color: #8250df;">Configuration management and automation</span> |
| [OVHcloud CLI](https://github.com/ovh/ovhcloud-cli) | <span style="color: #8250df;">Official unified command-line interface for OVHcloud products and account resources</span> |
| [cert-manager CLI](https://github.com/cert-manager/cmctl/) | <span style="color: #d73a49;">cert-manager CLI</span> |
| [CNPG CLI](https://github.com/cloudnative-pg/cloudnative-pg/) | <span style="color: #d73a49;">CloudNativePG CLI</span> |
| [HELM CLI](https://helm.sh/docs/helm/) | <span style="color: #0969da;">Kubernetes package manager</span> |
| [kops CLI](https://kops.sigs.k8s.io/) | <span style="color: #0969da;">Kubernetes cluster management</span> |
| [kubectl CLI](https://kubernetes.io/docs/reference/kubectl/) | <span style="color: #0969da;">Kubernetes command-line tool</span> |
| [Kustomize CLI](https://kubectl.docs.kubernetes.io/references/kustomize/) | <span style="color: #0969da;">Kubernetes native configuration management</span> |
| [k9s CLI](https://k9scli.io/) | <span style="color: #0969da;">Terminal UI for Kubernetes</span> |
| [SwarmCLI](https://github.com/Eldara-Tech/swarmcli) | <span style="color: #0969da;">Terminal UI for Docker Swarm</span> |
| [Terraform CLI](https://developer.hashicorp.com/terraform/cli) | <span style="color: #1a7f37;">Infrastructure as Code tool</span> |
| [Terragrunt CLI](https://terragrunt.gruntwork.io/) | <span style="color: #1a7f37;">Terraform wrapper for DRY configurations</span> |

> [!NOTE]
> Every script and file is reasonably well commented and relevant details can be found there.

> [!IMPORTANT]
> Check details before taking any action.

> [!CAUTION]
> User is responsible for any modification and execution of any parts from this repository.

---

## ⚡ Zero Effort Approach

GitHub Actions workflow file covers all necessary activities which are fully automated in GitHub (re-using Docker container approach as base for automation):

- <span style="color: #1a7f37;">Gathering and propagating latest available tool version to Docker preparation process</span>
- <span style="color: #0969da;">Building Docker hardened image</span>

---

## 🐳 Docker Container Approach

Docker build wrapper covers creation of a container built from a multistage Dockerfile using a dedicated builder stage to keep the tool preparation isolated and reproducible. Generated image contains the OVHcloud CLI with pre-enabled Bash completion.

| File | Description |
|------|-------------|
| [`Dockerfile`](Dockerfile) | <span style="color: #0969da;">Recipe for preparation of Docker container</span> |

### 🏗️ Container Images

| Registry | Network Support | Pull Command |
|----------|----------------|--------------|
| [**DockerHub CR**](https://hub.docker.com/r/developmententity/ovh-cloud-tools) | <span style="color: #1a7f37;">IPv4 & IPv6</span> | `docker pull developmententity/ovh-cloud-tools:initial` |
| [**GitHub CR**](https://github.com/users/stefanbosak/packages/container/package/ovh-cloud-tools) | <span style="color: #8250df;">IPv4 only</span> | `docker pull ghcr.io/stefanbosak/ovh-cloud-tools:initial` |

---

## 🌍 OVHcloud Environment

OVHcloud environment can be used via the `ovh-cloud-tools` container which is automatically generated and available within `ghcr.io`. Authenticate once inside the container and re-use the CLI directly:

```bash
ovhcloud login
```

Check out the [authentication documentation](https://github.com/ovh/ovhcloud-cli/blob/main/doc/authentication.md) for API credentials, configuration file (`~/.ovh.conf`), and environment variable based authentication options. Multiple accounts can be managed via [profiles](https://github.com/ovh/ovhcloud-cli/blob/main/doc/profiles.md):

```bash
ovhcloud config profile switch <name>
```

> [!NOTE]
> `ovhcloud-cli` ([ovh/ovhcloud-cli](https://github.com/ovh/ovhcloud-cli)) is the official CLI covering the full range of OVHcloud products (Public Cloud, Bare Metal, VPS, IAM, DNS, and more) — see the [available products table](https://github.com/ovh/ovhcloud-cli#available-products) upstream for current coverage.

---

<div align="center">

<span style="color: #8250df;">**Made with ❤️ for ☁️ OVHcloud ecosystem and 🔒 security**</span>

</div>
