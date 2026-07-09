# Les Volumes et le stockage persistant

## Introduction

Jusqu'à présent, toutes les applications que nous avons déployées étaient dites **sans état** (*stateless*). Si un Pod était supprimé puis recréé, aucune donnée importante n'était perdue.

Cependant, de nombreuses applications doivent conserver leurs données :

- une base de données ;
- un serveur de fichiers ;
- une application de gestion documentaire ;
- un CMS ;
- une application de commerce en ligne.

Dans ces cas, les données doivent survivre au redémarrage ou au remplacement des Pods.

Pour répondre à ce besoin, Kubernetes fournit un système de stockage basé sur les **Volumes**, les **PersistentVolumes (PV)** et les **PersistentVolumeClaims (PVC)**.

---

# Pourquoi un volume est-il nécessaire ?

Par défaut, les données écrites dans un conteneur sont temporaires.

Si un Pod est supprimé, toutes les données enregistrées dans son système de fichiers disparaissent.

Par exemple :

1. un Pod exécute une base de données ;
2. des utilisateurs ajoutent des informations ;
3. le Pod est supprimé ;
4. un nouveau Pod est créé.

Sans volume, toutes les données sont perdues.

Les volumes permettent de conserver ces données indépendamment du cycle de vie des Pods.

---

# Les Volumes

Un **Volume** est un espace de stockage accessible par un ou plusieurs conteneurs d'un même Pod.

Contrairement au système de fichiers interne d'un conteneur, un volume peut continuer d'exister tant que le Pod est en cours d'exécution.

Les volumes sont utilisés pour :

- partager des fichiers entre plusieurs conteneurs ;
- stocker temporairement des données ;
- monter des ConfigMaps ou des Secrets ;
- accéder à un stockage persistant.

---

# Exemple de Volume

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: nginx-volume

spec:
  containers:
    - name: nginx
      image: nginx

      volumeMounts:
        - name: data
          mountPath: /usr/share/nginx/html

  volumes:
    - name: data
      emptyDir: {}
```

Dans cet exemple :

- un volume nommé **data** est créé ;
- il est monté dans le conteneur ;
- les données sont conservées tant que le Pod existe.

---

# Les limites des Volumes

Le volume **emptyDir** est supprimé lorsque le Pod disparaît.

Il ne permet donc pas de conserver les données à long terme.

Pour un stockage persistant, Kubernetes utilise les PersistentVolumes.

---

# Les PersistentVolumes (PV)

Un **PersistentVolume (PV)** représente un espace de stockage disponible dans le cluster.

Il est créé par un administrateur ou automatiquement par un fournisseur cloud.

Le PV peut correspondre à :

- un disque local ;
- un disque Azure ;
- un disque AWS ;
- un disque Google Cloud ;
- un partage NFS ;
- un système de stockage compatible CSI.

Le Pod n'accède jamais directement au PV.

---

# Les PersistentVolumeClaims (PVC)

Un **PersistentVolumeClaim (PVC)** est une demande de stockage.

L'application indique simplement ses besoins :

- taille ;
- mode d'accès ;
- classe de stockage.

Kubernetes associe ensuite automatiquement le PVC à un PersistentVolume compatible.

---

# Fonctionnement

```text
Application
      │
      ▼
PersistentVolumeClaim
      │
      ▼
PersistentVolume
      │
      ▼
Disque / Stockage
```

Le développeur manipule principalement le PVC.

---

# Exemple de PersistentVolume

```yaml
apiVersion: v1
kind: PersistentVolume

metadata:
  name: pv-demo

spec:
  capacity:
    storage: 2Gi

  accessModes:
    - ReadWriteOnce

  hostPath:
    path: /data/pv
```

---

# Exemple de PersistentVolumeClaim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim

metadata:
  name: pvc-demo

spec:
  accessModes:
    - ReadWriteOnce

  resources:
    requests:
      storage: 2Gi
```

---

# Utiliser un PVC dans un Pod

```yaml
volumes:
  - name: storage

    persistentVolumeClaim:
      claimName: pvc-demo
```

Puis monter le volume :

```yaml
volumeMounts:
  - mountPath: /data
    name: storage
```

---

# Les modes d'accès

Les principaux modes d'accès sont :

### ReadWriteOnce (RWO)

Le volume est monté en lecture/écriture par un seul nœud.

C'est le mode le plus courant.

---

### ReadOnlyMany (ROX)

Plusieurs nœuds peuvent lire les données.

---

### ReadWriteMany (RWX)

Plusieurs nœuds peuvent lire et écrire simultanément.

---

# Bonnes pratiques

- Utiliser un PVC plutôt qu'un PV directement.
- Adapter la taille du stockage aux besoins.
- Choisir un StorageClass adapté.
- Ne jamais stocker des données importantes dans un `emptyDir`.

---

# À retenir

- Les données d'un conteneur sont temporaires.
- Les Volumes permettent de partager des données.
- Les PersistentVolumes représentent le stockage disponible.
- Les PersistentVolumeClaims permettent aux applications de demander du stockage.
- Les PVC sont la méthode recommandée pour utiliser un stockage persistant.