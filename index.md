Welcome to the DevOps and DevSecOps labs.

These are hands-on resources to help you learn DevOps, DevSecOps and Kubernetes.

## Pre-reqs

 - [Set up Kubernetes and a Git client](./setup/README.md) 
 - Download your repo
    - Open a terminal (PowerShell on Windows; any shell on Linux/macOS) 
    - Run: `git clone https://github.com/courselabs/kubernetes.git`
     - Open the folder: `cd kubernetes`
- _For advanced topics_
    - Install [Helm](https://helm.sh/docs/intro/install/), [ArgoCD](https://argoproj.github.io/argo-cd/getting_started/#2-download-argo-cd-cli) and [k3d](https://k3d.io/v4.4.8/#installation) command line tools
- _Optional_
    - Install [Visual Studio Code](https://code.visualstudio.com) (free - Windows, macOS and Linux) to browse the repo and documentation

## Core Kubernetes

- [Nodes](labs/nodes/README.md)
- [Pods](labs/pods/README.md)
- [Services](labs/services/README.md)
- [Deployments](labs/deployments/README.md)
- [ConfigMaps](labs/configmaps/README.md)

## Operating Kubernetes

- [Production readiness](labs/productionizing/README.md)
- [Monitoring](labs/monitoring/README.md)
- [Logging](labs/logging/README.md)

## Real Kubernetes

- [Troubleshooting](labs/troubleshooting/README.md)

## Continuous Integration and Continuous Deployment (CI/CD)

- [Helm](labs/helm/README.md)
- [GitHub Actions](labs/actions/README.md)

## Security in Depth

- [Static analysis](./labs/static-analysis/README.md)
- [Security scanning](./labs/scanning/README.md)
- [Building a golden image library](./labs/golden-images/README.md)
- [Container security controls](./labs/container-security/README.md)
