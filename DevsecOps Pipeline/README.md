# DevSecOps CI/CD Architecture Diagram (Build → Scan → Deploy)

```
┌────────────────────┐
│    Developer       │
│ (Code Commit / PR) │
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│   Git Repository   │
│ (GitHub / GitLab)  │
└─────────┬──────────┘
          │  Webhook
          ▼
┌──────────────────────────────────────────┐
│            CI Pipeline (Jenkins)          │
│                                          │
│  ┌──────────────┐                        │
│  │ Build Stage  │                        │
│  └──────┬───────┘                        │
│         │                                │
│  ┌──────▼─────────────┐                 │
│  │ Install Dependencies│                │
│  └──────┬─────────────┘                 │
│         │                                │
│  ┌──────▼─────────────┐                 │
│  │ Unit Tests +       │                 │
│  │ Code Coverage      │                 │
│  └──────┬─────────────┘                 │
│         │  coverage report               │
│  ┌──────▼─────────────┐                 │
│  │ SAST Analysis      │                 │
│  │ (SonarQube)        │                 │
│  │ + Quality Gate     │                 │
│  └──────┬─────────────┘                 │
│         │  PASS only                     │
│  ┌──────▼─────────────┐                 │
│  │ Docker Image Build │                 │
│  └──────┬─────────────┘                 │
│         │                                │
│  ┌──────▼─────────────┐                 │
│  │ Image Scan         │                 │
│  │ (Trivy)            │                 │
│  └──────┬─────────────┘                 │
│         │  No HIGH/CRIT CVEs             │
│  ┌──────▼─────────────┐                 │
│  │ Push Image         │                 │
│  │ (Docker Hub / ECR) │                 │
│  └──────┬─────────────┘                 │
└─────────┼───────────────────────────────┘
          │
          ▼
┌────────────────────┐
│   Deployment       │
│ (Kubernetes / EKS) │
└──────────────────
```
