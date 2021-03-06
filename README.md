## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/Diagram.jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

Ansible Playbook  
- _[Elk Install](Ansible/install-elk.yml)_
- _[DVWA](Ansible/ansible_config.yml)_
- _[FileBeat](Ansible/filebeat-playbook.yml)_
- _[MetricBeat](Ansible/metricbeat-playbook.yml)_

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly avaiable, in addition to restricting access to the network.
- Load balancers helpd defend against a DDOS attack. JumpBox (Jump Server) is a hardened and monitored device that spans two dissimilar security zones and provides a controlled means of access between them.

Integrating an ELK stack allows users to easily monitor the vulnerable VMs for changes to the filesystem and system performance. 
 - Filebeat monitors the log files or locations that you specify, collects log events, and index them for you.
- Metricbeat takes the metrics and statistics that it collects and ships them to the output that you specify.

The configuration details of each machine may be found below.

| Name     | Function                                      | IP Address    | Operating System |
|----------|-----------------------------------------------|---------------|------------------|
| Jump Box | Gateway                                  	   | 10.0.0.9      | Linux            |
| Web01    | Host for container running DVWA          	   | 10.0.0.10     | Linux            |
| Web02    | Host for container running DVWA               | 10.0.0.11     | Linux   	      |
| Web03    | Host for container running DVWA               | 10.0.0.12     | Linux     	      |
| Elk      | Monitoring and log aggregation for DVWA hosts | 10.1.0.4      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: 136.32.44.113 

Machines within the network can only be accessed by Internal network.


A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes                 | 136.32.44.113        |
| Web01     | No                  | Local Vnet           |
| Web02     | No                  | Local Vnet           |
| Web03     | No                  | Local Vnet           |
| Elk       | Yes                 | 136.32.44.113        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for quality replicas of the configuration which in turn speeds up deployments. 

The playbook implements the following tasks:
- Downloads and installs Docker on the ELK server
- Downloads, installs and starts ELK on a docker container on hosted on the ELK server
- Downloads, installs and starts filebeat on the docker container running on each web server, forwarding logs to the ELK server
- Downloads, installs and starts metricbeat on the docker container running on each web server, forwarding metrics to the ELK server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
| Name     | Function                                      | IP Address    | Operating System |
|----------|-----------------------------------------------|---------------|------------------|
| Web01    | Host for container running DVWA          	   | 10.0.0.10     | Linux            |
| Web02    | Host for container running DVWA               | 10.0.0.11     | Linux   	      |
| Web03    | Host for container running DVWA               | 10.0.0.12     | Linux    

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects linux logs. Which tracks things like user logins, failed access attempts, and when services are stopped or started 
- Metricbeat collects system metrics from the web servers. This will look for things like memory usage, drive space usage and availability  

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible config file to etc/ansible.
- Update the host file to include anything you would like to change using your Playbook.
- Run the playbook, and navigate to the ELK server to check that the installation worked as expected.
