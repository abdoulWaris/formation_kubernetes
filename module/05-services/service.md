# Les Services

## Introduction

Dans le chapitre précédent, nous avons appris à déployer une application avec un Deployment.

Cependant, un problème subsiste : les Pods sont des ressources **éphémères**. Lorsqu'un Pod est supprimé ou recréé, son adresse IP change. Les applications clientes ne peuvent donc pas s'appuyer sur l'adresse IP d'un Pod pour communiquer avec lui.

Pour résoudre ce problème, Kubernetes propose les **Services**.

Un Service fournit un point d'accès stable vers un ou plusieurs Pods.

---

## Pourquoi utiliser un Service ?

Un Service permet de :

- fournir une adresse IP stable ;
- exposer une application aux autres Pods ;
- répartir le trafic entre plusieurs Pods ;
- masquer les changements d'adresse IP des Pods.

Sans Service, chaque recréation d'un Pod obligerait les autres applications à mettre à jour son adresse IP.

---

## Fonctionnement

Un Service sélectionne les Pods grâce à leurs **labels**.

```text
              Service
                 │
                 ▼
        +----------------+
        | app = nginx    |
        +----------------+
          │     │      │
          ▼     ▼      ▼
        Pod1  Pod2   Pod3
```

Le Service redirige automatiquement les requêtes vers les Pods correspondants.

---

## Les différents types de Services

Kubernetes propose plusieurs types de Services.

### ClusterIP

C'est le type par défaut.

Le Service est uniquement accessible depuis le cluster Kubernetes.

Cas d'utilisation :

- communication entre microservices ;
- API internes ;
- bases de données.

```yaml
type: ClusterIP
```

---

### NodePort

Le Service est exposé sur un port de chaque nœud du cluster.

Il devient accessible depuis l'extérieur.

```yaml
type: NodePort
```

Exemple :

```
http://IP_DU_NODE:30080
```

---

### LoadBalancer

Le Service est exposé via un équilibreur de charge.

Principalement utilisé sur les plateformes cloud (Azure AKS, AWS EKS, Google GKE).

```yaml
type: LoadBalancer
```

---

### ExternalName

Permet d'associer un Service Kubernetes à un nom DNS externe.

Exemple :

```
database.example.com
```

---

## Exemple de Service

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

  type: ClusterIP
```

---

## Comprendre le manifeste

### selector

```yaml
selector:
  app: nginx
```

Le Service sélectionne tous les Pods possédant le label :

```yaml
app: nginx
```

---

### port

Le port utilisé par le Service.

```yaml
port: 80
```

---

### targetPort

Le port utilisé par le conteneur.

```yaml
targetPort: 80
```

---

### type

Détermine la manière dont le Service est exposé.

Exemples :

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

## Commandes utiles

Créer un Service :

```bash
kubectl apply -f service.yaml
```

Lister les Services :

```bash
kubectl get services
```

Afficher les détails :

```bash
kubectl describe service nginx-service
```

Supprimer un Service :

```bash
kubectl delete service nginx-service
```

---

## Bonnes pratiques

- Utiliser **ClusterIP** pour les communications internes.
- Utiliser **LoadBalancer** en environnement cloud.
- Réserver **NodePort** principalement aux environnements de développement ou de test.
- Vérifier que les labels du Service correspondent à ceux des Pods.

---

## À retenir

- Un Service fournit une adresse IP stable aux Pods.
- Il sélectionne les Pods grâce aux labels.
- Il répartit automatiquement le trafic.
- Il permet aux applications de communiquer sans connaître l'adresse IP des Pods.
