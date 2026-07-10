# Les StatefulSets

## Introduction

Dans les chapitres précédents, nous avons utilisé des **Deployments** pour déployer des applications.

Les Deployments sont parfaitement adaptés aux applications **sans état** (*stateless*), comme :

- un serveur web ;
- une API REST ;
- un microservice.

Dans ces cas, peu importe quel Pod répond à une requête, car ils sont tous identiques.

En revanche, certaines applications doivent conserver leur identité et leurs données :

- bases de données (MySQL, PostgreSQL, MongoDB) ;
- clusters Redis ;
- Apache Kafka ;
- Elasticsearch.

Pour ce type d'application, Kubernetes propose les **StatefulSets**.

---

# Pourquoi utiliser un StatefulSet ?

Contrairement aux Pods créés par un Deployment, les Pods d'un StatefulSet possèdent une identité stable.

Chaque Pod dispose :

- d'un nom unique ;
- d'un stockage persistant dédié ;
- d'un ordre de création et de suppression.

Cette identité est conservée même si le Pod est recréé.

---

# Deployment ou StatefulSet ?

| Deployment | StatefulSet |
|------------|-------------|
| Applications sans état | Applications avec état |
| Pods interchangeables | Pods identifiés de manière unique |
| Pas d'identité persistante | Identité persistante |
| Stockage facultatif | Stockage persistant recommandé |
| Création parallèle des Pods | Création ordonnée des Pods |

---

# Fonctionnement

Lorsqu'un StatefulSet crée plusieurs Pods, chacun reçoit un nom unique.

Exemple :

```text
mysql-0

mysql-1

mysql-2
```

Ces noms restent identiques même après un redémarrage.

---

# Stockage persistant

Chaque Pod possède son propre PersistentVolumeClaim.

Exemple :

```text
mysql-0
    │
    ▼
PVC mysql-data-mysql-0
    │
    ▼
PersistentVolume

-------------------------

mysql-1
    │
    ▼
PVC mysql-data-mysql-1
    │
    ▼
PersistentVolume
```

Chaque Pod dispose donc de son propre espace de stockage.

---

# Exemple de StatefulSet

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: nginx

spec:
  serviceName: nginx

  replicas: 2

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

          image: nginx

          ports:
            - containerPort: 80
```

---

# Le rôle du Headless Service

Un StatefulSet doit généralement être associé à un **Headless Service**.

Contrairement à un Service classique, il ne possède pas d'adresse IP unique.

```yaml
clusterIP: None
```

Il permet à chaque Pod d'être accessible individuellement.

Exemple :

```text
mysql-0.mysql

mysql-1.mysql

mysql-2.mysql
```

Cette fonctionnalité est essentielle pour les bases de données distribuées.

---

# Ordre de création

Les Pods sont créés un par un.

Exemple :

```text
mysql-0

↓

mysql-1

↓

mysql-2
```

Le Pod suivant n'est créé que lorsque le précédent est prêt.

---

# Ordre de suppression

La suppression s'effectue dans l'ordre inverse.

```text
mysql-2

↓

mysql-1

↓

mysql-0
```

Cela évite de perturber les applications distribuées.

---

# Commandes utiles

Créer un StatefulSet :

```bash
kubectl apply -f statefulset.yaml
```

Lister les StatefulSets :

```bash
kubectl get statefulsets
```

Lister les Pods :

```bash
kubectl get pods
```

Supprimer un StatefulSet :

```bash
kubectl delete statefulset nginx
```

---

# Cas d'utilisation

Les StatefulSets sont particulièrement adaptés pour :

- MySQL
- PostgreSQL
- MongoDB
- Redis
- Elasticsearch
- Apache Kafka
- Cassandra

---

# Bonnes pratiques

- Utiliser un StatefulSet uniquement lorsque l'application nécessite une identité stable.
- Associer un StatefulSet à un Headless Service.
- Utiliser un PersistentVolumeClaim pour chaque Pod.
- Continuer à utiliser un Deployment pour les applications stateless.

---

# À retenir

- Les StatefulSets sont destinés aux applications avec état.
- Chaque Pod possède un nom stable.
- Chaque Pod dispose de son propre stockage persistant.
- Les Pods sont créés et supprimés dans un ordre déterminé.
- Les StatefulSets sont généralement associés à un Headless Service.
