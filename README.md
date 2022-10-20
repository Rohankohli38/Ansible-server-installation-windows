# Ansible-server-installation-windows

Prerequisites to make connection between ansible control (Linux) and manage node (Windows)

## For Control Node

Install python3 and ansible
	
	sudo apt install python3
	sudo apt install ansible

Install pywinrm

	sudo apt install pyhton3-winrm

Go to /etc/ansible/hosts and define your host name with ip.

	 For eg-
	 [windows]
	 public-ip-address

	 [winhost:vars]
	 ansible_user=Administrator
	 ansible_password=H=TYCIeZFD&1!sW=FiaGA-XvQe(3@$EG
	 ansible_connection=winrm
	 ansible_port=5986
	 ansible_winrm_server_cert_validation=ignore

 
## For Manage Node

Go to the Manage node (Window server) and create a file with name **ConfigureRemotingForAnsible.ps1** and add all the content from the below link to the file –

> https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1

Next, run PowerShell as the **Administrator**

Execute the script using --- **.\ConfigureRemotingForAnsible.ps1**


## Your Windows Server is now ready for remote management with Ansible.

Now, Go to the control node and verify connection has been establish between control and manage node using following command -

	- ansible windows -m win_ping

***NOTE*** - If you got timeout error enable the inbound port **https-winrm**

---

## To install the application on window server we will use chocolatey that is used to manage application on windows

First install chocolatey on windows using following command on powershell

	Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

Now install chocolatey on control node (ubuntu) using following command 

	anisble-galaxy collection install chocolatey.chocolatey

---

### Ansible Playbooks to install mysql on window

Create a file with the name **mysql_install.yml** and add following code
	---
	- hosts: winhost
	  gather_facts: true
          tasks:
          - name: Install mysql
            win_chocolatey:
            name: mysql
      	    version: '8.0.31'
      	    state: present

Create a file with the name **psql_install.yml** and add follwing code

	---
	- hosts: winhost
          gather_facts: true
          tasks:
          - name: Install postgresql
            win_chocolatey:
            name: postgresql
            version: '15.0.1'
            state: present

Now run the playbook using 

	ansible-playbook mysql_install.yml

	ansible-playbook psql_install.yml

### Thanks 
