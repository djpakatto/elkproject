# elkproject
ELK Stack deployment and configuration using azure cloud solutions. 

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Path containing the network diagram: Images/ElkProjectND.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

This document contains the following details:
- Description of the topology 
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build	


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers receive any traffic that comes into the website and distributes it across multiple servers. It helps to mitigate DoS attacks. 
A jump box prevents all azure VM’s to be exposed to the public. It controls access to the other machines by allowing connections from specific IP addresses and forwarding to those machines.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
What does Filebeat watch for? 
Filebeat enables analysts to monitor files for suspicious changes. It collects data about the file system.

What does Metricbeat record?
It collects machine metrics, such as uptime, and CPU usage. Metricbeat makes it easy to collect specific information about the machines in the network

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web-1    |          | 10.0.0.7   | Linux            |
| Web-2    |          | 10.0.0.8   | Linux            |
| ElkVM1   |          | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
24.12.70.52

Machines within the network can only be accessed by the jump box and the web servers.
Jump Box: 40.122.215.250 or 10.0.0.4
Web-1: 10.0.0.7
Web-2: 10.0.0.8

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses         |
|----------|---------------------|------------------------------|
| Jump Box | Yes                 | 10.0.0.7 10.0.0.8 24.12.7052 |
| Web-1    | No                  | 10.0.0.4                     |
| Web-2    | No                  | 10.0.0.4                     |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... it is easier to replicate the configuration to a group of machines, and configure more machines at the same time. 

The playbook implements the following tasks:
- Specify the group to run the configuration, download and install docker module, configure the target VMs to use more memory, use sysctl to make the configurations persistent and run automatically after restart, download do ELK docker container and configure it to start with port mappings 5601, 9200, 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Screenshot of docker ps output](Images/ElkContainer.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
Web-1 (10.0.0.7) and Web-2 (10.0.0.8) VMs

We have installed the following Beats on these machines:
Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat: Collects data about the file system.
Metricbeat: Collects metrics, such as CPU usage, uptime, memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml file to /etc/Ansible/roles.
- Update the configuration file to include the host IP addresses for elasticsearch and kibana modules.
- Run the playbook, and navigate to (http://localhost:5601/app/kibana#/home) to check that the installation worked as expected.




