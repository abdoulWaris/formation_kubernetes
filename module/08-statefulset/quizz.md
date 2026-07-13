
# Quiz – Les StatefulSets

## Questions à choix multiples

### Question 1

À quoi sert principalement un StatefulSet ?

A. Déployer une application stateless

B. Déployer une application avec état

C. Exposer une application

D. Gérer le réseau

---

### Question 2

Quel type d'application est le plus adapté à un StatefulSet ?

A. API REST

B. Serveur web

C. Base de données

D. Front-end React

---

### Question 3

Quelle caractéristique possède un Pod d'un StatefulSet ?

A. Son nom change à chaque redémarrage.

B. Son nom est stable.

C. Son adresse IP est fixe.

D. Il ne peut jamais être supprimé.

---

### Question 4

Quel Service est généralement utilisé avec un StatefulSet ?

A. NodePort

B. LoadBalancer

C. Headless Service

D. ExternalName

---

### Question 5

Quelle propriété permet de créer un Headless Service ?

A.

```yaml
type: Headless
```

B.

```yaml
clusterIP: None
```

C.

```yaml
headless: true
```

D.

```yaml
serviceType: None
```

---

### Question 6

Dans quel ordre les Pods d'un StatefulSet sont-ils créés ?

A. Tous en même temps

B. Aléatoirement

C. Un par un

D. Selon la charge du cluster

---

### Question 7

Que se passe-t-il lorsqu'un Pod d'un StatefulSet est supprimé ?

A. Il n'est jamais recréé.

B. Il est recréé avec un nouveau nom.

C. Il est recréé avec le même nom.

D. Le StatefulSet est supprimé.

---

### Question 8

Pourquoi utilise-t-on généralement un PersistentVolumeClaim avec un StatefulSet ?

A. Pour accélérer Kubernetes.

B. Pour conserver les données de chaque Pod.

C. Pour créer plus de Pods.

D. Pour remplacer un Service.

---

## Questions courtes

### Question 9

Quelle est la principale différence entre un Deployment et un StatefulSet ?

---

### Question 10

Pourquoi un Headless Service est-il souvent associé à un StatefulSet ?

---

### Question 11

Donnez deux exemples d'applications utilisant généralement un StatefulSet.

---

### Question 12

Pourquoi les Pods d'un StatefulSet sont-ils créés dans un ordre précis ?
