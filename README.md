# eks-helm-chart
Replicaset:
===========
* Replicaset can be used to create pods 
* if one pod down another pod container will start executing
* replicaset automatically increased pods based on given specified number
* if there is any changes in replicaset , it won't reflect the changes in the pods
* but itself replica can reflect the changes.
* to overcome this problem we have to use "Deployments"
cmds:
=====
* kubectl apply -f "replicaset-name"
* kubectl get pods
* kubectl get pods "pod-name" -o yaml
* kubectl get "replicasetname"
* kubectl get pods | grep image

Deployments:
=============
* Deployments can update the changes in the pods 

prometheus helm chart:
======================
* helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
*  

