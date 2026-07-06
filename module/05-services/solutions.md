# Correction – Quiz Les Services

## Questions à choix multiples

### Question 1

**B. Fournir un point d'accès stable à une application**

---

### Question 2

**C. Grâce aux labels**

---

### Question 3

**C. ClusterIP**

---

### Question 4

**B. NodePort**

---

### Question 5

**D. LoadBalancer**

---

### Question 6

**A.**

```bash
kubectl get services
```

---

### Question 7

 **A. Définir le port utilisé par le conteneur**

---

### Question 8

 **B. Les adresses IP des Pods peuvent changer**

---

## Questions courtes

### Question 9

Le champ `port` correspond au port exposé par le Service. Le champ `targetPort` correspond au port sur lequel le conteneur écoute à l'intérieur du Pod.

---

### Question 10

Le type **ClusterIP** est utilisé pour permettre la communication entre applications à l'intérieur du cluster Kubernetes. Il n'est pas accessible depuis l'extérieur.

---

### Question 11

Les labels permettent au Service de sélectionner automatiquement les Pods vers lesquels il doit rediriger les requêtes.

---

### Question 12

Exemples de réponses :

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName
