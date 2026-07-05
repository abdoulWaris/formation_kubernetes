# Architecture Kubernetes

## Introduction

Kubernetes repose sur une architecture distribuée conçue pour gérer des applications conteneurisées à grande échelle.

Son objectif principal est de **maintenir en permanence l’état souhaité du système**, même en cas de panne d’une machine ou d’un conteneur.

Pour cela, Kubernetes est divisé en deux grandes parties :

* le **Control Plane** (qui pilote le cluster)
* les **Worker Nodes** (qui exécutent les applications)

---

# Vue globale de l’architecture

```text id="archk8s01"
                +----------------------+
                |    Control Plane     |
                |----------------------|
                | API Server           |
                | Scheduler            |
                | Controller Manager   |
                | etcd                 |
                +----------+-----------+
                           |
        -----------------------------------------
        |                   |                   |
        v                   v                   v

+-------------+   +-------------+   +-------------+
| Worker Node |   | Worker Node |   | Worker Node |
|-------------|   |-------------|   |-------------|
| kubelet     |   | kubelet     |   | kubelet     |
| kube-proxy  |   | kube-proxy  |   | kube-proxy  |
| Pods        |   | Pods        |   | Pods        |
+-------------+   +-------------+   +-------------+
```

---

# 1. Le Control Plane

Le Control Plane est le **cerveau de Kubernetes**.

Il prend toutes les décisions concernant le cluster.

## 1.1 API Server

* Point d’entrée principal de Kubernetes
* Reçoit toutes les requêtes (`kubectl`, API, CI/CD)
* Valide et traite les demandes

👉 Exemple :

```bash
kubectl apply -f deployment.yaml
```

Cette commande passe d’abord par l’API Server.

---

## 1.2 Scheduler

* Décide où exécuter les Pods
* Analyse les ressources disponibles (CPU, RAM)
* Assigne chaque Pod à un Worker Node

👉 Exemple :

* Node A = trop chargé
* Node B = libre
  → Scheduler choisit Node B

---

## 1.3 Controller Manager

* Surveille l’état du cluster
* Corrige automatiquement les différences entre :

  * état souhaité
  * état réel

👉 Exemple :

* 3 replicas demandés
* 1 pod tombe
  → il en recrée automatiquement 2

---

## 1.4 etcd

* Base de données distribuée de Kubernetes
* Stocke tout l’état du cluster :

  * pods
  * configurations
  * secrets
  * nodes

👉 C’est la “source de vérité” du cluster

---

# 2. Les Worker Nodes

Les Worker Nodes exécutent réellement les applications.

---

## 2.1 kubelet

* Agent principal sur chaque node
* Communique avec le Control Plane
* Lance et surveille les Pods

---

## 2.2 kube-proxy

* Gère le réseau dans le cluster
* Permet la communication entre Pods et Services
* Gère les règles de routage

---

## 2.3 Container Runtime

* Exécute les conteneurs
* Exemples :

  * containerd
  * CRI-O
  * Docker (anciennement)

---

## 2.4 Pods

* Plus petite unité Kubernetes
* Contient 1 ou plusieurs conteneurs
* Partage réseau et stockage

---

# 3. Fonctionnement global

Kubernetes fonctionne selon un cycle simple :

```text id="loopk8s"
Utilisateur (kubectl)
        ↓
API Server
        ↓
etcd (stockage de l’état)
        ↓
Scheduler (choix du node)
        ↓
kubelet (exécution)
        ↓
Pods lancés
```

---

# 4. Principe clé : l’état désiré

Kubernetes ne fonctionne pas en mode “commande”, mais en mode **déclaratif**.

Tu ne dis pas :

> “Lance un conteneur”

Tu dis :

> “Je veux 3 instances de mon application”

Et Kubernetes s’occupe du reste.

---

# 5. Exemple concret

Si tu écris :

```yaml
replicas: 3
```

Et qu’un pod crash :

👉 Kubernetes détecte la différence
👉 Il recrée automatiquement un pod
👉 Le cluster revient à l’état désiré

---

# 6. Résumé des composants

| Composant          | Rôle                     |
| ------------------ | ------------------------ |
| API Server         | Entrée du cluster        |
| Scheduler          | Placement des Pods       |
| Controller Manager | Auto-correction          |
| etcd               | Stockage de l’état       |
| kubelet            | Exécution des Pods       |
| kube-proxy         | Réseau                   |
| Container runtime  | Exécution des conteneurs |

---

# Ce qu’il faut retenir

* Kubernetes est séparé en Control Plane et Worker Nodes
* Le Control Plane prend les décisions
* Les Worker Nodes exécutent les applications
* etcd stocke l’état du cluster
* Kubernetes fonctionne en mode déclaratif (état souhaité)

---