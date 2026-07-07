# Quiz – Les ConfigMaps et les Secrets

## Questions à choix multiples

### Question 1

Quel est le rôle principal d'un ConfigMap ?

A. Stocker des images Docker

B. Stocker des données de configuration

C. Gérer les Pods

D. Gérer le réseau

---

### Question 2

Quel objet Kubernetes est destiné à stocker des informations sensibles ?

A. Service

B. Deployment

C. Secret

D. ReplicaSet

---

### Question 3

Les données d'un Secret sont généralement stockées :

A. En texte brut

B. Chiffrées automatiquement

C. Encodées en Base64

D. Compressées

---

### Question 4

Quelle commande permet d'afficher les ConfigMaps ?

A.

```bash
kubectl get configmaps
```

B.

```bash
kubectl get secrets
```

C.

```bash
kubectl get configs
```

D.

```bash
kubectl list configmaps
```

---

### Question 5

Quelle commande permet d'afficher les Secrets ?

A.

```bash
kubectl get secret
```

B.

```bash
kubectl get secrets
```

C.

```bash
kubectl show secrets
```

D.

```bash
kubectl list secrets
```

---

### Question 6

Comment un ConfigMap peut-il être utilisé dans un Pod ?

A. Comme variable d'environnement

B. Comme volume

C. Les deux

D. Aucun des deux

---

### Question 7

Parmi les informations suivantes, laquelle devrait être stockée dans un Secret ?

A. Le nom de l'application

B. Le port HTTP

C. Une clé API

D. L'environnement (dev, test, prod)

---

### Question 8

Pourquoi est-il préférable d'utiliser un ConfigMap plutôt que de modifier directement l'image Docker ?

A. Pour réduire la taille de l'image

B. Pour séparer la configuration de l'application

C. Pour accélérer Kubernetes

D. Pour créer plus de Pods

---

## Questions courtes

### Question 9

Quelle est la différence entre un ConfigMap et un Secret ?

---

### Question 10

Pourquoi les Secrets utilisent-ils Base64 ?

---

### Question 11

Citez deux exemples d'informations pouvant être stockées dans un ConfigMap.

---

### Question 12

Citez deux exemples d'informations devant être stockées dans un Secret.