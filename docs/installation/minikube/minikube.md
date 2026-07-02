
# Installation de Minikube

## 🎯 Cas d’utilisation

Minikube est utilisé pour :

- apprendre Kubernetes ;
- tester des manifestes YAML ;
- développer en local ;
- simuler un cluster Kubernetes sur une machine personnelle.

---

## ⚙️ Prérequis

Avant d’installer Minikube, assurez-vous d’avoir :

- Docker installé (recommandé) ou un hyperviseur (VirtualBox, Hyper-V, etc.)
- kubectl installé
- Une machine avec :
  - 2 CPU minimum
  - 2 Go de RAM minimum (4 Go recommandé)

Vérification :

```bash
docker --version
kubectl version --client
````

---

## 📦 Installation

### macOS

```bash
brew install minikube
```

---

### Windows

```powershell
choco install minikube
```

ou

```powershell
winget install Kubernetes.minikube
```

---

### Linux

```bash
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

---

##  Démarrer un cluster

```bash
minikube start
```

Avec Docker comme driver :

```bash
minikube start --driver=docker
```

---

##  Vérification

```bash
minikube status
kubectl get nodes
```

---

## Dashboard

```bash
minikube dashboard
```

---

## Test rapide

Créer un deployment :

```bash
kubectl create deployment nginx --image=nginx
kubectl get pods
```

## Exposer le service :

```bash
kubectl expose deployment nginx --type=NodePort --port=80
minikube service nginx
```

---

## Suppression du cluster

```bash
minikube delete
```

---

