# Quiz – Le réseau Kubernetes

## Questions à choix multiples

### Question 1

Quel composant attribue une adresse IP à chaque Pod ?

A. kubelet

B. kubectl

C. Le plugin CNI

D. etcd

---

### Question 2

Pourquoi est-il déconseillé d'utiliser directement l'adresse IP d'un Pod ?

A. Les Pods n'ont pas d'adresse IP

B. L'adresse IP peut changer si le Pod est recréé

C. Kubernetes interdit cette pratique

D. Les Pods utilisent uniquement IPv6

---

### Question 3

Quel composant assure la résolution des noms DNS dans Kubernetes ?

A. kube-proxy

B. CoreDNS

C. etcd

D. kubelet

---

### Question 4

Quel est le rôle principal d'un plugin CNI ?

A. Compiler les images Docker

B. Gérer le réseau des Pods

C. Créer les Deployments

D. Gérer les Secrets

---

### Question 5

Quel objet fournit une adresse stable vers un ou plusieurs Pods ?

A. ConfigMap

B. Service

C. Deployment

D. ReplicaSet

---

## Questions courtes

### Question 6

Pourquoi les Services sont-ils préférables aux adresses IP des Pods ?

---

### Question 7

Quel est le rôle de CoreDNS ?

---

### Question 8

Citez deux plugins CNI utilisés avec Kubernetes.

---

### Question 9

Les Pods situés sur deux nœuds différents peuvent-ils communiquer ? Expliquez brièvement.