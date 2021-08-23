### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram](/Diagram/ELK_Final.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration file may be used to install only certain pieces of it, such as Filebeat.

  ![Filebeat](/Ansible/roles/filebeat-playbook.yml)
  ![Metricbeat](/Ansible/roles/metricbeat-playbook.yml)

This document contains the following details:
- Description of the Network Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available and reliable, in addition to restricting access to the network.
What aspect of security do load balancers protect? 
- Load balancers provide several layers of security such as protection against DDoS attacks by distributing and dropping DDoS traffic before it arrives to your server. 

What is the advantage of a jump box? 
- An advantage of using a jump box is that it can be used as a secure and central point for admins to perform adminstrative tasks and access other servers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the application and system logs.

What does Filebeat watch for? 
- Filebeat watches the log files or file locations that you specify during configuration. It then ships those log files to Elasticsearch. 

What does Metricbeat record? 
- Metricbeat records metrics from the services that are running on the server. Just like Filebeat, those logs will accrue and ship to either Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name     | Function       | IP Address | Operating System    |
|----------|----------------|------------|---------------------|
| Jump Box | Gateway        | 10.0.0.4   | Linux (Ubuntu 20.04)|              |
| Web - 1  | VM via Docker  | 10.0.0.5   | Linux (Ubuntu 20.04)|
| Web - 2  | VM via Docker  | 10.0.0.7   | Linux (Ubuntu 20.04)|
| ELK - VM | Server         | 10.2.0.4   | Linux (Ubuntu 20.04)|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- 73.55.221.68

Machines within the network can only be accessed by our Jump Box Provisioner.
- Jump Box Provisioner - 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|--------------|---------------------|----------------------|
| Jump Box     |        Yes          |     73.55.221.68     |
| Web-1 / DVWA |        No           |       10.0.0.4       |
| Web-2 / DVWA |        No           |       10.0.0.4       |
| ELK-Server   |        No           |       10.0.0.4       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

- The main advantage from automating the configuration is a simpler and more efficient deployment of an application that can be duplicated.  

The playbook implements the following tasks:
- Install Docker
- Install Python3-pip
- Install Docker Module 
- Increase Virtual Memory and Use Memory
- Download and Launch a Docker ELK Container
- Enable Docker service on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Images](/Images/dockerps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 VM : 10.0.0.5 
- Web-2 VM : 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat 
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects audit logs, deprecation logs, and server logs which can be used to track events like logons, destination/source addresses, and timestamps. 
- Metricbeat collects data such as OS metrics, CPU data, memory usage, and any other data related to services that are running. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the "Ansible.cfg" file to "/etc/ansible/" .
- Update the "hosts" file to include the IP addresses of the web machine under "elk". 
- Run the playbook, and navigate to the ELK Server VM to check that the installation worked as expected.

Which file is the playbook? Where do you copy it? 
- The playbook is named "install-elk.yml". That file is located within the "roles" directory within the "/etc/ansible" file path. ![roles](/Ansible/roles/install-elk.yml)

Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- To run a playbook on a specific machine, the Ansible "hosts" file must be updated. Within the file, the IP address of the machine must be added to the corresponding hosts name which will later be used by the playbook to identify which machine is receiving the installation.  

Which URL do you navigate to in order to check that the ELK server is running?
- http://52.233.88.41:5601/app/kibana

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

