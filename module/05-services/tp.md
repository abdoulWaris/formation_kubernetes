# TP : Exposer une application avec un Service

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un Deployment ;
- créer un Service ;
- comprendre le rôle des labels ;
- accéder à une application via un Service.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifiez que votre cluster est opérationnel :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer un Deployment

Créer un fichier `deployment.yaml` :

```yaml
apiVersion: apps/v1
kind: Deployment

metadata:
  name: nginx-deployment

spec:
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
          image: nginx:latest

          ports:
            - containerPort: 80
```

Déployer l'application :

```bash
kubectl apply -f deployment.yaml
```

Vérifier :

```bash
kubectl get deployments
kubectl get pods
```

---

## Étape 2 : Créer un Service

Créer un fichier `service.yaml` :

```yaml
apiVersion: v1
kind: Service

metadata:
  name: nginx-service

spec:
  selector:
    app: nginx

  ports:
    - port: 80
      targetPort: 80

  type: NodePort
```

Déployer le Service :

```bash
kubectl apply -f service.yaml
```

---

## Étape 3 : Vérifier le Service

Afficher les Services :

```bash
kubectl get services
```

Afficher les détails :

```bash
kubectl describe service nginx-service
```

---

## Étape 4 : Tester l'application

Avec Kind ou Docker Desktop :

```bash
kubectl port-forward service/nginx-service 8080:80
```

Ouvrir ensuite :

```text
http://localhost:8080
```

La page d'accueil de Nginx doit s'afficher.

---

## Étape 5 : Vérifier les Endpoints

Afficher les Endpoints associés au Service :

```bash
kubectl get endpoints
```

Observer que les adresses IP correspondent aux Pods créés par le Deployment.

---

## Étape 6 : Supprimer le Service

```bash
kubectl delete service nginx-service
```

Vérifier :

```bash
kubectl get services
```

Le Service ne doit plus apparaître.

---

## Ce qu'il faut retenir

À l'issue de ce TP, vous savez :

- créer un Service ;
- associer un Service à des Pods grâce aux labels ;
- exposer une application ;
- accéder à une application via un Service ;
- vérifier les Endpoints associés à un Service.
