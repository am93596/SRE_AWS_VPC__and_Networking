# AWS Virtual Private Cloud (VPC)
## CIDR Block for VPC
## Internet Gateway
## Subnets
### Route Tables
#### Network Access Control List (NACLs)
##### Security Groups

![image](https://user-images.githubusercontent.com/88166874/132207816-f0b0c4c3-150a-4a52-a5c7-631592bba387.png)

- What is a VPC
- AWS isolated virtual network - It allows us to control virtual network environment including selection of your own IPs address range, we can create multiple subnets within one VPC with specific network configuration. We can use both IPv4 and IPv6 for most resources, it provides security for your services or instances  

- What is an Internet Gateway?
- An Internet Gateway - can transfer communications between an enterprise network and the internet - it allows internet access into the VPC  

- What is a Subnet?
- A Subnet is a segmented piece of a larger network - the goal of a subnet is to split a large network into a group of smaller, **interconnected** networks to help minimise traffic - or navigate traffic securely  

- Route Table (RT)
- RT contains a set of rules, called routes, that are used to determine where the network traffic from your subnet or gateway is directed  

- Network Access Control List (NACL)
- NACLs are stateless - we have to explicitly allow inbound and outbound rules - they are an added layer of security at subnet level  

- 4.3 billion IP addresses in the world (approximately)
- Step 1: Create a VPC with IPv valid CIDR block
  - `10.0.0.0/16` - next team member to use `10.10.0.0/16`
- Step 2: Create internet gateway
  - 2.1: Attach the IG to your VPC
- Step 3: Create route table
  - 3.1 Edit route and insert your IG
- Step 4: Create public subnet
  - `10.0.1.0/24`
  - 4.1: Associate public subnet with our RT
- Step 5: Create public NACLs
  - set inbound and outbound rules for this
- Step 6: Create a Security Group for our app
