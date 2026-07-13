# TP : Tester le réseau Kubernetes

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer deux Pods ;
- vérifier leurs adresses IP ;
- tester la communication entre eux ;
- utiliser le DNS Kubernetes.

---

## Étape 1 : Créer un Pod Nginx

```bash
kubectl run nginx --image=nginx
```

---

## Étape 2 : Créer un Pod Alpine

```bash
kubectl run alpine --image=alpine -- sleep 3600
```

---

## Étape 3 : Vérifier les Pods

```bash
kubectl get pods -o wide
```

Repérer l'adresse IP du Pod Nginx.

---

## Étape 4 : Tester la communication

Entrer dans le Pod Alpine :

```bash
kubectl exec -it alpine -- sh
```

Installer curl :

```sh
apk add curl
```

Tester l'accès au Pod Nginx :

```sh
curl http://<IP_DU_POD_NGINX>
```

La page d'accueil de Nginx doit s'afficher.

---

## Étape 5 : Utiliser un Service

Créer un Service :

```bash
kubectl expose pod nginx --port=80
```

Lister les Services :

```bash
kubectl get svc
```

Depuis le Pod Alpine :

```sh
curl http://nginx
```

Le DNS Kubernetes résout automatiquement le nom du Service.

---

## Étape 6 : Nettoyage

```bash
kubectl delete pod nginx
kubectl delete pod alpine
kubectl delete service nginx
```

---

## Ce qu'il faut retenir

- Les Pods communiquent grâce à leur adresse IP.
- Les Services offrent une adresse stable.
- Le DNS Kubernetes permet d'utiliser les noms des Services.