# L'histoire de Kubernetes

## Introduction

Pour comprendre Kubernetes, il est important de revenir sur l'évolution des infrastructures informatiques.

Kubernetes n'est pas apparu par hasard. Il est le résultat de plusieurs décennies d'évolution dans la manière de développer, déployer et maintenir les applications.

Chaque génération de technologies est venue résoudre les limites de la précédente.

---

# Les serveurs physiques

Pendant de nombreuses années, les applications étaient installées directement sur un serveur physique.

Une application occupait généralement une machine entière.

```
+-------------------------+
|     Serveur Physique    |
|-------------------------|
|      Application        |
|-------------------------|
|    Système d'exploitation|
+-------------------------+
```

Cette approche présentait plusieurs inconvénients :

* faible utilisation des ressources matérielles ;
* coûts d'infrastructure élevés ;
* déploiement lent ;
* maintenance complexe ;
* difficulté à faire évoluer les applications.

Par exemple, un serveur équipé de 32 Go de mémoire pouvait n'utiliser que 4 ou 5 Go, le reste demeurant inutilisé.

---

# L'arrivée de la virtualisation

Pour améliorer l'utilisation des serveurs, les entreprises ont adopté la virtualisation.

Grâce à un hyperviseur, plusieurs machines virtuelles peuvent fonctionner sur un même serveur physique.

```
+--------------------------------+
|      Serveur Physique          |
|--------------------------------|
|         Hyperviseur            |
|--------------------------------|
| VM1 | VM2 | VM3 | VM4          |
+--------------------------------+
```

Chaque machine virtuelle possède :

* son propre système d'exploitation ;
* ses propres bibliothèques ;
* son application.

Cette approche permet :

* une meilleure utilisation du matériel ;
* une meilleure isolation ;
* une réduction des coûts.

Cependant, les machines virtuelles restent relativement lourdes.

Chaque VM embarque un système d'exploitation complet, ce qui consomme davantage de mémoire, de stockage et de ressources processeur.

---

# Les conteneurs

Les conteneurs sont apparus comme une alternative beaucoup plus légère.

Contrairement aux machines virtuelles, plusieurs conteneurs partagent le même noyau du système d'exploitation.

```
+--------------------------------+
|        Serveur Linux          |
|--------------------------------|
| Docker Engine / containerd     |
|--------------------------------|
| Conteneur A                    |
| Conteneur B                    |
| Conteneur C                    |
+--------------------------------+
```

Les avantages sont nombreux :

* démarrage en quelques secondes ;
* faible consommation mémoire ;
* meilleure densité de déploiement ;
* portabilité entre environnements ;
* facilité de reproduction.

Les conteneurs ont profondément transformé le développement logiciel.

---

# Docker démocratise les conteneurs

Bien que la technologie des conteneurs existait déjà sous Linux (LXC), c'est Docker, lancé en 2013, qui l'a rendue accessible au plus grand nombre.

Docker simplifie :

* la création d'images ;
* le partage des applications ;
* l'exécution des conteneurs ;
* la reproductibilité des environnements.

Le célèbre principe **"Build once, Run anywhere"** devient une réalité.

Les développeurs peuvent désormais créer une image une seule fois et l'exécuter sur n'importe quel serveur compatible.

---

# Les limites de Docker

Docker fonctionne parfaitement sur une seule machine.

Mais dans un environnement professionnel, une application est souvent répartie sur plusieurs serveurs.

Très vite, de nouvelles problématiques apparaissent :

* où lancer un nouveau conteneur ?
* comment répartir les conteneurs sur plusieurs serveurs ?
* que faire si un serveur tombe en panne ?
* comment remplacer automatiquement un conteneur défaillant ?
* comment mettre à jour une application sans interrompre les utilisateurs ?
* comment répartir le trafic entre plusieurs instances ?
* comment augmenter automatiquement le nombre de conteneurs lors d'un pic de charge ?

Ces tâches deviennent rapidement impossibles à gérer manuellement lorsque l'on déploie des dizaines ou des centaines de conteneurs.

Il devient nécessaire d'utiliser un orchestrateur.

---

# Google et le projet Borg

Bien avant Kubernetes, Google gérait déjà des millions de conteneurs dans ses centres de données.

Pour répondre à ses besoins, l'entreprise développe en interne un orchestrateur nommé **Borg**.

Pendant plus de dix ans, Borg permet à Google de faire fonctionner des services tels que :

* Google Search ;
* Gmail ;
* Google Maps ;
* YouTube.

Borg introduit plusieurs concepts devenus incontournables :

* planification automatique des charges de travail ;
* auto-réparation des applications ;
* montée en charge automatique ;
* gestion déclarative ;
* haute disponibilité.

Les ingénieurs de Google acquièrent une immense expérience grâce à Borg.

---

# La naissance de Kubernetes

En 2014, Google décide de partager une partie de cette expertise avec la communauté open source.

Kubernetes est créé par plusieurs ingénieurs ayant travaillé sur Borg.

Le projet est rapidement adopté par de nombreuses entreprises.

En 2015, Google confie Kubernetes à la **Cloud Native Computing Foundation (CNCF)** afin de garantir un développement ouvert et indépendant.

Aujourd'hui, Kubernetes est devenu le standard mondial pour l'orchestration de conteneurs.

---

# Pourquoi le nom Kubernetes ?

Le mot **Kubernetes** provient du grec κυβερνήτης (*kubernetes*), qui signifie :

* pilote ;
* capitaine ;
* barreur.

Ce nom symbolise parfaitement son rôle : piloter automatiquement des milliers de conteneurs répartis sur plusieurs serveurs.

L'abréviation **K8s** est obtenue en remplaçant les huit lettres situées entre le **K** et le **s**.

---

# Kubernetes aujourd'hui

Aujourd'hui, Kubernetes est utilisé par des entreprises de toutes tailles.

La majorité des fournisseurs cloud proposent un service Kubernetes managé :

* Azure Kubernetes Service (AKS)
* Amazon Elastic Kubernetes Service (EKS)
* Google Kubernetes Engine (GKE)
* Oracle Kubernetes Engine (OKE)

Il est également possible d'installer Kubernetes sur sa propre infrastructure avec des outils comme :

* kubeadm ;
* Kind ;
* Minikube ;
* k3s ;
* MicroK8s.

Grâce à son écosystème très riche, Kubernetes est devenu le cœur de nombreuses plateformes DevOps et Cloud Native.

---

# Ce qu'il faut retenir

À la fin de ce chapitre, vous devez retenir que :

* les serveurs physiques utilisaient mal les ressources ;
* les machines virtuelles ont amélioré l'isolation mais restaient lourdes ;
* les conteneurs ont apporté légèreté et portabilité ;
* Docker a popularisé l'utilisation des conteneurs ;
* l'orchestration est devenue indispensable avec la multiplication des conteneurs ;
* Google a créé Borg, dont Kubernetes s'inspire largement ;
* Kubernetes est aujourd'hui la référence mondiale pour l'orchestration des applications conteneurisées.
