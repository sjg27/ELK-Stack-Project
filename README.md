# ELK-Stack-Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

/diagrams/RedTeam-NetworkDiagram_v2.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-playbook.yml
  - metric-playbook.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly persistent, in addition to restricting access to the network.

- It protects against Denial of Service attacks and mass influx of traffic.

- One advantage of a jump box is that it's a gateway this a point to have a firewall to keep out anyone that does not belong there.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics and system logs.

- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat collects machine metrics, such as uptime.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | DVWA     | 10.0.0.5   | Linux            |
| Web-2    | DVWA     | 10.0.0.6   | Linux            |
| Web-3    | DVWA     | 10.0.0.7   | Linux            |
| ELK      | Kibana   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the virtual machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- 173.3.8.222

Machines within the network can only be accessed by SSH.

- My local machine is able to access the ELK VM and Web VM through the container within the Jump-Box-Provisioner VM.
..* 173.3.8.222

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 173.3.8.222          |
| Web-1    | No                  |                      |
| Web-2    | No                  |                      |
| Web-3    | No                  |                      |
| ELK      | No                  |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- Infrastructure as Code allows us to reuse the same code to across multiple devices without needing to waste time logging into each device. 

The playbook implements the following tasks:

- Install Docker
- Install Python3-Pip
- Install Docker module
- Increase Virtual Memory
- Download and Launch the Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

/Images/docker_ps.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:

- Filebeat was installed on these VMs:
..- Web-1
..- Web-2
..- Web-3

- Metricbeat was installed on these VMs:
..- Web-1
..- Web-2
..- Web-3

These Beats allow us to collect the following information from each machine:

- Filebeats monitors and collects log files, then forwards it to Elasticsearch or Logstash. For example, if someone was trying to SSH into one of the Web VMs, Filebeat will record if they were successful or not and the IP address they accessed from. 

- Metricbeat collects the metrics and statistics and forwards them to Elasticsearch or Logstash. For example, it can track how much the CPU is being used and how many requests are coming through the site

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yaml file to the roles folder.
- Update the hosts file to include the internal IP of Web VMs.
- Run the playbook, and navigate to the ELK VM to check that the installation worked as expected.

- install-elk.yml
- Move this file to the roles folder
- The hosts file under /etc/ansible allows you to create groups and place the internal IPs of a VM.
..- In the yaml file you specify which host will be affected by this file.
- http://your.ELK.VM.IP:5601/app/kibana
