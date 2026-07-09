# TP : Utiliser un volume persistant avec un PersistentVolumeClaim

## Objectifs

À la fin de ce TP, vous serez capable de :

- créer un PersistentVolume ;
- créer un PersistentVolumeClaim ;
- monter un volume dans un Pod ;
- vérifier que les données sont stockées dans le volume.

---

## Prérequis

- Un cluster Kubernetes (Kind, Minikube ou Docker Desktop)
- kubectl installé

Vérifier que le cluster est opérationnel :

```bash
kubectl get nodes
```

---

## Étape 1 : Créer un PersistentVolume

Créer un fichier `pv.yaml`.

```yaml
apiVersion: v1
kind: PersistentVolume

metadata:
  name: pv-demo

spec:
  capacity:
    storage: 1Gi

  accessModes:
    - ReadWriteOnce

  hostPath:
    path: /tmp/pv-demo
```

Créer le volume :

```bash
kubectl apply -f pv.yaml
```

Vérifier :

```bash
kubectl get pv
```

---

## Étape 2 : Créer un PersistentVolumeClaim

Créer un fichier `pvc.yaml`.

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
      storage: 1Gi
```

Créer le PVC :

```bash
kubectl apply -f pvc.yaml
```

Vérifier :

```bash
kubectl get pvc
```

Le statut doit être :

```text
Bound
```

---

## Étape 3 : Créer un Pod utilisant le PVC

Créer un fichier `pod.yaml`.

```yaml
apiVersion: v1
kind: Pod

metadata:
  name: storage-demo

spec:
  containers:
    - name: nginx
      image: nginx

      volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: storage

  volumes:
    - name: storage

      persistentVolumeClaim:
        claimName: pvc-demo
```

Créer le Pod :

```bash
kubectl apply -f pod.yaml
```

---

## Étape 4 : Vérifier le montage

Afficher les Pods :

```bash
kubectl get pods
```

Entrer dans le Pod :

```bash
kubectl exec -it storage-demo -- sh
```

Créer un fichier :

```bash
echo "Bonjour Kubernetes" > /usr/share/nginx/html/index.html
```

Vérifier :

```bash
cat /usr/share/nginx/html/index.html
```

Quitter :

```bash
exit
```

---

## Étape 5 : Vérifier la persistance

Supprimer le Pod :

```bash
kubectl delete pod storage-demo
```

Le recréer :

```bash
kubectl apply -f pod.yaml
```

Retourner dans le Pod :

```bash
kubectl exec -it storage-demo -- sh
```

Afficher le fichier :

```bash
cat /usr/share/nginx/html/index.html
```

Le fichier est toujours présent.

---

## Étape 6 : Nettoyage

```bash
kubectl delete pod storage-demo
kubectl delete pvc pvc-demo
kubectl delete pv pv-demo
```

---

## Ce qu'il faut retenir

À l'issue de ce TP, vous savez :

- créer un PersistentVolume ;
- créer un PersistentVolumeClaim ;
- monter un volume dans un Pod ;
- vérifier que les données persistent après la recréation d'un Pod.