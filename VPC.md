1. Create VPC
	Name Tag: Anything
	IPv4 CIDR block : any range like 10.0.0.0/16

2. Create Subnet (Private and Public)
	Name tag: PrivatePVC
	VPC : Select Current Running VPC
	Availability Zone: As you ned
	IPv4 CIDR block: 10.0.1.0/24

3. Same for Public VPC
	Just Change IPv4CIDR Block: 10.0.2.0/24

4. Create Internat Gateway
	Name: MyGateway
	Then Attach to Running VPC

4.1 Customize the route table
	Create Route Table as Name Main Route
		Edit subnet Assosciate
			Select PrivateVPC
4.2 Create route table for PublicVPC named as custom
	Edit subnet Associate 
		select publicVPC

5. Create NAT Gatway
	Subnet: Select PublicVPC
	Elastic IP Allocation: Create

6. Again Edit the main route table
	Edit route
		add route 0.0.0.0/0 -------> NAT Gateway

6.1 Same for custom route 
	Edit route
		add route 0.0.0.0/0 ---------> Internet Gateway

7. Launch 2 instances one for private and one for public

8. Open terminal at local machine
	ssh-add -k your_key_name.pem
	ssh -A ec2-user@public_ip_address_of_public_instance

9. Now login private instance from public instance
	ssh ec2-user@private_ip_address_of_private_instance


Done!!!!!

