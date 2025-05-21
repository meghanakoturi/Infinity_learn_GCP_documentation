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











