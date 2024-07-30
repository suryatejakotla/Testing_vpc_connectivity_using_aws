# Testing_vpc_connectivity_using_aws
![image](https://github.com/user-attachments/assets/3816476c-be7b-4b43-8f0b-06e4c954da64)


##Get ready to:

>⬆️ Connect to your Public Server from the AWS Management Console.

>🤝 Test connectivity between your EC2 instances.

>🛜 Test VPC connectivity with the internet.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Log in to your AWS Account.

Head to the VPC set up page that uses a resource map.

Set up a VPC with the same architecture as what you've built in previous projects.

1 Availability Zone

1 public subnet with CIDR block `10.0.0.0/24`

1 private subnet with CIDR block `10.0.1.0/24`

0 NAT gateways or VPC endpoints.

##Create your VPC.

![2](https://github.com/user-attachments/assets/970776ff-2855-4010-b37c-b756bf0a4ff5)

Rename your resources

Let's tidy up our resources' names! Take 3 minutes to:

Rename your VPC to 

- Rename your private subnet 

+ Rename your public subnet.

* Rename your public route table.

- Rename your private route table. 

+ Rename your internet gateway. 

* Rename your VPC's default NACL.

##Create new resources

- Create a NEW network ACL for your private subnet that does not allow any inbound or outbound traffic.
- Investigate the inbound rules of the default security groups set up for you.

![3](https://github.com/user-attachments/assets/4daaf045-6413-4d3f-b487-eba5f9226bc1)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![4](https://github.com/user-attachments/assets/16bb1557-6b92-4681-ba3f-b29d91572ae7)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

#Launch a new EC2 instance in NextWork Public Subnet

![6](https://github.com/user-attachments/assets/66c79128-ca4e-4a4a-9e95-644d0c60fee4)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
##Launch an EC2 instance:

- Key pair: NextWork key pair.
  
>[!NOTE:]
>If you've never created  key pair, or you've deleted it, create a new key pair using the default settings.

- VPC: VPC from the drop-down in the VPC list.

- Subnet:  Public Subnet

- Update Auto-assign public IP to Enable.

- Security Group:  Public Security Group

### add Inbound security rules  to the public security group


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

![7](https://github.com/user-attachments/assets/1fb137a9-9dac-4e69-a07d-04989db7f4b0)



-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### connect to the public server 



![image](https://github.com/user-attachments/assets/8cab229e-c871-4c1f-bd23-069a98e2688c)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- Let's investigate what happened by reviewing our security settings.

- Look at you go, this is an iconic move for anyone testing their VPC's connectivity!

- Investigate your public subnet's Route table and Network ACL tabs.

**ping to the private server of ec2 instance.**

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://github.com/user-attachments/assets/03ad6bfc-1fb6-4d63-9f8f-1f7fd08a6574)


###Your public subnet's route table

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


![image](https://github.com/user-attachments/assets/e1554289-d497-4a7c-a3a3-977697b5ebec)


###Your public subnet's network ACLs.



###Add a new rule for SSH traffic, with Anywhere-IPv4 as the source type.


**Connect to your public server again.**


Phew! Success.

![8](https://github.com/user-attachments/assets/e9b6a804-506b-451b-b716-20ad666cb7ec)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
- Get your Public Server to talk to your Private Server (hellooo!)


- Troubleshoot another connection issue (detective mode stays on!)


- Leave open the EC2 Instance Connect tab, but find and copy your private server's Private IPv4 address in a new tab.


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
![image](https://github.com/user-attachments/assets/e63bc317-33ea-4b18-af37-685349b0ef5d)

- To resolve this connectivity error, let's investigate whether NextWork Private Server is allowing in ICMP traffic.


▶️ Alright, resuming now!

- Leave open the EC2 Instance Connect tab, but investigate your private subnet's Route table and Network ACL in a new tab.


- Aha! Mystery solved.

- Edit NextWork Private NACL to add a new inbound rule:

- Type: All ICMP - IPv4.

- Source: your public subnet's IPv4 CIDR block.

- Add the same rule for your private network ACL's outbound rules.

- Before we finish, investigate your private server's security groups - does this security group allow ICMP traffic? (Nope!)

- Create a new inbound security group rule:

- Type: All ICMP - IPv4.

- Source: NextWork Public Security Group.

- Revisit the EC2 Instance Connect tab that's connected to NextWork Public Server.


- Woah! Lots of new lines coming through in the terminal.

![9](https://github.com/user-attachments/assets/0f398930-8b20-41e8-9e81-347691ec0281)


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


![image](https://github.com/user-attachments/assets/99cab36f-6055-42d2-9df4-55cf6cc17f93)


- Your Public Server now gets replies from the Private Server!


#Test VPC connectivity with the internet

- Since your NextWork Public Route Table has a route from the NextWork Public Subnet to an internet gateway, you can validate that resources in NextWork Public Subnet can access the internet!


- In this step, you're going to:

###Get your Public Server to talk to the internet (off we go!)

###Troubleshoot an error response (awesome learnings here!)

- Quit the ping command in your terminal.
- Run a new command: `curl example.com`

![10](https://github.com/user-attachments/assets/9fa3e62a-b56a-47e1-99a5-c09e6582df62)


- Now let's try running curl with the URL that your terminal returned. Run 
`curl https://learn.nextwork.org/projects/aws-host-a-website-on-s3`


>[!results]


> **Congratulations!!**


>That was a massive success in testing your VPC's connectivity between your subnets and with the external internet.










