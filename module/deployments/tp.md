# TP : Déployer une application avec un Deployment

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un Deployment ;
- observer les Pods créés automatiquement ;
- mettre à l'échelle une application ;
- mettre à jour une image ;
- revenir à une version précédente ;
- supprimer un Deployment.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifier que le cluster est opérationnel :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer le manifeste

Créer un fichier `deployment.yaml`.

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

---

## Étape 2 : Déployer l'application

Créer le Deployment :

```bash
kubectl apply -f deployment.yaml
```

Résultat attendu :

```text
deployment.apps/nginx-deployment created
```

---

## Étape 3 : Vérifier le Deployment

Afficher les Deployments :

```bash
kubectl get deployments
```

Afficher les ReplicaSets :

```bash
kubectl get replicasets
```

Afficher les Pods :

```bash
kubectl get pods
```

Vous devez obtenir trois Pods en état **Running**.

---

## Étape 4 : Observer un Pod

Choisir un Pod puis afficher ses informations :

```bash
kubectl describe pod <nom-du-pod>
```

Observer :

- les labels ;
- l'image utilisée ;
- le nœud sur lequel il est exécuté ;
- les événements.

---

## Étape 5 : Mettre à l'échelle

Augmenter le nombre de répliques :

```bash
kubectl scale deployment nginx-deployment --replicas=5
```

Vérifier :

```bash
kubectl get pods
```

Vous devez maintenant avoir cinq Pods.

Réduire ensuite le nombre de Pods :

```bash
kubectl scale deployment nginx-deployment --replicas=2
```

Vérifier de nouveau :

```bash
kubectl get pods
```

---

## Étape 6 : Mettre à jour le Deployment

Modifier l'image :

```bash
kubectl set image deployment/nginx-deployment nginx=nginx:1.27
```

Suivre le déploiement :

```bash
kubectl rollout status deployment/nginx-deployment
```

Afficher les Pods :

```bash
kubectl get pods
```

Vous constaterez que Kubernetes remplace progressivement les anciens Pods par les nouveaux.

---

## Étape 7 : Historique et rollback

Afficher l'historique :

```bash
kubectl rollout history deployment/nginx-deployment
```

Revenir à la version précédente :

```bash
kubectl rollout undo deployment/nginx-deployment
```

Vérifier :

```bash
kubectl rollout status deployment/nginx-deployment
```

---

## Étape 8 : Supprimer le Deployment

```bash
kubectl delete deployment nginx-deployment
```

Vérifier :

```bash
kubectl get deployments
kubectl get pods
```

Les Pods ont également été supprimés.

---

# Ce qu'il faut retenir

Au cours de ce TP, vous avez appris à :

- créer un Deployment ;
- observer les Pods et le ReplicaSet associés ;
- modifier le nombre de répliques ;
- effectuer une mise à jour progressive ;
- revenir à une version précédente ;
- supprimer un Deployment.