aws_lb
=========

Ansible Role: aws_lb
This Ansible role facilitates the management of AWS EC2 instance which will be used for creating a load balancer using haproxy service.

Tasks:
including variables: 

Load predefined variables necessary for configuring and provisioning load balancer.

getting info of load balancer[running/stopped] from AWS:

Utilizes the ec2_instance_info module to collect data about running or stopped load balancers in the specified AWS region.
Filters instances tagged with app: lb and having the states "running" or "stopped".

updating variable file with load balancer info:

Uses the template module to update a variable file (vars/main.yml) with the latest gathered load balancer information from AWS.
This task uses jinja file to update variable file

refreshing variables:

Includes the updated variables from the variable file to ensure the playbook has access to the latest information.



starting existing load balancer if already present in AWS:

Attempts to start existing load balancers if they are already present in AWS.
Uses the ec2_instance module to start instances with the provided instance IDs.
Instance IDs are fetched from variable coming from vars/main.yml file

Handle Load Balancer Count:

Displays a message indicating the number of load balancers found (lb_count) using the debug module.
If no load balancers are found, prompts the user with an option to launch a new load balancer or skip the operation using the pause module.

launching new load balancer, if required:

Launches a new load balancer using the ec2_instance module if no load balancers are present and the user opts to create one.
Configures the new load balancer with specific parameters such as instance type, security group, subnet ID, etc.

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

region: (string) The AWS region where the load balancer is managed (e.g., ap-south-1).
name: (string) name of load banlancer.
instance_type: (string) The instance type for the load balancer instances (e.g., t2.micro).
key_name: (string) The name of the SSH key pair used for the load balancer instances.
vpc_subnet_id: (string) The ID of the subnet where the load balancer instances are launched (e.g., subnet-05cfe7fcb9b8f24cf).
security_group: (string) The name of the security group assigned to the load balancer instances.
count: count of number of to launch load balancer.
image_id: (string) ami id used to launch load balancer.

Example Playbook
----------------

- name: testing role
  hosts: localhost
  become: true
  vars_files:
    - credentials.yml
  roles:
    - aws_lb


Author Information
------------------

Name - Nehal Patodiya
LinkedIn - linkedin.com/in/nehal-patodiya-5aa4501b5
