https://medium.com/@vishal.sharma./running-jenkins-in-kubernetes-cluster-with-persistent-volume-da6584edc126
https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html

To attach PV to jenkins deployment, follow the steps

1. Delete existing storage class gp2 created by EKS.
2. Create new SC with this link - https://docs.aws.amazon.com/eks/latest/userguide/storage-classes.html
3. To create PV we need EBS CSI addon, to create addon on EKS use the below links
  a) https://docs.aws.amazon.com/eks/latest/userguide/ebs-csi.html
  b) https://docs.aws.amazon.com/eks/latest/userguide/csi-iam-role.html
  c) https://docs.aws.amazon.com/eks/latest/userguide/managing-ebs-csi.html
4. While enabling the connection between jenkins cloud with EKS kube controlplane, use this link
    https://github.com/helm/charts/issues/1092
