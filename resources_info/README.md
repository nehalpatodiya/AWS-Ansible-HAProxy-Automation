resources_info
=========

Ansible Role: resources_info
This Ansible role facilitates the collection of data pertaining to load balancers and web servers hosted on Amazon Web Services (AWS). It automates the process of gathering information on instances tagged as load balancers (lb) and web servers (web), irrespective of their state (running or stopped). The collected data is then stored in variable files for further processing and analysis.

Tasks:
including variables: 

This task involves importing variables from the specified directory (vars) into the playbook.

gathering data of load balancer & webservers[running/stopped] from AWS.:

Utilizing the ec2_instance_info Ansible module, this task retrieves information about instances tagged as lb or web from AWS. It filters instances based on their tags and state (running or stopped). The AWS access and secret keys provided are used for authentication.

updating variable file with load balancer & webservers info.:

Uses the template module to update a variable file (vars/main.yml) with the latest gathered load balancer and web servers information from AWS.
This task uses jinja file to update variable file.

refreshing variables:

Includes the updated variables from the variable file to ensure the playbook has access to the latest information.

debugging output: 

This task provides debugging information, displaying counts of running and stopped load balancers and web servers. Additionally, it outputs detailed information about the gathered instance data for further inspection and analysis.

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

Example Playbook
----------------

- name: testing role
  hosts: localhost
  become: true
  vars_files:
    - credentials.yml
  roles:
    - resources_info

Author Information
------------------

Name - Nehal Patodiya
LinkedIn - linkedin.com/in/nehal-patodiya-5aa4501b5
