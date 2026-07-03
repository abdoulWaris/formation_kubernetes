# Installation de Kubernetes avec Docker Desktop

## ⚙️ Prérequis

Avant de commencer, assurez-vous d'avoir installé :

- Docker Desktop
- kubectl (optionnel, Docker Desktop peut l'installer automatiquement)

Vérifiez que Docker fonctionne :

```bash
docker --version
docker info
```
## Activer Kubernetes

1. Ouvrez **Docker Desktop**.
2. Cliquez sur **Settings** (ou **Preferences** sur macOS).
3. Sélectionnez **Kubernetes**.
4. Cochez **Enable Kubernetes**.
5. Cliquez sur **Apply & Restart**.

Docker Desktop télécharge automatiquement les composants nécessaires et crée un cluster Kubernetes local.

> **Remarque :**
> Le démarrage du cluster peut prendre quelques minutes lors de la première installation.

---

## 🔍 Vérification

Vérifiez que le cluster est opérationnel :

```bash
kubectl cluster-info
```

Lister les nœuds :

```bash
kubectl get nodes
```

Résultat attendu :

```text
NAME             STATUS   ROLES           AGE
docker-desktop   Ready    control-plane   2m
```

Vérifiez également les composants système :

```bash
kubectl get pods -n kube-system
```

---

## 🧪 Test rapide

Créer un Deployment Nginx :

```bash
kubectl create deployment nginx --image=nginx
```

Vérifier qu'il est bien créé :

```bash
kubectl get deployments
kubectl get pods
```

Exposer le Deployment :

```bash
kubectl expose deployment nginx --type=NodePort --port=80
```

Accéder à l'application :

```bash
kubectl port-forward service/nginx 8080:80
```

Puis ouvrez votre navigateur à l'adresse :

```text
http://localhost:8080
```

La page d'accueil de **Nginx** doit s'afficher.

---

## 🧹 Nettoyage

Supprimer le service :

```bash
kubectl delete service nginx
```

Supprimer le Deployment :

```bash
kubectl delete deployment nginx
```

---

## ⚠️ Limites

- Un seul cluster Kubernetes est disponible.
- Les possibilités de personnalisation sont limitées.
- Moins adapté aux scénarios avancés (multi-nœuds, CI/CD, tests complexes).
- Principalement destiné au développement local.

---