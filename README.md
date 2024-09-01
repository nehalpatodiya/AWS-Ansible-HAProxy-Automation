# Automating HAProxy Deployment on AWS Infrastructure with Ansible

This project highlights the effectiveness of Ansible in automating AWS infrastructure setup, configuring HAProxy as a reverse proxy, and managing Apache web servers. It takes full advantage of Ansible's powerful automation and orchestration features.

## Project Overview

The project achieves the following objectives:

1. **AWS EC2 Instance Provisioning**:
   - Launches EC2 instances on AWS for both the HAProxy load balancer and backend web servers.
   - Uses Ansible's ec2 module to dynamically provision these instances.

2. **Passwordless Authentication**:
   - Sets up passwordless authentication between the Ansible control node and EC2 instances, enhancing both security and automation. (Refer to [Setup Passwordless Authentication](#setup-passwordless-authentication))

3. **HAProxy Configuration**:
   - Configures HAProxy on the load balancer instance to enable reverse proxy functionality.
   - Automates the HAProxy configuration updates whenever new managed nodes (Apache web servers) are added to the inventory.

4. **Backend Web Server Configuration**:
   - Configures Apache (httpd) on the backend web servers.
   - Deploys a sample HTML page with dynamic content to easily distinguish between different servers.
