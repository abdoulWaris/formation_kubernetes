# TP — Comprendre l’architecture Kubernetes

## Objectif

Dans ce TP, tu vas explorer un cluster Kubernetes et identifier les composants de son architecture :

* Control Plane
* Worker Nodes
* Pods
* Services système

Tu vas utiliser uniquement `kubectl`.

---

## ⚙️ Prérequis

Avant de commencer, assure-toi que :

* Kubernetes est installé (Kind / Minikube / Docker Desktop)
* `kubectl` fonctionne

Vérification :

```bash id="checkkub"
kubectl version
kubectl cluster-info
kubectl get nodes
```

---

## 1. Observer les nœuds du cluster

```bash id="nodes1"
kubectl get nodes -o wide
```

### 🔍 Questions :

* Combien de nodes sont affichés ?
* Quel est leur rôle ?

---

## 2. Explorer les composants du cluster

```bash id="components1"
kubectl get pods -n kube-system
```

### 🔍 Questions :

* Quels pods sont liés au Control Plane ?
* Peux-tu repérer `etcd`, `scheduler`, `controller-manager` ?

---

## 3. Inspecter un node

```bash id="describe-node"
kubectl describe node <nom-du-node>
```

### 🔍 Questions :

* Quelle quantité de CPU est disponible ?
* Quelle quantité de mémoire est allouée ?
* Quels Pods tournent sur ce node ?

---

## 4. Comprendre le rôle du kube-system

```bash id="kubesys"
kubectl get namespaces
kubectl get pods -n kube-system
```

### 🔍 Questions :

* À quoi sert le namespace `kube-system` ?
* Pourquoi ces Pods sont-ils critiques ?

---

## 5. Observer l’état du cluster

```bash id="clusterinfo"
kubectl cluster-info
```

### 🔍 Questions :

* Quel composant est exposé comme point d’entrée principal ?
* Que peut-on déduire de ce résultat ?

---

## 6. Challenge (optionnel)

### 🔥 Trouver les Pods du Control Plane

Essaye d’identifier :

* API Server
* Scheduler
* Controller Manager
* etcd

💡 Indice :
Ils sont généralement dans le namespace `kube-system`.

---

## 📌 Conclusion

À la fin de ce TP, tu dois être capable de :

* Identifier les composants du Control Plane
* Lister les Worker Nodes
* Comprendre où tournent les services système
* Utiliser `kubectl` pour explorer un cluster
