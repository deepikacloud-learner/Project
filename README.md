# AWS VPC Peering Project

## Project Overview

This project demonstrates how to establish secure network connectivity between two Amazon Virtual Private Clouds (VPCs) using VPC Peering.

## Objectives

- Create two separate VPCs.
- Configure VPC Peering between the VPCs.
- Update route tables to enable communication.
- Configure security groups to allow the required traffic.
- Test connectivity between resources in both VPCs.

## AWS Services Used

- Amazon VPC
- VPC Peering
- EC2 (if used in your lab)
- Route Tables
- Security Groups

## Architecture
```mermaid
flowchart TB
    subgraph AWS["AWS Region: us-east-2"]
        direction LR
        subgraph A["VPC-A | 10.0.0.0/16"]
            direction TB
            SA["Private Subnet A<br/>10.0.1.0/24"]
            ECA["EC2-A<br/>Private IP: 10.0.1.x"]
            RTA["Route Table A"]
            EP["SSM Interface Endpoints<br/>ssm, ssmmessages, ec2messages"]
            SA --> ECA
            ECA -.-> EP
            RTA
        end
        PCX["VPC Peering<br/>Active"]
        subgraph B["VPC-B | 20.0.0.0/16"]
            direction TB
            SB["Private Subnet B<br/>20.0.1.0/24"]
            ECB["EC2-B<br/>20.0.1.178"]
            RTB["Route Table B"]
            SB --> ECB
            RTB
        end
        RTA <-->|"Peering routes"| PCX
        PCX <-->|"Peering routes"| RTB
        ECA <-->|"Private traffic"| ECB
    end
    EP -.-> SSM["AWS Systems Manager<br/>Session Manager"]
```
Two VPCs are connected using a VPC Peering connection. Route tables are configured to allow traffic between the required networks.

## Implementation Steps

1. Create two VPCs with non-overlapping CIDR blocks.
2. Create subnets in both VPCs, if required.
3. Create a VPC Peering connection.
4. Accept the peering request.
5. Update the route tables on both sides.
6. Configure security groups to allow the required traffic.
7. Test connectivity between the VPCs.
   

## Testing and Validation

The VPC Peering connectivity was validated by testing communication between EC2 instances in the private subnets.

- **Source:** EC2-A in VPC-A
- **Destination:** EC2-B in VPC-B
- **Test:** ICMP ping
- **Result:** Successful
- **Packet loss:** 0%

The successful ping test confirms private network connectivity between the two VPCs through the VPC Peering connection.

## Key Learnings

- VPC Peering configuration
- Route table management
- Security group configuration
- Private network connectivity
- AWS network troubleshooting
  ## Project Screenshots

The following screenshots document the VPC Peering implementation and validation.

### 1. VPC Configuration

### 2. VPC Peering Connection

### 3. Private Subnets and Route Tables

### 4. SSM VPC Endpoints

### 5. EC2 Connectivity Test

### 1. VPC Configuration
![VPC Created](<Vpc A&B Created.png>)

### 2. Private Subnets
![Private Subnets](<Private subnet created A&B.png>)

### 3. Route Tables
![Route Table A](<Created Route Table-A.png>)
![Route Tables A and B](<Created RT-A&B.png>)

### 4. Route Table Associations
![RT-A](<RT-A route associated B.png>)
![RT-B](<RT-B route associate A.png>)

### 5. Connectivity Testing
![VPC-A to VPC-B](<Test VPC-A TO VPC -B.png>)
![VPC-B to VPC-A](<Test VPC-B TO VPC-A.png>)

## Author

Deepika Vijayakumar

GitHub: https://github.com/deepikacloud-learner
