
# Correction – Quiz Les StatefulSets

## Questions à choix multiples

### Question 1

**B. Déployer une application avec état**

---

### Question 2

**C. Base de données**

---

### Question 3

**B. Son nom est stable.**

---

### Question 4

**C. Headless Service**

---

### Question 5


```yaml
clusterIP: None
```

---

### Question 6

 **C. Un par un**

---

### Question 7

 **C. Il est recréé avec le même nom.**

---

### Question 8

**B. Pour conserver les données de chaque Pod.**

---

## Questions courtes

### Question 9

Un **Deployment** est conçu pour les applications **sans état** (*stateless*), où tous les Pods sont interchangeables. Un **StatefulSet** est destiné aux applications **avec état** (*stateful*), où chaque Pod possède une identité stable et, généralement, son propre stockage persistant.

---

### Question 10

Le **Headless Service** permet à chaque Pod du StatefulSet d'être joignable individuellement grâce à un nom DNS unique. Cela est indispensable pour de nombreuses applications distribuées, comme les bases de données en cluster.

---

### Question 11

Exemples de réponses :

- MySQL
- PostgreSQL
- MongoDB
- Redis
- Apache Kafka
- Elasticsearch
- Cassandra

---

### Question 12

Les Pods sont créés dans un ordre précis afin de garantir une initialisation correcte des applications distribuées. Chaque Pod attend que le précédent soit opérationnel avant d'être créé, ce qui facilite le démarrage et la synchronisation des services.
