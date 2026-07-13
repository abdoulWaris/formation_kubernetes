# Correction – Quiz Le réseau Kubernetes

## Questions à choix multiples

1.   C. Le plugin CNI

2.   B. L'adresse IP peut changer si le Pod est recréé.

3.   B. CoreDNS

4.   B. Gérer le réseau des Pods

5.   B. Service

---

## Questions courtes

### Question 6

Les Pods étant éphémères, leur adresse IP peut changer lorsqu'ils sont recréés. Un Service fournit une adresse stable qui reste identique, même si les Pods changent.

---

### Question 7

CoreDNS assure la résolution des noms DNS à l'intérieur du cluster. Il permet aux Pods de communiquer en utilisant les noms des Services plutôt que leurs adresses IP.

---

### Question 8

Exemples :

- Calico
- Flannel
- Cilium
- Weave Net

---

### Question 9

Oui. Grâce au plugin CNI, les Pods peuvent communiquer entre eux même lorsqu'ils sont déployés sur des nœuds différents du cluster.