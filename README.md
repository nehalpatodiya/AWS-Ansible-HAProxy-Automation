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

## Setup Passwordless Authentication

Before running any playbooks, set up passwordless authentication between the Ansible control node (master) and the EC2 instances (worker nodes). Follow these steps:

1. **Generate SSH Key Pair**:
   - On the Ansible control node, generate an SSH key pair using `ssh-keygen`. Keep the default location for the keys.

   ```bash
   ssh-keygen -t rsa -b 2048
   ```

2. **Copy the Public Key**:
   - Copy the public key to the worker nodes using Ansible's `authorized_key` module or manually. Replace `USER` with the appropriate SSH user and `WORKER_IP` with the IP address of each worker node.

   ```bash
   ansible -i aws_ec2.yml all -m authorized_key -a "user=USER key=$(cat ~/.ssh/id_rsa.pub)" --private-key=/path/to/your/key.pem
   ```

   - Or, manually copy the public key to `~/.ssh/authorized_keys` on each worker node.

3. **Test SSH Access**:
   - Verify that passwordless authentication works by SSHing into the worker nodes without a password:

   ```bash
   ssh -i /path/to/your/key.pem USER@WORKER_IP
   ```

   You should be able to log in without being prompted for a password.
