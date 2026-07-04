# TP : Découverte des Pods

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un Pod ;
- consulter son état ;
- afficher ses logs ;
- accéder au conteneur ;
- supprimer un Pod.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifiez votre cluster :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer un fichier YAML

Créer un fichier `pod.yaml` :

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-pod

spec:
  containers:
    - name: nginx
      image: nginx:latest
      ports:
        - containerPort: 80
```

---

## Étape 2 : Déployer le Pod

```bash
kubectl apply -f pod.yaml
```

Résultat attendu :

```text
pod/nginx-pod created
```

---

## Étape 3 : Vérifier le Pod

```bash
kubectl get pods
```

Résultat attendu :

```text
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          10s
```

---

## Étape 4 : Obtenir des informations

```bash
kubectl describe pod nginx-pod
```

Observer notamment :

- l'adresse IP ;
- le Node sur lequel le Pod est exécuté ;
- les événements.

---

## Étape 5 : Consulter les logs

```bash
kubectl logs nginx-pod
```

---

## Étape 6 : Se connecter au conteneur

```bash
kubectl exec -it nginx-pod -- /bin/bash
```

Une fois connecté :

```bash
ls
```

Puis quitter :

```bash
exit
```

---

## Étape 7 : Redirection de port

Exposer temporairement le Pod :

```bash
kubectl port-forward pod/nginx-pod 8080:80
```

Ouvrir ensuite :

```text
http://localhost:8080
```

La page d'accueil de Nginx doit s'afficher.

---

## Étape 8 : Supprimer le Pod

```bash
kubectl delete pod nginx-pod
```

Vérifier :

```bash
kubectl get pods
```

Le Pod ne doit plus apparaître.
