# TP : Utiliser un ConfigMap et un Secret

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un ConfigMap ;
- créer un Secret ;
- injecter des variables d'environnement dans un Pod ;
- vérifier que les données sont accessibles depuis un conteneur.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifier que le cluster est opérationnel :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer un ConfigMap

Créer un fichier `configmap.yaml` :

```yaml
apiVersion: v1
kind: ConfigMap

metadata:
  name: app-config

data:
  APP_NAME: "Formation Kubernetes"
  APP_ENV: "development"
  APP_PORT: "8080"
```

Créer le ConfigMap :

```bash
kubectl apply -f configmap.yaml
```

Vérifier :

```bash
kubectl get configmaps
kubectl describe configmap app-config
```

---

## Étape 2 : Créer un Secret

Encoder les valeurs en Base64 :

```bash
echo -n "admin" | base64
echo -n "password123" | base64
```

Créer le fichier `secret.yaml` :

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: app-secret

type: Opaque

data:
  username: YWRtaW4=
  password: cGFzc3dvcmQxMjM=
```

Créer le Secret :

```bash
kubectl apply -f secret.yaml
```

Vérifier :

```bash
kubectl get secrets
kubectl describe secret app-secret
```

---

## Étape 3 : Créer un Pod utilisant le ConfigMap et le Secret

Créer un fichier `pod.yaml` :

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: env-demo

spec:
  containers:
    - name: alpine
      image: alpine:latest
      command: ["sleep", "3600"]

      envFrom:
        - configMapRef:
            name: app-config

      env:
        - name: DB_USERNAME
          valueFrom:
            secretKeyRef:
              name: app-secret
              key: username

        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: app-secret
              key: password
```

Créer le Pod :

```bash
kubectl apply -f pod.yaml
```

---

## Étape 4 : Vérifier les variables d'environnement

Se connecter au Pod :

```bash
kubectl exec -it env-demo -- sh
```

Afficher les variables :

```bash
printenv
```

Ou afficher uniquement :

```bash
echo $APP_NAME

echo $APP_ENV

echo $DB_USERNAME

echo $DB_PASSWORD
```

Quitter le conteneur :

```bash
exit
```

---

## Étape 5 : Nettoyage

Supprimer les ressources :

```bash
kubectl delete pod env-demo
kubectl delete configmap app-config
kubectl delete secret app-secret
```

---

## Ce qu'il faut retenir

À l'issue de ce TP, vous savez :

- créer un ConfigMap ;
- créer un Secret ;
- utiliser des variables d'environnement dans un Pod ;
- séparer la configuration de l'application de son image Docker.