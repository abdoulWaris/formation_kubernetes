# Correction – Quiz Les Volumes

## Questions à choix multiples

### Question 1

  **B. Pour conserver ou partager des données**

---

### Question 2

  **C. Il est supprimé**

---

### Question 3

  **C. emptyDir**

---

### Question 4

  **A. PersistentVolume**

---

### Question 5

  **C. PersistentVolumeClaim**

---

### Question 6

  **C. ReadWriteOnce**

---

### Question 7

 

```bash
kubectl get pv
```

---

### Question 8

  **C. Demander un espace de stockage**

---

## Questions courtes

### Question 9

Un **PersistentVolume (PV)** représente un espace de stockage disponible dans le cluster. Un **PersistentVolumeClaim (PVC)** est une demande de stockage effectuée par une application. Kubernetes associe automatiquement un PVC à un PV compatible.

---

### Question 10

Le volume **emptyDir** est supprimé lorsque le Pod disparaît. Toutes les données qu'il contient sont donc perdues, ce qui le rend inadapté aux applications nécessitant une conservation des données, comme les bases de données.

---

### Question 11

Exemples de réponses :

- ReadWriteOnce (RWO)
- ReadOnlyMany (ROX)
- ReadWriteMany (RWX)

---

### Question 12

Le PVC permet de demander du stockage sans connaître les détails de l'infrastructure sous-jacente. Il rend les applications plus portables et facilite leur déploiement sur différents environnements.