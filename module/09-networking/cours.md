# Le réseau dans Kubernetes

## Introduction

Dans un cluster Kubernetes, les applications sont réparties dans plusieurs Pods pouvant être exécutés sur différents nœuds.

Pour fonctionner correctement, ces Pods doivent pouvoir communiquer entre eux, accéder aux Services et être joignables par les utilisateurs lorsque cela est nécessaire.

Kubernetes fournit un modèle réseau unifié qui simplifie ces communications, quelle que soit la localisation des Pods dans le cluster.

---

# Le modèle réseau Kubernetes

Kubernetes repose sur plusieurs principes fondamentaux :

- chaque Pod possède sa propre adresse IP ;
- tous les Pods peuvent communiquer entre eux sans traduction d'adresse (NAT) ;
- les Pods peuvent communiquer avec les Services ;
- les nœuds peuvent communiquer avec tous les Pods.

Cette architecture permet aux applications distribuées de fonctionner sans avoir à gérer la complexité du réseau sous-jacent.

---

# Communication entre les Pods

Chaque Pod reçoit une adresse IP unique lors de sa création.

Deux Pods peuvent communiquer directement en utilisant cette adresse IP.

Exemple :

```text
+-----------+          +-----------+
|  Pod A    | -------> |  Pod B    |
|10.244.0.2 |          |10.244.1.5 |
+-----------+          +-----------+
```

Cependant, les adresses IP des Pods sont temporaires.

Si un Pod est recréé, une nouvelle adresse IP lui est attribuée.

C'est pourquoi les applications utilisent généralement des Services plutôt que les adresses IP des Pods.

---

# Le DNS Kubernetes

Chaque cluster Kubernetes possède un service DNS (généralement CoreDNS).

Lorsqu'un Service est créé, un nom DNS lui est automatiquement associé.

Par exemple :

```text
api.default.svc.cluster.local
```

Les Pods peuvent alors communiquer en utilisant ce nom plutôt que l'adresse IP du Service.

Exemple :

```bash
curl http://api
```

Le DNS résout automatiquement le nom vers l'adresse IP correspondante.

---

# Les espaces de noms (Namespaces)

Les noms DNS tiennent compte du Namespace.

Exemple :

```text
frontend.default.svc.cluster.local

backend.production.svc.cluster.local
```

Deux Services portant le même nom peuvent donc coexister dans des Namespaces différents.

---

# Le rôle des Services

Les Pods étant temporaires, leur adresse IP change au cours du temps.

Les Services fournissent un point d'accès stable vers un ou plusieurs Pods.

Ils assurent également la répartition du trafic entre les différentes instances.

```text
Utilisateur
      │
      ▼
 Service
  /   |   \
 ▼    ▼    ▼
Pod1 Pod2 Pod3
```

---

# Les plugins CNI

Kubernetes ne gère pas directement le réseau.

Il s'appuie sur une interface appelée **Container Network Interface (CNI)**.

Le plugin CNI est chargé de :

- attribuer une adresse IP aux Pods ;
- permettre la communication entre les Pods ;
- connecter les Pods aux nœuds du cluster.

Parmi les plugins les plus utilisés :

- Calico
- Flannel
- Cilium
- Weave Net

Chaque plugin possède ses propres fonctionnalités et performances.

---

# Communication entre les nœuds

Lorsqu'un Pod souhaite communiquer avec un autre Pod situé sur un autre nœud, le plugin CNI établit automatiquement la connexion.

Le développeur n'a aucune configuration particulière à réaliser.

```text
+--------------------+
| Node 1             |
|  Pod A             |
+---------+----------+
          |
          |
========== Réseau ==========
          |
          |
+---------+----------+
| Node 2             |
|  Pod B             |
+--------------------+
```

---

# Vérifier le réseau

Afficher les Services :

```bash
kubectl get services
```

Afficher les Pods avec leur adresse IP :

```bash
kubectl get pods -o wide
```

Afficher le DNS :

```bash
kubectl get svc -n kube-system
```

---

# Bonnes pratiques

- Toujours communiquer via un Service.
- Éviter d'utiliser directement les adresses IP des Pods.
- Utiliser des Namespaces pour isoler les applications.
- Choisir un plugin CNI adapté à l'environnement.

---

# À retenir

- Chaque Pod possède une adresse IP unique.
- Les Pods peuvent communiquer entre eux.
- Les Services fournissent une adresse stable.
- CoreDNS permet la résolution des noms.
- Les plugins CNI assurent la connectivité du cluster.