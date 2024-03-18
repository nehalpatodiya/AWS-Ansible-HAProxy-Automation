aws_web
=========

Ansible Role: aws_web

This Ansible role facilitates the management of web servers on the Amazon Web Services (AWS) cloud platform. It automates tasks related to provisioning and scaling web server instances based on user-defined requirements.

Tasks:

including variables.: 
Load predefined variables necessary for configuring and provisioning web servers.

getting info of webservers[running/stopped] from AWS.:

Utilize the ec2_instance_info module to gather information about existing web servers in the specified AWS region. This includes instances with both "running" and "stopped" states, tagged with the "app: web" label.

updating variable file with webservers info.:

Uses the template module to update a variable file (vars/main.yml) with the latest gathered web servers information from AWS.
This task uses jinja file to update variable file

refreshing variables.:

Includes the updated variables from the variable file to ensure the playbook has access to the latest information.

starting existing web servers if already present in AWS.:

Attempts to start existing web servers if they are already present in AWS.
Uses the ec2_instance module to start instances with the provided instance IDs.
Instance IDs are fetched from variable coming from vars/main.yml file

Handle web server Count:

Displays a message indicating the number of web servers found (web_count) using the debug module.
If no web servers are found, prompts the user with an option to launch a new web servers or skip the operation using the pause module.

launching more webservers, if required.:

Launches a new web servers using the ec2_instance module if no web servers are present and the user opts to create one.
Configures the new web servers with specific parameters such as instance type, security group, subnet ID, etc.

Requirements
------------

Python boto3 library must be installed on the Ansible control node to enable interaction with AWS services.

AWS credentials (access_key and secret_key) must be provided to interact with AWS services.

Proper permissions and access rights are required by Controller Node to perform operations on AWS resources.

Role Variables
--------------

Variables to be passed from outside:

access_key: (string) AWS access key required to authenticate with AWS services.
secret_key: (string) AWS secret key required for authentication.

Variables in vars/:

region: (string) The AWS region where the web servers is managed (e.g., ap-south-1).
name: (string) name of web servers.
instance_type: (string) The instance type for the web servers instances (e.g., t2.micro).
key_name: (string) The name of the SSH key pair used for the web servers instances.
vpc_subnet_id: (string) The ID of the subnet where the web servers instances are launched (e.g., subnet-05cfe7fcb9b8f24cf).
security_group: (string) The name of the security group assigned to the web servers instances.
count: count of number of to launch web servers.
image_id: (string) ami id used to launch web servers.

Example Playbook
----------------

- name: testing role
  hosts: localhost
  become: true
  vars_files:
    - credentials.yml
  roles:
    - aws_web

Author Information
------------------

Name - Nehal Patodiya
LinkedIn - linkedin.com/in/nehal-patodiya-5aa4501b5