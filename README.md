## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](Diagrams/Final_Network_Map.drawio.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above or alternatively, in portions.  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system load.

The configuration details of each machine may be found below.

| Name         | Function   | IP Address | Operating System |
|--------------|------------|------------|------------------|
| Jump Box     | Gateway    | 10.0.0.1   | Linux            |
| VM-1         | DVWA Server| 10.0.0.5   | Ubuntu           |
| VM-2         | DVWA Server| 10.0.0.6   | Ubuntu           |
| VM-3         | DVWA Server| 10.0.0.7   | Ubuntu           |
| ELK Server   | DVWA Server| 10.1.0.4   | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 67.176.125.108
- 209.170.239.101
- 97.102.240.63

Machines within the network can only be accessed by Jump-Box.
- 10.0.0.1

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  | Yes                 | 67.176.125.108       |
|VM-1      | No                  | 10.0.0.4             |
|VM-2      | No                  | 10.0.0.4             |
|VM-3      | No                  | 10.0.0.4             |
|Elk Server| Yes                 | 67.176.125.108       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows the network to be rebuilt quickly and without human error. 
If for whatever reason, the network needs to grow or is rebuilt, the process can take minutes instead of hours or days. 

The playbook implements the following tasks:
- Increasing the memory usage through sysctl
- Install Docker.io and Python3
- Download ELK and launch the ELK docker container
- Ensure that the ELK container is started on startup and is part of the system service when booting up

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS command](Images/elk_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeats allows the monitoring of system logs, file logs and other log data from each individual server.
- Metricbeats allws the monitoring of system performance, CPU usage, memory usage and other system metrics. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the ansible control node.
- Update the hosts file to include an [elk] section with the private IP of the server to be configured. 
- Update the Elk-Configuration.yml file to update IP, username and password settings and copy to the ansible control module.
- Run the playbook, and navigate to the IP of the new ELK server through port 5601 to check that the installation worked as expected.
