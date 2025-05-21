# Overview
This section provides a foundational understanding of how Infinity Learn utilizes Google Cloud Platform (GCP) to support its infrastructure, applications, and business operations.

# Purpose of the Document
This document is a comprehensive guide to the GCP infrastructure used by Infinity Learn. It is intended for:

1. Internal DevOps, Cloud Engineering, and Security teams

2. Onboarding of new engineers

3. Compliance and audit reviews

4. Infrastructure scaling and troubleshooting

5. Documentation of best practices

# Architecture
Infinity Learn's cloud infrastructure on GCP is designed to ensure scalability, high availability, performance, and security for its digital learning platform. The architecture follows modern cloud-native principles using a combination of managed services, container orchestration, automated deployment pipelines, and centralized monitoring.The system is organised into multiple service project for different environments (development, staging and production), all are governed by a host project that handles shared resourses and centralized management.

# Landing Zones
This section provides a high-level overview of the Infinity Learn architecture. Understanding how the application is structured is essential for developers, administrators, and anyone who wants to customize or maintain the system.The GCP Landing Zone is a foundational concept in Google Cloud, especially important when organizations aim to implement a secure, scalable, and well-structured environment for managing cloud resources across multiple projects.

In GCP, the Landing Zone provides a framework for organizing and securing resources while ensuring adherence to best practices in:
- Access control
- Compliance
- Governance

# Core Components of a Landing Zone
A Landing Zone typically consists of several interrelated elements:
- Projects – Logical containers for your cloud resources.
- Folders – Groupings of projects by function, environment, or department.
- Organizational Units – Structural divisions at the GCP organization level.
- Resources – Actual infrastructure components such as virtual machines, storage, and networking configurations.
These components are designed to:
1. Manage and isolate workloads

2. Apply consistent security policies

3. Enable centralized monitoring and cost management

4. Enforce appropriate levels of access control

To better understand the GCP Landing Zone structure, it’s important to explore the concept of Host and service projects.To support scalability, governance, and secure management, Infinity Learn’s GCP Landing Zone is structured using two main types of projects:

# 1. Host Project
# 2. Service Projects
Infinity Learn’s Google Cloud Platform (GCP) architecture is built upon a robust and secure foundation known as the GCP Landing Zone. This landing zone represents a structured, scalable, and compliant environment for managing cloud resources across various projects. It follows best practices for access control, security, and governance. The core idea behind this structure is to separate the infrastructure management and governance layer from the application workloads by using a Host Project and multiple Service Projects. This model allows Infinity Learn to maintain centralized control while enabling independent application environments.

At the center of the architecture lies the Host Project, which is responsible for providing the core infrastructure and organizational-wide governance. It serves as the administrative backbone of the cloud environment and includes essential shared services such as logging, monitoring, identity and access management (IAM), and networking. The Host Project typically manages network infrastructure components like the Virtual Private Cloud (VPC), enabling a unified and secure networking layer across all environments. It also defines IAM policies that enforce consistent access control and governance rules throughout the organization. Additionally, the Host Project may include resource managers for organizing and managing service projects under various folders and organizational units.

Complementing the Host Project are the Service Projects, which are dedicated to running the actual application workloads. These projects typically represent different environments—such as development, staging, and production—or correspond to specific teams or services within Infinity Learn. Service Projects host resources like virtual machines, containers, databases, and storage buckets. While these projects are independently managed, they often inherit policies and network configurations from the Host Project, ensuring compliance and connectivity while retaining isolation between environments. This separation provides scalability and flexibility, as service teams can manage their resources without compromising overall governance.

By adopting this architecture, Infinity Learn ensures that its cloud infrastructure is modular, secure, and adaptable to changing business needs. The clear separation between infrastructure governance (Host Project) and application environments (Service Projects) supports a cloud-native approach that enhances operational efficiency, improves security posture, and facilitates easier management of cloud resources across the organization.

# Folder structure
The folder structure in Google Cloud Platform (GCP) plays a critical role in organizing projects logically within an organization like Infinity Learn. Folders serve as containers that group related projects based on departments, environments, business units, or use cases, creating a structured and hierarchical model for managing cloud resources. This hierarchical setup not only enhances clarity and resource organization but also allows for efficient policy enforcement and billing segregation. For example, Infinity Learn can create top-level folders for various business units such as Sales, HR, or Finance, and within each of these, further organize subfolders for different environments like development, staging, or production.

One of the key benefits of this structure is policy inheritance. IAM roles, organizational policies, and security configurations applied at a higher level (e.g., folder or organization level) automatically propagate down to the nested folders and projects. This ensures consistent access control and governance across the entire cloud infrastructure. The Root Organization sits at the top of this hierarchy, acting as the container for all folders and projects within the GCP organization. Overall, this well-defined folder structure enables centralized management, simplifies permission handling, and supports scalable, enterprise-grade cloud operations for Infinity Learn.
![image](https://github.com/user-attachments/assets/3b261ef7-7efc-4f7e-8534-87842e097fdb)

# User Access
- How to Grant Ownership Access in Infinity Learn GCP
# 1. Granting Ownership at the Organization Level
To give a user Ownership access across the entire Infinity Learn organization, follow these steps:

1. Log in to the Google Cloud Console.

2. Select Infinity Learn from the organization dropdown at the top.

3. Navigate to IAM & Admin > IAM.

4. Click + Add.

5. Enter the user’s email address.

6. Assign the role Owner.

7. Click Save.

This grants the user full administrative rights over all projects and resources under the Infinity Learn organization.

# 2. Granting Ownership at the Project Level
To give a user ownership only on a specific project within Infinity Learn:

1. Log in to the Google Cloud Console.

2. Select the specific project (under Infinity Learn) from the project dropdown.

3. Go to IAM & Admin > IAM.

4. Click + Add.

5. Enter the user’s email address.

6. Assign the role Owner (or a less privileged role if desired).

7. Click Save.

This limits the user’s full admin permissions to only that project without affecting other projects or the overall organization.

# Service Accounts in Google Cloud Platform (GCP)
What is a Service Account?
A Service Account is a special type of account used by applications or virtual machines (VMs) to interact with GCP APIs and services securely — without needing a user’s personal credentials.

- Unlike a user account, a service account is intended for non-human use.

- It acts as an identity for your application or service running on GCP.

- You assign IAM roles to service accounts, defining what actions they can perform.

# Why Use Service Accounts?
- Automation: To allow apps, VMs, or scripts to access resources securely.

- Security: Grants minimum permissions needed (principle of least privilege).

- Auditing: Activities by service accounts are logged separately, making tracking easier.

- Separation of duties: Service accounts are managed independently from user accounts.

# How to Create and Use a Service Account in Infinity Learn
Step 1: Create a Service Account
1. Open the Google Cloud Console.

2. Select the project within the Infinity Learn organization where the service account will be used.

3. Go to IAM & Admin > Service Accounts.

4. Click + Create Service Account.

5. Enter a name and description for the service account.

6. Click Create.

Step 2: Assign Roles to the Service Account
1. In the same creation flow, assign appropriate roles to the service account (e.g., Storage Admin, Compute Admin, Cloud SQL Client, etc.).

2. Click Continue and then Done.

Step 3: Generate and Download Service Account Keys (Optional)
1. If your application needs to authenticate outside GCP (e.g., from local or external servers), generate a JSON key:

2. Find the service account in the list.

3. Click Actions > Manage keys.

4. Click Add Key > Create new key.

5. Select JSON and download the key file.

- Important: Keep this key secure. Avoid committing it to code repositories.

Step 4: Use the Service Account
1. Assign the service account to your GCP resources (VMs, Cloud Functions, etc.).

2. Use the key file for authentication in your applications if needed.

3. The service account will now perform actions according to the assigned permissions.

# Virtual Private Cloud (VPC)
A Virtual Private Cloud (VPC) is a logically isolated network within Google Cloud Platform (GCP) where you can launch and manage your resources such as Compute Engine instances, Kubernetes clusters, and more.

For Infinity Learn, the VPC provides a secure and flexible network environment to connect cloud resources privately and control traffic flows.

- Key Concepts of VPC
1. Subnetworks (Subnets):
Logical subdivisions within a VPC, each in a specific region. Subnets contain IP address ranges (CIDR blocks) for resources.

2. Routes:
Rules that define how packets travel within and outside the VPC.

3. Firewalls:
Control incoming and outgoing traffic to resources based on rules.

4. Peering:
Allows communication between VPCs privately without going over the internet.

5. Cloud NAT:
Enables outbound internet access for resources without public IPs.

# 🔐 VPC Network Configuration – Infinity Learn
1. Organizational VPC Structure
   
In Infinity Learn’s GCP Organization, a structured and centralized VPC setup is used for network management and environment isolation. The base folder is:

- fld-il-network/

Under this folder, we maintain two shared VPC host projects:

- fld-il-net-preprod-shared – Used for development and staging environments

- fld-il-net-prod-shared – Used for production environment

Each of these projects contains a shared VPC network and associated subnets.
![image](https://github.com/user-attachments/assets/7cd4741d-2adb-414f-8b5f-96c51d532376)

2. Shared VPC Configuration
   
You can view and manage Shared VPCs under:
GCP Console → VPC Network → Shared VPC
Each environment-specific project is attached to the corresponding shared VPC host project, ensuring that all networking resources (like subnets and firewalls) are centrally managed.
![image](https://github.com/user-attachments/assets/41362883-76b0-4df9-bd95-77d3764d3ee3)

3. Subnet Utilization
Each Shared VPC has region-specific subnets that are reused across different projects:

- Subnets are predefined under each VPC.

- These subnets are assigned non-overlapping CIDR blocks.

- Environments (Dev, QA, Stage, Prod) pick subnets based on region and team-specific allocations.

4. Benefits of This Setup
✅ Centralized Network Management: VPC rules and subnets are centrally defined under host projects.
✅ Environment Isolation: Dev, staging, and prod environments are isolated using different VPC host projects.
✅ Security & Compliance: Firewall rules and IAM policies are managed at the shared VPC level for consistency.
✅ Scalability: New projects can be added to the shared VPCs easily without changing core network configurations.

# 🌐 VPC Setup 
In Infinity Learn's GCP organization, we follow a structured approach to network setup using Shared VPCs. If you want to create a new VPC in your organization, follow the steps below.

1 🛠️ Creating a New VPC in Infinity Learn

1.1 To create a new VPC in our GCP organization (infinitylearn.com):

Go to the GCP Console:
Navigate to the GCP console and select the appropriate host project under the Infinity Learn organization. For example:

- fldr-il-network

- fldr-il-net-preprod-shared

- fldr-il-net-prod-shared

1.2 Select the Correct Host Project:
If you're setting up a VPC for dev/staging, choose fldr-il-net-preprod-shared.
For production environments, use fldr-il-net-prod-shared.

1.3 Navigate to VPC Networks:
Go to VPC Network > VPC networks, then click "Create VPC network".

1.4 Choose Custom Mode:

Select Custom Mode (recommended) to manually define subnets.

Provide a meaningful name for the network.

1.5 Add Subnets:

Add required subnets for each region you plan to deploy resources in.

Example:

Name: subnet-dev-use1

Region: us-east1

CIDR: 10.1.0.0/24

1.6 Enable Routing Options:

Choose Global dynamic routing if using hybrid connectivity.

Otherwise, keep the default regional routing.

1.7 Private Google Access:
For subnets that require access to Google APIs (e.g., Cloud Storage, Pub/Sub) without public IPs, enable Private Google Access for the subnet.

# 👥 Grant Access to Subnet Users
🔐 Note: In GCP, users do not get access to subnets directly. Instead, permissions must be granted via IAM roles in the host project or folder where the VPC resides. This ensures only authorized principals can create/attach resources like VMs to the subnet.
To allow developers or service accounts to use the new subnets:

- Go to IAM & Admin > IAM in the host project where the VPC is created.

- Assign the role Compute Network User (roles/compute.networkUser) on the subnet or VPC network.

This lets users attach VMs and other resources to the subnet.

🔐 Tip: Always assign access at the least privilege level – only to the required project or subnet, not at the org level.

# 🔥 Configure Firewall Rules
1. Navigate to VPC Network > Firewall

2. Click Create Firewall Rule

3. Configure the settings:

✅ Required Fields:
- Name: e.g., allow-ssh-http-https

- Network: Select the newly created VPC (e.g., il-custom-vpc-prod)

- Priority: Default 1000 (lower number = higher priority)

- Direction of Traffic:

- Ingress: For incoming traffic

- Action on Match: Allow

- Target–Choose who this rule should apply to:

      - All instances in the network: Applies to every VM in the VPC.

      - Specified target tags: Applies only to VMs with a specific network tag.

🔸 If you choose this, you must:

- Create a custom network tag (e.g., web-access).

- Attach that tag to the VM that should receive traffic.

      - Go to VM > Edit > Network Tags and enter web-access.

- Specified service accounts: Applies to instances using a particular service account.

- Source Filter (for Ingress):

IP Ranges like 0.0.0.0/0 (all IPs) or restrict (e.g., 192.168.1.0/24)

Optional: Apply based on source tags or service accounts

- Protocols and Ports:

     tcp:22 for SSH

     tcp:80 for HTTP

     tcp:443 for HTTPS

Use all for all traffic if needed

🛠 Optional Fields:
Description: e.g., “Allow web + SSH access to tagged instances”

Log Config: Enable if traffic logging is required for monitoring/auditing

# ✅ Final Checks
Ensure route propagation is set correctly (especially for hybrid setups or VPN).

Confirm the subnet permissions are assigned to the right user groups or service accounts.

Tag your VPC resources clearly for visibility and auditing.

# Instance Launch – Detailed
To launch a VM instance in Google Cloud:

![image](https://github.com/user-attachments/assets/f3fdd869-5ada-44da-8b0e-2236643acaa9)


➤ Step-by-Step Instructions:
1. Go to Compute Engine > VM instances.

2. Click "Create Instance".

➤ Configuration Options:
- Name:
Example: (use a meaningful name for easy tracking).

- Region & Zone:
Select based on latency needs (e.g., us-east1-b for East Coast deployments).

- Machine type:
Choose based on workload:

E2 series for general workloads.

N2 or higher for compute-heavy tasks.

- Boot Disk:

OS: Debian, Ubuntu, or a Custom Image (e.g., il-base-image) if previously created.

- Firewall:

Enable Allow HTTP and Allow HTTPS checkboxes if you're launching a web server.

🏷️ Network Configuration Enhancements:
Add Network Tags:

These tags are essential if you want to apply firewall rules to specific instances only.
Once tagged, configure corresponding rules via VPC network > Firewall rules (e.g., allow ports 22, 80, 443 for web-frontend tag).

- Network Interfaces:

Network: Select "Shared with me" if using a Shared VPC setup.

Subnetwork: Choose from subnets shared by host project.

External IP: Set to None if this instance should be private only (no public exposure).

- 🔍 Observability – Ops Agent Setup:
Under "Management, security, disks, networking, sole tenancy", go to the Observability section.

Choose to install Ops Agent for:

Metrics collection (CPU, memory, disk, network)

Logs (Syslog, Apache, Nginx, etc.)

Recommended for all production VMs.

- 🔐 Security – Service Account:
In the Security section:

Attach a custom service account with the least-privileged roles needed by the instance.

Enable or disable API access scopes as per your app’s requirement (e.g., Storage Read, Pub/Sub Publisher).

- ✅ Final Steps:
Review all configurations.

Click "Create" to launch the VM.

- Use Serial Console Access
If SSH is totally broken, try Serial Console (requires enabling first):

Go to VM Instance > Edit

Enable "Enable serial port access"

Save, then click on "Connect to serial console"

# Monitoring
- Use Cloud Monitoring to track performance and uptime:

Go to Monitoring > Dashboards.

Use the VM Instance dashboard to monitor:

CPU usage

Memory usage

Disk I/O

Network traffic

Enable uptime checks and alerting policies (e.g., notify if CPU > 80% for 5 mins).

Integrate with Cloud Logging for deep log visibility.

![image](https://github.com/user-attachments/assets/e625032d-cba3-4a66-9525-53d4c35eb2ba)

- To install the Ops Agent later through the Observability (Monitoring) tab or manually via SSH, the user or service account performing the installation must have sufficient IAM roles/permissions on the VM.

✅ Required Permissions to Install Ops Agent

🔒 Minimum IAM Role (Preferred)

    Role: roles/compute.osAdminLogin

Name: Compute OS Admin Login

Purpose: Allows SSH access with admin rights (required for agent installation)

This role includes:

    compute.instances.get

    compute.instances.setMetadata

    compute.instances.osLogin

    compute.instances.osLogin.admin

✅ Alternative Combination of Roles (if granular control is needed)
If you prefer fine-grained control, assign the following roles:

    roles/compute.instanceAdmin.v1 – to manage VM instances

    roles/compute.osLoginAdmin – to allow sudo access

    roles/logging.admin – for log writing

    roles/monitoring.admin – for monitoring configuration

📌 Note:
To install the agent via the Cloud Console (Observability tab), the underlying API calls require compute.instances.updateMetadata permission, which is included in the roles above.

If you are using OS Login, ensure the user has roles/compute.osAdminLogin or higher.

🛠️ Optional: Service Account Permissions
If the VM uses a custom service account, ensure it has these roles too:

    roles/logging.logWriter

    roles/monitoring.metricWriter

These are required for the Ops Agent to send logs and metrics to Cloud Monitoring and Logging.

# Volume Increase (Persistent Disk Resize)

Persistent disks in GCP are resizable, but resizing the boot disk has specific steps and scenarios.

1 Standard Boot Disk Resize (Sufficient Free Space)

If there is available space and the VM is responsive:

1.1 Go to Compute Engine > Disks

1.2 Click on the boot disk (usually named like instance-name or instance-name-boot).

1.3 Click Edit > Resize, and increase the size (e.g., from 10 GB to 20 GB).

1.4 Save the changes.

🛠️ Resize the File System

SSH into the VM and run:
            
    sudo resize2fs /dev/sda1

 Note: Device name (/dev/sda1) might differ based on image. Use lsblk or df -h to confirm.

 2 When Boot Disk is Full (Can't SSH or Resize Internally)
 
If the boot disk is full and the VM cannot even run the resize2fs command:

🚫 SSH fails or file system is too full to resize

Workaround: Resize by Detaching and Attaching to Another VM

2.1 Stop the affected instance.

2.2 Go to Compute Engine > Disks

- Select the boot disk of the affected VM

- Click Detach

2.3 Attach this disk to a helper VM:

- Go to the helper VM > Edit

- Attach the disk as a secondary disk

2.4 SSH into the helper VM

2.5 Mount the attached disk

    sudo mkdir /mnt/recovery
    sudo mount /dev/sdb1 /mnt/recovery 
Delete unnecessary files to free up space.    

2.6 Unmount and detach the disk from the helper VM.

2.7 Reattach the disk to the original instance as the boot disk.

2.8 Start the original instance.

2.9 Once booted, run:
         
    sudo resize2fs /dev/sda1

📌 Tips

Always take snapshots before resizing or modifying disks.

Check your disk quota in the region before increasing size.

Use Cloud Monitoring alerts to notify before disk reaches critical usage (e.g., > 90%).

# Image Creation

To create an image (for backups or replication):

1. Go to Compute Engine > Images.

2. Click "Create Image".

3. Choose:

3.1 Source disk: Select the running instance's disk.

3.2 Name: e.g., il-base-image

3.3 Click Create.

✅ Use this image later to launch preconfigured instances.

















