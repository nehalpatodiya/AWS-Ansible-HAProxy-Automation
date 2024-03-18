configuring_web
=========

Ansible Role: configuring_web
This Ansible role is designed to automate the setup and configuration of web servers using the Apache HTTP Server (httpd) on target hosts. It ensures consistent deployment of web services across your infrastructure.

Tasks:

refreshing inventory:

Ensures that the Ansible inventory is up-to-date for accurate management of target systems.

install httpd service on all webservers:

Installs the Apache HTTP Server package (httpd) on all designated web servers.

copy index.html in all webservers:

Copies a customized index.html file to the web server's document root directory.
The template for the index.html file is sourced from the files/webpage/my.html file in the Ansible project directory.
This task ensures that the web server serves the appropriate content to visitors.

starting httpd service and enabeling it:

Starts the Apache HTTP Server service (httpd) on the target hosts.
Enables automatic startup of the httpd service to ensure it restarts upon system reboot.

Requirements
------------

Python boto3 library must be installed on the Ansible control node to enable interaction with AWS services.

Proper permissions and access rights are required by Controller Node to perform operations on AWS resources.

Example Playbook
----------------

- name: testing role
  hosts: tag_app_web
  become: true
  roles:
    - configuring_web

Author Information
------------------

Name - Nehal Patodiya
LinkedIn - linkedin.com/in/nehal-patodiya-5aa4501b5
