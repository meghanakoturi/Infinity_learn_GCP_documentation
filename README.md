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



