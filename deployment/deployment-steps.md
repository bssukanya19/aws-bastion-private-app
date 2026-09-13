# Deployment Steps

## 1. Create VPC

Created VPC:

- Name: task1-vpc
- CIDR: 10.0.0.0/16

## 2. Create Subnets

Created public and private subnets.

Public subnets:

- 10.0.1.0/24
- 10.0.3.0/24

Private subnet:

- 10.0.4.0/24

## 3. Internet Gateway

Created and attached an Internet Gateway to the VPC.

## 4. NAT Gateway

Created NAT Gateway for private subnet internet access.

## 5. Route Tables

Public route table:

- 0.0.0.0/0 → Internet Gateway

Private route table:

- 0.0.0.0/0 → NAT Gateway

## 6. Bastion Host

Created a public EC2 instance as the Bastion Host.

Bastion allows SSH access from the administrator's IP.

## 7. Private EC2

Created a private EC2 instance without a public IP.

The private server runs Nginx.

## 8. Security Groups

### Bastion-SG

- SSH 22 from administrator IP

### ALB-SG

- HTTP 80 from Internet

### App-SG

- SSH 22 from Bastion-SG
- HTTP 80 from ALB-SG

## 9. Nginx

Installed Nginx on the private EC2.

Application files were placed in:

    /var/www/html/

## 10. Target Group

Created target group:

    privateTargetgroup

Protocol:

    HTTP : 80

Registered the private EC2 as the target.

## 11. Application Load Balancer

Created an Internet-facing Application Load Balancer.

Listener:

    HTTP : 80

The listener forwards requests to:

    privateTargetgroup

## 12. Testing

Opened the ALB DNS name in a web browser.

The application was successfully displayed from the private EC2.
