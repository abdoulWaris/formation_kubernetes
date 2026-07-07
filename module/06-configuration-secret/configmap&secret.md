# Les ConfigMaps et les Secrets

## Introduction

Jusqu'à présent, nos applications utilisent des valeurs directement définies dans les fichiers YAML ou intégrées à l'image Docker.

Cette approche fonctionne pour des exemples simples, mais elle devient rapidement difficile à maintenir lorsqu'une application doit être déployée dans plusieurs environnements (développement, test, production).

Par exemple, une application peut avoir besoin de connaître :

- le nom de l'application ;
- l'adresse d'une API ;
- l'environnement d'exécution ;
- le port utilisé ;
- un mot de passe de base de données ;
- une clé d'API.

Il est déconseillé de stocker ces informations directement dans l'image Docker ou dans le code source.

Kubernetes fournit deux ressources permettant de gérer ces données :

- **ConfigMap**, pour les données de configuration ;
- **Secret**, pour les données sensibles.

---

# Les ConfigMaps

## Qu'est-ce qu'un ConfigMap ?

Un ConfigMap est une ressource Kubernetes permettant de stocker des données de configuration sous forme de paires clé/valeur.

Ces informations peuvent ensuite être utilisées par les Pods sans modifier l'image Docker.

Exemple :

```text
APP_NAME=Formation Kubernetes
APP_ENV=development
APP_PORT=8080
```

---

## Pourquoi utiliser un ConfigMap ?

Les ConfigMaps permettent de :

- séparer la configuration de l'application ;
- réutiliser une même image Docker dans plusieurs environnements ;
- modifier certains paramètres sans reconstruire l'image ;
- faciliter la maintenance.

---

## Exemple de ConfigMap

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

Lister les ConfigMaps :

```bash
kubectl get configmaps
```

Afficher son contenu :

```bash
kubectl describe configmap app-config
```

---

## Utiliser un ConfigMap

Un ConfigMap peut être utilisé :

- comme variable d'environnement ;
- comme fichier monté dans un volume.

Exemple avec des variables d'environnement :

```yaml
envFrom:
  - configMapRef:
      name: app-config
```

Toutes les clés du ConfigMap deviennent alors des variables d'environnement dans le conteneur.

---

# Les Secrets

## Qu'est-ce qu'un Secret ?

Un Secret est une ressource Kubernetes destinée à stocker des informations sensibles.

Exemples :

- mots de passe ;
- jetons d'authentification ;
- clés API ;
- certificats TLS.

---

## Pourquoi utiliser un Secret ?

Les Secrets permettent de :

- éviter d'écrire des informations sensibles dans les manifestes ;
- centraliser les données sensibles ;
- limiter leur exposition.

---

## Exemple de Secret

Les valeurs doivent être encodées en Base64.

```bash
echo -n "admin" | base64
echo -n "password123" | base64
```

Créer le manifeste :

```yaml
apiVersion: v1
kind: Secret

metadata:
  name: db-secret

type: Opaque

data:
  username: YWRtaW4=
  password: cGFzc3dvcmQxMjM=
```

Créer le Secret :

```bash
kubectl apply -f secret.yaml
```

Lister les Secrets :

```bash
kubectl get secrets
```

---

## Utiliser un Secret

Comme variable d'environnement :

```yaml
env:
  - name: DB_USERNAME
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: username

  - name: DB_PASSWORD
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: password
```

---

# ConfigMap ou Secret ?

| ConfigMap | Secret |
|------------|--------|
| Configuration | Données sensibles |
| Texte simple | Valeurs encodées en Base64 |
| Informations publiques | Informations confidentielles |
| Nom d'application | Mot de passe |
| URL d'API | Clé API |

---

# Bonnes pratiques

- Utiliser un ConfigMap pour toutes les données de configuration.
- Utiliser un Secret pour les informations sensibles.
- Ne jamais stocker un mot de passe dans un ConfigMap.
- Éviter de conserver des secrets dans un dépôt Git.

---

# À retenir

- Un ConfigMap stocke des données de configuration.
- Un Secret stocke des informations sensibles.
- Les deux peuvent être utilisés comme variables d'environnement ou comme fichiers.
- Ils permettent de séparer la configuration de l'application de son image Docker.