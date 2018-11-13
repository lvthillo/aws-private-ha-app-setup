# aws-private-ha-app-setup

This template will deploy a VPC which contains two public subnets (using an Internet Gateway) and two private subnets. There are also two EC2 applications created which are hosted in private subnets in different Availability Zones (HA). The EC2's will host an Apache server. It was able to download the ```httpd``` package from the internet by using a NAT Gateway. Also an additional EC2 is created in a public subnet (public IP) to make this EC2 reachable from the internet. This EC2 will serve as bastion host. It is possible to ```SSH``` inside the bastion host and connect from there to the private EC2 instances which are hosting the basic website.   

### Prerequisites
* Define parameters in parameters.json
* Create a key pair on AWS and define this key pair in your parameters.json

### Diagram
![foto1](https://user-images.githubusercontent.com/14105387/48376436-3bc02d80-e6cb-11e8-875f-bc84f6e99ae3.png)
