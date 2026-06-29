# ☸️ Formation Kubernetes

Une formation complète sur **Kubernetes**, conçue pour apprendre progressivement l'orchestration de conteneurs, depuis les concepts fondamentaux jusqu'au déploiement d'applications en production.

Cette formation alterne **théorie**, **démonstrations**, **travaux pratiques**, **mini-projets** et **bonnes pratiques** afin de développer une compréhension approfondie de Kubernetes, et non uniquement de ses commandes.

---

# 📚 Table des matières

* À propos
* Objectifs de la formation
* Public visé
* Programme
* Distributions Kubernetes
* Prérequis
* Installation
* Structure du projet
* Déroulement des modules
* Ressources utiles
* Contribution
* Licence

---

# À propos

Kubernetes est aujourd'hui la plateforme de référence pour l'orchestration de conteneurs. Utilisé aussi bien par les startups que par les grandes entreprises, il permet de déployer, maintenir et faire évoluer des applications distribuées de manière fiable et automatisée.

Cette formation a été pensée pour permettre à chacun de :

* comprendre les principes de Kubernetes ;
* maîtriser son architecture interne ;
* apprendre à administrer un cluster ;
* déployer des applications modernes ;
* découvrir les bonnes pratiques utilisées en entreprise ;
* préparer les certifications Kubernetes (CKA, CKAD ou CKS).

Chaque module combine une partie théorique avec une mise en pratique immédiate afin de consolider les connaissances acquises.

---

# 🎯 Objectifs de la formation

À la fin de cette formation, vous serez capable de :

* Comprendre l'architecture complète de Kubernetes.
* Déployer et administrer un cluster Kubernetes.
* Concevoir des applications cloud-native.
* Déployer des microservices.
* Gérer le stockage et le réseau.
* Sécuriser un cluster.
* Superviser les applications.
* Automatiser les déploiements avec Helm et GitOps.
* Mettre en œuvre les bonnes pratiques de production.

---

# 👨‍💻 Public visé

Cette formation s'adresse à :

* Développeurs
* Administrateurs systèmes
* Ingénieurs DevOps
* Architectes Cloud
* Étudiants
* Toute personne souhaitant apprendre Kubernetes de manière progressive.

---

# 📖 Programme de la formation

La formation est organisée en plusieurs modules progressifs.

Chaque module comprend :

* 📚 Théorie
* 💻 Démonstrations
* 🧪 Travaux pratiques
* 🎯 Exercices
* 💡 Bonnes pratiques
* ❓ Quiz
* 🛠️ Défis de dépannage (Debug Labs)

Les principaux sujets abordés sont :

* Introduction à Kubernetes
* Architecture Kubernetes
* Pods
* ReplicaSets
* Deployments
* Services
* ConfigMaps
* Secrets
* Volumes
* Persistent Volumes
* StatefulSets
* DaemonSets
* Jobs & CronJobs
* Networking
* Ingress
* Helm
* RBAC
* Network Policies
* Monitoring
* Logging
* Autoscaling
* GitOps
* CI/CD
* Déploiement d'une architecture complète

---

# ☸️ Distributions Kubernetes

Selon votre environnement, plusieurs distributions sont disponibles.

## 🏠 Développement local

| Distribution   | Description              | Cas d'utilisation          |
| -------------- | ------------------------ | -------------------------- |
| Minikube       | Cluster Kubernetes local | Formation et développement |
| Kind           | Kubernetes dans Docker   | Tests, CI/CD               |
| Docker Desktop | Kubernetes intégré       | Développement rapide       |
| Podman Desktop | Alternative légère       | Développement              |

---

## 🚀 Production

| Distribution | Description               |
| ------------ | ------------------------- |
| kubeadm      | Installation officielle   |
| Kubespray    | Déploiement avec Ansible  |
| k3s          | Distribution légère       |
| RKE          | Kubernetes Rancher        |
| MicroK8s     | Kubernetes minimal Ubuntu |

---

## ☁️ Cloud Managé

* Azure Kubernetes Service (AKS)
* Amazon Elastic Kubernetes Service (EKS)
* Google Kubernetes Engine (GKE)
* Oracle Kubernetes Engine (OKE)

---

# 📋 Prérequis

Avant de commencer cette formation, il est recommandé de connaître :

* Linux
* Docker
* Les bases des réseaux
* Git
* La ligne de commande

Logiciels nécessaires :

* Docker
* kubectl
* Une distribution Kubernetes (Kind recommandé)

---

# ⚙️ Installation

Plusieurs options d'installation sont proposées :

* Docker Desktop
* Kind
* Minikube
* kubeadm
* k3s
* MicroK8s

Chaque méthode est documentée étape par étape dans le dossier **docs/**.

---

# 📂 Structure du projet

```text
formation-Kubernetes/
│
├── README.md
│
├── modules/
│   ├── 01-introduction/
│   ├── 02-architecture/
│   ├── 03-pods/
│   ├── 04-deployments/
│   ├── 05-services/
│   ├── 06-configmaps-secrets/
│   ├── 07-storage/
│   ├── 08-statefulsets/
│   ├── 09-networking/
│   ├── 10-ingress/
│   ├── 11-helm/
│   ├── 12-monitoring/
│   ├── 13-security/
│   ├── 14-cicd/
│   └── 15-projet-final/
│
├── manifests/
│
├── exercices/
│
├── solutions/
│
├── scripts/
│
├── docs/
│
├── images/
│
└── ressources/
```

---

# 📚 Déroulement d'un module

Chaque chapitre suit la même structure afin de faciliter l'apprentissage.

```text
Introduction

↓

Théorie

↓

Démonstration

↓

Travaux pratiques

↓

Exercices

↓

Débogage

↓

Quiz

↓

Bonnes pratiques
```

---

# 🧪 Partie pratique

Tout au long de la formation, vous apprendrez notamment à :

* créer des Pods ;
* déployer des applications ;
* exposer des services ;
* utiliser ConfigMaps et Secrets ;
* gérer le stockage persistant ;
* configurer le réseau ;
* installer Helm ;
* sécuriser un cluster ;
* superviser Kubernetes ;
* déployer une application complète en production.

Chaque chapitre contient plusieurs laboratoires pratiques inspirés de cas réels rencontrés en entreprise.

---

# 🛠️ Projet final

La formation se termine par la réalisation d'un projet complet intégrant notamment :

* plusieurs microservices ;
* une base de données persistante ;
* un Ingress ;
* Helm ;
* ConfigMaps ;
* Secrets ;
* RBAC ;
* Monitoring avec Prometheus et Grafana ;
* déploiement automatisé via CI/CD.

L'objectif est de mettre en pratique l'ensemble des notions étudiées au cours de la formation.

---

# 📖 Ressources utiles

- [Documentation officielle Kubernetes](https://kubernetes.io/docs/)
- [Kubernetes by Example](https://kubernetesbyexample.com/)
- [Play with Kubernetes](https://labs.play-with-k8s.com/)
- [Helm Documentation](https://helm.sh/docs/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/)
- [Kind Documentation](https://kind.sigs.k8s.io/)
- [kubeadm Documentation](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/)
- [k3s Documentation](https://k3s.io/)

---

# 🤝 Contribution

Les contributions sont les bienvenues ! Pour contribuer :

1. Fork le projet
2. Créer une branche pour votre fonctionnalité (`git checkout -b feature/AmazingFeature`)
3. Commit vos changements (`git commit -m 'Add some AmazingFeature'`)
4. Push vers la branche (`git push origin feature/AmazingFeature`)
5. Ouvrir une Pull Request

---

# 📄 Licence

Ce projet est distribué sous licence MIT.

---

## ✍️ Auteur

**abdoulWaris**

Formation réalisée dans un objectif pédagogique afin de partager les bonnes pratiques Kubernetes et de proposer un parcours complet mêlant théorie et pratique.
