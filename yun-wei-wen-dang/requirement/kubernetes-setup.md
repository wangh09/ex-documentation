# Kubernetes cluster setup

## 1. Create the k8s cluster

### a\) AWS

###### Build a aws role，and choose IAM by Services Page

###### ![](/assets/aws_IAM.png)

###### Choose Users and click Add user button

###### ![](/assets/setup_user_1.png)

###### Configure user information shown on the page

###### ![](/assets/setup_user_2.png)

###### Configure user privieleges and choose and add correct permissions policies. create user at last

###### ![](/assets/aws permissions.png)

###### Back to user page, click username, then choose security credentials tab page. click create access key and record access key ID and secret.

###### ![](/assets/aws-role-credential.png)

###### TODO: These credentials will be used when creating kubernetes cluster.

* ###### Create kubernetes cluster.

`curl -o kubectl https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/darwin/amd64/kubectl`

* Create aws account configurations

```
1. Download aws cli command (https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/awscli-install-linux-al2017.html)
2. Run "aws condfiguration" command and fill in the correct key and password that are from aws access key
```

And the other steps, please follow this link  [https://linoxide.com/linux-how-to/eksctl-create-kubernetes-cluster-amazon-eks/](https://linoxide.com/linux-how-to/eksctl-create-kubernetes-cluster-amazon-eks/)

When everything is done. two nodes will be generated. and this cluster is just for test environment.

* ###### Configure ECR settings

```
1  Run aws command: "aws ecr get-login | sh" will generate ~/.docker/config.json
2. This file config.json will be imported to kubernetes secret key for pulling images from ECR
3. And this credential will also be used to push or pull images from ECR
```

## Appendix

* [https://linoxide.com/linux-how-to/eksctl-create-kubernetes-cluster-amazon-eks/](https://linoxide.com/linux-how-to/eksctl-create-kubernetes-cluster-amazon-eks/)

* [https://docs.aws.amazon.com/zh\_cn/eks/latest/userguide/what-is-eks.html](https://docs.aws.amazon.com/zh_cn/eks/latest/userguide/what-is-eks.html)

* [https://docs.aws.amazon.com/zh\_cn/cli/latest/userguide/awscli-install-linux-al2017.html](https://docs.aws.amazon.com/zh_cn/cli/latest/userguide/awscli-install-linux-al2017.html)

### b\) Google Cloud

### c\) Aliyun



