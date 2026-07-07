# Correction – Quiz Les ConfigMaps et les Secrets

## Questions à choix multiples

### Question 1

  **B. Stocker des données de configuration**

---

### Question 2

  **C. Secret**

---

### Question 3

  **C. Encodées en Base64**

---

### Question 4

 

```bash
kubectl get configmaps
```

---

### Question 5

 

```bash
kubectl get secrets
```

---

### Question 6

  **C. Les deux**

Un ConfigMap peut être utilisé comme variable d'environnement ou être monté sous forme de volume.

---

### Question 7

  **C. Une clé API**

---

### Question 8

  **B. Pour séparer la configuration de l'application**

---

## Questions courtes

### Question 9

Un **ConfigMap** stocke des données de configuration non sensibles (nom d'application, URL, port, environnement). Un **Secret** est destiné aux informations sensibles comme les mots de passe, les clés API ou les certificats.

---

### Question 10

Les valeurs des Secrets sont encodées en Base64 afin de pouvoir être représentées sous forme de texte dans les fichiers YAML. Cet encodage ne constitue **pas un mécanisme de chiffrement**.

---

### Question 11

Exemples de réponses :

- nom de l'application ;
- environnement (`development`, `test`, `production`) ;
- URL d'une API ;
- numéro de port ;
- paramètres de configuration.

---

### Question 12

Exemples de réponses :

- mot de passe ;
- clé API ;
- jeton d'authentification (token) ;
- certificat TLS ;
- identifiant d'une base de données.