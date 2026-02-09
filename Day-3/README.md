#### INSTRUCTOR DETAILS

### Lab Session - Creation of a Ubuntu EC2 Instance

1. **Sign in to AWS Management Console:**
   - Navigate to the EC2 Dashboard at [AWS Management Console](https://console.aws.amazon.com/ec2/).

2. **Launch Instance:**
   - Click on "Launch Instance" to start the instance creation process.

3. **Choose AMI:**
   - In the "Step 1: Choose an Amazon Machine Image (AMI)" section, search for "Ubuntu" in the search bar.
   - Select the Ubuntu AMI of your choice (e.g., Ubuntu Server 20.04 LTS).

4. **Choose Instance Type:**
   - Select an instance type based on your requirements (e.g., t2.micro for a free-tier eligible instance). Click "Next: Configure Instance Details" when ready.

5. **Configure Instance:**
   - Configure instance details such as:
     - Number of instances to launch.
     - Network settings (usually default VPC and subnet settings are fine).
     - Optionally, configure advanced settings like IAM role, monitoring, and instance shutdown behavior. Click "Next: Add Storage" when ready.

6. **Add Storage:**
   - Specify the storage requirements for your instance. The default settings are typically sufficient for basic needs. Click "Next: Add Tags" when ready.

7. **Add Tags:**
   - Optionally, add tags to your instance for easier identification and management. Click "Next: Configure Security Group" when ready.

8. **Configure Security Group:**
   - Configure security group settings to control inbound and outbound traffic to your instance. At least allow SSH (port 22) access for Linux instances. You may also want to allow HTTP (port 80) or HTTPS (port 443) depending on your application needs.

9. **Review Instance Launch:**
   - Review all your instance details. Ensure everything is configured correctly. Click "Launch" when ready.

10. **Select Key Pair:**
    - In the pop-up window, select an existing key pair or create a new key pair. Key pairs are used to securely connect to your instance via SSH.

11. **Access Instance:**
    - Once the instance is launched, note the public IP address or DNS name of your instance from the EC2 dashboard.

12. **Connect to Ubuntu Instance:**
    - Use SSH to connect to your Ubuntu instance. Open a terminal on your local machine (Linux/Mac) or use PuTTY on Windows:
      ```
      ssh -i /path/to/private-key.pem ubuntu@public-ip-address
      ```
      Replace `/path/to/private-key.pem` with the path to your private key file, `ubuntu` with the default username for Ubuntu instances, and `public-ip-address` with the public IP address of your instance.

13. **Start Using Ubuntu Instance:**
    - You are now connected to your Ubuntu EC2 instance. Start installing applications, configuring services, and exploring the capabilities of Ubuntu on AWS.
----
### AWS Elastic IP (EIP)

AWS Elastic IP (EIP) is a static, public IP address that can be allocated to your AWS resources, such as Amazon EC2 instances, to enable communication with the internet.

#### Key Features and Benefits:

1. **Static IP Address**
   - Unlike dynamic IP addresses that can change when an instance is stopped or started, an EIP remains constant.

2. **Persistent Association**
   - An EIP remains associated with your AWS account until you choose to release it, ensuring continuity of services and reliable access.

3. **Flexibility**
   - EIPs can be remapped to another instance within your account, allowing you to quickly recover from instance or availability zone failures.

4. **Availability**
   - EIPs enable your AWS resources to have a fixed public IP address, facilitating communication with the internet or external systems.

#### Use Cases:

1. **Web Hosting**
   - Assign an EIP to your EC2 instance running a web server to ensure users can reliably access your website.

2. **Disaster Recovery**
   - Quickly remap an EIP to a standby instance in case of failure, minimizing downtime and ensuring business continuity.

3. **Dynamic DNS**
   - Use an EIP with dynamic DNS services to maintain consistent access to applications even when underlying instances change.

#### Important Considerations:

- **Cost**
  - While EIPs themselves are free, AWS charges you if an EIP is associated with a stopped instance or not associated with any instance.

- **Limits**
  - AWS limits the number of EIPs you can have per region. You can request an increase if necessary.

- **Best Practices**
  - Use EIPs sparingly and release them when no longer needed to avoid unnecessary charges.

#### How to Allocate and Associate an EIP:

1. **Allocate an EIP**:
   - In the AWS Management Console, go to the EC2 Dashboard.
   - Click on "Elastic IPs" in the sidebar.
   - Click the "Allocate new address" button and confirm.

2. **Associate an EIP with an EC2 Instance**:
   - Select the allocated EIP.
   - Click on the "Actions" dropdown and select "Associate address."
   - Choose the instance or network interface you want to associate the EIP with, and confirm the association.

----
### AWS Security Groups

A security group acts as a virtual firewall for your EC2 instances to control incoming and outgoing traffic.

#### Key Features and Benefits:

1. **Inbound and Outbound Rules**
   - **Inbound Rules**: Control the incoming traffic to your instance.
   - **Outbound Rules**: Control the outgoing traffic from your instance.

2. **Default Security Group**
   - If you don't specify a security group when you launch an instance, Amazon EC2 uses the default security group.

3. **Flexible Rule Management**
   - You can add, modify, or remove rules in a security group at any time.
   - New and modified rules are automatically applied to all instances associated with the security group.

4. **Multiple Security Groups**
   - You can specify one or more security groups when you launch an instance.
   - Amazon EC2 evaluates all rules from all security groups associated with an instance to decide whether to allow traffic.

#### How Security Groups Work:

- **Creating Security Groups**:
  - In the AWS Management Console, go to the EC2 Dashboard.
  - Click on "Security Groups" in the sidebar.
  - Click the "Create security group" button and define the group name, description, and VPC.
  - Add inbound and outbound rules as needed.

- **Inbound and Outbound Rules**:
  - **Inbound Rules**: Define which traffic is allowed to reach your instance. Example: Allow SSH access on port 22 from a specific IP range.
  - **Outbound Rules**: Define which traffic is allowed to leave your instance. Example: Allow all outbound traffic to any destination.

- **Modifying Security Groups**:
  - Select the security group you want to modify.
  - Add, edit, or remove inbound and outbound rules as necessary.
  - Changes are automatically applied to all associated instances.

#### Example Use Cases:

1. **Web Servers**:
   - Allow inbound HTTP (port 80) and HTTPS (port 443) traffic from anywhere.
   - Allow SSH (port 22) access only from a specific IP address or range.

2. **Database Servers**:
   - Allow inbound traffic only from specific application servers.
   - Restrict outbound traffic to limit external connections.

3. **Application Servers**:
   - Allow inbound traffic on specific ports required by the application.
   - Allow outbound traffic to databases and other services.

#### Important Considerations:

- **Stateful Nature**:
  - Security groups are stateful, meaning if you allow an incoming request from an IP, the response is automatically allowed.

- **Evaluation of Rules**:
  - When Amazon EC2 decides whether to allow traffic to reach an instance, it evaluates all of the rules from all of the security groups associated with the instance.

- **Changes Applied Automatically**:
  - Any changes to security group rules are immediately applied to all associated instances without needing to restart them.

By effectively managing security groups, you can enhance the security of your AWS environment by controlling access to and from your EC2 instances.

----
### Spot Instances, On-Demand Instances, Savings Plans, Reserved Instances, Dedicated Hosts, Scheduled Instances, Capacity Reservations


Amazon EC2 offers a variety of instance purchasing options to help you optimize costs and meet your specific workload requirements. Here are the main options:

1. **Spot Instances**
   - **Description**: Allows you to bid on unused EC2 capacity at potentially lower prices than On-Demand instances.
   - **Use Cases**:
     - Fault-tolerant workloads
     - Big data analysis
     - Batch processing
     - CI/CD workloads

2. **On-Demand Instances**
   - **Description**: Allows you to pay for compute capacity by the hour or second, with no long-term commitments.
   - **Use Cases**:
     - Short-term, spiky, or unpredictable workloads
     - Applications being developed or tested for the first time

3. **Savings Plans**
   - **Description**: Offers significant savings over On-Demand instances in exchange for committing to a consistent amount of usage (measured in USD per hour) for a 1- or 3-year term.
   - **Use Cases**:
     - Long-term, stable workloads
     - Ability to commit to consistent usage for cost savings

4. **Reserved Instances**
   - **Description**: Provides a significant discount (up to 75%) compared to On-Demand pricing in exchange for a 1- or 3-year commitment.
   - **Use Cases**:
     - Steady-state workloads
     - Applications with predictable usage patterns

5. **Dedicated Hosts**
   - **Description**: Physical EC2 servers dedicated for your use, helping you address compliance requirements and reduce costs by using your existing server-bound software licenses.
   - **Use Cases**:
     - Licensing requirements that do not support multi-tenancy or cloud deployments
     - Compliance and regulatory requirements

6. **Scheduled Instances**
   - **Description**: Allows you to purchase instances that are always available on the specified recurring schedule, matching your capacity needs.
   - **Use Cases**:
     - Predictable workloads that require a fraction of a day, week, or month
     - Batch processing during specific times

7. **Capacity Reservations**
   - **Description**: Ensures that you have reserved capacity for your EC2 instances in a specific Availability Zone for any duration.
   - **Use Cases**:
     - Applications requiring guaranteed compute capacity
     - Business-critical workloads that need to avoid capacity constraints

### Summary

- **Spot Instances**: Cost-effective for fault-tolerant and flexible workloads.
- **On-Demand Instances**: Best for short-term, unpredictable workloads without upfront commitment.
- **Savings Plans**: Offer cost savings for consistent usage over a long term.
- **Reserved Instances**: Suitable for predictable and steady-state applications with long-term commitments.
- **Dedicated Hosts**: Address licensing and compliance requirements with dedicated physical servers.
- **Scheduled Instances**: Ideal for predictable workloads requiring specific schedules.
- **Capacity Reservations**: Guarantee capacity for business-critical applications.

Each of these options provides different pricing models and flexibility, allowing you to optimize costs while meeting the specific needs of your workloads.

----
### Lab Session - Opening a Support Ticket with AWS

### Example Description for an EBS Issue: Unable to Mount in Linux Server

Here is an example of a detailed description you might provide for an issue where you are unable to mount an EBS volume on a Linux server:

---

**Service**: Elastic Block Store (EBS)  
**Category**: Volume Availability  
**Severity**: System impaired  

**Description**:
I am experiencing an issue with mounting an EBS volume on my Linux server. The details are as follows:

- **Volume ID**: vol-0abc12345def67890
- **Instance ID**: i-0abc12345def67890
- **Issue**: Unable to mount the EBS volume to the EC2 instance.

Please assist in diagnosing and resolving this issue, as it is preventing us from accessing important data on the EBS volume. Can we have a quick call to discuss this further?

----

### Metadata and User Data in Amazon EC2

#### Metadata

**Definition**: EC2 instance metadata provides dynamic information about an instance at runtime, such as instance ID, instance type, public IP address, and more.

- **Access**: Metadata is accessible from within the instance using a special endpoint:
  - Endpoint URL: `http://169.254.169.254/latest/meta-data/`
  - Example: `http://169.254.169.254/latest/meta-data/instance-id`

- **Usage**:
  - Retrieving instance-specific information dynamically.
  - Automation scripts that need to fetch details about the instance at runtime.
  - Monitoring and debugging tools that require current instance metadata.

#### User Data

**Definition**: User data allows you to pass custom startup scripts or configuration to your EC2 instances during launch.

- **Purpose**:
  - **Automation**: Configure instances automatically with software installs, updates, or specific configurations.
  - **Initialization**: Run custom scripts or commands upon instance startup.
  - **Setup**: Customize instance behavior based on launch parameters.

- **Format**: User data is provided as plain text or base64-encoded data, attached to the instance at launch.
  
- **Access**:
  - Specify user data through the AWS Management Console, CLI, or SDKs when launching instances.
  - Retrieve and execute user data scripts inside the instance during initialization.

#### Example Use Cases

1. **Metadata**:
   - **Instance Identification**: Fetching instance ID for logging or monitoring purposes.
   - **Networking**: Retrieving public or private IP addresses dynamically.
   - **Instance Type**: Determining hardware characteristics for workload optimization.

2. **User Data**:
   - **Configuration Management**: Installing and configuring software packages (e.g., Apache, MySQL) upon instance launch.
   - **Custom Scripts**: Running scripts for setup tasks like environment variable configuration or application deployment.
   - **Automation**: Initializing instances with predefined configurations to streamline deployment processes.

#### Security Considerations

- **Metadata**: Accessible only from within the instance, ensuring security of instance-specific information.
- **User Data**: Should not contain sensitive information unless encrypted or securely managed, as it's readable during instance initialization.
