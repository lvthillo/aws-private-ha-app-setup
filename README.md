# aws-private-ha-app-setup

This template will deploy a VPC which contains two public subnets (using an Internet Gateway) and two private subnets. There are also two EC2 applications created which are hosted in private subnets in different Availability Zones (HA). The EC2's will check when the NAT Gateway is working and install + host an Apache server. There EC2s were able to download the ```httpd``` package from the internet by using that NAT Gateway. Also an additional EC2 is created in a public subnet (public IP) to make this EC2 reachable from the internet. This EC2 will serve as bastion host. It is possible to ```SSH``` inside the bastion host and connect from there to the private EC2 instances which are hosting the basic website.   

### Prerequisites
* Create a key pair on AWS and define this key pair in your parameters.json
* Define parameters in parameters.json

### Create stack
Create stack using AWS CLI:
```
$ aws cloudformation create-stack --stack-name app --template-body file://template.yaml --parameters file://parameters.json 
```

### Diagram
![foto1](https://user-images.githubusercontent.com/14105387/48376436-3bc02d80-e6cb-11e8-875f-bc84f6e99ae3.png)

### Resources
Resources created in initial ChangeSet:
<img width="910" alt="screen shot 2018-11-13 at 18 43 12" src="https://user-images.githubusercontent.com/14105387/48434905-53ef8580-e77b-11e8-9e86-a0e5b857633c.png">

### Test application environment
* Visit Load Balancer: http://alb-xxx.eu-west-1.elb.amazonaws.com/
<img width="1438" alt="blur1" src="https://user-images.githubusercontent.com/14105387/48435653-53f08500-e77d-11e8-8ff2-6a5ea814689a.png">

* Test LB by turning of an EC2 instance.
* SSH to Bastion Host
```
$ ssh-add -K demo-key.pem
Identity added: demo-key.pem (demo-key.pem)
# SSH to Public IP of bastion host
$ ssh -A ec2-user@xx.xx.xx.xx 
```
* SSH from inside Bastion Host to private application instances
```
# SSH from Bastion host to private instances
$ ssh ec2-user@10.0.3.219
$ exit
$ ssh ec2-user@10.0.4.113
$ exit
```
