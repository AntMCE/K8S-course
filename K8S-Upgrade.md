# Kubeadm Upgrade (Ubuntu)

# Master Nodes 

## drain

`kubectl drain cks-controlplane`

## upgrade kubeadm

`apt-get update
apt-cache show kubeadm | grep 1.22
apt-mark unhold kubeadm
apt-mark hold kubectl kubelet
apt-get install kubeadm=1.22.5-00
apt-mark hold kubeadm`

## kubeadm upgrade

`kubeadm version # correct version?
kubeadm upgrade plan
kubeadm upgrade apply 1.22.5`

## kubelet and kubectl

`apt-mark unhold kubelet kubectl
apt-get install kubelet=1.22.5-00 kubectl=1.22.5-00
apt-mark hold kubelet kubectl`

## restart kubelet

`service kubelet restart
service kubelet status`

## show result

`kubeadm upgrade plan
kubectl version`

## uncordon

`kubectl uncordon cks-controlplane`

# Worker Nodes

## drain

`kubectl drain cks-node`

## upgrade kubeadm

`apt-get update
apt-cache show kubeadm | grep 1.22
apt-mark unhold kubeadm
apt-mark hold kubectl kubelet
apt-get install kubeadm=1.22.5-00
apt-mark hold kubeadm`

## kubeadm upgrade

`kubeadm version # correct version?
kubeadm upgrade node`

## kubelet and kubectl

`apt-mark unhold kubelet kubectl
apt-get install kubelet=1.22.5-00 kubectl=1.22.5-00
apt-mark hold kubelet kubectl`

## restart kubelet

`service kubelet restart
service kubelet status`

## uncordon

`kubectl uncordon cks-node`
