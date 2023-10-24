## 88. Overview of Load Balancers

***

## 89. Create EC2 Security Groups

* A security group acts as a `virtual firewall` that controls the traffic for one or more instances.

* When you launch an instance, you associate one or more security groups with the instance.

* You `add rules` to `each security group` that allow traffic to or from its associated instances.

* You can modify the rules for a security group at any time; the new rules are automatically applied to all instances that are associated with the security group. When we decide whether to allow traffic to reach an instance, we evaluate all the rules from all the security groups that are associated with the instance.

### ELB (load balancer) security group
* add this rule
    - HTTP TCP 80 Anywhere
    - copy `Group ID`
  
### Web tier security group
* add these rules
    - HTTP TCP 80 Custom IP `<load-balancer-sg Group ID>`
    - SSH TCP 22 My IP
    - copy `Group ID`
* add this rule
    - MySql TCP 3306 Custom IP `<web-servers-sg Group ID>`

***

## 90. Create an ELB Load Balancer

* EC2 / Load balancers / Create load balancer
    - application or classic
    - name: web-elb
    - http & https
    - default VPC
    - add two subnets
* configure security groups
    - choose "load-balancer" security group which we just setup
* configure routing
    - target group: web-servers-tg1
    - ping path: /ping
    - allows us to define a "healthy" web server
    - load balancer will only forward to healthy web servers
* register targets
* create

***

## 91. Implementing the Load Balancer

### Create an AMI (Amazon Machine Image)
* EC2 / Instances / right-click instance / create image
    - image name: web-architecture-2019-10-31
    - description: web server 2019 October 31
    - no reboot: unchecked 
    - allowing your instance to reboot gives a better image
* create image

### Launch a new instance of your AMI in a new availability zone (AZ)
* what AZ is your current instance running in?
    - EC2 / instances / look at the availability zone and make note of it
* launch a new instance from your AMI
    - EC2 / AMIs / right click / launch / next: configure
* subnet: `<choose a different AZ>` / next: storage / next
* tag
    - value: web-server-0002
* security group
    - choose the "web-tier" security group we created
* launch
    - specify "key pair" we want the instance to use
* launch instance

### Add new EC2 instance to load balancer's target group
* add the new instance to the target group
* enter load balancer DNS into a browser to see your load balancer in action
    - refresh your browser to see the switching between web-servers-sg

***

## 92. Connecting to your MySQL Server using MySQL Workbench

***

## 93. Hands-on Exercise

***

## 94. Hands-on Solution

***

## 95. Autoscaling & CloudFront

***








