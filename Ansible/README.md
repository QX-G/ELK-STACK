## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

BOOTCAMP-LIFE/Diagrams/ELK_VM.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - BOOTCAMP-LIFE/Ansible/install-elk-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly resposive, in addition to restricting access to the network.
- Deploying a load balancer in this fashion will allow users to mask true IP addresses when on a public network. A load balancer also aids in the protection from DDOS attacks by dispersing network traffic.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system resources.
- Filebeat watches log files specified by the adminstartor and collects log events.
- Metricbeat tracts the metrics of services runnning on a server and send them to Elasticsearch

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| NAME         | FUNCTION | IP ADDRESS | OPERATING SYSTEM |   |
|--------------|----------|------------|------------------|---|
| JUMP-BOX-PRO | GATEWAY  | 40.117.250 | LINUX            |   |
| WEB-0        | SERVER   | 10.0.0.7   | LINUX            |   |
| WEB-1        | SERVER   | 10.0.0.8   | LINUX            |   |
| WEB-2        | SERVER   | 10.0.0.10  | LINUX            |   |
| QX-EAST-ELK  | MONITOR  | 10.1.0.5   | LINUX            |   |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only JUMP-BOX-PRO can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- MY IP Address: 73.82.193.73

Machines within the network can only be accessed by JUMP-BOX-PRO via SSH
- PRIVATE IP ADDRESS: 10.0.0.9

A summary of the access policies in place can be found in the table below.

| NAME         | PUBLIC ACCESS    | ALLOWED IP ADDRESSES   |
|--------------|------------------|------------------------|
| JUMP-BOX-PRO | Yes with SSH KEY | 73.82.193.73           |
| WEB-0        | NO               | 10.0.0.9               |
| WEB-1        | NO               | 10.0.0.9               |
| WEB-2        | NO               | 10.0.0.9               |
| QX-EAST-ELK  | via HTTP         | 73.82.193.73/ 10.0.0.9 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... 
this will allow for both faster deployment of new machines/ redeployment of previous machines and guarentee consistency of configuration within each machine enviorment.

The playbook implements the following tasks:
- Firstly, Docker will be downloaded and installed enabling ELK to be installed inside a docker container that will be created.
- Next, python-pip3 will be installed to help with package managment.
- The playbook will then increase the size of the VM.max map count, which increases the amount of data that can be tracked by your ELK deployment.
- Finally, ELK will be installed inside a docker container.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!BOOTCAMP-LIFE/Diagrams/ELK.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB-0 10.0.0.7
- WEB-1 10.0.0.8
- WEB-2 10.0.0.10

We have installed the following Beats on these machines:
- FILEBEAT and METRICBEAR

These Beats allow us to collect the following information from each machine:
- Fileebeat monitors the system for any file system changes made
 Metricbeat logs system utilization. We can use metricbeat logs to ensure our server is balanced properly allowing for a fast, efficent and secure server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible directory.
- Update the hosts file to include the IP address of your VM
- Run the playbook, and navigate to IP:5601 (Kibana) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- playbooks can be located in /ansible/playbook and copied to /etc/ansible/playbook
- _Which file do you update to make Ansible run the playbook on a specific machine? /ansible/hosts 
How do I specify which machine to install the ELK server on versus which to install Filebeat on? by adding the given IP of the server under the specifed groups.
- http://[ELK-PUBLIC-IP]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._