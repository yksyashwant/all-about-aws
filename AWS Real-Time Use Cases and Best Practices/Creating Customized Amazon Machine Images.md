# Creating Customized Amazon Machine Images (AMIs)

- Custom AMIs allow you to standardize your AWS deployments, ensuring consistency across your environment.
- With a custom AMI, you can pre-configure software, settings, and other requirements, so every EC2 instance launched from it is ready to use without additional setup.

## **1. Prepare the Base EC2 Instance**

### **1.1 Launch a Base EC2 Instance**
- Select a base AMI from the AWS Marketplace or the public AMIs, such as Amazon Linux, Ubuntu, or Windows Server.
- Choose an instance type that matches your performance needs.

### **1.2 Connect to the EC2 Instance**
- Use **SSH** for Linux instances or **Remote Desktop Protocol (RDP)** for Windows instances to connect to the EC2 instance.

### **1.3 Install Software and Configure Settings**
- Install required software, libraries, and dependencies.
- Apply updates, patches, and security configurations.
- Configure environment variables, scripts, and other custom settings.

#### Example Setup Script:
```bash
#!/bin/bash

# Update the system
echo "Updating the system..."
sudo yum update -y

# Install essential tools
echo "Installing essential tools..."
sudo yum install -y git wget curl telnet

# Install Python 3 and pip
echo "Installing Python 3 and pip..."
sudo yum install python3 -y
sudo pip3 install --upgrade pip

# Install Java 11 
echo "Installing Java 11 ..."
amazon-linux-extras install java-openjdk11 -y

# Install Docker
echo "Installing Docker..."
sudo yum install docker -y
sudo systemctl enable docker
sudo systemctl restart docker

# Install MySQL client
echo "Installing MySQL client..."
sudo yum install mysql -y

# Install PostgreSQL client
echo "Installing PostgreSQL client..."
sudo amazon-linux-extras enable postgresql14
sudo yum install postgresql -y

# Final Verifications
echo "Verifying installed software versions:"
python3 --version
docker --version
mysql --version
psql --version

echo "Setup script execution completed successfully."
```

### **1.4 Test the Configuration**
- Ensure all installed software and configurations work as expected.

---

## **2. Clean Up the Instance**
Before creating the AMI, clean up the instance to remove unnecessary files and logs:

1. **Remove Temporary Files**:
   - Clear logs in `/var/log/` for Linux or `C:\Windows\Temp` for Windows.

2. **Remove SSH Keys**:
   - Delete any private keys or sensitive data.

3. **Stop Unnecessary Services**:
   - Ensure only required services are running.

---

## **3. Create a Custom AMI**

### **3.1 Stop the EC2 Instance**
- While not strictly necessary, stopping the instance ensures a clean snapshot.

### **3.2 Create the AMI**
1. In the AWS Management Console:
   - Navigate to **Instances**.
   - Right-click the instance and select **Image and templates > Create Image**.
2. Provide a name, description, and optional tags for the AMI.
3. Click **Create Image**.

### **3.3 Wait for the AMI Creation**
- Monitor the progress in the **AMIs** section of the console.

---

## **4. Use the Custom AMI**

### **4.1 Launch New Instances**
- Use the custom AMI to launch new EC2 instances with the preconfigured settings.

### **4.2 Share the AMI (Optional)**
- Share the AMI with other AWS accounts if needed by modifying its permissions.

### **4.3 Deregister AMIs (Optional)**
- If an AMI is no longer needed, deregister it from the **AMIs** section.

---

## **5. Automate the Process (Optional)**
For large-scale or frequent customization needs, consider using automation tools:

1. **AWS Systems Manager (SSM)**:
   - Use SSM Automation Documents to standardize and automate AMI creation.
2. **HashiCorp Packer**:
   - A popular tool to create custom AMIs using code-based templates.
3. **CloudFormation or Terraform**:
   - Automate infrastructure and AMI creation workflows.

---

## **Best Practices**
- **Versioning**: Use a clear versioning system for your AMIs to track changes over time.
- **Security**: Always include the latest updates and security patches.
- **Testing**: Test new AMIs before using them in production.
- **Cost Management**: Regularly clean up unused AMIs and associated snapshots.
