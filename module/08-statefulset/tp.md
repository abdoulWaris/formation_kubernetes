# TP : Déployer un StatefulSet

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un Headless Service ;
- déployer un StatefulSet ;
- observer l'identité stable des Pods ;
- comprendre le lien entre StatefulSet et stockage persistant.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifier que le cluster fonctionne :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer un Headless Service

Créer un fichier `headless-service.yaml` :

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx

spec:
  clusterIP: None

  selector:
    app: nginx

  ports:
    - port: 80
```

Créer le service :

```bash
kubectl apply -f headless-service.yaml
```

Vérifier :

```bash
kubectl get services
```

---

## Étape 2 : Créer le StatefulSet

Créer un fichier `statefulset.yaml` :

```yaml
apiVersion: apps/v1
kind: StatefulSet

metadata:
  name: nginx

spec:
  serviceName: nginx

  replicas: 3

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

Créer le StatefulSet :

```bash
kubectl apply -f statefulset.yaml
```

---

## Étape 3 : Observer les Pods

Afficher les Pods :

```bash
kubectl get pods
```

Résultat attendu :

```text
nginx-0

nginx-1

nginx-2
```

Observer leur création :

```bash
kubectl get pods --watch
```

Vous remarquerez que les Pods sont créés un par un.

---

## Étape 4 : Supprimer un Pod

Supprimer le Pod `nginx-1` :

```bash
kubectl delete pod nginx-1
```

Quelques instants plus tard :

```bash
kubectl get pods
```

Le Pod recréé conserve le même nom :

```text
nginx-1
```

---

## Étape 5 : Modifier le nombre de réplicas

Augmenter le nombre de Pods :

```bash
kubectl scale statefulset nginx --replicas=5
```

Vérifier :

```bash
kubectl get pods
```

Résultat :

```text
nginx-0

nginx-1

nginx-2

nginx-3

nginx-4
```

---

## Étape 6 : Réduire le nombre de réplicas

```bash
kubectl scale statefulset nginx --replicas=2
```

Les Pods sont supprimés dans l'ordre inverse :

```text
nginx-4

nginx-3

nginx-2
```

---

## Étape 7 : Nettoyage

```bash
kubectl delete statefulset nginx
kubectl delete service nginx
```

---

## Ce qu'il faut retenir

À l'issue de ce TP, vous savez :

- créer un StatefulSet ;
- créer un Headless Service ;
- identifier les Pods d'un StatefulSet ;
- observer leur création et leur suppression ordonnées.
