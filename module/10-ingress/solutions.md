# Correction – Quiz Les Ingress

## Questions à choix multiples

1.   B. Exposer des applications HTTP/HTTPS

2.   C. Service

3.   B. Ingress Controller

4.   C. par domaine et par chemin

5.   B. HTTP/HTTPS

---

## Questions courtes

### Question 6

Un Ingress permet de centraliser l'accès à plusieurs applications derrière une seule adresse IP ou un seul point d'entrée. Il évite d'exposer chaque application avec un NodePort différent et facilite la gestion des routes HTTP/HTTPS.

---

### Question 7

L'Ingress Controller lit les ressources Ingress et configure le routage des requêtes vers les Services correspondants.

---

### Question 8

Exemples :

- NGINX Ingress Controller
- Traefik
- HAProxy Ingress
- AWS Load Balancer Controller
- Azure Application Gateway Ingress Controller

---

### Question 9

Non. Un Ingress ne communique pas directement avec les Pods. Il redirige les requêtes vers un ou plusieurs Services, qui se chargent ensuite d'acheminer le trafic vers les Pods.