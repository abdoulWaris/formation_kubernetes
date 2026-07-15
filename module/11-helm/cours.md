# Helm

## Introduction

Au cours des chapitres précédents, nous avons créé plusieurs ressources Kubernetes :

- Pods
- Deployments
- Services
- ConfigMaps
- Secrets
- PersistentVolumeClaims
- Ingress

Chaque application nécessite souvent plusieurs fichiers YAML.

Lorsque le nombre de ressources augmente, leur gestion devient rapidement complexe.

Pour simplifier le déploiement et la maintenance des applications Kubernetes, la communauté a développé **Helm**, souvent présenté comme le gestionnaire de paquets de Kubernetes.

---

# Qu'est-ce que Helm ?

Helm est un outil open source permettant d'installer, de configurer et de mettre à jour des applications Kubernetes.

Au lieu d'écrire plusieurs fichiers YAML à chaque projet, Helm regroupe toutes les ressources d'une application dans un **Chart**.

Un Chart peut ensuite être installé en une seule commande.

---

# Pourquoi utiliser Helm ?

Helm offre plusieurs avantages :

- simplifier le déploiement d'applications ;
- éviter la duplication des fichiers YAML ;
- personnaliser facilement une installation ;
- faciliter les mises à jour ;
- partager des applications sous forme de Charts.

---

# Les principaux concepts

## Chart

Un Chart est un package contenant toutes les ressources Kubernetes nécessaires au déploiement d'une application.

---

## Repository

Un Repository est un dépôt contenant plusieurs Charts.

Exemples :

- Bitnami
- Artifact Hub

---

## Release

Une Release correspond à une instance installée d'un Chart.

Un même Chart peut être installé plusieurs fois avec des configurations différentes.

---

# Structure d'un Chart

```text
mon-chart/
│
├── Chart.yaml
├── values.yaml
├── templates/
│     ├── deployment.yaml
│     ├── service.yaml
│     └── ingress.yaml
└── charts/
```

---

# Le fichier Chart.yaml

Il contient les informations principales du Chart.

Exemple :

```yaml
apiVersion: v2

name: demo-chart

description: Mon premier Chart Helm

version: 1.0.0

appVersion: "1.0"
```

---

# Le fichier values.yaml

Il contient les valeurs personnalisables.

Exemple :

```yaml
replicaCount: 2

image:
  repository: nginx
  tag: latest

service:
  port: 80
```

---

# Les templates

Les fichiers du dossier **templates** utilisent le moteur de templates de Helm.

Exemple :

```yaml
replicas: {{ .Values.replicaCount }}
```

Lors de l'installation, Helm remplace cette expression par la valeur définie dans `values.yaml`.

---

# Installation d'un Chart

Installer un Chart :

```bash
helm install mon-nginx bitnami/nginx
```

Lister les Releases :

```bash
helm list
```

---

# Mise à jour

Mettre à jour une Release :

```bash
helm upgrade mon-nginx bitnami/nginx
```

---

# Désinstallation

Supprimer une Release :

```bash
helm uninstall mon-nginx
```

---

# Repositories

Ajouter un dépôt :

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Mettre à jour les dépôts :

```bash
helm repo update
```

Rechercher un Chart :

```bash
helm search repo nginx
```

---

# Bonnes pratiques

- Utiliser un fichier values.yaml pour personnaliser les installations.
- Versionner les Charts.
- Éviter de modifier directement les Charts téléchargés.
- Utiliser des Charts officiels lorsque cela est possible.

---

# À retenir

- Helm est le gestionnaire de paquets de Kubernetes.
- Un Chart regroupe les ressources d'une application.
- Une Release correspond à une installation d'un Chart.
- Les templates permettent de générer des fichiers YAML dynamiques.
- Helm facilite le déploiement et la maintenance des applications Kubernetes.