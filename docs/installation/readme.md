## Playgrounds Kubernetes

Si vous ne souhaitez pas installer Kubernetes sur votre ordinateur, il existe des **playgrounds en ligne** permettant d'utiliser un cluster Kubernetes directement depuis un navigateur web.

Ces plateformes sont particulièrement utiles pour :

- découvrir Kubernetes rapidement ;
- réaliser des exercices sans configuration locale ;
- suivre des tutoriels interactifs ;
- expérimenter des commandes `kubectl`.

### Plateformes recommandées

- **Killercoda** : propose des laboratoires interactifs avec des scénarios guidés et un véritable environnement Kubernetes accessible depuis le navigateur.

> **Remarque :** Les playgrounds sont très pratiques pour apprendre et réaliser des démonstrations. Toutefois, pour les travaux pratiques de cette formation, nous privilégierons une installation locale afin de se rapprocher des conditions rencontrées en entreprise et de mieux comprendre l'administration d'un cluster Kubernetes.

# Installation de Kubernetes

Il existe plusieurs façons d'installer Kubernetes selon votre besoin.

Cette formation présente les principales solutions utilisées en développement et en production.

| Distribution | Cas d'utilisation |
|--------------|------------------|
| Kind | Développement, tests, CI/CD |
| Minikube | Formation et développement local |
| Docker Desktop | Découverte rapide de Kubernetes |
| kubeadm | Installation d'un cluster Kubernetes en production |

## Quelle solution choisir ?

### 🟢 Débutant

 Docker Desktop

Installation rapide avec un cluster intégré.

---

### 🟢 Formation

Minikube

Simple à prendre en main et riche en fonctionnalités.

---

### 🟢 Développement

 Kind

Rapide, léger et idéal pour les travaux pratiques.

---

### 🟢 Production

kubeadm

Permet de créer un véritable cluster Kubernetes.

---

## Autres distributions Kubernetes

Cette formation se concentre sur les distributions pouvant être installées et utilisées localement.

Il existe également d'autres solutions Kubernetes destinées à des besoins spécifiques :

- **k3s** : une distribution Kubernetes légère, idéale pour les environnements Edge, l'IoT, les Raspberry Pi ou les petits clusters.
- **Azure Kubernetes Service (AKS)** : le service Kubernetes managé de Microsoft Azure.
- **Amazon Elastic Kubernetes Service (EKS)** : le service Kubernetes managé d'AWS.
- **Google Kubernetes Engine (GKE)** : le service Kubernetes managé de Google Cloud.

Ces solutions ne sont pas abordées dans cette partie de la formation, car elles nécessitent un compte cloud, des ressources d'infrastructure et peuvent engendrer des coûts. Elles feront l'objet d'une formation dédiée consacrée au déploiement de Kubernetes dans le cloud.

 ---

Choisissez ensuite le guide correspondant :

- installation/kind
- installation/minikube
- installation/docker-desktop
- installation/kubeadm