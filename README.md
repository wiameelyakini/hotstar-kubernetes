# 🚀 DevOps Lab – CI/CD Pipeline with Jenkins, SonarQube & Docker on AWS

> **Lab personnel DevOps** — Mise en place d'un pipeline CI/CD complet pour le déploiement d'une application Next.js (clone Hotstar) sur infrastructure AWS.

---

## 🎯 Objectif

Mettre en pratique un workflow DevOps de bout en bout : de l'intégration continue (Jenkins + SonarQube) à la conteneurisation (Docker) et au déploiement sur cluster Kubernetes managé (AWS EKS).

---

## 🛠️ Stack technique

| Catégorie | Outils |
|---|---|
| **CI/CD** | Jenkins (pipeline déclaratif Groovy) |
| **Qualité de code** | SonarQube + Quality Gates |
| **Sécurité** | Trivy (scan images Docker), OWASP Dependency Check |
| **Conteneurisation** | Docker, Docker Hub |
| **Orchestration** | Kubernetes, Amazon EKS |
| **Infrastructure** | AWS EC2, Security Groups, IAM |
| **IaC** | Terraform (provisioning serveur de monitoring) |
| **Monitoring** | Prometheus, Grafana, Blackbox Exporter |
| **Versioning** | Git, GitHub |

---

## ✅ Ce que j'ai implémenté

### Phase 1 — Infrastructure & outillage
- Provisioning d'une instance EC2 (Ubuntu) sur AWS
- Configuration des Security Groups (ouverture des ports Jenkins, SonarQube, Docker, SMTP...)
- Installation automatisée des outils via scripts shell : Jenkins, Docker, SonarQube (conteneur), kubectl, eksctl, Terraform, Trivy

### Phase 2 — Pipeline CI/CD Jenkins
- Intégration d'un **repository GitHub privé** via Personal Access Token
- Configuration des plugins Jenkins : SonarQube Scanner, NodeJS, OWASP Dependency Check, Docker Pipeline, Blue Ocean
- Rédaction du **Jenkinsfile déclaratif** (Groovy) couvrant les stages :
  - `Git Checkout`
  - `SonarQube Analysis` + Quality Gate
  - `OWASP Dependency Check`
  - `npm install`
  - `Trivy FS Scan`
  - `Docker Build & Push` (Docker Hub)
  - `Trivy Image Scan`
  - `Deploy to Container`
- Configuration des **alertes email** via Gmail SMTP (Jenkins post-build actions)

### Phase 3 — Déploiement Kubernetes (EKS)
- Création du cluster EKS via `eksctl`
- Application des manifests Kubernetes (`deployment` + `service` LoadBalancer)
- Vérification de l'**auto-healing** Kubernetes (suppression de pod et observation du redémarrage automatique)

---

## 📂 Structure du projet

```
├── Jenkinsfile              # Pipeline déclaratif CI/CD
├── Dockerfile               # Build de l'image applicative
├── K8S/
│   └── manifest.yml         # Deployment + Service Kubernetes
├── Terraform/               # Provisioning du serveur de monitoring
├── scripts/                 # Scripts d'installation des outils DevOps
└── promotheus_configfile.txt # Configuration Prometheus + Blackbox Exporter
```

---

## 📌 Points clés retenus

- L'importance des **Quality Gates** SonarQube pour bloquer un pipeline en cas de code non conforme
- La gestion des **credentials Jenkins** (tokens GitHub, Docker Hub, SonarQube) sans exposition dans le code
- La différence entre `NodePort` et `LoadBalancer` en Kubernetes pour l'exposition d'un service
- Le fonctionnement du **self-healing Kubernetes** : le cluster recrée automatiquement les pods supprimés pour maintenir le `replicaSet` souhaité

---

## 👩‍💻 Auteure

**Wiame EL YAKINI** — Ingénieure Infrastructure & DevOps

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/wiame-el-yakini/)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/wiameelyakini)
