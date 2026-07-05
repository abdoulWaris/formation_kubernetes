# Correction – Quiz Les Pods

## Questions à choix multiples

### Question 1

  C. Le Pod

---

### Question 2

  B. Un ou plusieurs conteneurs

---

### Question 3

  A. Une adresse IP

---

### Question 4

  B.

```bash
kubectl get pods
```

---

### Question 5

  C.

```bash
kubectl describe pod <nom-du-pod>
```

---

### Question 6

  B.

```bash
kubectl logs <nom-du-pod>
```

---

### Question 7

  B. Il n'est pas automatiquement recréé en cas de suppression ou de panne.

---

### Question 8

  B. Deployment

---

## Questions courtes

### Question 9

Un Pod est la plus petite unité déployable dans Kubernetes. Il encapsule un ou plusieurs conteneurs qui partagent les mêmes ressources réseau et, éventuellement, des volumes.

---

### Question 10

Exemples de réponses :

- `kubectl get pods`
- `kubectl describe pod <nom>`
- `kubectl logs <nom>`
- `kubectl exec -it <nom> -- /bin/bash`
- `kubectl delete pod <nom>`

---

### Question 11

Un Deployment permet de gérer automatiquement les Pods. Il peut recréer un Pod en cas de panne, gérer les mises à jour, le nombre de répliques et le scaling.

---

### Question 12

Les conteneurs d'un même Pod partagent :

- la même adresse IP ;
- le même espace réseau ;
- les ports ;
- les volumes définis dans le Pod (si présents).