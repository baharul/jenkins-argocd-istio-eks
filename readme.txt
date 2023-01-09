
EKS CLUSTER CREATION:

1. Use eks-cluster-creation.yaml to deploy EKS with one managed OnDemand Instance Node Group && SPOT node instance group.
2. Use cluster-autoscaler.yaml to deploy cluster autoscaler for autoscaling Nodes in EKS.
Ref: https://www.youtube.com/watch?v=gwmdboC-BtE&t=262s && https://www.youtube.com/playlist?list=PLiMWaCMwGJXkbN7J_j3qFEZVBacdoYCPJ



KANIKO:

1. From 1.24 onwards, kubernetes doesnt support Docker and docker cli commands, so kaniko is needed to build and push docker image.
    a) https://devopscube.com/build-docker-image-kubernetes-pod/
    b) https://computingforgeeks.com/build-container-images-using-kaniko-in-kubernetes/
    c) https://blog.csanchez.org/2020/10/07/building-docker-images-with-kaniko-pushing-to-amazon-elastic-container-registry-ecr/
    d) https://medium.com/clarusway/how-to-use-images-from-a-private-container-registry-for-kubernetes-aws-ecr-hosted-private-13a759e2c4ea


JENKINS(Jenkins Folder):

1. Deploy Jenkins with Master slave concept with the yamls inside the Jenkins folder

    https://medium.com/@vishal.sharma./running-jenkins-in-kubernetes-cluster-with-persistent-volume-da6584edc126
    https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html

To attach PV to jenkins deployment, follow the steps

2. Delete existing storage class gp2 created by EKS.
3. Create new SC with this link - https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html
4. To create PV we need EBS CSI addon, to create addon on EKS use the below links
  a) https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html
  b) https://docs.aws.amazon.com/eks/latest/userguide/csi-iam-role.html
  c) https://docs.aws.amazon.com/eks/latest/userguide/managing-ebs-csi.html
5. While enabling the connection between jenkins cloud with EKS kube controlplane, use this link
    helm/charts#1092

6. Sample Jenkinsfile placed inside the Jenkins folder - Ref - https://github.com/kunchalavikram1427/jenkins-end-to-end-pipeline/blob/master/Jenkinsfile



ARGOCD(argocd Folder):

1. kubectl create namespace argocd
2. kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
3. kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
4. kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
5. Create outpath Role, for argoCdToken to be used in Jenkinsfile for creating argocd app.
   a) https://medium.com/geekculture/create-a-new-user-in-argocd-using-the-cli-and-configmap-8cbb27cf5904


ARGOCD - HELM CHARTS for APP DEPLOYMENT:

1. We use APP of APPS model to deploy applications in EKS.
2. Please refer this url to get idea = https://github.com/LukeMwila/microservice-example-helm-charts





