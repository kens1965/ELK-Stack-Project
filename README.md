
**Automated ELK Stack Deployment**

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

**Description of the Topology**

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

The network begins with creating a resource group, which is a logical grouping of all resources, such as the virtual network, firewalls, virtual computers, and other resources needed for setup. During configuration, rules were created to deny access to the virtual machines so that no one can get access to the virtual machines until we want them to.

The virtual network is a collection of virtual machines that can communicate with one another, through use of IP addresses and subnets. A security group is created, which will be the firewall for the network. The firewall is a designed set of rules to to block or allow network traffic. Rules can be set on single or multiple ports, coming and going from a single IP address or multiple IP's.

Five virtual machines have been set up in this system. In one virtual network, a jump box and three servers were created. The three servers create redundancy - if one machine fails, the other two machines can remain running. A second virtual network was created for the ELK stack, consisting of a server and a security group (firewall).

Load balancing ensures that the application will be highly available, in addition to restricting access to the network. Load Balancers maintain Availability, which is a part of the CIA triad aspect in security. The load balance evenly distributes traffic and helps to mitigate DoS attacks.

The jump box is an important part of this network, as it serves as a gateway router. All traffic is sent through this single node and access to other machines can be controlled by allowing connections to specific IP addresses. Using the jump box makes it much easier to secure and monitor each virtual machine behind the gateway.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic. The ELK stack can easily collect logs from multiple machines into a single database. It can also build graphs, charts, and other visualizations from network data.

Filebeat collects data about the file system and enables analysts to monitor files for suspicious changes. Metricbeat collects machine metrics, such as uptime and CPU usage.

The configuration details of each machine may be found below.

| Name      | Function   | IP Address | Operating System |
|---------- |----------  |------------|------------------|
| Jump Box  | Gateway    | 10.0.0.4   | Linux            |
| Web-1     | Server     | 10.0.0.5   | Linux            |
| Web-2     | Server     | 10.0.0.6   | Linux            |
| Web-3     | Server     | 10.0.0.8   | Linux            |
| ELK-One   | Log Server | 10.1.0.4   | Linux            |

Each virtual machine is configured with a container. One VM may have many containers on it. Containers are advantageous because they are lightweight, share resourcers, are easily duplicated, and create redundancy. If one container has a problem, it can be killed and a new one created without the website going down. 

Docker is the program used to manage the containers in each VM. Docker is used to install Ansible, a provisioning tool can make automated configuration changes to servers. This will ensure that the automated configurations will perform exacting the same way every time they are run.

**Access Policies**

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Personal IP.

Machines within the network can only be accessed by the jump box. The ELK server is configured to have access from a personal IP address through port 5601.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible | Allowed IP Addresses     |
|-------------- |---------------------|----------------------    |
| Jump Box      |     Yes             | Personal IP Only         |
| Web_1         |     No              | 10.0.0.5                 |
| Web_2         |     No              | 10.0.0.6                 |
| Web_3         |     No              | 10.0.0.8                 |
| Elk-One       |     No              | 10.1.0.4 and Personal IP |
| Load Balancer |     Yes             | Open                     |

**Elk Configuration**

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is extremely easy to use. Through the use of Playbooks, multiple machines can be configured with a single command once the playbook is created. If one of the servers is compromised, it can be removed and relaunched through the use of a playbook.

The ansible-playbook install-elk.yml implements the following tasks:
- Installs docker.io, the engine that is used to run the containers.
- Installs Python3-pip, the package that is used to install Python software.
- Downloads the docker container and configures it to start on ports 5601, 9200 and 5044.
- Starts the container and enables the docker service on boot.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance:

![image](https://user-images.githubusercontent.com/81202358/112737761-e519be00-8f2a-11eb-8076-caf492e3a964.png)

**Target Machines & Beats**

This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5, Web-2 10.0.0.6, Web-3 10.0.0.8

We have installed the following Beats on these machines:
- Filebeat

Filebeat allow us to collect the following information from each machine:
- Filebeat helps generate and organize log files to send to Logstash and Elasticsearch. Specifically, it logs information about the file system, including what files have changed and when. It is often used to collect logs generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQL databases.

**Using the Playbook for Filebeat**

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the filebeat.yml file to the /etc/ansible/roles directory.
- Update the configuration file to include the private IP address of the Elk Server to the Elasticsearch and Kibana
  sections of the configuration file.
- Run the playbook, and SSH to the Elk Server to check that the installation worked as expected by running docker ps.

**Q&A**
- _Which file is the playbook? Where do you copy it?_ The playbook is a file that ends in .yml. It can be copied from /etc/ansible when in
   the ansible container.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ The machine on which to install the ELK server can be specified in _host_ file, located in the Ansible directory. The machine to install Filebeat can be specified in filebeat-config.yml playbook, located in the ansible directory.
- _Which URL do you navigate to in order to check that the ELK server is running?_ http://(Elk Server Public IP address)/app/kibana

**How to Use the Ansible Build**

The commands needed to run Ansible for the ELK Server are:

- ssh (user name)@(Jump Box Public IP)
- sudo docker container list -a (locate the Ansible container)
- sudo docker start (name of the container)
- sudo docker attach (name of the container)
- cd /etc/ansible
- ansible-playbook install-elk.yml (configures the Elk Server and starts the container on the server)
- cd /etc/ansible/roles
- ansible-playbook filebeat.yml (installs Filebeat)
