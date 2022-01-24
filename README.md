## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.
Load blancers help protect against Distributed Denial of Service (DDos) attacks. Jump boxes allow for a much more secure access point to an internal network by allowing a single machine to be hardned and monitored at all times vs all machines being hardned and monitored. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system services.
Filebeat monitors for any changes done to the machine. Metricbeat monitors for any changes done to the services of the machine. 

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| ELK Stack| Log Server| 10.1.0.4   | Linux            |
| Web1     | Web Server | 10.0.0.5   | Linux            |
| Web2     | Web Server | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from specified whitelisted address through secuirty group settings

Machines within the network can only be accessed by the Jumpbox.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes              | Based of Security group    |
|  Web1, Web2 |    No      |     10.0.0.4     |
|  Elk Stack |       Yes          |  Based on Security group   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it produces a repeatable and known output every single time it's ran. Allowing for indefent expansion if needed.

The playbook implements the following tasks:
- Installs Docker 
- Installs Python3
- Increases virutal memory allocation

Running 'docker ps' on the ELK stack machine after successfully configuring the ELK instance should have an output similar to this.
 
 ```
CONTAINER ID   IMAGE                 COMMAND                  CREATED       STATUS         PORTS                                                                             NAMES
5f7b8ad9eb4f   sebp/elk:761          "/usr/local/bin/star…"   10 days ago   Up 5 minutes   0.0.0.0:5044->5044/tcp, 0.0.0.0:5601->5601/tcp, 0.0.0.0:9200->9200/tcp, 9300/tcp   elk
f5ab0d801344   cyberxsecurity/dvwa   "/main.sh"               10 days ago   Up 5 minutes   0.0.0.0:80->80/tcp                                                                 dvwa
```
### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 at 10.0.0.5
- Web2 at 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat monitors a set location or logs and logs any changes done to them. Any sort of moving, deleting, and edits are reported back to the ELK stack through filebeat. Allowing for tracking of when things where changed in said files.
- Metricbeat monitors system services and logs them. Metricbeat collects all data coming into a monitored system, allowing users to pinpoint when certain events took place. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible playbook file to /etc/ansible.
- Update the host file to include the IP's to the VM's you want to install Filebeat and Metricbeat.
- Run the playbook, and navigate to [http://public_IP_for_ELK:5601/app/kibana] to check that the installation worked as expected.
