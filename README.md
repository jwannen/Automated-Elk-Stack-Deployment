# Automated-Elk-Stack-Deployment

The files in this repository were used to configure the network depicted below.

[Project 1 Network Diagram](https://github.com/jwannen/Automated-Elk-Stack-Deployment/blob/master/Diagrams/Project-1-Network-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Project 1 Network Diagram file may be used to install only certain pieces of it, such as Filebeat.

[filebeat-playbook.yml](https://github.com/jwannen/Automated-Elk-Stack-Deployment/blob/master/Ansible/filebeat-playbook.yml.txt)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high-traffic to the network.
  - What aspect of security do load balancers protect? Load balancers distribute traffic evenly among     the servers and help mitigate against DoS attacks.
  - What is the advantage of a jump box? It allows a secure path into the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs.
  - What does Filebeat watch for? It keeps logs of file changes.
  - What does Metricbeat record? It monitors and analyzes system CPU, memory, and load.

The configuration details of each machine may be found below. Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address                               | Operating System |
|----------|----------|------------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.4(private) 40.77.98.233(public)   | Linux            |
| ELK VM   | Server   | 10.1.0.4(private) 52.237.162.111(public) | Linux            |
| Web-1 VM | Server   | 10.0.0.5(private)                        | Linux            |
| Web-2 VM | Server   | 10.0.0.6(private)                        | Linux            |
| Web-3 VM | Server   | 10.0.0.7(private)                        | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 75.168.111.224

Machines within the network can only be accessed by the Jump Box.
 - Which machine did you allow to access your ELK VM? Jump Box
 - What was its IP address? 10.0.0.4/40.77.98.233

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 75.168.111.224       |
| Elk VM   | No                  | 10.0.0.4             |
| Web-1 VM | No                  | 10.0.0.4             |
| Web-2 VM | No                  | 10.0.0.4             |
| Web-3 VM | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows you to setup many servers at once. 
 - What is the main advantage of automating configuration with Ansible? You can setup up multiple servers very rapidly with playbooks.

The playbook implements the following tasks:
 - Install Docker: Installs the Docker engine for running containers.
 - Install Pip3: Installs the Python software.
 - Install Docker Python Module: Installs the Python client for Docker.
 - Use More Memory: Increases memory
 - Download and Launch Elk Container: Publishes ports and starts the container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker PS Screenshot](https://github.com/jwannen/Automated-Elk-Stack-Deployment/blob/master/Images/DockerPS.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
 - Web-1 VM 10.0.0.5
 - Web-2 VM 10.0.0.6
 - Web-3 VM 10.0.0.7
 
We have installed the following Beats on these machines:
 - Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
 - Filebeat will keep logs on files and changes therein. Metricbeat will log CPU and Memory usage, load and network traffic.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to /etc/ansible/roles/files.
- Update the filebeat-configuration.yml file to include the ELK's IP on lines #1106 and #1806.
- Run the playbook, and navigate to http://52.237.162.111:5601/app/kibana to check that the             installation worked as expected.

 - Which file is the playbook? filebeat-playbook.yml
 - Where do you copy it? /etc/ansible/roles
 - Which file do you update to make Ansible run the playbook on a specific machine?
   /etc/ansible/hosts
 - How do I specify which machine to install the ELK server on versus which to install Filebeat on?
   You need to list the VM IP's under the bracketed hosts names in the host file and list that host      name in the yml playbook after 'hosts:'
 - Which URL do you navigate to in order to check that the ELK server is running?                        http://52.237.162.111:5601
