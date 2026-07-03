> **💡 Conseil**
>
> Cette méthode est présentée à titre informatif afin de découvrir l'installation officielle de Kubernetes.
> Les travaux pratiques de cette formation seront réalisés avec **Kind**, plus simple à installer et parfaitement adapté à un environnement de développement.

# Installation avec kubeadm

## 🎯 Cas d'utilisation

kubeadm est l'outil officiel recommandé par Kubernetes pour créer un cluster.

Il est principalement utilisé pour :

- créer un cluster Kubernetes sur une infrastructure physique ou virtuelle ;
- mettre en place un environnement proche de la production ;
- apprendre l'administration d'un cluster Kubernetes ;
- déployer Kubernetes dans un datacenter ou sur des machines virtuelles.

---

## ⚙️ Prérequis

Avant de commencer, assurez-vous de disposer de :

- Une ou plusieurs machines Linux (Ubuntu recommandé)
- Un utilisateur avec les droits `sudo`
- Un accès Internet
- Un minimum de :
  - 2 CPU
  - 2 Go RAM
  - 20 Go disque

> ⚠️ kubeadm n'est pas supporté sur Windows/macOS (utiliser une VM), dans le guide je vous montre comment installer Kubadm avec 1 master et 2 worker

---

## 🧠 Préparation du système (TOUTES LES MACHINES)

### Désactiver le swap

```bash
sudo swapoff -a
sudo sed -i '/swap/d' /etc/fstab
```

---

### Modules kernel Kubernetes

```bash
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter
```

---

### Configuration réseau sysctl

```bash
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

sudo sysctl --system
```

---

## 📦 Installation de containerd (TOUTES LES MACHINES)

```bash
sudo apt update
sudo apt install -y containerd
```

Configuration :

```bash
sudo mkdir -p /etc/containerd
containerd config default | sudo tee /etc/containerd/config.toml
```

Activer systemd cgroup :

```bash
sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/' /etc/containerd/config.toml
```

Redémarrer :

```bash
sudo systemctl restart containerd
sudo systemctl enable containerd
```

---

## ☸️ Installation kubeadm / kubelet / kubectl (TOUTES LES MACHINES)

```bash
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl gpg
```

Clé Kubernetes :

```bash
sudo mkdir -p /etc/apt/keyrings

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | \
sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes.gpg
```

Repository :

```bash
echo "deb [signed-by=/etc/apt/keyrings/kubernetes.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /" | \
sudo tee /etc/apt/sources.list.d/kubernetes.list
```

Installation :

```bash
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

---

## 🚀 Initialisation du cluster (MASTER UNIQUEMENT)

```bash
sudo kubeadm init --pod-network-cidr=192.168.0.0/16
```

---

## ⚙️ Configuration kubectl (MASTER)

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

---

## 🌐 Installation du réseau (CNI) (MASTER)

Exemple avec Calico :

```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/calico/v3.29.1/manifests/tigera-operator.yaml
```

---
> Si vous n'avez pas besoin de worker node vous pouvez rester là et exécuter les commandes de test pour verifier que votre cluster est bien installé
# Optionnel
---
## ➕ Ajout des Worker Nodes

Sur le master :

```bash
kubeadm token create --print-join-command
```

Puis exécuter sur chaque worker :

```bash
sudo kubeadm join <MASTER_IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

---

## 🔍 Vérification

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
NAME       STATUS   ROLES           AGE
master     Ready    control-plane   5m
```
ou 

```text
NAME       STATUS   ROLES           AGE
master     Ready    control-plane
worker-1   Ready    <none>
worker-2   Ready    <none>
```

Afficher les Pods système :

```bash
kubectl get pods -n kube-system
```

---

## 🧪 Test rapide

Créer un Deployment Nginx :

```bash
kubectl create deployment nginx --image=nginx
```

Vérifier son déploiement :

```bash
kubectl get deployments
kubectl get pods
```

Exposer le Deployment :

```bash
kubectl expose deployment nginx --type=NodePort --port=80
```

## 🧹 Reset cluster (optionnel)

```bash
sudo kubeadm reset
```

---

## 🧠 Résumé

kubeadm est l'outil officiel permettant d'installer un cluster Kubernetes sur une ou plusieurs machines Linux. Il offre une grande flexibilité et constitue un excellent choix pour comprendre le fonctionnement interne de Kubernetes et administrer un cluster proche des environnements de production.

 ## Liens 
 pour les plus curieux je vous invite à lire mon article medium sur le sujet où j'ai utilisé le cloud Azure et calico comme CNI: [installation-kubeadm-medium](https://medium.com/@wariskonate63/creating-kubernetes-cluster-using-azure-vms-409277cbf8d0/) 