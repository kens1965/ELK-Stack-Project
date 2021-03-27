# ELK-Stack-Project
First project for U of M Cybersecurity Boot Camp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(https://github.com/kens1965/ELK-Stack-Project/blob/main/Diagrams/Elk-Stack-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/kens1965/ELK-Stack-Project/blob/main/ansible-Playbooks/Install-Elk.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load Balancers maintain Availability, which is a part of the CIA triad aspect in security.

The jump box is an important part of this network, as it serves as a gateway router. All traffic is sent through this single node and access to other machines can be controlled by allowing connections to specific IP addresses. Using the jump box makes it much easier to secure and monitor each virtual machine behind the gateway.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
Filebeat collects data about the file system and enables analysts to monitor files for suspicious changes. Metricbeat collects machine metrics, such as uptime and CPU usage.

The configuration details of each machine may be found below.

| Name      | Function | IP Address | Operating System |
|---------- |----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4   | Linux            |
| Web-1     | VM       | 10.0.0.5   | Linux            |
| Web-2     | VM       | 10.0.0.6   | Linux            |
| Web-3     | VM       | 10.0.0.8   | Linux            |
| ELK-One   | VM       | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.240.161.193 (Personal IP)

Machines within the network can only be accessed by SSH. The only machine that is able to connect to the ELK Server is the jump box, IP address 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses     |
|----------|---------------------|----------------------    |
| Jump Box |     No              | Personal IP Only         |
| Web_1    |     No              | 10.0.0.4                 |
| Web_2    |     No              | 10.0.0.4                 |
| Web_3    |     No              | 10.0.0.4                 |
| Elk-One  |     No              | 10.0.0.4 and Personal IP |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is extremely easy to use. Through the use of Playbooks, multiple machines can be configure with a single command once the Playbook is created.

The playbook implements the following tasks:
-- Installs docker.io, the engine that is used to run the containers.
-- Installs Python3-pip, the package that is used to install Python software.
-- Downloads the docker container and configures it to start on ports 5601, 9200 and 5044.
-- Starts the container and enables the docker service on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:


![image](https://user-images.githubusercontent.com/81202358/112737687-31b0c980-8f2a-11eb-9918-51610d1e384d.png)


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
