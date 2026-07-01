# Quiz — Architecture Kubernetes (avec correction)

---

## 1. QCM

1. C
2. B
3. C
4. B
5. A

---

## 2. Vrai / Faux

6. Vrai
7. Faux
8. Vrai
9. Faux

---

## 3. Questions courtes (Correction)

### 10. Explique en une phrase le rôle de kubelet.

**Réponse :**
Le kubelet est l’agent présent sur chaque Worker Node qui exécute et surveille les Pods en s’assurant qu’ils correspondent à l’état souhaité défini par le Control Plane.

---

### 11. Quelle est la différence entre Control Plane et Worker Node ?

**Réponse :**
Le Control Plane est responsable de la gestion et de la prise de décision du cluster (planification, contrôle, état), tandis que les Worker Nodes exécutent concrètement les applications sous forme de Pods.

---

### 12. Pourquoi etcd est-il important dans Kubernetes ?

**Réponse :**
etcd est la base de données clé-value distribuée de Kubernetes. Il stocke l’ensemble de l’état du cluster (Pods, configurations, secrets, nodes). Sans etcd, Kubernetes ne peut pas fonctionner car il ne peut pas connaître l’état souhaité du système.

---