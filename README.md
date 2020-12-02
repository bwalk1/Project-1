# Project-1
This Repository contains the breakdown of a fully functioning ELK Stack that I created and deployed with my classmates.

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/Elkstack.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the "yaml" file may be used to install only certain pieces of it, such as Filebeat.

  install-elk.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly regulated, in addition to restricting access to the network.

    The "Load Balancers" protect the flow of internet traffic and help to prevent the over-loading of servers. The "Jump-Box-Machine" allows us to gain secure access to a machine in the network before moving throughout it.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the LOGS and system TRAFFIC.

    Filebeat is a good program to monitor changes of log files within a system and other forms of log data with set parameters.

    Metricbeat is another service that comes in handy, when looking for system operations and services running on a machine or location that you specify.

The configuration details of each machine may be found below.

| Name     | Function     | IP Address | Operating System |
|----------|--------------|------------|------------------|
| Jump Box | Gateway      | 10.0.0.1   | Linux            |
| Web 1    | Distribution | 10.0.0.5   | Linux            |
| Web 2    | Distribution | 10.0.0.6   | Linux            |
| ELK VM   | Logging      | 10.0.0.4   | Linux            |    

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the "Jump-Box" machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

    The only white listed IP is from the home machine of the person running the system. In this instance, it was my own IP of "184.103.42.74".

Machines within the network can only be accessed by using SSH.

    The Elk Machine was accessed using SSH from our ansible control node which was located within the Jump-Box-Machine. The IP address of the Jump-Box-Machine was "40.118.173.60" which again only allowed access from our white-listed IP.  

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses                                           |
|----------|---------------------|----------------------------------------------------------------|
| Jump Box | Yes                 | 184.103.42.74 (White-Listed IP)                                |
|  Web 1   | No                  | 10.0.0.4 (Jump-Box Private IP) 184.103.42.74 (White-Listed IP) |
|  Web 2   | No                  | 10.0.0.4 (Jump-Box Private IP) 184.103.42.74 (White-Listed IP) |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is time efficient and easily repeatable.
    

The playbook implements the following tasks:

- Installs Docker
- Installs Python
- Increases Virtual Memory
- Assigns the Increased Memory
- Downloads and launches Docker Elk Container 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Diagrams/docker_ps.png)

### Target Machines & Beats

This ELK server is configured to monitor the following machines:

- 10.0.0.5 (Web 1)
- 10.0.0.6 (Web 2)

We have installed the following Beats on these machines:
- File-Beat
- Metric-Beat

These Beats allow us to collect the following information from each machine:

    File-Beat is used to collect different types of Log data within a set of self defined parameters. With File-Beat you are able to monitor log files within those parameters that you specify and see when and where those log files are changing.
    Metric-Beat excels at monitoring what services and or operations are running on a single or set of machines. For example, if a particular system or operation is malfunctioning, it will throw and error and Metric-Beat will identify the cause and location of the error.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the File-Beat Configuration file to the Web VMs.
- Update the File-Beat Configuration file to include the IP Address of the Web Servers. 
- Run the playbook, and navigate to http://[your.VM.IP]:5601/app/kibana  to check that the installation worked as expected. The VM IP should be from the ELK VM.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

-curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-7.6.1-amd64.deb
-dpkg -i filebeat-7.4.0-amd64.deb
-filebeat modules enable system
-filebeat setup
-filebeat -e
