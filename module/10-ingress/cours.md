# Les Ingress

## Introduction

Dans le chapitre précédent, nous avons découvert comment les Pods communiquent entre eux grâce aux Services et au réseau Kubernetes.

Cependant, lorsqu'une application doit être accessible depuis l'extérieur du cluster, il est nécessaire de mettre en place un mécanisme d'exposition.

Pour cela, Kubernetes propose plusieurs solutions comme les Services de type **NodePort** ou **LoadBalancer**.

Lorsque plusieurs applications doivent être accessibles via HTTP ou HTTPS, la solution la plus adaptée est l'**Ingress**.

---

# Pourquoi utiliser un Ingress ?

Sans Ingress, chaque application web devrait être exposée individuellement.

Par exemple :

```text
Application A → NodePort 30080

Application B → NodePort 30081

Application C → NodePort 30082
```

Cette approche devient rapidement difficile à maintenir.

Un Ingress permet de centraliser l'accès aux applications.

---

# Qu'est-ce qu'un Ingress ?

Un **Ingress** est une ressource Kubernetes qui définit des règles de routage HTTP et HTTPS.

Il permet de diriger les requêtes des utilisateurs vers le Service approprié selon :

- le nom de domaine ;
- le chemin de l'URL.

L'Ingress ne remplace pas les Services.

Il agit comme une couche supplémentaire située devant eux.

---

# Architecture

```text
                Internet
                    │
                    ▼
           Ingress Controller
                    │
         ┌──────────┴──────────┐
         ▼                     ▼
     Service A             Service B
         │                     │
         ▼                     ▼
      Pods A               Pods B
```

---

# L'Ingress Controller

Un Ingress ne fonctionne pas seul.

Il nécessite un **Ingress Controller** chargé d'appliquer les règles définies.

Parmi les contrôleurs les plus utilisés :

- NGINX Ingress Controller
- Traefik
- HAProxy Ingress
- AWS Load Balancer Controller
- Azure Application Gateway Ingress Controller

---

# Routage par nom de domaine

Un Ingress peut diriger les requêtes selon le domaine.

Exemple :

```text
api.mon-site.com
```

vers l'API.

Et :

```text
admin.mon-site.com
```

vers une interface d'administration.

---

# Routage par chemin

Un Ingress peut également utiliser le chemin de l'URL.

Exemple :

```text
/produits
```

vers un Service.

Et :

```text
/admin
```

vers un autre Service.

---

# Exemple d'Ingress

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: demo-ingress

spec:
  rules:
    - host: demo.local

      http:

        paths:

          - path: /

            pathType: Prefix

            backend:

              service:

                name: nginx

                port:

                  number: 80
```

---

# HTTPS

L'Ingress peut gérer les certificats TLS.

Cela permet de sécuriser les communications en HTTPS.

Les certificats peuvent être créés manuellement ou automatiquement avec des outils comme **cert-manager**.

---

# Vérification

Afficher les Ingress :

```bash
kubectl get ingress
```

Obtenir les détails :

```bash
kubectl describe ingress demo-ingress
```

---

# Bonnes pratiques

- Utiliser un seul Ingress Controller par cluster (ou selon les besoins).
- Préférer HTTPS pour les applications exposées.
- Organiser les routes par domaine ou par chemin.
- Conserver les Services comme point d'accès aux Pods.

---

# À retenir

- Un Ingress permet d'exposer des applications HTTP/HTTPS.
- Il redirige les requêtes vers les Services.
- Il nécessite un Ingress Controller.
- Il peut effectuer un routage par domaine ou par chemin.
- Il facilite la gestion de plusieurs applications accessibles depuis Internet.