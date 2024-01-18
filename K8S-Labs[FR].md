# [Labs] Initiation à Kubernetes 

    Auteur: Anthony MACLE
    Courriel: ame@k8sgo.io
    Licence: CC-BY-4.0
    Version: 1.1

<!--- Forked from  --->

<a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />Ce support de formation est distribué sous la license <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.

## Environnement

Chaque participant a accès à son environnement, il est composant d'un cluster Kubernetes, voici les paramètres:

| Clé        | Valeur                 |
| ---------- | ---------------------- |
| Adresse IP | livré aux participants |
| Kubeconfig | livré aux participants |

## La difficulté des excercices est exprimée en nombre de Wheel

☸️ -> Facile

☸️☸️ -> Moyen 

☸️☸️☸️ -> Difficile

## 1 - Mon premier pod Kubernetes ☸️☸️ 

- [ ] Création d'un *pod* nommé **votre trigamme**
  - [ ] Utilisant l'image **httpd:2.4.41-alpine**
  - [ ] Le conteneur doit être nommé **pod1-container**
  - [ ] Dans le namespace **votre prénom**
  - [ ] Le pod doit seulement être déployé sur le noeud Master  **Point Bonus** indice: Il faut ajouter une *toleration* et un spécifier un *nodeName*
        https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodename / https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#concepts


## 2 - Mon premier déploiement Kubernetes ☸️☸️ 

Dans cet exercice, vous allez déployer un *conteneur* dans un *POD* unique propulsé par un simple *déploiement*.

- [ ] Création d'un *deploiement* nommé whoami
  - [ ] Utilisant l'image **containous/whoami**
  - [ ] Utilisant le port interne **80/TCP**
  - [ ] Dans le namespace **votre prénom**
- [ ] Création d'un service nommé **whoami**
  - [ ] Ecoutant sur le port **80**
  - [ ] Lié au deploiement **whoami**
  - [ ] Type de service: **NodePort**
- [ ] Accéder au service whoami depuis votre moteur de recherche

## 3 - Stockage persistant ☸️☸️

Dans cet exercice, vous allez déployer un *Deployment* utilisant un *Stockage Persistant*.

- [ ] Création d'un PersistentVolume
  - [ ] Créer un **PV** nommé **pv-votre_trigramme**
  - [ ] Le PV devra faire **1Gi**
  - [ ] Son accessMode sera ReadWriteOnce
  - [ ] hostPath /vol/votre_trigramme
  - [ ] Le *PV* n'aura pas StorageClass défini
- [ ] Création d'un PersistentVolumeClaim
  - [ ] Créer un **PVC** nommé **pvc-votre_trigramme**
  - [ ] Le *PVC* n'aura pas StorageClass défini
  - [ ] Le *PVC* demandera une volumétrie de **1Gi**
  - [ ] Son accessMode sera ReadWriteOnce
- [ ] Création d'un *déploiement*
  - [ ] Créer un deployment nommé **app-pv-votre_trigramme**
  - [ ] Utilisant l'image **httpd:2.4.41-alpine**
  - [ ] Utilisant le **PVC** précédemment créé
  - [ ] Dans le namespace **votre prénom**
  - [ ] Le volume doit monter /tmp/safari-data 
  


## 3 - Scheduler un Pod manuellement [ Scénario de Scheduler KO ]


- [ ] 
- [ ] 


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

## 6 - Debuger le deployment "setra-app" dans le namespace setra ☸️☸️☸️

- [ ] Lister les applications installées via Helm
- [ ] Mettre à jour les repo Helm
- [ ] Recherche des matrices de compatibilité
- [ ] Chercher une version spécifique d'un repo Helm
- [ ] Upgrader une application installé via Helm (avec version spécifique)

## 7 - Debuger le deployment "axians-app" dans le namespace axians ☸️☸️☸️

- [ ] Lister les applications installées via Helm
- [ ] Mettre à jour les repo Helm
- [ ] Recherche des matrices de compatibilité
- [ ] Chercher une version spécifique d'un repo Helm
- [ ] Upgrader une application installé via Helm (avec version spécifique)

## 8 - Etendre les droits du user trainee via RBAC☸️☸️

- [ ] Ajouter le droit de modifier les resources deployments au niveau de tout le cluster
- [ ] Supprimer le droit de pouvoir lister les secrets au niveau de tout le cluster
- [ ] Ajouter tous les droits dans le namespace Dev

## 9 - Cronjob & Job ☸️

- [ ] Créer un Cronjob qui instancie l'image XXX
- [ ] Dans le namespace **votre prénom**
- [ ] 3 versions historiques du Job doivent être conservées
- [ ] Un job doit être déclenché manuellement depuis ce Cronjob

## 10 - ServiceAccount ☸️

- [ ] Créer un ServiceAccount nommé "SA-Monitoring"
- [ ] Dans le namespace **votre prénom**
- [ ] Créer un Token d'une durée de 3 mois pour ce ServiceAccount 


## 11 - Network Policies ☸️☸️☸️

- [ ] Appliquer une Network Policiy sur le pod **sensitive-pod**
- [ ] Identifier le namespace dans lequel se trouve le pod
- [ ] La policy doit refuser toutes les connexions entrentes
- [ ] La policy autorise le flux sortant uniquement vers 

## 12 - Administrer les Pods en fonction de leur label ☸️☸️

- [ ] Dans le namespace **votre prénom**
- [ ] Ajouter le label delete=ok aux pods ayant déjà le label env=test
- [ ] Supprimer tous les pods ayant le label delete=ok


## 13 - Deployment Rollout ☸️☸️

- [ ] Dans le namespace **votre prénom**
- [ ] Il y un deployment nommé "sophia-app", il faut vérifier le statut de ses pods
- [ ] Vérifier l'hitorique de rollout deployment
- [ ] Revenir à un deployment fonctionnel en utilasant une commande de type "kubectl rollout" et en précisant la **REVISION** antérieur souhaitée
- [ ] Nous savons que le déploiement initial fonctionnait correctement
