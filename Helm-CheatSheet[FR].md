# Mettre à jour Helm.
```
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```
# Lister les applications installées via Helm.
```
helm list -A
```
# Ajouter un repo Helm en local.
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
# Lister les repos locaux.
```
helm repo list
```

# Installer une application via Helm en précisant des paramètres spécifiques (storageClass).
```
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring alertmanager.persistentVolume.storageClass="gp2",server.persitentVolume.storageClass="gp2”
```
# Ajuster la configuration d'une application installée via Helm en utilisant un fichier de configuration spécifique.
```
helm upgrade --namespace monitoring -f /root/extraScrapeConfigs.yaml prometheus prometheus-community/kube-prometheus-stack
```
# Mettre à jour les repo présents localement 
```
helm repo update
```
# Chercher une version spécifique d'un repo
```
helm search repo hashicorp/vault -l
```
# Mettre à jour une application installée via Helm en précisant la version cible souhaitée et en passant un fichier de configuration custom
```
helm   upgrade vault hashicorp/vault  -f ./vault-override-values.yml --version 0.27.0 -n vault
```

