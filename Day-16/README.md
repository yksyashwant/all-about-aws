### What is VPC Peering ?
- In AWS, VPC peering is a network connection between two VPCs that enables you to route traffic between them using private IP addresses.
- Instances in either VPC can communicate with each other as if they are within the same network.
- VPC peering can be classified into two types based on the geographical location of the VPCs:

### Intra-Region VPC Peering
Intra-region VPC peering refers to peering connections between VPCs within the same AWS region.

#### Characteristics:
- **Low Latency**: Since the VPCs are in the same region, the latency is typically very low.
- **High Bandwidth**: The bandwidth available for data transfer is high.
- **Reduced Costs**: Data transfer charges are generally lower compared to inter-region data transfer.

#### Use Cases:
- **Microservices Architecture**: Different microservices running in separate VPCs within the same region can communicate securely and efficiently.
- **Data Segregation**: Separate environments (e.g., development, testing, production) in different VPCs within the same region can interact when necessary.

### Inter-Region VPC Peering
Inter-region VPC peering refers to peering connections between VPCs in different AWS regions.

#### Characteristics:
- **Cross-Region Communication**: Enables communication between resources in different regions, which is crucial for global applications.
- **Higher Latency**: Since the VPCs are in different regions, the latency is higher compared to intra-region peering.
- **Higher Costs**: Data transfer costs between regions are higher compared to intra-region transfers.

#### Use Cases:
- **Global Applications**: Applications with a global user base that require resources in multiple regions to communicate.
- **Disaster Recovery**: Replicating data and services across regions for disaster recovery and business continuity.
