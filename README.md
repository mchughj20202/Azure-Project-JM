# Azure-Project-JM
Azure Network environment diagram, playbooks, images and more
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Diagram: https://github.com/mchughj20202/Azure-Project-JM/blob/main/Azure%20network%20diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml file may be used to install only certain pieces of it, such as Filebeat.

Playbooks:https://github.com/mchughj20202/Azure-Project-JM/blob/main/elk-playbook.yml
https://github.com/mchughj20202/Azure-Project-JM/blob/main/metricbeat-playbook.yml
https://github.com/mchughj20202/Azure-Project-JM/blob/main/filebeat-playbook.yml
https://github.com/mchughj20202/Azure-Project-JM/blob/main/webservers-playbook.yml


The playbook files elk-playbook.yml and filebeat-playbook.yml will both be needed to create a successful ELK stack.

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers help defend against DDos attacks, by shifting traffic equally between machines. Jump boxes provide a secure location to allow access into a network, acting as a security point.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
What does Filebeat watch for?: Filebeat transfers log files and collects log events.
What does Metricbeat record?: Metricbeat records data from the operating system and from the running services and provides metrics and statistics.


The configuration details of each machine may be found below.




| Name        | IP Address | Function          | OS                              |
|----------------|----------------|--------------------|-------------------------------|
| JumpBox   | 10.0.0.4    | Ansible             | Linux (ubuntu 18.04)  |
| Web 1 VM | 10.0.0.5    | Docker-DVWA  | Linux (ubuntu 18.04)  |
| web 2 VM  | 10.0.0.6    | Docker-DVWA  | Linux (ubuntu 18.04)  |
| ELK VM     | 10.0.0.11  | Elk                    | Linux (ubuntu 18.04)  |



### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the elk machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address: 100.2.110.216


Machines within the network can only be accessed by ssh.

Which machine did you allow to access your ELK VM? What was its IP address?

Only the jumpbox was allowed access to the ELK VM, its IP is 10.0.0.4
A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses   |
|----------           |---------------------|----------------------  |
| Jump Box      | No                    | Personal IP Only       |
| Web1 VM      | No                    | 10.0.0.4               |
| web2 VM       | No                    | 10.0.0.4               |
| ELK VM         | No                    | 10.0.0.4 & Personal IP |



### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automating machine setup through Ansible is time efficient, easy to use and simple to implement. By writing playbooks to install desired services,you are able to configure multiple machines, services and commands with one file.



The playbook implements the following tasks:

Ex: ELK stack playbook
1. Install docker.io ,python3-pip and docker module
2. Increase virtual memory
3. Download and launch container, open specific ports
4. Enable service on boot



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Screenshot : https://github.com/mchughj20202/Azure-Project-JM/blob/main/dockerps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
TODO: List the IP addresses of the machines you are monitoring: 10.0.0.5, 10.0.0.6

We have installed the following Beats on these machines:
-TODO: Specify which Beats you successfully installed: Filebeat and metricbeat

These Beats allow us to collect the following information from each machine:
 Filebeat is a lightwright shipper that collects log data and events and uses elasticsearch to index the data

- Metricbeat collects metrics from the operating system and from services. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat.yml file to the /etc/ansible/roles/files/ directory
- Update the configuration file to include the Private IP of the ELK-stack-VM to the ElasticSearch and Kibana sections of the configuration file.
- Run the playbook, and navigate to the ELK-stack-VM, then run “docker ps” to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
 Which file is the playbook? Where do you copy it?:The playbook is called [filebeat-playbook.yml], you copy this into your  /etc/ansible/roles/files/ directory
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_

You will need to update the filebeat.yml file which is a configuration file that will drop into the Elk-Server in the playbook. Create a new group in the host.cfg file and add a new group called [webservers] and add the Private IP of the Elk-Server to the group. Then when configuring the filebeat.yml file you need to designate the Private IP of the Elk-Server in two lines of the .yml file. Lines 1106 and 1806 are the needed to be updated with the Private IP

- _Which URL do you navigate to in order to check that the ELK server is running?

The URL to use to verify the ELK-stack-VM is running is the Public IP on port 5601 (0.0.0.0:5601) , on the kibana app.
