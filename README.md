# Elk-Stack-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Elk Stack Diagram](https://github.com/kphanswims15/Elk-Stack-Project/blob/main/Day3/ElkStackDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _YAML_ file may be used to install only certain pieces of it, such as Filebeat.

  - [Install ELK](https://github.com/kphanswims15/Elk-Stack-Project/blob/main/Day1/install-elk.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _efficient_, in addition to restricting _access_ to the network.
- Load balancers protect against DDos attacks. So if one server goes down then the load balancer redistrubtes work to other servers keeping the whole system from going down. An advantage of a jump box is that you have to connect to it first in order to do any administrative task. You can also use it to streamline maintenance of a system by only having to update the jumpbox. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _file system_ and system _metrics_.
- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticserach or Logstash for indexing
- Metricbeat helps monitor servers by collecting metrics from the system and services runnign on the server. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.1.0.4   | Linux            |
| Web-1    | Server   | 10.1.0.5   | Linux            |
| Web-2    | Server   | 10.1.0.9   | Linux            |
| ELKVM    | Server   | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the _public_ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Only from my public ip address

Machines within the network can only be accessed by _ssh_.
- JumpBoxProvisioner
- public IP: 20.94.229.3
- private IP: 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|--------------------- |
| Jump Box | Yes                 | 20.94.229.3          |
| Web-1    | No                  | 10.1.0.5             |
| Web-2    | No                  | 10.1.0.9             |
| ELKVM    | No                  | 10.2.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- automation is more efficent and reduces opportunity for mistakes to be introdcued to the system. The configuration also has been tested and troubleshooted.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install Docker python module
- Adds more virtual memory 
- Downloads and launchs a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://github.com/kphanswims15/Elk-Stack-Project/blob/main/Day1/docker%20ps%20results.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1: 10.1.0.5
- Web-2: 10.1.0.9

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeats collects and sends log data which can provide access information
- Metricbeats collects and sends metric data of what is running on a server which can provide information on memory and usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _playbook_ file to _Ansible Control Node_.
- Update the _hosts_ file to include webserver and elk
- Run the playbook, and navigate to _Kibana (http://20.110.7.92:5601/app/kibana#/home)_ to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
- cd /etc/ansible
- mkdir files
- git clone https://github.com/kphanswims15/Elk-Stack-Project.git
- cp /Elk-Stack-Project/README/roles/* /etc/ansible
