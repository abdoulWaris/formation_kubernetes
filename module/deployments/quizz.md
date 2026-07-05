# Quiz – Les Deployments

## Questions à choix multiples

### Question 1

Quel est le rôle principal d'un Deployment ?

A. Stocker des données

B. Gérer automatiquement des Pods

C. Créer des Services

D. Gérer les utilisateurs

---

### Question 2

Quel objet est créé automatiquement par un Deployment ?

A. ConfigMap

B. Secret

C. ReplicaSet

D. Namespace

---

### Question 3

À quoi sert le champ `replicas` ?

A. Définir le nombre de nœuds du cluster

B. Définir le nombre de Pods souhaités

C. Définir le nombre de conteneurs dans un Pod

D. Définir le nombre de Services

---

### Question 4

Quelle commande permet d'afficher les Deployments ?

A.

```bash
kubectl get deployment
```

B.

```bash
kubectl list deployments
```

C.

```bash
kubectl get deployments
```

D.

```bash
kubectl describe deployments
```

---

### Question 5

Quelle commande permet de modifier le nombre de répliques d'un Deployment ?

A.

```bash
kubectl resize deployment
```

B.

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

C.

```bash
kubectl update deployment
```

D.

```bash
kubectl set replicas
```

---

### Question 6

Quelle commande permet de mettre à jour l'image d'un Deployment ?

A.

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.27
```

B.

```bash
kubectl image update
```

C.

```bash
kubectl apply image
```

D.

```bash
kubectl edit image
```

---

### Question 7

Quelle fonctionnalité permet de revenir à une version précédente d'un Deployment ?

A. Restart

B. Rollback

C. Rollout

D. Scaling

---

### Question 8

Que se passe-t-il si un Pod géré par un Deployment est supprimé ?

A. Rien

B. Le cluster s'arrête

C. Kubernetes recrée automatiquement un nouveau Pod

D. Le Deployment est supprimé

---

## Questions courtes

### Question 9

Expliquez le rôle d'un ReplicaSet.

---

### Question 10

Quelle est la différence entre un Pod et un Deployment ?

---

### Question 11

Pourquoi est-il recommandé d'utiliser plusieurs répliques pour une application ?

---

### Question 12

Citez deux avantages des Deployments par rapport aux Pods.