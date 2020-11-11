# Ansible_AWS
## Task Description:

## 🔅Provision EC2 instances through ansible.

## 🔅 Retrieve the IP Address of instances using the dynamic inventory concept.

## 🔅Configure the web servers through the ansible role.

## 🔅Configure the load balancer through the ansible role.

## 🔅The target nodes of the load balancer should auto-update as per the status of web servers.

## What is Load Balancer ?
### A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across a number of servers. Load balancers are used to increase capacity (concurrent users) and reliability of applications. They improve the overall performance of applications by decreasing the burden on servers associated with managing and maintaining application and network sessions, as well as by performing application-specific tasks.

<img src = "images/.png">
## What is haproxy ?
### HAProxy is free, open source software that provides a high availability load balancer and proxy server for TCP and HTTP-based applications that spreads requests across multiple servers. It is written in C and has a reputation for being fast and efficient.

## Lets Get Started with our Task
### First install ansible and boto in rhel8 using commad: pip3 install anisble boto3 .Boto is the Amazon Web Services (AWS) SDK for Python. It enables Python developers to create, configure, and manage AWS services, such as EC2 and S3. Boto provides an easy to ##use, object-oriented API, as well as low-level access to AWS services. In my system i have already installed .

<img src = "images/.png">
### Now next we will create 2 yml files one for webserver and another for the load balancer

### Webserver.yml
<img src = "images/.png">
### loadbalancer.yml
<img src = "images/.png">
### Now run both the files to deploy the webservers and loadbalancer in aws .I haved created a pass.yml file where my credentials are stored.

<img src = "images/.png">
### Our webserver and load balancer is deployed in aws we can check by going to the aws console to see that everything is working or not.

<img src = "images/.png">
### Now we need to create 2 roles in our system for configuring the webserver and the load balancer for that we will use ansible galaxy command to make a webserver adn loadbalancer role i have already made the roles so i can list them.

<img src = "images/.png">
### We need to setup the dynamic inventory to do all the configurations in the load balancer so i have used a host.py file which we have to make it executable by using chmod +x host.py which will retrive all the ips from aws instances and made changes in ansible.cfg file so to work with dynamic ips.

<img src = "images/.png">
### host.py file
<img src = "images/.png">
### Now we can check that all the webservers and loadbalancer are pingable to each other we can check by pinging them.

<img src = "images/.png">
<img src = "images/.png">
### We can se the ip of all the launched instances which inclued our 4 webservers and 1 loadbalancer .

<img src = "images/.png">
### Now we will configure webserver by creating a yml file inside our webserver roles and also the handler file.

<img src = "images/.png">
<img src = "images/.png">
### Now we will do confifurtaion for the loadbalancer we will go roles of loadbalancer and install the haproxy package inside the loadbalancer before that we need to install haproxy in our localsystem and we have to configure the haproxy.cfg file because we will copy the configuration file to the loadbalancer machine to avoid the manual configuration inside the loadbalancer machine.

<img src = "images/.png">
### main.yml file of loadbalancer
<img src = "images/.png">
### handler file for haproxy
<img src = "images/.png">
### Now we will make a roles.yml fil to execute both the roles file at same time inside the roles file.

<img src = "images/.png">
### Now we will run the roles.yml file by ansible-playbook roles.yml command and will login to the loadbalancer to check that if our configuration is done or not.

<img src = "images/.png">
<img src = "images/.png">
### Now we will go inside our load balancer to check the status of our haproxy and haproxy.cfg file to see that all the configurations of the file we made.

<img src = "images/.png">
### We can see that haproxy is active and working and we will check the haproxy.cfg file under the director /etc/haproxy/haproxy.cfg

<img src = "images/.png">
<img src = "images/.png">
### We can see that we have binded our loadbalancer to port 8080 and all the webserver ips are added to the list. if anyone from the world will come to loadbalancer public ip:8080 (ip of load balancer):8080 it will redirect them to the webservers as the user will refresh the page the ip that is shown in the web page will change because of the concept of load balancer.

<img src = "images/.png">
<img src = "images/.png">
<img src = "images/.png">
<img src = "images/.png">
## Thanks for reading !!!!!!!!!!!!!!!!
