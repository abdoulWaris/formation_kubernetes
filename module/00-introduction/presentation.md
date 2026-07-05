# Présentation de Kubernetes

## Introduction

Les applications modernes doivent être capables de gérer un grand nombre d'utilisateurs, de monter rapidement en charge et de rester disponibles même lorsqu'une partie de l'infrastructure rencontre des problèmes.

Pendant longtemps, les applications étaient installées directement sur des serveurs physiques. Cette approche présentait de nombreuses limites : faible utilisation des ressources, déploiements complexes, difficultés de maintenance et forte dépendance au matériel.

L'arrivée de la virtualisation a permis d'exécuter plusieurs machines virtuelles sur un même serveur, améliorant ainsi l'utilisation des ressources. Toutefois, les machines virtuelles restent relativement lourdes puisqu'elles embarquent chacune leur propre système d'exploitation.

Les conteneurs ont ensuite révolutionné le déploiement des applications en offrant un environnement léger, rapide à démarrer et facilement reproductible. Docker est devenu la solution la plus populaire pour créer et exécuter ces conteneurs.

Cependant, lorsque le nombre de conteneurs augmente, leur gestion devient rapidement complexe. Il faut être capable de les démarrer, les arrêter, les remplacer en cas de panne, les mettre à jour sans interruption de service, répartir la charge entre plusieurs instances et gérer les ressources disponibles sur plusieurs serveurs.

C'est précisément pour répondre à ces problématiques que Kubernetes a été créé.

---

# Qu'est-ce que Kubernetes ?

Kubernetes (souvent abrégé **K8s**) est une plateforme open source d'orchestration de conteneurs.

Le nom **Kubernetes** provient du grec κυβερνήτης (*kubernetes*), qui signifie **pilote**, **barreur** ou **capitaine de navire**. Cette origine reflète parfaitement son rôle : piloter automatiquement les applications conteneurisées.

Le raccourci **K8s** est obtenu en remplaçant les huit lettres situées entre le **K** et le **s** du mot *Kubernetes*.

Kubernetes automatise le déploiement, la mise à l'échelle, la maintenance et la gestion des applications exécutées dans des conteneurs.

Plutôt que de gérer manuellement chaque conteneur, l'administrateur décrit simplement l'état souhaité du système. Kubernetes se charge ensuite de maintenir cet état en permanence.

Par exemple, si vous indiquez que votre application doit toujours disposer de cinq instances en fonctionnement, Kubernetes surveillera continuellement le cluster. Si une instance tombe en panne, une nouvelle sera automatiquement créée afin de conserver les cinq instances demandées.

---

# Pourquoi Kubernetes est-il nécessaire ?

Docker permet de créer et d'exécuter des conteneurs sur une machine.

Mais dans un environnement de production, une seule machine est rarement suffisante. Une application moderne est généralement répartie sur plusieurs serveurs afin d'assurer la haute disponibilité, la tolérance aux pannes et la montée en charge.

Sans Kubernetes, de nombreuses tâches devraient être réalisées manuellement :

* démarrer les conteneurs sur différents serveurs ;
* surveiller leur état de santé ;
* redémarrer les conteneurs en cas de panne ;
* répartir le trafic entre plusieurs instances ;
* effectuer les mises à jour sans interruption de service ;
* ajouter automatiquement de nouvelles instances lors des pics de charge.

Toutes ces opérations deviennent rapidement difficiles à maintenir lorsque plusieurs dizaines, voire plusieurs centaines de conteneurs sont déployés.

Kubernetes automatise l'ensemble de ces tâches.

---

# Les principales fonctionnalités de Kubernetes

Kubernetes offre de nombreuses fonctionnalités permettant d'administrer efficacement des applications distribuées.

Parmi les plus importantes :

* Déploiement automatisé des applications
* Mise à l'échelle automatique (scaling)
* Auto-réparation des conteneurs (Self-Healing)
* Répartition de charge (Load Balancing)
* Découverte automatique des services (Service Discovery)
* Gestion du stockage persistant
* Gestion des configurations et des secrets
* Mises à jour progressives (Rolling Updates)
* Retour arrière en cas d'échec (Rollback)
* Gestion des ressources CPU et mémoire
* Haute disponibilité
* Orchestration multi-nœuds

---

# Comment fonctionne Kubernetes ?

Le fonctionnement de Kubernetes repose sur une idée simple : **l'état désiré** (*Desired State*).

L'utilisateur décrit ce qu'il souhaite obtenir à l'aide de fichiers YAML.

Par exemple :

* trois répliques d'une application ;
* une base de données persistante ;
* une limite de mémoire de 512 Mo ;
* une exposition sur le port 80.

Kubernetes compare ensuite en permanence l'état réel du cluster avec cet état désiré.

Si une différence apparaît, il prend automatiquement les mesures nécessaires pour rétablir la situation.

Cette approche est appelée le **modèle déclaratif**.

---

# Kubernetes et Docker

Une confusion fréquente consiste à penser que Kubernetes remplace Docker.

En réalité, ces technologies répondent à des besoins différents.

Docker permet de construire et d'exécuter des conteneurs.

Kubernetes orchestre ces conteneurs sur un ou plusieurs serveurs.

On peut résumer leur rôle de la manière suivante :

* Docker crée les conteneurs.
* Kubernetes les organise, les surveille et les administre.

Aujourd'hui, Kubernetes peut fonctionner avec plusieurs moteurs de conteneurs compatibles avec la norme OCI, comme **containerd** ou **CRI-O**.

---

# Cas d'utilisation

Kubernetes est utilisé dans de nombreux contextes :

* applications web à fort trafic ;
* architectures microservices ;
* plateformes SaaS ;
* applications cloud natives ;
* traitements Big Data ;
* intelligence artificielle ;
* plateformes e-commerce ;
* streaming vidéo ;
* pipelines DevOps.

Les principaux fournisseurs cloud proposent tous un service Kubernetes managé :

* Azure Kubernetes Service (AKS)
* Amazon Elastic Kubernetes Service (EKS)
* Google Kubernetes Engine (GKE)

---

# Ce qu'il faut retenir

À l'issue de ce chapitre, vous devez retenir que :

* Kubernetes est une plateforme d'orchestration de conteneurs.
* Il automatise le déploiement et l'administration des applications.
* Il repose sur un modèle déclaratif basé sur l'état désiré.
* Il garantit la disponibilité des applications grâce à ses mécanismes d'auto-réparation.
* Il est devenu le standard de facto pour le déploiement d'applications cloud natives.
