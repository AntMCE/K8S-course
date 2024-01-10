# drain

`kubectl drain cks-controlplane`

# upgrade kubeadm

`apt-get update
apt-cache show kubeadm | grep 1.22
apt-mark unhold kubeadm
apt-mark hold kubectl kubelet
apt-get install kubeadm=1.22.5-00
apt-mark hold kubeadm`
