# aws-fargate-cloudformation
A CloudFormation template to create an ECS cluster with the Fargate launch type service and an application load balancer.

It opens port 80 of the container to the world and port 22 to a chosen single IP address. The ELB Listener opens port 443 and redirects HTTP traffic to HTTPS.

It also passes some environment variables from AWS Parameter Store to the container (see `Secrets` in the `ContainerDefinitions` section).

## Prerequisties 

1. An existing VPC and subnets
2. A docker image pushed to a repository (e.g. Amazon ECR)
3. An existing SSL certificate

## All resources to be created

* LoadBalancerSecurityGroup
* ContainerSecurityGroup
* ELBTargetGroup
* ELBLoadBalancer
* ELBListener
* ELBListenerPortRedirect
* ECSCluster
* ECSTaskDefinition
* ECSService

After the CloudFormation stack creation is finished, you need to point a domain or subdomain to the ELB Load Balancer endpoint. To do this, go to AWS Route53, select a hosted zone, add a new A alias record, and choose the proper endpoint from the list.
