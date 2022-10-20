# Ansible-server-installation-windows

Prerequisites to make connection between ansible control (Linux) and manage node (Windows)

## For Control Node

Install python3 and ansible
	
	sudo apt install python3
	sudo aptcinstall ansible

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

#Your Windows Server is now ready for remote management with Ansible.

 Now, Go to the control node and verify connection has been establish between control and manage node using following command -

		- ansible –m win_ping windows

NOTE - If you got timeout error enable the inbound port https-winrm

