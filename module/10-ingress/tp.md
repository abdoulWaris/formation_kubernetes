# TP : Exposer une application avec un Ingress

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un Deployment ;
- créer un Service ;
- créer un Ingress ;
- accéder à l'application via un nom de domaine local.

---

## Prérequis

- Un cluster Kubernetes
- Un Ingress Controller installé (ex. NGINX Ingress Controller)

---

## Étape 1 : Déployer Nginx

```bash
kubectl create deployment nginx --image=nginx
```

---

## Étape 2 : Créer un Service

```bash
kubectl expose deployment nginx --port=80
```

---

## Étape 3 : Créer un Ingress

Créer un fichier `ingress.yaml` :

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress

metadata:
  name: nginx-ingress

spec:
  rules:
    - host: nginx.local

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

Déployer :

```bash
kubectl apply -f ingress.yaml
```

---

## Étape 4 : Vérifier

```bash
kubectl get ingress
```

Afficher les détails :

```bash
kubectl describe ingress nginx-ingress
```

---

## Étape 5 : Tester

Ajouter dans le fichier `hosts` de votre machine :

```text
127.0.0.1 nginx.local
```

Puis ouvrir :

```text
http://nginx.local
```

La page d'accueil de Nginx doit s'afficher.

---

## Étape 6 : Nettoyage

```bash
kubectl delete ingress nginx-ingress
kubectl delete service nginx
kubectl delete deployment nginx
```

---

## Ce qu'il faut retenir

- L'Ingress redirige les requêtes HTTP/HTTPS vers les Services.
- Un Ingress Controller est indispensable pour que les règles soient appliquées.