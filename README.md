# Ansible-server-installation-windows

##Prerequisites to make connection between ansible control (Linux) and manage node (Windows)
1.	CentOS 7 (Control Node)
username - centos

2.	Window server 2016 SQL server (Managed Node)
 Username – Administrator
Password - TxD4W-@dU@;ZKiAlq.6sJNt-dB398mMc
Steps To make connection between Control and manage node. 
1.	Install Python and ansible on Control node. 

2.	Install pyhton2-winrm on control node. 

$ sudo yum –y install python2-winrm

3.	Go to /etc/ansible/hosts and define your host name with ip.

 

4.	Go to the Manage node (Window server) and create a file with name ConfigureRemotingForAnsible.ps1 and add all the content from the below link to the file –
https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1
5.	Next, run PowerShell as the Administrator

6.	Modify the execution rules of the PowerShell scripts to allow the execution of the script.

	Set-ExecutionPolicy RemoteSigned

7.	Execute the script.
	.\ConfigureRemotingForAnsible.ps1

Your Windows Server is now ready for remote management with Ansible.
8.	Now, Go to the control node and verify connection has been establish between control and manage node using following command -

$ ansible –m win_ping winhost

NOTE - If you got timeout error enable the inbound port https-winrm
Now , make sure that sql.zip file is available with 
9.	Unzip the zip file and verify all the content

 

10.	Make sure to comment out add the roles path to /etc/ansible/ansible.cfg file 

 

11.	 Now run your main.yml playbook in your playbooks directory and verify your files are copied and executed successfully on window server. 
   



