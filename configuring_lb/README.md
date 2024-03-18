configuring_lb
=========

Ansible Role: configuring_lb
This Ansible role automates the setup and configuration of HAProxy as a load balancer on target systems. It streamlines the process of deploying HAProxy, managing its configuration file, and ensuring the service is started and enabled for seamless load balancing across multiple web servers.

Tasks:

refreshing ansible inventory:

Ensures that the Ansible inventory is up-to-date for accurate management of target systems.

install haproxy service:

Installs the HAProxy package on the target system, ensuring it is present for load balancing purposes.

copy haproxy config file containing info of all webservers to load balancer:

Copies the HAProxy configuration file containing information about all web servers to the appropriate directory on the target system. This ensures that HAProxy is configured to distribute traffic effectively.

starting haproxy service & enabeling it:

Initiates the HAProxy service on the target system and configures it to start automatically upon system boot. This ensures continuous operation of the load balancer.

Requirements
------------

Python boto3 library must be installed on the Ansible control node to enable interaction with AWS services.

Proper permissions and access rights are required by Controller Node to perform operations on AWS resources.

Example Playbook
----------------

- name: testing role
  hosts: tag_app_lb
  become: true
  roles:
    - configuring_lb

Author Information
------------------

Name - Nehal Patodiya
LinkedIn - linkedin.com/in/nehal-patodiya-5aa4501b5
