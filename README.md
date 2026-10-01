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

Connectivity was tested between the VPCs after configuring the peering connection and routing. Add your actual test results and screenshots here.

## Key Learnings

- VPC Peering configuration
- Route table management
- Security group configuration
- Private network connectivity
- AWS network troubleshooting

## Author

Deepika Vijayakumar

GitHub: https://github.com/deepikacloud-learner
