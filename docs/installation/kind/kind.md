# Installation de Kubernetes

## Introduction

Avant de pouvoir déployer des applications sur Kubernetes, il est nécessaire de disposer d'un cluster.

Il existe plusieurs façons d'installer Kubernetes selon le contexte d'utilisation :

* apprentissage ;
* développement local ;
* tests ;
* production ;
* cloud.

Dans cette formation, nous utiliserons principalement **Kind** pour les travaux pratiques, car il est léger, rapide à installer et largement utilisé pour les tests et les environnements de développement.

---
# Ce qu'il faut retenir

À la fin de ce chapitre, vous serez capable de :

* expliquer les différentes distributions Kubernetes ;
* installer Docker ;
* installer kubectl ;
* installer Kind ;
* créer un cluster Kubernetes local ;
* vérifier que le cluster fonctionne correctement ;
* supprimer un cluster si nécessaire.
---

# Les prérequis

Avant de commencer, assurez-vous d'avoir installé les outils suivants :

* Git
* Docker Desktop ou Docker Engine
* kubectl
* Une distribution Kubernetes (Kind recommandé)

Vérifiez les versions installées :

```bash
docker --version
kubectl version --client
git --version
```

---

# Les différentes distributions Kubernetes

Il existe plusieurs distributions Kubernetes adaptées à différents besoins.

| Distribution   | Cas d'utilisation                    |
| -------------- | ------------------------------------ |
| Kind           | Développement et tests               |
| Minikube       | Formation et développement local     |
| Docker Desktop | Développement rapide                 |
| kubeadm        | Installation d'un cluster Kubernetes |
| k3s            | Clusters légers et Edge Computing    |
| AKS            | Kubernetes managé sur Azure          |
| EKS            | Kubernetes managé sur AWS            |
| GKE            | Kubernetes managé sur Google Cloud   |

Dans cette formation, nous utiliserons **Kind**.

---

# Pourquoi choisir Kind ?

Kind (**Kubernetes IN Docker**) permet de créer un cluster Kubernetes directement à l'intérieur de conteneurs Docker.

Ses principaux avantages sont :

* installation rapide ;
* faible consommation de ressources ;
* idéal pour les TP ;
* possibilité de créer plusieurs clusters ;
* très utilisé dans les pipelines CI/CD.

---

# Installation de Docker

Si Docker n'est pas installé :

Téléchargez Docker Desktop depuis :

https://www.docker.com/products/docker-desktop

Vérifiez ensuite l'installation :

```bash
docker version
```

---

# Installation de kubectl

## Windows

```powershell
winget install Kubernetes.kubectl
```

## macOS

```bash
brew install kubectl
```

## Linux

```bash
sudo snap install kubectl --classic
```

Vérification :

```bash
kubectl version --client
```

---

# Installation de Kind

## Windows

```powershell
winget install Kubernetes.kind
```

## macOS

```bash
brew install kind
```

## Linux

```bash
curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64

chmod +x kind

sudo mv kind /usr/local/bin/
```

Vérification :

```bash
kind version
```

---

# Création d'un cluster

Créer un cluster nommé **formation-k8s** :

```bash
kind create cluster --name formation-k8s
```

Après quelques instants, Kubernetes démarre.

---

# Vérifier le cluster

Lister les clusters Kind :

```bash
kind get clusters
```

Afficher les informations du cluster :

```bash
kubectl cluster-info
```

Lister les nœuds :

```bash
kubectl get nodes
```

Résultat attendu :

```text
NAME                         STATUS   ROLES           AGE
formation-k8s-control-plane  Ready    control-plane   2m
```

---

# Vérifier les composants système

Afficher les Pods système :

```bash
kubectl get pods -n kube-system
```

Vous devriez retrouver plusieurs composants, notamment :

* etcd
* kube-apiserver
* kube-controller-manager
* kube-scheduler
* CoreDNS

---

# Supprimer un cluster

Si vous souhaitez repartir de zéro :

```bash
kind delete cluster --name formation-k8s
```
---
