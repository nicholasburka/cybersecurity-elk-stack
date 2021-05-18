## Automated ELK Stack Deployment
Nicholas Burka

The files in this repository were used to configure the network depicted below.

![](Images/RedTeamNetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible Playbook file may be used to install only certain pieces of it, such as Filebeat.

  - /etc/ansible/roles/filebeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Using a Jump Box secures the VM's from direct access, and allows each VM running the DVWA to be easily installed with the same configuration, which can be modified and reinstalled using Ansible.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the filesystem and system logs. Filebeat and Metricbeat monitor the file system and system metrics respectively.

The configuration details of each machine may be found below.

| Name       | Function       | IP Address | Operating System |
|------------|----------------|------------|------------------|
| Jump Box   | Gateway        | 10.0.0.9   | Linux            |
| ELK-Server | Log monitoring | 10.1.0.4   | Linux            |
| Web-1      | DVWA Server    | 10.0.0.8   | Linux            |
| Web-2      | DVWA Server    | 10.0.0.7   | Linux            |
| Web-3      | DVWA Server    | 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box can accept connections from the Internet. Access to this machine is allowed from the following IP addresses:
68.199.113.44

Machines within the network can only be accessed by the Jump Box and Load Balancer.  

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses      | Protocol   |
|---------------|---------------------|---------------------------|------------|
| Jump Box      | Yes                 | 68.199.113.44             | SSH        |
| ELK Server    | Yes / No            | 68.199.113.44 / 10.0.0.9  | HTTP / SSH |
| Load Balancer | Yes                 | 68.199.113.44             | HTTP       |
| Web VM's      | No                  | 10.0.0.9                  | SSH        |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because each VM can be configured identically and automatically.

The playbook implements the following tasks:
- Installing Docker and Python 3
- Installing the ELK Stack
- Enabling the ELK Stack to run on startup

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.7
- 10.0.0.4

We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat: collects filesystem logs, which we use to track changes to web server files like the access log, site images, etc.
- Metricbeat (not installed): collects system metrics, like CPU & memory usage information.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ``filebeat_config.yml`` file to ``/etc/ansible/filebeat_config.yml``.
- Update the ``/etc/ansible/hosts`` file to include the [elkserver] IP address.
- Run the playbook, and navigate to http://68.199.113.44:5601 to check that the installation worked as expected.
