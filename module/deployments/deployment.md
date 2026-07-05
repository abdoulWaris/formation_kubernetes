# Les Deployments

## Introduction

Dans le chapitre précédent, nous avons appris à créer un Pod.

Bien qu'il soit possible de déployer directement un Pod, cette pratique est rarement utilisée en production. En effet, un Pod est une ressource éphémère : s'il est supprimé ou si le nœud sur lequel il s'exécute tombe en panne, Kubernetes ne le recrée pas automatiquement.

Pour résoudre ce problème, Kubernetes propose le **Deployment**.

Le Deployment est l'une des ressources les plus utilisées de Kubernetes. Il permet de déployer, mettre à jour et administrer automatiquement des Pods.

---

## Pourquoi utiliser un Deployment ?

Un Deployment apporte plusieurs fonctionnalités essentielles :

- création automatique des Pods ;
- auto-réparation (Self-Healing) ;
- mise à l'échelle (Scaling) ;
- mises à jour progressives (Rolling Updates) ;
- retour à une version précédente (Rollback).

Le Deployment garantit que le nombre de Pods souhaité est toujours disponible.

---

## Fonctionnement

Un Deployment ne crée pas directement les Pods.

Il crée un **ReplicaSet**, qui lui-même crée les Pods.

L'architecture est donc la suivante :

```text
Deployment
      │
      ▼
 ReplicaSet
      │
      ▼
     Pods
```

Dans la majorité des cas, l'utilisateur manipule uniquement le Deployment.

---

## Création d'un Deployment

Exemple :

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
  replicas: 3

  selector:
    matchLabels:
      app: nginx

  template:

    metadata:
      labels:
        app: nginx

    spec:
      containers:
        - name: nginx
          image: nginx:latest

          ports:
            - containerPort: 80
```

---

## Comprendre le manifeste

### replicas

```yaml
replicas: 3
```

Indique que trois Pods doivent toujours être disponibles.

---

### selector

```yaml
selector:
  matchLabels:
    app: nginx
```

Permet au Deployment d'identifier les Pods qu'il gère.

---

### template

Le template décrit le modèle utilisé pour créer chaque Pod.

Tout Pod créé par ce Deployment sera identique à ce modèle.

---

## Les principales commandes

Créer un Deployment :

```bash
kubectl apply -f deployment.yaml
```

Lister les Deployments :

```bash
kubectl get deployments
```

Lister les ReplicaSets :

```bash
kubectl get replicasets
```

Lister les Pods :

```bash
kubectl get pods
```

---

## Mise à l'échelle (Scaling)

Augmenter le nombre de Pods :

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Réduire le nombre de Pods :

```bash
kubectl scale deployment nginx-deployment --replicas=2
```

Kubernetes crée ou supprime automatiquement les Pods nécessaires.

---

## Mise à jour

Modifier l'image utilisée :

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.27
```

Vérifier le déploiement :

```bash
kubectl rollout status deployment/nginx-deployment
```

---

## Rollback

Afficher l'historique :

```bash
kubectl rollout history deployment/nginx-deployment
```

Revenir à la version précédente :

```bash
kubectl rollout undo deployment/nginx-deployment
```

---

## Suppression

Supprimer un Deployment :

```bash
kubectl delete deployment nginx-deployment
```

Le ReplicaSet et les Pods associés sont également supprimés.

---

## Bonnes pratiques

- Utiliser un Deployment pour les applications stateless.
- Définir plusieurs répliques afin d'assurer la haute disponibilité.
- Utiliser des images versionnées (`nginx:1.27`) plutôt que `latest`.
- Effectuer les mises à jour avec les mécanismes de rollout.

---

## À retenir

- Un Deployment gère automatiquement les Pods.
- Il crée un ReplicaSet qui maintient le nombre souhaité de Pods.
- Il permet le scaling, les mises à jour et les rollbacks.
- C'est la ressource la plus utilisée pour déployer une application sur Kubernetes.