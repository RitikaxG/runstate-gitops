# runstate-gitops

**GitOps repository for deploying RunState to Kubernetes using Argo CD, External Secrets, and automated image updates.**

This repository contains the declarative Kubernetes manifests used to deploy RunState in a GitOps workflow. It separates application source code from deployment state and is responsible for infrastructure wiring, application deployment, secrets integration, ingress, and autoscaling.

---

## What it is

This repo manages the Kubernetes deployment state for **RunState**.

It includes:

- Argo CD application bootstrapping
- Kubernetes manifests for the RunState services
- image update flow through Argo CD Image Updater
- External Secrets integration
- ingress and autoscaling configuration

This repo works together with the main application repo:

- **App source:** [`runState`](https://github.com/RitikaxG/runState)
- **Deployment state:** `runstate-gitops`

---

## Core highlights

- **Argo CD GitOps workflow**
- **Kustomize-based app manifests**
- **Automated image updates**
- **External Secrets integration**
- **Ingress configuration**
- **Horizontal Pod Autoscaler**
- **Separation of app code and deployment state**
- **Production-style Kubernetes setup**

---

## Architecture

This repo is responsible for deploying and managing:

- **RunState API deployment**
- **monitoring-pusher**
- **worker-monitoring**
- **worker-status-change**
- **worker-notification**
- **ConfigMap + secrets wiring**
- **Ingress**
- **HPA**
- **Argo CD config**
- **Image Updater integration**

Deployment flow:

1. Code is pushed in the main application repo.
2. CI builds and pushes a new image.
3. GitOps repo tracks the image tag / desired image state.
4. Argo CD reconciles the cluster to match this repository.

---

## Key features

- Declarative Kubernetes manifests
- GitOps deployment with Argo CD
- Image automation flow
- External Secrets for runtime secrets
- Ingress-based access
- Horizontal scaling configuration
- Clear separation between development and deployment concerns

---

## Repo structure

```txt
runstate-gitops/
├── apps/
│   └── runstate/   # Application manifests for RunState
├── bootstrap/      # Argo CD bootstrap applications
└── infra/          # Supporting GitOps infrastructure configs
```

---

## Local usage

Clone the repo:

```bash
git clone https://github.com/RitikaxG/runstate-gitops.git
cd runstate-gitops
```

Update manifests or image references, then commit and push:

```bash
git add .
git commit -m "update runstate deployment"
git push
```

Argo CD will reconcile the cluster to match the repository state.

---

## Related repos

- **Main application repo:** [runState](https://github.com/RitikaxG/runState)

---

## What I learned

Through this repo, I learned how to:

- separate application code from deployment state,
- structure Kubernetes manifests cleanly,
- use Argo CD for GitOps-based deployment,
- integrate External Secrets into a Kubernetes workflow,
- automate image rollout through GitOps,
- think about deployment as a repeatable, declarative system.

This repo helped me understand how modern backend systems are not only built, but also shipped and operated.
