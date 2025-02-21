# Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources

![image](https://github.com/SarKaushik/Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources/assets/85201993/a8ce8564-0274-4dca-afe9-c0e6cc3294a8)

In this real-world scenario, I assumed the role of a Cloud Specialist tasked with orchestrating the migration of users and managing AWS Identity and Access Management (IAM) resources.

The objective was to seamlessly migrate 100 users while ensuring each account had Multi-factor Authentication (MFA) enabled, adhering to stringent security protocols.

To streamline operations and eliminate manual, repetitive tasks within the AWS console, automation of these processes became paramount.


![image](https://github.com/SarKaushik/Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources/assets/85201993/01783462-8e31-40f4-b8c6-67aadac0b9c2)


In crafting a robust cloud user migration process from legacy systems to cloud-based infrastructure, a pivotal element was the development of automated scripts. Leveraging tools like Gitbash, AWS CLI, and shell scripting, I effectively streamlined the migration effort, reducing manual intervention and enhancing efficiency.

AWS CLI (Command Line Interface) serves as a powerful tool for interacting with various AWS services directly from the command line. It offers a comprehensive set of commands for managing resources, configuring settings, and automating tasks within AWS environments. By leveraging AWS CLI, users can script repetitive tasks, perform complex operations, and integrate AWS functionality into automated workflows.

Shell scripting, on the other hand, provides a means to automate tasks and execute commands directly within a Unix-based shell environment. It enables users to create sequences of commands, handle file operations, and manipulate data efficiently. Shell scripts are particularly useful for automating system administration tasks, performing batch operations, and orchestrating complex processes.

```

INPUT=$1
OLDIFS=$IFS
IFS=',;'

[ ! -f $INPUT ] && { echo "$INPUT file not found"; exit 99; }

command -v dos2unix >/dev/null || { echo "dos2unix tool not found. Please, install dos2unix tools before running the script."; exit 1; }

dos2unix $INPUT

while //Implemented While logic

```


The provided shell script automates the creation of IAM users, assignment to groups, and configuration of login profiles within AWS. It accepts a CSV file containing user details (username, group, password) as input and iterates through each record, utilizing AWS CLI commands to create users, set passwords, and assign them to specified groups. Additionally, it ensures that passwords are set to require a reset upon initial login, enhancing security. The script also performs necessary checks such as file existence and ensures compatibility by converting line endings using dos2unix utility.



![image](https://github.com/SarKaushik/Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources/assets/85201993/7d13aad4-2397-4338-b5d3-a373997211e0)


![image](https://github.com/SarKaushik/Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources/assets/85201993/eaabbb70-2849-4363-98c5-e3c5267b6c50)

![image](https://github.com/SarKaushik/Automated-user-migration-and-administration-of-AWS-Identity-and-Access-Management-IAM-resources/assets/85201993/6cc199de-7c94-4533-bc07-37d7e5b98cc7)

Ensured the implementation of Multi-factor Authentication (MFA) for each user created in AWS IAM. This step bolstered security measures by requiring an additional layer of authentication, aligning with best practices for user management in the cloud environment.

In addition to enabling Multi-factor Authentication (MFA) for each created user in AWS IAM, I assigned an Enforced MFA policy to each group.

Through meticulous automation using Gitbash, AWS CLI, and shell scripting, the project achieved seamless user migration and management in AWS IAM. By enforcing Multi-factor Authentication (MFA) for each user and implementing an Enforced MFA policy for groups, the cloud environment attained heightened security levels. This endeavor exemplifies the power of automation in simplifying complex processes while upholding stringent security standards in cloud infrastructure management.
