# Module 5 VPC Creation Lab

## Overview
This AWS networking lab was created as part of my preparation for the AWS Certified Cloud Practitioner exam, focusing specifically on networking fundamentals. In this lab, I built a custom Virtual Private Cloud (VPC) from scratch, including an Internet Gateway, two public subnets, and two private subnets distributed across two Availability Zones for high availability. The project helped reinforce my understanding of core networking components such as route tables, subnet isolation, and internet access configuration within AWS.

## Steps

### 1. Create the VPC
- 1.1 First navigate to the VPC service on the AWS console.
  - There will already be one VPC created for you in each region when you make the AWS account. To create a new one, click the create VPC button in the top right. Give it an appopriate name and set its CIDR range. This range essentially determines the available range of IPv4 addresses for the resources placed within the VPC.

  ![image](https://github.com/user-attachments/assets/45dddc2d-7bac-431d-a1e8-de3e15704789)

### 2. Create the subnets
- 2.1 I will be creating four total subnets. One private and one public subnet for two different availability zones. To create the first subnet go to the subnet section on the left side of the VPC console and select create subnet.
  
  ![image](https://github.com/user-attachments/assets/96661ee3-9648-406a-9ae7-7215a438c200)

- 2.2 I will first create the private subnet for AZ 1. I first select the new VPC I just created give the subnet a name, set the availability zone to our first chosen zone, and set the CIDR block for this subnet. I went with 10.0.1.0/24 which gives this subnet 256 potential IPv4 addresses to assign. Then I select create subnet.

  ![image](https://github.com/user-attachments/assets/8bf23ef9-4304-4932-b2a7-bdd90b0df2bf)

- 2.3 I then created the second private subnet using the same steps. Except this time, I set the CIDR block to 10.0.2.0/24 and the availability zone to my second option.
  
  ![image](https://github.com/user-attachments/assets/af7b257b-bdd5-42e6-9bf4-b56e172c3c42)

- 2.4 Then go into actions and edit the subnet settings for both of the private subnets and deselect the enable IPv4 public auto assign for both. These are private subnets that should not be able to reach the internet, so they don't need these to be assigned.

  ![image](https://github.com/user-attachments/assets/b71fe2f0-5c11-4af1-8f18-491eea790917)

  ![image](https://github.com/user-attachments/assets/79fceea5-4e90-4ee3-afe1-424f0c5fe857)

- 2.5 Then repeat the steps for the two public subnets. There should be one public subnet per AZ and each should have their own CIDR block as shown below. Also, this time the public IPv4 auto assign should be set.
  
  ![image](https://github.com/user-attachments/assets/983e8f91-b8ea-4191-a611-ae927429a84e)

### 3. Create Internet Gateway

- 3.1 At this point of the project, the public subnets can't actually access the internet. We have to set an internet gateway that acts as a bridge from our VPC to the internet. To do this, first go to the internet gateway section on the left side of the VPC console and select create internet gateway. Give it a simple name and select create.

- 3.2 After creation, it must be connected to the VPC we created. Go to actions in the top right of the internet gateway dashboard and select attach to VPC. It should give an attached indicator if done correctly.

  ![image](https://github.com/user-attachments/assets/247cfdba-37fb-4569-a9b9-16ff95ea8e07)

  ![image](https://github.com/user-attachments/assets/f96c8d5b-bab9-4737-9a77-06ccd51b0aa2)

### 4. Create Routing Table

- 4.1 Even though the interent gateway is connected to our VPC, any instances within our subnets wouldn't know how to reach it without the proper guidance. This is where a routing table comes in. To do this, go to the route tables section of the console and select route table. Give the table a name and link it to our VPC.

  ![image](https://github.com/user-attachments/assets/c3e4face-bde3-4f1d-8717-0e5d51853c6b)

- 4.2 Next click edit routes in the bottom right to create the route to our internet gateway.

  ![image](https://github.com/user-attachments/assets/9f1ac5cd-d625-491f-bdd9-0cc954d3cf02)

- 4.3 Within that screen, select add new route. Make the destination 0.0.0.0/0 and the target the internet gateway we created. This is essentially saying send any outbound traffic that is traveling out of the VPC throught the internet gateway.

  ![image](https://github.com/user-attachments/assets/a70b30de-1fc1-4a0f-9a71-6f3d546555e4)

-4.4 Then go into subnet associations and edit subnet associations. Select our two public subnets to be associated with the routing table we created. The routes will therefore only apply to the public subnets and not to our private subnets which shouldnt access the internet gateway.

![image](https://github.com/user-attachments/assets/5a3ae9f3-42dd-4270-bd1e-ba00732e91f5)

## Conclusion
This lab provided a hands-on opportunity to solidify key networking concepts within AWS by building a custom VPC architecture from the ground up. By configuring public and private subnets across multiple Availability Zones, attaching an Internet Gateway, and setting up appropriate route tables, I gained a deeper understanding of how AWS handles network traffic and isolation. This exercise reinforced the relationship between subnets, route tables, and gateways, and prepared me for questions related to networking on the AWS Certified Cloud Practitioner exam.
