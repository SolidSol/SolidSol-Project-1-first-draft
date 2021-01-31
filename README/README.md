## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Azure Elk Deployment](../HW12-Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the (YAML) file may be used to install only certain pieces of it, such as Filebeat.

  - Elk-Playbook.yml._

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly (dynamic), in addition to restricting (access) to the network.

- (Question): "What aspect of security do load balancers protect?" 
  A.) A load-balancer, in this case a Load-balancer of the software variaty have features and policy controls to stop bad traffic from ever reaching the main application, two main examples being (rate limiting) and (URL filtering). Both software and physical Load-balancers work on layers 4-7 of the OSI model (transportation, session application, presentation). Load-balancers protect against threats like (S.Q.L injection) and (Cross-site scripting (XSS)). 

- (Question): "What is the advantage of a jump box?"  
  A.) A Jump Box is a window server that is a bridge between two trusted networks. The Jump Box is in most cases security hardened and is the main entryway to your server group. The Jump Box is usually built in front of other servers to add a security layer preventing all Azure VM's from being exposed to the public. Advantages of using a Jump box, it allows you to focus all the monitoring and logging on that one box and also a jump box allows you to turn ir off to stop all RDP (Remote Desktop Protocal) to everything when you know its not needed. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the (Configuration) and system (Files).

- (Question): What does Filebeat watch for? 
  A.) "Filebeat" watches and monitors the log files or locations that users specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing. Filebeat is a lightweight shipper for forwarding and centralizing log data. Installed as an agent on the server.

- (Question): What does Metricbeat record? 
  A.) "Metricbeat" kinda like Filebeat, but Metricbeat is a lightweight shipper that periodically collects metrics from the operating system and from services running on the server. It akes the metrics and statistics that it collects and ships them to the output that you specify.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name         | Function  | IP Address | Operating System |
|--------------|-----------|------------|------------------|
| Jump Box     | Gateway   | 10.0.0.1   | Linux            |
| Web-1        | Web server| 10.0.0.5   | Linux            |
| Web-2        | Web server| 10.0.0.6   | Linux            |
| ElkProject1VM| Web Server| 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the (Jump Box Provisioner) machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- (Question): Add whitelisted IP addresses
  A.)My Ip

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses |
|--------------|---------------------|----------------------|
| Jump Box     | Yes                 | 10.0.0.1 10.0.0.2    |
| Web-1        | No                  | 52.183.102.245       |
| Web-2        | No                  | 52.183.102.245       |
| ElkProject1VM| No                  | 52.183.102.245       |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...A.) Using Ansible allows for universal changes to be made within any of the VMs associated with the AnsibleThis allows for Universal changes to be made within any of the VMs associated with the Ansible. Keeps things consitant and fluid with the playbook established.

- (Question): What is the main advantage of automating configuration with Ansible?
  A.) One of the main advantages of "Automation" within Ansible is the use of roles. Ansible Roles provide the groundwork or the road map for either fully independent,or interdependent collections of variables, tasks, files, templates and modules. These Roles simplify the writing of complex playbooks. The Rolse themselfs are not the Playbooks, but rather simple functionalities within the playbook. Basically the "legos" to your larger machine.

The playbook implements the following tasks:
- (Question): In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Elk Instalation:) Creating a new vNet which we needed to be located in the same (resource group), most of the setting stayed consistant, my focus was on the adding Peering, which established the connection between all vNets. Importan for allowing traffic to pass between said vNets a
- Install Docker): we had to create a playbook that installed Docker and configured the containers, -name: Config elk VM with Docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.1.0.4
10.0.0.4
10.0.0.5
10.0.0.6


- List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- : Specify which Beats you successfully installed
 A.) Filebeat and MetricBeat

These Beats allow us to collect the following information from each machine:
- (Question): In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.
 A.) Filebeat watches/monitors log files, log events and locations that users specify,   Example: Inputs and harvesters
 A.) Metricbeat watches for any information in the file system which has been changed/altered and time frame. Takes the statistics

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to Jump box to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?
 A.) ansible.cfg
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
 A.) Elk.yml
- _Which URL do you navigate to in order to check that the ELK server is running?
 A.)http://[ElkProject1VM-ip]:5601/app/kibana

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
