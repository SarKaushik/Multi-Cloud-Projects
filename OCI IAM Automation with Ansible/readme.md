
# OCI IAM Automation with Ansible

This project automates the creation of groups, policies, and users in **Oracle Cloud Infrastructure (OCI)** using **Ansible Playbooks**.  



![OCI IAM](OCI_IAM.png)


**Identity and Access Management (IAM) in OCI** is used to securely control access to cloud resources. It enables administrators to define **who** can access specific resources and **what actions** they can perform.  

- **Users**: Individual identities within OCI. Each user is assigned credentials and can be added to one or more groups.  
- **Groups**: A collection of users. Instead of assigning permissions to users one by one, groups allow easier management of access by assigning policies at the group level.  
- **Policies**: Rules written in a human-readable language that specify access permissions. For example, a policy can allow a group of users to manage compute instances or read object storage.  
- **Compartments**: Logical partitions within OCI to organize and isolate resources. IAM policies can be scoped to compartments, ensuring better access control and resource segregation.  
- **Dynamic Groups**: Special groups where membership is determined by resource attributes (e.g., all instances with a specific tag), often used to give permissions to resources like compute instances.  
- **Federation**: Integration with an external identity provider (e.g., Microsoft Active Directory, Oracle Identity Cloud Service) to enable single sign-on (SSO) for users.  

By automating these IAM components with Ansible, the project ensures **consistent, repeatable, and secure** provisioning of access controls across OCI environments.

## Benefits of Using This Automation

- **Time-saving**: Automates the creation of multiple users, groups, and policies, reducing manual effort significantly.  
- **Consistency**: Ensures uniform configuration and access policies across all users and groups, eliminating human errors.  
- **Scalability**: Easily add or update a large number of users and permissions without repetitive manual steps.  
- **Security**: Reduces the risk of misconfigured access controls, ensuring users have the right level of access.  
- **Reusability**: The Ansible playbooks can be reused across different compartments or OCI environments with minimal changes.  
- **Auditability**: Provides a repeatable and documented process for IAM management, making audits and compliance checks easier.  
- **Efficiency**: Frees up administrator time to focus on higher-value tasks instead of repetitive IAM setup.  

## Prerequisites

You should have the following compartments already created in OCI:  
- `networkingResources`  
- `computeResources`  
- `databaseResources`  

---
### Steps using the Cloud Shell in OCI

## Setting up environment
Replace the placeholders with your own **Tenancy OCID** and **Compartment OCIDs**:

```bash
export PARENT_COMPARTMENT_OCID=<insert-TENANCY-ocid>
export NETWORKING_COMPARTMENT_OCID=<insert-NETWORKING_COMPARTMENT-ocid>
export COMPUTE_COMPARTMENT_OCID=<insert-COMPUTE_COMPARTMENT-ocid>
export DB_COMPARTMENT_OCID=<insert-DB_COMPARTMENT-ocid>

### Creating and accessing a folder to download the code
mkdir tcb-bmc-iam
cd tcb-bmc-iam

## Running the Ansible Playbooks from Cloud Shell
ansible-playbook tcb-bmc-iam-creating-groups-and-policies.yaml
ansible-playbook tcb-bmc-iam-creating-users-cloud-admin.yaml
ansible-playbook tcb-bmc-iam-creating-users-dba-admin.yaml
ansible-playbook tcb-bmc-iam-creating-users-network-admin.yaml
ansible-playbook tcb-bmc-iam-creating-users-compute-admin.yaml
ansible-playbook tcb-bmc-iam-creating-users-operators.yaml
