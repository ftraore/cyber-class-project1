### Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://github.com/ftraore/cyber-class-project1/blob/main/Diagrams/Diagram.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as filebeat.
- Enter the playbook file. install-elk.yml
 
![install-elk.yml](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration

- Beats in Use

![filebeat-config.yml](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/filebeat-config.yml)

![filebeat-playbook.yml](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/filebeat-playbook.yml)

![metricbeat-config.yml](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/metricbeat-config.yml)

![metricbeat-playbook.yml](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/metricbeat-playbook.yml)

- Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
- Load balancing ensures that the application will be highly available, efficient, performant, in addition to restricting access to the network.
- What aspect of security do load balancers protect? Load balancers protect and contribute to the availability and resiliency aspect of security of the CIA triad.
- What is the advantage of a jump box? A jump box is a secure computer that all admins first connect to before launching any administrative task or use as an origination point to connect to other servers or untrusted environments. It is a Secure Administrative Workstation (SAW).

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the monitoring and system security.
- What does Filebeat watch for? Filebeat watches for log files or location for log events.
- What does Metricbeat record? Metricbeat records the metrics and statistics.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System    |
|----------|----------|------------|---------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux (ubuntu 18.04)|
|          |          |            |                     |
| Web-1    | Server   | 10.0.0.5   | Linux (ubuntu 18.04)|
|          |          |            |                     |
| Web-2    | Server   | 10.0.0.6   | Linux (ubuntu 18.04)|
|          |          |            |                     |                 
| Web-3    | Server   | 10.0.0.7   | Linux (ubuntu 18.04)|
|          |          |            |                     |
| Web-Elk  | Server   | 10.1.0.4   | Linux (ubuntu 18.04)|
 

### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Add whitelisted IP addresses: Host IP address (personal IP address)
Machines within the network can only be accessed by SSH.
- Which machine did you allow to access your ELK VM? The Jump-Box is the only machine allowed to access the ELK VM What was its IP address? IP address of the Jump-Box: 10.0.0.4 

A summary of the access policies in place can be found in the table below. 

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | No                  | Host IP              |
|           |                     |                      |
| Web-1     | No                  | 10.0.0.4             |
|           |                     |                      |
| Web-2     | No                  | 10.0.0.4             |
|           |                     |                      |
| Web-3     | No                  | 10.0.0.4             |
|           |                     |                      |
| Web-Elk   | No                  | 10.0.0.4             |


### Elk Configuration 
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- What is the main advantage of automating configuration with Ansible? The main advantage of automating configuration with Ansible is saving time and the ease of use. The use of one single command with the playbook allow us with the playbook to configure multiple machines at the same and do more. 
The playbook implements the following tasks:
- In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._

•	Install: docker.io

•	Install: python3-pip

•	Install: docker module

•	Increase virtual memory: sysctl -w vm.max_map_count=262144

•	Download and launch a docker elk container

•	Enable service docker on boot docker_container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![image](https://github.com/ftraore/cyber-class-project1/blob/main/Diagrams/Run%20docker%20ps.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1/IP: 10.0.0.5, Web-2/IP: 10.0.0.6, Web-3/IP: 10.0.0.7
We have installed the following Beats on these machines:
- filebeat and metricbeat
These Beats allow us to collect the following information from each machine:
- Filebeat collects log files which we use to track information about usage patterns, activities, and operations within an operating system like system logs and web logs while Metricbeat collects system-level metrics which we use to track CPU, memory usage, network traffics and load of a server.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the  file to 
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.
- Which file is the playbook? install-elk.yml Where do you copy it?_ /etc/ansible/roles

- Which file do you update to make Ansible run the playbook on a specific machine? hosts How do I specify which machine to install the ELK server on versus which to install Filebeat on? Nano /etc/ansible/hosts  then add a group called [elk] and specify the ELKserver IP and ansible_python_interpreter=/usr/bin/python3 versus 
nano /etc/ansible/ filebeat-config.yml Scroll to line #1106 and replace the IP address with the IP address of your ELK machine and scroll to line #1806 and replace the IP address with the IP address of your ELK machine.

- Which URL do you navigate to in order to check that the ELK server is running? http://[your.VM.IP]:5601/app/kibana
_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc

From host:
. ssh [username]@[Jump-Box-Public-IP]
. sudo docker start [ansible container]
. sudo docker attach [ansible container]
. cd /etc/ansible/roles or where the playbook is located
. ansible-playbook install-elk.yml
. ssh [username]@[Elkserver_Private_IP]
. sudo snap install nmap (for first user)
. nmap -Pn 80 [Elkserver_Public_IP]
. sudo docker ps
. curl http://localhost:5601/app/kibana

### Additional files

- Topology

![image](https://github.com/ftraore/cyber-class-project1/blob/main/Diagrams/Topology.PNG)

- Other updated files

  ![ansible.cfg](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/ansible.cfg)
  
  ![hosts.cfg](https://github.com/ftraore/cyber-class-project1/blob/main/Ansible/hosts.cfg)

