# Quiz – Les Pods

## Questions à choix multiples

### Question 1

Quelle est la plus petite unité déployable dans Kubernetes ?

A. Le Node

B. Le Service

C. Le Pod

D. Le Deployment

---

### Question 2

Un Pod peut contenir :

A. Un seul conteneur uniquement

B. Un ou plusieurs conteneurs

C. Plusieurs machines virtuelles

D. Uniquement des images Docker

---

### Question 3

Les conteneurs d'un même Pod partagent :

A. Une adresse IP

B. Le même système d'exploitation

C. Un cluster Kubernetes

D. Une image Docker

---

### Question 4

Quelle commande permet d'afficher la liste des Pods ?

A.

```bash
kubectl pods
```

B.

```bash
kubectl get pods
```

C.

```bash
kubectl show pods
```

D.

```bash
kubectl list pods
```

---

### Question 5

Quelle commande affiche les informations détaillées d'un Pod ?

A.

```bash
kubectl logs
```

B.

```bash
kubectl get pod
```

C.

```bash
kubectl describe pod <nom-du-pod>
```

D.

```bash
kubectl inspect pod
```

---

### Question 6

Quelle commande permet d'afficher les logs d'un Pod ?

A.

```bash
kubectl get logs
```

B.

```bash
kubectl logs <nom-du-pod>
```

C.

```bash
kubectl describe logs
```

D.

```bash
kubectl print logs
```

---

### Question 7

Quel est le principal inconvénient d'un Pod créé directement en production ?

A. Il ne peut pas contenir de conteneur.

B. Il n'est pas automatiquement recréé en cas de suppression ou de panne.

C. Il ne peut pas utiliser d'image Docker.

D. Il ne peut pas communiquer sur le réseau.

---

### Question 8

Quel objet Kubernetes est généralement utilisé pour gérer les Pods en production ?

A. ConfigMap

B. Deployment

C. Secret

D. Namespace

---

## Questions courtes

### Question 9

Expliquez en une ou deux phrases ce qu'est un Pod.

---

### Question 10

Citez deux commandes utiles pour administrer un Pod.

---

### Question 11

Pourquoi est-il recommandé d'utiliser un Deployment plutôt qu'un Pod directement ?

---

### Question 12

Que partage l'ensemble des conteneurs présents dans un même Pod ?