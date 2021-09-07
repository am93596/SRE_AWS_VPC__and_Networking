# AWS Virtual Private Cloud (VPC)

![image](https://user-images.githubusercontent.com/88166874/132207816-f0b0c4c3-150a-4a52-a5c7-631592bba387.png)

## What is a VPC
- AWS isolated virtual network - It allows us to control virtual network environment including selection of your own IPs address range, we can create multiple subnets within one VPC with specific network configuration. We can use both IPv4 and IPv6 for most resources, it provides security for your services or instances  

## What is an Internet Gateway?
- An Internet Gateway - can transfer communications between an enterprise network and the internet - it allows internet access into the VPC  

## What is a Subnet?
- A Subnet is a segmented piece of a larger network - the goal of a subnet is to split a large network into a group of smaller, **interconnected** networks to help minimise traffic - or navigate traffic securely  

## What is a Route Table (RT)
- RT contains a set of rules, called routes, that are used to determine where the network traffic from your subnet or gateway is directed  

## Network Access Control List (NACL)
- NACLs are stateless - we have to explicitly allow inbound and outbound rules - they are an added layer of security at subnet level  

> There are approximately 4.3 billion IP addresses in the world!  

- Step 1: Create a VPC with IPv valid CIDR block
  - Set location to Ireland
  - Search for `VPC` and hit `Enter`
  - Click `Launch VPC Wizard`
  - Click `Select`
  - Fill in the IPv4 CIDR Block for the VPC (e.g. `10.102.0.0/16`)
  - Name the VPC (e.g. `SRE_amy_vpc`)
  - Give the public subnet IPv4 CIDR (e.g. `10.102.2.0/24`)
  - Give the subnet name (e.g. `SRE_amy_public_sb`)
  - Click `Create VPC`
- Step 2: Create internet gateway
  - Navigate to `Internet Gateways` (on the left-hand side)
  - Click `create internet gateway`
  - Add a name tag (e.g. SRE_amy_ig)
  - Click `create`
  - attached ig automatically
    - If it didn't, click the IG, then click `Actions` -> `Attach VPC`
- Step 3: Create route table (if not automatically done)
  - Navigate to `Route Tables` (on the left-hand side)
  - Click `Create route table`
  - Fill in the name box: `SRE_amy_vpc_route_table`
  - Choose the VPC you made from the drop-down menu
  - Click `Create route table`
  - Connecting to the IG:
    - Select the route table
    - Click `Actions` -> `Edit routes`
    - Click `Add route` and fill in the destination as `0.0.0.0/0`, then select `Internet Gateway` from the Target drop-down menu and select your new IG
    - Click `Save`
- Step 4: Create public subnet
  - Navigate to `Subnets` and click `Create subnet`
  - Select the VPC you created earlier
  - Name the subnet (e.g. SRE_amy_public_sb)
  - Select Availability Zone eu-west-1a
  - Set the IPv4 CIDR Block to `10.102.2.0/24`
  - Click `Create subnet`
  - Associate public subnet with our RT
    - Once the subnet has been created, navigate to `Route Tables`, select your route table, and click `Actions` -> `Edit subnet associations`
    - Select your new subnet and click `Save associations`
- Repeat Step 4 for the private subnet, with the IPv4 CIDR Block set to `10.102.3.0/24`
- Step 5: Create public NACL
  - Here are the inbound rules for the public NACL - put your own IP in rule 1 with `/32` after
![public_nacl_inbound_rules](https://user-images.githubusercontent.com/88166874/132323496-3b94c814-21ec-4d75-94e7-4daeeed0e249.jpg)
  - Here are the outbound rules for the public NACL - put the IP for your private subnet in rule 1 with `/24` after
![public_nacl_outbound_rules](https://user-images.githubusercontent.com/88166874/132323508-c356f68a-2b94-4fd9-9f23-c1f271796bb9.PNG)
- Step 6: Create Security Groups for our app
  - Here are the Security Group inbound rules for the app instance - put your own IP in the rule for port 22, with `/32` after
![app_security_group_rules](https://user-images.githubusercontent.com/88166874/132345857-6367d4d7-bc32-47ca-b2d2-8f4697b25d64.jpg)
  - Here are the Security Group inbound rules for the db instance - put the IP for your app machine in the rule for port 27017 with `/32` after, and put your own IP in the rule for port 22 with `/32` after
 ![db_security_group_rules](https://user-images.githubusercontent.com/88166874/132345001-99f5cefc-0079-48ad-936d-f47676c4e3f5.jpg)


## AWS Regions and AWS Availability Zones
- AWS has multiple regions (over 100); each region has at least 2 or more availability zones
- Restriction. Redundancy. 
- An Availability Zone (AZ) is one or more discrete data centres with redundant power, networking, and connectivity ... (see rest of screenshot)
- Differences?
- **UNFINISHED**

> S3 Notes: (https://github.com/am93596/SRE_amy_s3/blob/main/README.md)
