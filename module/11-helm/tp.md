# TP : Déployer Nginx avec Helm

## Objectifs

À la fin de ce TP, vous serez capable de :

- installer Helm ;
- ajouter un repository ;
- installer un Chart ;
- mettre à jour une Release ;
- supprimer une Release.

---

## Étape 1 : Vérifier Helm

```bash
helm version
```

---

## Étape 2 : Ajouter le dépôt Bitnami

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Mettre à jour :

```bash
helm repo update
```

---

## Étape 3 : Rechercher un Chart

```bash
helm search repo nginx
```

---

## Étape 4 : Installer Nginx

```bash
helm install mon-nginx bitnami/nginx
```

---

## Étape 5 : Vérifier l'installation

Afficher les Releases :

```bash
helm list
```

Afficher les Pods :

```bash
kubectl get pods
```

Afficher les Services :

```bash
kubectl get svc
```

---

## Étape 6 : Modifier le nombre de répliques

Créer un fichier `values.yaml` :

```yaml
replicaCount: 3
```

Mettre à jour la Release :

```bash
helm upgrade mon-nginx bitnami/nginx -f values.yaml
```

Vérifier :

```bash
kubectl get deployments
```

---

## Étape 7 : Désinstaller

```bash
helm uninstall mon-nginx
```

---

## Ce qu'il faut retenir

- Helm simplifie le déploiement d'applications Kubernetes.
- Une Release peut être mise à jour sans recréer toutes les ressources.
- Les valeurs sont personnalisées grâce au fichier `values.yaml`.