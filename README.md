# ELK_project
ReadTeam
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/urtok/ELK_project/blob/main/ELK_diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

 - Play book file: elk_playbook.yml.

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
- Load balancer provides availability by redirecting the client to wed-server that is less used. Advantage of Jump Box establish secure connection via ssh with virtual machines. Enables to build ansible with docker.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metric and system files.
- What does Filebeat watch: for logs and events.
- What does Metricbeat record: cpu and other harware usage

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-box | Gateway  | 10.0.0.7 & 52.188.152.121 | Linux |
| WEB-1    |  VM      | 10.0.0.8   |  Linux           |
| WEB-2    |  VM      | 10.0.0.9   |  Linux           |
| WEB-3    |  VM      | 10.0.0.10  |  Linux           |
|ELK-stack |  VM      | 10.2.0.4   |  Linux           |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 71.225.237.188

Machines within the network can only be accessed by ansible container.
-Jump Box is allowed to access ELK VM through ansible container. ELK's private ip: 10.2.0.4 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | yes                 | 71.225.237.188       |
| Web-1         |    no          |   10.0.0.0/24                     |
| Web-2         |    no           |   10.0.0.0/24                   |
| web-3          |    no                 |   10.0.0.0/24
|ELK            |     yes                 |  71.225.237.188|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
-Ansible is fast and performs all functions over SSH. Also it automates tasks.

The playbook implements the following tasks:
- created new Virtual Network in US2 region
- created peer to peer connections with VMs
- configured ELK stack has 2vCPUs and 4GiB of memory.
- Added the new VM to Ansible’s hosts file in jump-box-provisioner993
- Created an Ansible playbook that installs Docker and configures an ELK container
- restricted access to ELK-stack

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/urtok/ELK_project/blob/main/docker_ps.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8, 10.0.0.9, 10.0.0.10

We have installed the following Beats on these machines:
- insatlled Filebeat

These Beats allow us to collect the following information from each machine:
- Filebeat is an agent which runs on servers. Filebeat monitors the log files, collects log events, and forwards them to Logstash and then to Elasticsearch.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config file to ansible container .
- Update the filebeat-config.yml file to include you ELK VM ip address.
- Run the playbook, and navigate to Filebeat installation page on the ELK's GUI to check that the installation worked as expected.

- Playbook is yml file. Stores in /etc/ansible/ directory
- _Which file do you update to make Ansible run the playbook on a specific machine? - In /etc/ansible/hosts.
How do I specify which machine to install the ELK server on versus which to install Filebeat on? - By adding the ip in the hosts file.
- http://104.209.142.138:5601/app/kibana#/home/

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
ansible-playbook install-elk.yml 
ansible-playbook filebeat-install.yml


