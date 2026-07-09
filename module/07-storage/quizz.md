# Quiz – Les Volumes et le stockage persistant

## Questions à choix multiples

### Question 1

Pourquoi utilise-t-on un volume dans Kubernetes ?

A. Pour créer un Pod

B. Pour conserver ou partager des données

C. Pour exposer une application

D. Pour créer un Service

---

### Question 2

Que devient le système de fichiers d'un conteneur lorsqu'un Pod est supprimé ?

A. Il est conservé

B. Il est déplacé vers un autre Pod

C. Il est supprimé

D. Il est sauvegardé automatiquement

---

### Question 3

Quel type de volume est supprimé lorsque le Pod disparaît ?

A. PersistentVolume

B. PersistentVolumeClaim

C. emptyDir

D. NFS

---

### Question 4

Quel objet représente le stockage disponible dans un cluster Kubernetes ?

A. PersistentVolume

B. Pod

C. Deployment

D. ConfigMap

---

### Question 5

Quel objet est utilisé par une application pour demander du stockage ?

A. PersistentVolume

B. Service

C. PersistentVolumeClaim

D. ReplicaSet

---

### Question 6

Quel est le mode d'accès le plus courant ?

A. ReadOnlyMany

B. ReadWriteMany

C. ReadWriteOnce

D. WriteOnly

---

### Question 7

Quelle commande affiche les PersistentVolumes ?

A.

```bash
kubectl get pv
```

B.

```bash
kubectl get volume
```

C.

```bash
kubectl get storage
```

D.

```bash
kubectl get disk
```

---

### Question 8

Quel est le rôle d'un PersistentVolumeClaim ?

A. Créer un Pod

B. Créer un disque

C. Demander un espace de stockage

D. Exposer une application

---

## Questions courtes

### Question 9

Quelle est la différence entre un PersistentVolume et un PersistentVolumeClaim ?

---

### Question 10

Pourquoi un `emptyDir` n'est-il pas adapté pour une base de données ?

---

### Question 11

Citez deux modes d'accès aux PersistentVolumes.

---

### Question 12

Pourquoi est-il recommandé d'utiliser un PVC plutôt qu'un PV directement ?