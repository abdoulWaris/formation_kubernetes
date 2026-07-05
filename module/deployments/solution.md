# Correction – Quiz Les Deployments

## Questions à choix multiples

### Question 1

   **B. Gérer automatiquement des Pods**

---

### Question 2

   **C. ReplicaSet**

---

### Question 3

   **B. Définir le nombre de Pods souhaités**

---

### Question 4

   **C.**

```bash
kubectl get deployments
```

---

### Question 5

   **B.**

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

---

### Question 6

   **A.**

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.27
```

---

### Question 7

   **B. Rollback**

---

### Question 8

   **C. Kubernetes recrée automatiquement un nouveau Pod**

---

## Questions courtes

### Question 9

Le ReplicaSet garantit qu'un nombre défini de Pods est toujours en cours d'exécution. Si un Pod est supprimé ou tombe en panne, il en crée automatiquement un nouveau.

---

### Question 10

Un **Pod** est la plus petite unité déployable de Kubernetes qui exécute un ou plusieurs conteneurs. Un **Deployment** est une ressource qui gère automatiquement les Pods, notamment leur création, leur mise à jour, leur mise à l'échelle et leur remplacement en cas de panne.

---

### Question 11

Utiliser plusieurs répliques améliore la disponibilité de l'application. Si un Pod devient indisponible, les autres continuent de répondre aux requêtes. Cela permet également de répartir la charge entre plusieurs instances.

---

### Question 12

Exemples de réponses :

- création automatique des Pods ;
- auto-réparation (Self-Healing) ;
- mise à l'échelle (Scaling) ;
- mises à jour progressives (Rolling Updates) ;
- retour à une version précédente (Rollback) ;
- meilleure disponibilité des applications.