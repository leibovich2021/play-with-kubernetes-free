how to play with kubernetes FREE(4 hours)

go to site 
https://labs.play-with-k8s.com

and login your github or dockerhub account
and press start

press on:
+ADD NEW INSTANCE

step one :
Initializes cluster master node:

1. kubeadm init --apiserver-advertise-address $(hostname -i) --pod-network-cidr 10.5.0.0/16


step two : 
Initialize cluster networking:
1. kubectl apply -f https://raw.githubusercontent.com/cloudnativelabs/kube-router/master/daemonset/kubeadm-kuberouter.yaml


now we have master


for connect betwen nodes create another node(node2)
and get into it and press you command for join:
 
1.  kubeadm join 192.168.0.18:6443 --token ylvnm7.beudtfz6m12258p1 \
    --discovery-token-ca-cert-hash sha256:6c55e17e6c349d00ff830bd0c5d234f0c5e9bf400a71caf78124299c85a2d52d 
    
now we go us master node and check if this work
    
1. kubectl get nodes:
    
[node1 ~]$ kubectl get nodes
NAME    STATUS   ROLES                  AGE     VERSION
node1   Ready    control-plane,master   2m11s   v1.20.1

how change name of ROLES:

1. kubectl get nodes --show-labels

[node1 ~]$ kubectl get nodes --show-labels
NAME    STATUS   ROLES                  AGE   VERSION   LABELS
node1   Ready    control-plane,master   11m   v1.20.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node1,kubernetes.io/os=linux,node-role.kubernetes.io/control-plane=,node-role.kubernetes.io/master=
node2   Ready    <none>                 10m   v1.20.1   beta.kubernetes.io/arch=amd64,beta.kubernetes.io/os=linux,kubernetes.io/arch=amd64,kubernetes.io/hostname=node2,kubernetes.io/os=linux

for change us nodes:

kubectl label node node2 node-role.kubernetes.io/(new name)=

1.  kubectl label node node2 node-role.kubernetes.io/worker=

and now we check :

1. kubectl get nodes

[node1 ~]$ kubectl get nodes
NAME    STATUS   ROLES                  AGE   VERSION
node1   Ready    control-plane,master   13m   v1.20.1
node2   Ready    worker                 12m   v1.20.1


GOODLUCK
