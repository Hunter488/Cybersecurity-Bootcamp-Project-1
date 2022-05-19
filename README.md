# Cybersecurity Bootcamp Project 1
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Network Diagram](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Images/Network%20Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YML file may be used to install only certain pieces of it, such as Filebeat.

![ELK Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Install-ELK.yml)

![Filebeat Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Filebeat-playbook.yml)

![Metricbeat Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Metricbeat-playbook)

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
Load balancers help ensure environment availability through distribution of incoming data to web servers. Jump boxes allow administration of multiple systems and provide an additional layer between the outside and internal network environment.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the event logs and system metrics.

Filebeat monitors directories and specific log files.
Metricbeat monitors your servers by collecting metrics from the system and services running on the server. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| Web 1    | Server   | 10.1.0.5   | Linux            |
| Web 2    | Server   | 10.1.0.6   | Linux            |
|ELK Server|Log Server| 10.0.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

-Personal IP Address

Machines within the network can only be accessed by the jumpbox provisioner.
The Elk Machine can be accessed from a designated IP address through port 5601.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | Personal IP          |
| Web 1    | No                  | 10.1.0.5             |
| Web 2    | No                  | 10.1.0.6             |
|ELK Server| Yes                 | Personal IP          |
|Load Balancer| Yes              | Open                 |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because servcies running can be limited, system installation and update can be streamlined, and processes become more replicable.

The playbook implements the following tasks:

* Installs docker.io, pip3 and the docker module
* Increases the VM memory
* Uses sysctl module
* Downloads and launches the docker container for the ELK Server


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

* Web 1 (10.1.0.5)
* Web 2 (10.1.0.6)

We have installed the following Beats on these machines:

* Metricbeat
* Filebeat

These Beats allow us to collect the following information from each machine:

* Metricbeat records metrics and statistical data from the operating system and from services running on the server
* Filebeat is a log data shipper for local files. Installed as an agent on your servers, Filebeat monitors the log directories or specific log files, tails the files, and forwards them either to Elasticsearch or Logstash for indexing. An examle of such are the logs produced from the MySQL database supporting our application.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the configuration file from your Ansible container to your Web VM's
- Update the /etc/ansible/hosts file to include the IP address of the Elk Server VM and webservers.
- Run the playbook, and navigate to http://[Elk_VM_Public_IP]:5601/app/kibana to check that the installation worked as expected.
- _Which file is the playbook?_ the playbook files are listed below:
- ![ELK Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Install-ELK.yml)
- ![Filebeat Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Filebeat-playbook.yml)
- ![Metricbeat Installation](https://github.com/Hunter488/Cybersecurity-Bootcamp-Project-1/blob/main/Ansible/Metricbeat-playbook)
- _Where do you copy it?_ /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine?_ /etc/ansible/hosts.cfg
- _How do I specify which machine to install the ELK server on versus which to install Filebeat on?_ You specify which machine to install by updating the host files with ip addresses of web/elk servers and selecting which group to run on in ansible.
- _Which URL do you navigate to in order to check that the ELK server is running?_ http://[Elk_VM_Public_IP]:5601/app/kibana
