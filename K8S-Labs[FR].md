# [Labs] Initiation à Kubernetes 

    Auteur: Anthony MACLE
    Courriel: ame@k8sgo.fr
    Licence: CC-BY-4.0
    Version: 1.0

<!--- Forked from  --->

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Ce support de formation est distribué sous la license <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

## Environnement

Chaque participant a accès à son environnement, il est composant d'un cluster Kubernetes, voici les paramètres:

| Clé        | Valeur                 |
| ---------- | ---------------------- |
| Adresse IP |                        |
| Kubeconfig | (livré au participant) |

## La difficulté des excercices est exprimée en nombre de Wheel:

☸️ -> Facile

☸️☸️ -> Moyen 

☸️☸️☸️ -> Difficile

## 1 - Mon premier pod Kubernetes ☸️☸️ 

- [ ] Création d'un *pod* nommé pod1
  - [ ] Utilisant l'image **httpd:2.4.41-alpine**
  - [ ] Le conteneur doit être nommé **pod1-container**
  - [ ] Dans le namespace **votre prénom**
  - [ ] Le pod doit seulement être déployé sur le noeud Master  **Point Bonus**


## 1 - Mon premier déploiement Kubernetes ☸️☸️ 

Dans cet exercice, vous allez déployer un *conteneur* dans un *POD* unique propulsé par un simple *déploiement*.

- [ ] Création d'un *deploiement* nommé whoami
  - [ ] Utilisant l'image **containous/whoami**
  - [ ] Utilisant le port interne **80/TCP**
  - [ ] Dans le namespace **votre prénom**
- [ ] Création d'un service nommé **whoami**
  - [ ] Ecoutant sur le port **80**
  - [ ] Lié au deploiement **whoami**
  - [ ] Type de service: **NodePort**
  - [ ] Récupérer le port utilisé sur la machine hôte
- [ ] Accéder au service whoami depuis votre poste client

## 2 - Stockage persistant ☸️☸️☸️

Dans cet exercice, vous allez déployer un *Deployment* propulsant une base de données sur un *Stockage Persistant*.

- [ ] Création d'un PersistentVolumeClaim pour MariaDB
  - [ ] Créer un **PVC** nommé **mariadb**
  - [ ] Le *PVC* utilisera la classe de Stockage par defaut
  - [ ] Le *PVC* demandera une volumétrie de **1Go**
- [ ] Création d'un *déploiement* nommé mariadb
  - [ ] Utilisant l'image **mariadb:latest**
  - [ ] Utilisant le port interne **3306/TCP**
  - [ ] Utilisant le **PVC** précédemment créé pour héberger ses bases de données
  - [ ] Créer un compte utilisateur nommé **wordpress**
  - [ ] Créer un mot de passe pour l'utilisateur **wordpress**
  - [ ] Le mot de passe *root* de MariaDB devra etre généré automatiquement
  - [ ] Créer une base de données nommée **wordpress**
- [ ] Création d'un service nommé **mariadb**
  - [ ] Ecoutant sur le port **56100** 
  - [ ] Lié au déploiement **mariadb**
  - [ ] Type de Service: **ClusterIP**
- [ ] Création d'un *Pod* ephémaire de debug
  - [ ] Utilisant l'image **ubuntu:latest**
  - [ ] Installer le paquet **mariadb-client**
  - [ ] Installer un client **mariadb**
  - [ ] Réaliser une connexion pour valider le bon fonctionnement

## 3 - Déploiement d'une application complexe

Source: [Gist](https://gist.github.com/davoult/9fb6f9f604bf2da2a060eeb91e69c4bb)

- [ ] Déploiement des composants dans un espace de nom
- [ ] Correction des problèmes
- [ ] Exposition de l'application au travers d'un **ingress**


## 4 - Mise à jour d'un cluster K8S via Kubeadm ☸️☸️ 

 
- [ ] Skew Policy à connaitre https://kubernetes.io/releases/version-skew-policy/
- [ ] Matrice de compatibilité des ressources (API Version) et des Outils.
- [ ] Mise à jour du noeud Master
- [ ] Mise à jour des noeuds Worker


## 5 - Initiation à Helm ☸️

- [ ] Lister les applications installées via Helm
- [ ] Mettre à jour les repo Helm
- [ ] Recherche des matrices de compatibilité
- [ ] Chercher une version spécifique d'un repo Helm
- [ ] Upgrader une application installé via Helm (avec version spécifique)

## 5 - Debuger le deployment "setra-app" dans le namespace setra ☸️☸️☸️

- [ ] Lister les applications installées via Helm
- [ ] Mettre à jour les repo Helm
- [ ] Recherche des matrices de compatibilité
- [ ] Chercher une version spécifique d'un repo Helm
- [ ] Upgrader une application installé via Helm (avec version spécifique)

## 5 - Debuger le deployment "axians-app" dans le namespace axians ☸️☸️☸️

- [ ] Lister les applications installées via Helm
- [ ] Mettre à jour les repo Helm
- [ ] Recherche des matrices de compatibilité
- [ ] Chercher une version spécifique d'un repo Helm
- [ ] Upgrader une application installé via Helm (avec version spécifique)
