# elk-project

### Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
![alt text](https://github.com/etiennelaeticia/elk-project/blob/7949d9011fe82978232f60e184727eb0a4b736f8/Diagrams/Elk-Final.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml and config file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:

Description of the Topology
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored


### How to Use the Ansible Build


Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

###### What aspect of security do load balancers protect? 
* Availability, Web Traffic, Web Security
###### What is the advantage of a jump box?
* Automation, Security, Network Segmentation, Access Control

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system log files.

###### What does Filebeat watch for?
* Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
###### What does Metricbeat record?
* Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.
Note: Use the Markdown Table Generator to add/remove values from the table.

| Name  |Function   |  IP Address |  Operating System |   
|---|---|---|---|
| Jump Box| Gateway     | 10.0.0.7 |  Linux |   
| DVWA 1  | Web Server  | 10.0.0.5 | Linux   |   
| DVWA 2  | Web Server  | 10.0.0.6 |  Linux | 
|  ELK | Monitoring   | 10.1.0.6  | Linux  | 
|  GE-GT-Load-balancer | Load balancer   | Static External IP |   |
|  Home Workstation |   | External IP or PublicIP|   |


Access Policies
The machines on the internal network are not exposed to the public Internet.
Only the Elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
* Workstation Public IP (76.214.125.179) through TCP 5601.

Machines within the network can only be accessed by Workstation and Jump-Box-Provisioner.
* Jump-Box-Provisioner IP : 10.0.0.4 via SSH port 22
* Workstation Public IP via port TCP 5601

A summary of the access policies in place can be found in the table below.


| Name  | Publicly Accessible |Allowed IP Addresses |
|---|---|---|
| Jump Box  | Yes  | Workstation Public IP(76.214.125.179) on SSH 22   |
| ELK | Yes  | 	Workstation Public IP (76.214.125.179) using TCP 5601 / 10.0.0.1-254 10.1.0.1-254 on SSH 22   |
| DVWA 1  | No   | 10.0.0.1-254 10.1.0.1-254 on SSH 22   |
| DVWA 2  | No  | 10.0.0.1-254 10.1.0.1-254 on SSH 22 |
|  GE-GT-Load-balancer | Yes   | Workstation Public IP(76.214.125.179) on HTTP 80 |   



Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because Ansible lets you quickly and easily deploy multitier apps. You won't need to write custom code to automate your systems; you list the tasks required to be done by writing a playbook, and Ansible will figure out how to get your systems to the state you want them to be in.


The playbook implements the following tasks:

* Specify a different group of machines as well as a different remote user
  `- name: Config elk VM with Docker
    hosts: elk
    remote_user: sysadmin
    become: true
    tasks:`
    
* Increase System Memory :
 `- name: Use more memory
  sysctl:
    name: vm.max_map_count
    value: '262144'
    state: present
    reload: yes`

* Launching and Exposing the container with these published ports:
`5601:5601
 9200:9200
 5044:5044`


The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.
Note: The following image link needs to be updated. Replace docker_ps_output.png with the name of your screenshot image file.


Target Machines & Beats
This ELK server is configured to monitor the following machines:

* Web-1 : 10.0.0.5
* Web-2 : 10.0.0.6

We have installed the following Beats on these machines:
* ELK Server, Web1 and Web2
* The ELK Stack Installed are: FileBeat and MetricBeat

These Beats allow us to collect the following information from each machine:

* Filebeat: log events
* Metricbeat: metrics and system statistics

Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:
SSH into the control node and follow the steps below:

Copy the _____ file to _____.
Update the _____ file to include...
Run the playbook, and navigate to ____ to check that the installation worked as expected.

TODO: Answer the following questions to fill in the blanks:

Which file is the playbook? Where do you copy it?
Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
_Which URL do you navigate to in order to check that the ELK server is running?
