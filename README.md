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
*  helm search repo prometheus-community
// get all prometheus related files
* install prometheus helm chart
* helm install prometheus prometheus-community/kube-prometheus-stack
* kubectl get pods
* kubectl get svc
====================================================
* for every service there is only single "load balancer"
* to overcome this problem we have to go for "NGINX ingress controller"
NGINX ingress controller supports NetWork Load Balancer


steps for NGINX ingress controller:
====================================
Add the Ingress-NGINX Helm Repository:
* helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
  helm repo update
* Install the NGINX Ingress Controller using Helm:
  helm install my-nginx-ingress ingress-nginx/ingress-nginx --namespace ingress-nginx --create-namespace
* Verify the Installation:
  kubectl get pods --namespace ingress-nginx
* To upgrade release version
  helm upgrade my-release oci://ghcr.io/nginx/charts/nginx-ingress --version 2.0.1

ingress.yaml:
==============
controller:
service:
internal:
enabled: false
targetPorts:
http: http
https: http
annotations:
service.beta.kubernetes.io/aws-load-balancer-backend-protocol: tcp
service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: '60'
service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: 'true'
service.beta.kubernetes.io/aws-load-balancer-type: nlb
service.beta.kubernetes.io/aws-load-balancer-ssl-cert: arn:aws:acm:us-east-1:633788536644:certificate/274d4c80-dc76-4296-b3ed-d959cbe837ba
service.beta.kubernetes.io/aws-load-balancer-ssl-ports: 443

Configuration explanation:
---------------------------
internal: enabled: false:
This specifies that the service is not internal. It means the LoadBalancer is internet-facing and can be accessed from outside the VPC.

targetPorts:
http: http and https: http: These define the target ports for the HTTP and HTTPS traffic. Essentially, HTTP traffic is directed to the HTTP port, and HTTPS traffic is also directed to the HTTP port (indicating SSL termination will be handled by the load balancer).

annotations:
service.beta.kubernetes.io/aws-load-balancer-backend-protocol: tcp:
This annotation specifies that the backend protocol is TCP. This means the load balancer will forward TCP traffic to the instances.
service.beta.kubernetes.io/aws-load-balancer-connection-idle-timeout: '60':
Sets the idle connection timeout to 60 seconds. This means the load balancer will close connections that are idle for 60 seconds.
service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: 'true':
Enables cross-zone load balancing, allowing the load balancer to distribute traffic across instances in all Availability Zones.
service.beta.kubernetes.io/aws-load-balancer-type: nlb:
Specifies that the type of load balancer to be used is a Network Load Balancer (NLB).
service.beta.kubernetes.io/aws-load-balancer-ssl-cert:
Provides the ARN of an SSL certificate in AWS Certificate Manager (ACM) to handle SSL termination at the load balancer. The provided ARN is arn:aws:acm:us-east-1:633788536644:certificate/274d4c80-dc76-4296-b3ed-d959cbe837ba.
service.beta.kubernetes.io/aws-load-balancer-ssl-ports: 443:
Specifies that SSL termination should occur on port 443. This means HTTPS traffic is terminated at the load balancer and forwarded to the backend using HTTP.



* kubectl get ingress
* kubectl get pods
* kubectl get svc

write some rules:
=================
any request comes and send to the load balancer 

ingress:
--------




