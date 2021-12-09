# Elkstack-Project1
project 1 of UC Davis Cybersecurity Bootcamp

The files in this repository were used to configure the network depicted below.

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the included yaml file may be used to install only certain pieces of it, such as Filebeat.

![Untitled Diagram drawio (1)](https://user-images.githubusercontent.com/85532538/145465810-ec381db1-a191-4f9a-a2d6-7155b22c99b3.png)


This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

- Filebeat monitors log files for locations that can be specified by a system administrator. Filebeat can then be used to forward and aggregate all relatable data to a centralized location 

- Metricbeat can be utilized to record metrics and statistics in respect to each service being run on various systems. Similarly, Metricbeat will send all data to a centralized location for ease of monitoring.   

- Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.

|   Name   |   Function  |   IP Address   | Operating System |
|:--------:|:-----------:|:--------------:|:----------------:|
|  Host OS | Workstation |     x.x.x.x    |    Windows 10    |
| Jump-Box |   Gateway   |    10.0.0.9    |   Ubuntu Server  |
|  ELK-VM  |  Elk Stack  |    10.1.0.4    |   Ubuntu Server  |
|  Web-VM1 | DVWA Server |    10.0.0.7    |   Ubuntu Server  |
|  Web-VM2 | DVWA Server |    10.0.0.8    |   Ubuntu Server  |
|  Web-VM3 | DVWA Server |    10.0.0.6    |   Ubuntu Server  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from my personal IP adress.

Machines within the network can only be accessed by the Jump Box. 

*** ELK-VM also accepts public connections but only from my personal IP adress.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses      |
|----------|---------------------|----------------------     |
| Jump-Box | Yes                 | x.x.x.x                   |
| ELK-VM   | Yes                 | x.x.x.x & 10.0.0.4        |
| Web-VM1  | No                  | 10.0.0.7                  |
| Web-VM2  | No                  | 10.0.0.8                  |
| Web-VM3  | No                  | 10.0.0.6                  |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automation allows for the quick configuration of multiple containers. This allows both rapid elasticity as well as scalability. 

The [playbook](https://github.com/altezzaw/Elkstack-/files/7688117/Elk-configuration.yml) implements the following tasks:

   - Configure elk with Docker
   - Increase virtual memory
   - Use more memory
   - Install Docker.io
   - Install Python3-pip
   - Install Python Docker Module
   - Download and launch a Docker Web Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![sebpelk](https://user-images.githubusercontent.com/85532538/145469540-d51d581f-2d2b-41a1-8ad4-1018ec3901c9.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- 10.0.0.6
- 10.0.0.7
- 10.0.0.8

We have installed the following Beats on these machines:

- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

- Filebeat allows you to monitor and collect log files or location, you can find graphs depicting the traffic to your server, the amount of unique connections, and the type of errors received by these connections. As well as the source IP, geolocation, and url they accessed it from.

- Metricbeat allows you to collect and analyze the metrics of your applications. Metricbeat will show Inbound and Outbound traffic, Memory usage, Disk usage, CPU usage, In and Out packet loss, and many other metrics.


### Using the Playbooks
In order to use the playbooks, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Update the etc/ansible/hosts file to include the local IP and the group name as well as the python interpreter. To specify the machine you want to Install the playbook on you need to add the group name that you entered into the hosts file into the playbook YAML file (ex. "hosts: websevers or hosts: elk")

- Run the Web playbook to install dvwa on all three of the web servers, navigate to http://[Your.VM.Public.IP]/dvwa/setup.php to ensure the servers are up and running. 
  - ansible-playbook [web-playbook.txt](https://github.com/altezzaw/Elkstack-/files/7688106/web-playbook.yml)

- Run the elk playbook, and navigate to http://[Your.VM.Public.IP]:5601/app/kibana check that the installation worked as expected.
  - ansible-playbook [Elk-configuration.txt](https://github.com/altezzaw/Elkstack-/files/7688117/Elk-configuration.yml)

- From there you can run the Filebeat and Metricbeat yaml files to start receiving data from the web servers.
  - ansible-playbook [Filebeat-config.txt](https://github.com/altezzaw/Elkstack-/files/7688166/Filebeat-config.yml)
  - ansible-playbook [Metricbeat-config.txt](https://github.com/altezzaw/Elkstack-/files/7688173/Metricbeat-config.txt)


![image](https://user-images.githubusercontent.com/85532538/145470124-dac258e1-951f-4ca0-873c-089b41061397.png)



