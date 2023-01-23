         ___        ______     ____ _                 _  ___  
        / \ \      / / ___|   / ___| | ___  _   _  __| |/ _ \ 
       / _ \ \ /\ / /\___ \  | |   | |/ _ \| | | |/ _` | (_) |
      / ___ \ V  V /  ___) | | |___| | (_) | |_| | (_| |\__, |
     /_/   \_\_/\_/  |____/   \____|_|\___/ \__,_|\__,_|  /_/ 
 ----------------------------------------------------------------- 


Hi there! Welcome to AWS Cloud9!

In this assignment  by the Manager (Professor) is that we will deploy  static web servers on Linux-based virtual machines using configuration management and Linux administration tools. The Infrastructure was created in terraform whereas webserver are deployed using Ansible.

Following are the steps that you should follow inorder to deploy the sucessfull webserver on linux based Machines:


Prerequisites
Deploy the Webserver by using the terraform code before.


1. First of all Install the ansibe using the command >> sudo yum install ansible -y. You verify the sucessfull verfication by running the command >> ansibe --version.

2. Update the file by using the command >> sudo vim /etc/ansible/ansible.cfg and uncomment this in the file  "host_key_checking = False" present in the default section in the file.

3. This command will run and return the Ping from the both linux flavoured machines (RedHat, Debian) >> ansible -i hosts.txt BothInstances -m ping  
4. This command will run and return  both linux flavoured machines (RedHat, Debian) deployed >> ansible -i hosts.txt BothInstances -m setup -a "filter=ansible_os_family"

5. To Use the Ansible Configuration more Dynamically run the commands in the following order. 
   5.1) First of Install the python library -- sudo yum install python-boto3
   5.2) Update the file by using the command  >> sudo vim /etc/ansible/ansible.cfg >> update the value of "enable_plugins" to this "enable_plugins = aws_ec2"
   
6. To display the dynamic inventory in the form of tree run the command >> ansible-inventory -i aws_ec2.yaml --graph
7. To Deploy the webserver on existing 4 machines run the Command >>  ansible-playbook -i aws_ec2.yaml Safeer007playbook.yaml 
8. We will deploy one more linux-based machine and re-deploy the webserver by using the command in Step 7. it should only deploy on the new instance not all of the instance.

9. This command will retun the out put that webserver on Redhat machines are sucessfully deployed >> ansible -i aws_ec2.yaml tag_AmazonLinuxRedHat -m uri -a "url=http://localhost" -u ec2-user --private-key ~/.ssh/Safeer007key
10. This command will retun the out put that webserver on Debian machines are sucessfully deployed  ansible -i aws_ec2.yaml tag_UbuntuDebian -m uri -a "url=http://localhost" -u ubuntu --private-key ~/.ssh/Safeer007key

PostCondition 
Destroy all the webservers.

Happy coding!
