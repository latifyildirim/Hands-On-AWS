# Hands-on VPC-01 : Configuring of VPC

Purpose of the this hands-on training is to create VPC and configure VPC with components.

## Learning Outcomes

At the end of the this hands-on training, students will be able to;

- learn how to create VPC,

- learn how to create subnet,

- learn how to set route tables as public and private,


## Outline

- Part 1 - Creating VPC, Subnet and Subnet associations



## Part 1 - Creating VPC, Subnet and Subnet associations

STEP 1: Create VPC

- First, go to the VPC and select Your VPC section from the left-hand menu, click create VPC.

- `Resources to create` :

```text
VPC only 

Note: After you  create VPC and all other components, show how you can do it easly via the option of "VPC, subnets, etc."
```

- create a vpc named "latif-vpc-a" with `10.7.0.0/16` CIDR
    - no ipv6 CIDR block
    - tenancy: default

- click create

- explain the vpc descriptions

- enable DNS hostnames for the vpc 'latif-vpc-a'

  - select 'latif-vpc-a' on VPC console ----> Actions ----> Edit DNS hostnames
  - Click enable flag
  - Click save 

STEP 2: Create an internet gateway named 'latif-igw'

- Go to the Internet Gateways from left hand menu

- Create Internet Gateway
   - Name Tag "latif-igw" 
   - Click create button

-  attach the internet gateway 'latif-igw' to the vpc 'latif-vpc-a'
  - Actions ---> attach to VPC
  - Select VPC named "latif-vpc-a"
  - Push "Attach Internet gateway"

STEP 3 : Configuring Route Table

- Go to the Route Tables from left hand menu

- rename the route table of the vpc 'latif-vpc-a' as 'latif-default-rt'

- select Routes on the sub-section

- click edit routes

- click add route

- add a route
    - destination ------> 0.0.0.0/0 (any network, any host)
    - As target;
      - Select Internet Gateway
      - Select 'latif-igw'
      - save routes

- explain routes in the latif-default-rt

STEP 4: Create Subnets
- Go to the Subnets from left hand menu
- Push create subnet button
```text
1. 
Name tag          :latif-az1a-public-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1a
IPv4 CIDR block   :10.7.1.0/24

2. 
Name tag          :latif-az1a-private-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1a
IPv4 CIDR block   :10.7.2.0/24

3. 
Name tag          :latif-az1b-public-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1b
IPv4 CIDR block   :10.7.4.0/24

4. 
Name tag          :latif-az1b-private-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1b
IPv4 CIDR block   :10.7.5.0/24

5. 
Name tag          :latif-az1c-public-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1c
IPv4 CIDR block   :10.7.7.0/24

6. 
Name tag          :latif-az1c-private-subnet
VPC               :latif-vpc-a
Availability Zone :us-east-1c
IPv4 CIDR block   :10.7.8.0/24
```
- explain the subnet descriptions and reserved ips (why 251 instead of 256)

STEP 5: Route Tables

- Go to the Route Tables from left hand menu

- Select 'latif-default-rt' and click the Subnet Association from sub-section

- show the default subnet associations on the route table 
latif-default-rt (internet access is available even on private subnets)
- push the create route table button

- create a private route table (not allowing access to the internet) 
  - name: 'latif-private-rt'
  - VPC : 'latif-vpc-a'
  - click create button

- show the routes in the route table latif-private-rt,

- click Subnet association button and show the route table latif-private-rt with private subnets

- Click Edit subnet association
- select private subnets;
  - latif-az1a-private-subnet
  - latif-az1b-private-subnet
  - latif-az1c-private-subnet
  - and click save

- create a public route table (allowing access to the internet) 

- push the create route table button
  - name: 'latif-public-rt'
  - VPC : 'latif-vpc-a'
  - click create button

- show the routes in the route table latif-public-rt,

- click Subnet association button and show the route table 

-Show the default route table subnet association . There are only 3 subnet implicitly.

- latif-public-rt with public subnets

- Click Edit subnet association

- select public subnets;
  - latif-az1a-public-subnet
  - latif-az1b-public-subnet
  - latif-az1c-public-subnet
  - and click save

- select Routes on the sub-section of latif-public-rt

- click edit routes

- click add route

- add a route
    - destination ------> 0.0.0.0/0 (any network, any host)
    - As target;
      - Select Internet Gateway
      - Select 'latif-igw'
      - save routes    
      
STEP 6: enable Auto-Assign Public IPv4 Address for public subnets

- Go to the Subnets from left hand menu

  - Select 'latif-az1a-public-subnet' subnet ---> Action ---> Modify auto-assign IP settings  ---> select 'Enable auto-assign public IPv4 address' ---> Save

  - Select 'latif-az1b-public-subnet' subnet ---> Action ---> Modify auto-assign
  IP settings  ---> select 'Enable auto-assign public IPv4 address' ---> Save

  - Select 'latif-az1c-public-subnet' subnet ---> Action ---> Modify auto-assign
  IP settings  ---> select 'Enable auto-assign public IPv4 address' ---> Save

- Create two instances . One is in the Private and the other one is in Public subnet. Show the public and private IPs of instances. 

- Compare the IP of instance and Subnet CIDR block.


