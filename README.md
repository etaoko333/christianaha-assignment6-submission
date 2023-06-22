## Key learnings, experience and your main selling points.

This section will be used to write your profile for your CV. So record your key learnings and experience on a weekly basis so we can track your progress and learning.

| Number      |           Subject              | What you have learnt this week and how might you describe this at an interview?   |
| :---        |            :----:              | :---  |
| 1  | Collaboration                           | working together with one or more people to complete a project or task or develop ideas or processes. In a workplace setting, the people who are collaborating must communicate clearly and share knowledge effectively   |
| 2  | Communication                           | As a DevOps engineer, communication means effectively communicating with various teams involved in the software development process. This includes developers, testers, project managers, and other stakeholders. 
   |
| 3  | Automation/CICD                         | CI/CD is a method to frequently deliver apps to customers by introducing automation into the stages of app development. The main concepts attributed to CI/CD are continuous integration, continuous delivery, and continuous deployment.
Cloud services provider and designed to allow application providers, ISVs, and vendors to quickly and securely host your applications   |
| 4  | AWS                                     | Cloud services provider and designed to allow application providers, ISVs, and vendors to quickly and securely host your applications  |
| 5  | Kubernetes                              | is an open-source system for automating deployment, scaling, and management of containerized applications.
| 6  | Terraform                               | erraform allows you to automate and manage infrastructure as code. is a tool for building, changing and versioning infrastructure safely and efficiently. Terraform can manage existing and popular cloud service providers as well as custom in-house solutions. Configuration files describe to Terraform the components needed to run a single application or your entire datacenter   |  |
| 7  | Linux                                   | An operating system   |
| 8  | System and Application Design           | System design is the process of designing the elements of a system such as the architecture, modules and components, the different interfaces of those components and the data that goes through that system
Enable the team to be faster and more agile   |
| 9  | Productivity                            | Enable the team to be faster and more agile   |
| 10 | Yourself and your abilities             | YYYYYYY

## Kubernetes, Docker, Containerisation and Virtualisation

1.  What is a Kubernetes ingress and what role does it serve? What is a Kubernetes ingress and what role does it serve? Ans: In Kubernetes, an Ingress is an API object that manages external access to services running within a cluster. It serves as a traffic controller that acts as an entry point to the cluster and allows external users to access the services hosted inside the cluster. The Ingress resource provides a set of rules and configuration for routing incoming HTTP and HTTPS traffic from an external source to specific services within the cluster.
The primary role of an Ingress is to expose HTTP and HTTPS routes, handle load balancing, and provide features like SSL termination, path-based routing, and name-based virtual hosting. It enables users to define a set of rules to determine how incoming requests are forwarded to the appropriate backend services.
In simpler terms, an Ingress is like a reverse proxy that sits between the external users and the services within the Kubernetes cluster, allowing traffic to be efficiently routed and managed based on specific rules and configurations.
What is a service in Kubernetes? Ans: In Kubernetes, a Service is an abstraction layer that defines a logical set of pods and a policy by which to access them. It provides a stable network endpoint (IP address and port) to access a group of pods, allowing other components within or outside the cluster to communicate with them.
The main purpose of a Service is to enable communication between different parts of an application or between different applications within a Kubernetes cluster. Instead of directly addressing individual pods, which are ephemeral and can change dynamically, other components can interact with a Service to access the pods it represents. This abstraction allows for decoupling and simplifies the management of network connectivity.

2.  What is a service in Kubernetes? A Service is associated with a label selector that identifies the pods it represents. The Service monitors the underlying pods and dynamically routes traffic to them based on the defined policy. It can distribute traffic evenly across all the pods or use different strategies like session affinity to ensure requests from the same client are sent to the same pod.
Kubernetes provides several types of Services:
1.	ClusterIP: The default type, which exposes the Service on an internal IP address reachable only within the cluster.
2.	NodePort: Exposes the Service on a static port on each selected node's IP address. It allows access to the Service from outside the cluster by mapping a port on the node to the Service.
3.	LoadBalancer: Automatically provisions an external load balancer in cloud environments and assigns a stable external IP address to the Service. It allows external clients to access the Service directly.
4.	ExternalName: Maps the Service to an external DNS name without the need for a selector or a cluster IP. It is useful when the Service needs to point to an external service located outside the cluster.
By using Services, applications and components within a Kubernetes cluster can communicate with each other consistently, regardless of the dynamic nature of the pods. Services provide a reliable and scalable way to expose and access microservices or other network-based resources within the cluster.




## Linux administration and shell scripting

1. Research the concept of heredoc in shell scripting. Use this site as a resource - https://stackoverflow.com/questions/2953081/how-can-i-write-a-heredoc-to-a-file-in-bash-script
2. Write a bash shell script which when run will create a file called <b>myconfig.conf</b> with the following as content of the file.
```
name=outcomer
town=mytown
class=seven
gender=male
```

Ans: #!/bin/bash
# Create the content
content="name=outcomer\ntown=mytown\nclass=seven\ngender=male"
# Write the content to the file
echo -e "$content" > myconfig.conf
# Provide confirmation
echo "myconfig.conf file has been created with the following content:"
cat myconfig.conf
Save the script in a file, for example, create_config.sh. Then, make it executable using the following command in the terminal:
bashCopy code
chmod +x create_config.sh 
To run the script and create the myconfig.conf file, execute the following command:
bashCopy code
./create_config.sh 
After running the script, you will see the confirmation message along with the content of the myconfig.conf file.

3. Write a bash script which will take a single argument and which when run will create a file called <b>myconfigparams.conf</b> with the following as content of the file. The argument should substitute the placeholder ????? below
```
name=?????
town=mytown
class=seven
gender=male
```
ans: #!/bin/bash

if [ $# -ne 1 ]; then
  echo "Usage: $0 <name>"
  exit 1
fi

name=$1
town="mytown"
class="seven"
gender="male"

cat > myconfigparams.conf <<EOF
name=$name
town=$town
class=$class
gender=$gender
EOF
./create_config.sh John
name=John
town=mytown
class=seven
gender=male
echo "File myconfigparams.conf created successfully."


4. The following scripts is used as part of user data in an EC2 instance provisioning. Analyse the script and explain what it is doing?
```
#!/bin/bash -xe
     sudo apt-get update -y # good practice to update existing packages
     sudo apt-get install -y awscli
     sudo apt install -y jq 
     sudo mkdir /etc/ssl/nginx
     # install the key and secret 
     aws secretsmanager get-secret-value --secret-id nginxcert --region ${AWS::Region} | jq --raw-output '.SecretString'| tr -d '"{}' | sudo tee /etc/ssl/nginx/nginx-repo.crt
     aws secretsmanager get-secret-value --secret-id nginxkey --region ${AWS::Region} | jq --raw-output '.SecretString'| tr -d '"{}' | sudo tee /etc/ssl/nginx/nginx-repo.key
     # Add the repo
     sudo wget https://cs.nginx.com/static/keys/nginx_signing.key && sudo apt-key add nginx_signing.key 
     sudo wget https://cs.nginx.com/static/keys/app-protect-security-updates.key && sudo apt-key add app-protect-security-updates.key
     sudo apt-get install -y apt-transport-https lsb-release ca-certificates
     printf "deb https://pkgs.nginx.com/plus/ubuntu `lsb_release -cs` nginx-plus\n" | sudo tee /etc/apt/sources.list.d/nginx-plus.list
     sudo wget -P /etc/apt/apt.conf.d https://cs.nginx.com/static/files/90pkgs-nginx
     # Install and start 
     sudo apt-get update -y # good practice to update existing packages
     sudo apt-get install nginx-plus -y # install web server   
     sudo systemctl start nginx.service # start webserver
```

## CICD, Infrastructure as as Code (IaC), Terraform, Packer and Ansible

1. Write the definition of an EC2 resource in Terraform specifying the following as part of the user data.
```
#!/bin/bash
yum update -y
amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
yum install -y httpd mariadb-server
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```
ans: 1.	#!/bin/bash -xe: This line specifies that the script is written in Bash and enables command tracing and error handling.
2.	sudo apt-get update -y: This command updates the existing packages on the EC2 instance. It ensures that the package manager has the latest information about available packages.
3.	sudo apt-get install -y awscli: This command installs the AWS Command Line Interface (CLI), which allows interaction with various AWS services from the command line.
4.	sudo apt install -y jq: This command installs the jq tool, which is a lightweight and flexible command-line JSON processor.
5.	sudo mkdir /etc/ssl/nginx: This command creates a directory /etc/ssl/nginx where the SSL certificates for Nginx will be stored.
6.	aws secretsmanager get-secret-value --secret-id nginxcert --region ${AWS::Region} | jq --raw-output '.SecretString'| tr -d '"{}' | sudo tee /etc/ssl/nginx/nginx-repo.crt: This command retrieves the secret value from AWS Secrets Manager using the nginxcert secret ID. It extracts the secret string, removes unnecessary characters, and then writes the result to /etc/ssl/nginx/nginx-repo.crt.
7.	aws secretsmanager get-secret-value --secret-id nginxkey --region ${AWS::Region} | jq --raw-output '.SecretString'| tr -d '"{}' | sudo tee /etc/ssl/nginx/nginx-repo.key: This command is similar to the previous one but retrieves the secret value using the nginxkey secret ID. It extracts the secret string, removes unnecessary characters, and writes the result to /etc/ssl/nginx/nginx-repo.key.
8.	sudo wget https://cs.nginx.com/static/keys/nginx_signing.key && sudo apt-key add nginx_signing.key: This command downloads the Nginx signing key and adds it to the apt keyring, allowing verification of Nginx packages during installation.
9.	sudo wget https://cs.nginx.com/static/keys/app-protect-security-updates.key && sudo apt-key add app-protect-security-updates.key: This command downloads another signing key for Nginx App Protect security updates and adds it to the apt keyring.
10.	sudo apt-get install -y apt-transport-https lsb-release ca-certificates: This command installs necessary packages for HTTPS transport, LSB release information, and CA certificates.
11.	printf "deb https://pkgs.nginx.com/plus/ubuntu lsb_release -cs nginx-plus\n" | sudo tee /etc/apt/sources.list.d/nginx-plus.list: This command appends an entry to the nginx-plus.list file, specifying the Nginx Plus repository URL based on the Ubuntu codename obtained from lsb_release -cs command.
12.	sudo wget -P /etc/apt/apt.conf.d https://cs.nginx.com/static/files/90pkgs-nginx: This command downloads an apt configuration file to /etc/apt/apt.conf.d directory, which sets package installation preferences for Nginx.
13.	sudo apt-get update -y: This command updates the package manager again to ensure it has the latest information about the newly added Nginx repository.
14.	sudo apt-get install nginx-plus -y: This command installs the Nginx Plus web server package.
15.	sudo systemctl start nginx.service: This command starts the Nginx web server service.

2. Launch an EC2 instance and manually run the following scripts to install Jenkins. Also run post installation checks to ensure all is running well.
From (https://phoenixnap.com/kb/install-jenkins-ubuntu)
```
#!/bin/bash
sudo apt update
sudo apt install openjdk-11-jdk -y
sudo apt install maven -y

curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
sudo systemctl status jenkins
sudo systemctl enable --now jenkins
sudo ufw enable
sudo ufw allow 8080
sudo ufw status
```


## System Architecture and Application Design, Cloud Computing (AWS)

1. You have recently joined an organisation and your boss asked your to review centralised Identity and Key management systems with a view to centralising 
the management of SSH keys. She suggests that you look into FreeIPA, LDAP, Active Directory. Research these products and describe how they might solve your problems.
1.	Ans: FreeIPA:
•	FreeIPA is an open-source Identity and Access Management (IAM) solution.
•	It combines several components, including LDAP directory services, Kerberos authentication, and Certificate Authority (CA) services.
•	FreeIPA provides centralized user and group management, authentication, and authorization.
•	It includes a web-based management interface for easy administration.
•	FreeIPA supports SSH key management, allowing users to upload and manage their public keys for authentication purposes.
•	With FreeIPA, you can enforce strong access controls, manage user permissions, and audit SSH key usage.
2.	LDAP (Lightweight Directory Access Protocol):
•	LDAP is a protocol used for accessing and maintaining directory information services.
•	It provides a hierarchical structure for organizing and storing user identities and attributes.
•	LDAP servers act as a centralized repository for user information, including SSH keys.
•	By using LDAP, you can create a centralized directory of user accounts and associate SSH public keys with user entries.
•	LDAP also supports access controls, allowing you to define who can read or modify user entries and their associated SSH keys.
•	LDAP-based solutions like OpenLDAP or Microsoft Active Directory can be used for managing SSH keys in a centralized manner.
3.	Active Directory (AD):
•	Active Directory is a directory service provided by Microsoft Windows Server.
•	It offers centralized user management, authentication, and authorization services for Windows-based environments.
•	Active Directory supports storing user attributes, including SSH keys, as part of user profiles.
•	Administrators can configure Group Policies to manage SSH key settings across the network.
•	Windows-based systems can leverage Active Directory for SSH key authentication and authorization.
•	Third-party tools and utilities can also integrate with Active Directory to manage SSH keys.
All three systems—FreeIPA, LDAP, and Active Directory—provide mechanisms for centralizing user management and can be used to manage SSH keys effectively. The choice between them depends on the specific requirements, existing infrastructure, and preferences of the organization. FreeIPA is a comprehensive open-source solution, while LDAP and Active Directory offer more specialized functionality. Consider evaluating the features, compatibility, ease of integration, and support options of each system to determine the best fit for your organization's needs.



2. We want to launch an EC2 instance that will host a website and we want to complete the installation and configuration of the website after the provisioning of the EC2 instance user user data and the shell script below. Launch an EC2 instance using using an AWS Linux 2 Kernel 5.10 AMI and using the script below complete the exercise, including post implementation checks to ensure all went well.
```
#!/bin/bash
yum update -y
amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2
yum install -y httpd mariadb-server
systemctl start httpd
systemctl enable httpd
usermod -a -G apache ec2-user
chown -R ec2-user:apache /var/www
chmod 2775 /var/www
find /var/www -type d -exec chmod 2775 {} \;
find /var/www -type f -exec chmod 0664 {} \;
echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

Some useful Post implementation checks

```
SSH onto the server and perform the following;
Logs 
less /var/log/cloud-init-output.log

Check user data entry:
curl -sL http://169.254.169.254/latest/user-data

View the AMI details
cat /etc/image-id

Check running processes on the server
ps -ef | grep ssm

ps -ef | grep apache

ps -ef | grep php

systemctl --type=service --state=running

systemctl list-units --type=service

systemctl list-units --type=service --state=active

systemctl status sshd

on the browser go to the website
http://<IP>:80
```

3. Install and configure the MERN stack using the material in this link https://www.linode.com/docs/guides/how-to-create-a-mern-stack-application/


4. You are implementing the design of two systems that are supposed to talk to each other. Come up with five questions that will help you better understand how these systems integrate with each other, that is the <b> the connective tissues </b>.
1.	Ans: What communication protocols or APIs are used for interaction between the systems?
•	Understanding the protocols or APIs utilized for communication helps determine the mechanisms and standards employed for exchanging data between the systems. Examples include RESTful APIs, SOAP, message queues, webhooks, or direct database connections.
2.	What data formats or message structures are exchanged between the systems?
•	Inquire about the specific data formats, such as JSON, XML, CSV, or binary formats, to comprehend how information is packaged and interpreted by each system. This knowledge is vital for data transformations and ensuring compatibility.
3.	How is authentication and authorization managed between the systems?
•	Determine the authentication and authorization mechanisms in place to secure the communication between the systems. This could involve OAuth, JWT (JSON Web Tokens), API keys, or other authentication protocols to establish trust and protect sensitive information.
4.	Are there any event-driven or real-time interactions between the systems?
•	Explore whether the systems rely on event-driven architecture or if real-time interactions are required. This could involve triggering actions in one system based on events occurring in another, or maintaining synchronized data in near real-time.
5.	How is error handling and exception management handled during integration?
•	Inquire about the strategies for handling errors, exceptions, and failures that may occur during the integration process. This can include mechanisms for error reporting, retry policies, logging, and ensuring data consistency between the systems.



5. When building a Three-tier architecture involving a Load balancer and an Auto-Scaling Group what steps would you take to ensure that there is a <b>connective tissue </b> between these two components? Refer to this document - https://docs.aws.amazon.com/autoscaling/ec2/userguide/attach-load-balancer-asg.html

6. At what level of the network OSI or TCP/IP stack does the following devices operate?

* 	Ans: Switches:
•	Switches operate at the data link layer (Layer 2) of the OSI model.
•	They forward data packets based on the MAC addresses of devices connected to the local area network (LAN).
•	Switches use Ethernet frames to transmit data within the network.
2.	Routers:
•	Routers operate at the network layer (Layer 3) of the OSI model.
•	They forward data packets between different networks or subnets based on IP addresses.
•	Routers use routing tables to determine the best path for forwarding data across networks.
3.	AWS Application Load Balancer (ALB):
•	AWS ALB operates at the application layer (Layer 7) of the OSI model.
•	It is a load balancing service provided by Amazon Web Services.
•	ALB can distribute incoming application traffic across multiple targets (such as EC2 instances) within an Amazon Web Services (AWS) environment.
•	ALB uses advanced routing techniques and supports features like path-based routing, host-based routing, and SSL/TLS termination.
4.	AWS Network Load Balancer (NLB):
•	AWS NLB operates at the transport layer (Layer 4) of the OSI model.
•	It is another load balancing service provided by Amazon Web Services.
•	NLB is designed to handle high-volume, low-latency traffic.
•	NLB forwards traffic based on IP addresses and transport layer protocols (such as TCP or UDP).
•	It supports features like load balancing across multiple ports, static IP addresses, and preservation of the client's source IP.

7. With respect to network communication define what these terms mean.
1.	Ans: Encapsulation:
•	Encapsulation refers to the process of wrapping data with additional protocol-specific information as it travels through different layers of the network stack.
•	In each layer of the OSI or TCP/IP model, a new header is added around the original data, creating a hierarchical structure of headers and payloads.
•	Each layer encapsulates the data from the layer above it, adding relevant control information, such as source and destination addresses, protocol information, and error checking.
2.	De-encapsulation:
•	De-encapsulation is the reverse process of encapsulation.
•	As data is received at the destination, each layer of the network stack peels off its respective header, extracting the encapsulated payload.
•	De-encapsulation occurs sequentially from the lowest layer to the highest layer until the original data is obtained.
3.	Packets:
•	In network communication, data is divided into smaller units called packets.
•	Packets are the basic units of data transmission across networks.
•	Each packet consists of a header, payload, and sometimes a trailer.
•	The header contains control information such as source and destination addresses, packet sequence numbers, and error detection codes.
•	The payload contains the actual data being transmitted.
4.	Payload:
•	The payload refers to the actual data being carried by a packet or frame.
•	It is the information that is being transmitted from the source to the destination.
•	The payload is encapsulated within the headers and trailers of the network protocol.
5.	Headers:
•	Headers are blocks of information added to the beginning of data at each layer of the network stack.
•	Headers contain control information specific to that layer and facilitate the routing, delivery, and handling of data.
•	Headers typically include source and destination addresses, protocol information, sequence numbers, and other relevant metadata.
6.	Trailers:
•	Trailers are blocks of information added to the end of data at certain network layers.
•	Trailers are optional and not present in every layer or protocol.
•	They may contain additional information, such as error detection or error correction codes, used to ensure data integrity during transmission.



8. Why is a device operating at layer 4 of the OSI model more performant than one operating at layer 7?
ans:1.	Ans: Scope of Processing:
•	Layer 4 devices, such as transport layer protocols like TCP (Transmission Control Protocol) and UDP (User Datagram Protocol), primarily focus on the transport of data and establishing reliable connections between source and destination.
•	Layer 4 devices deal with a narrower scope of processing compared to layer 7 devices, which handle application-specific protocols, content inspection, and advanced routing techniques.
•	The reduced scope of processing in layer 4 devices allows them to handle a higher volume of traffic and perform their functions more efficiently.
2.	Complexity of Operations:
•	Layer 7 devices, operating at the application layer, are responsible for handling complex tasks such as protocol decoding, content analysis, and application-level routing.
•	They need to understand and interpret higher-level protocols, such as HTTP, SMTP, or FTP, which involve analyzing message structures, headers, and payloads.
•	The additional complexity and processing requirements of layer 7 operations can introduce latency and overhead, potentially impacting overall performance.
3.	Stateful vs. Stateless Processing:
•	Layer 4 devices can operate in a stateful or stateless manner.
•	Stateless layer 4 devices, like network switches, perform forwarding based on IP addresses and transport layer ports without maintaining session-specific information.
•	Stateful layer 4 devices, such as firewalls or load balancers, maintain session state information, including connection tracking and handling features like NAT (Network Address Translation).
•	Stateless processing in layer 4 devices allows for more streamlined and efficient forwarding, enhancing performance.
4.	Flexibility vs. Specificity:
•	Layer 7 devices often require more processing power and resources to handle the specific needs of various applications, such as content inspection, protocol manipulation, or advanced routing based on application-level information.
•	Layer 4 devices, on the other hand, focus on transporting data reliably and efficiently across networks, catering to a broader range of applications without the need for detailed application-specific handling.
•	The flexibility of layer 4 devices allows them to handle a wider variety of traffic without being tied to specific application requirements, leading to better overall performance.

9. What roles does the Instance Metadata Service (IMDS) play in the architecture of the EC2 service?
 ans: Instance Metadata Retrieval:
•	The IMDS provides a service that allows EC2 instances to access metadata about themselves.
•	EC2 instances can query the IMDS to retrieve information such as instance ID, instance type, security group information, IAM role details, public and private IP addresses, and more.
•	This metadata is valuable for applications running on EC2 instances to dynamically adapt their behavior based on the instance-specific information.
2.	Dynamic Configuration:
•	The IMDS enables EC2 instances to dynamically configure themselves based on metadata.
•	Instance-specific information retrieved from the IMDS can be used to determine application configurations, network settings, environment variables, or any other parameters required for proper operation.
•	This allows for greater flexibility and automation in managing and deploying applications on EC2 instances.
3.	Security Credentials:
•	The IMDS plays a critical role in the secure delivery of temporary security credentials to EC2 instances.
•	When an EC2 instance is launched with an IAM role assigned, it can retrieve its security credentials (access key, secret access key, and session token) from the IMDS.
•	These credentials are obtained securely and automatically rotated, eliminating the need to manually manage and distribute long-term credentials on the instances.
4.	API Authentication:
•	The IMDS is also responsible for authenticating API requests made from within EC2 instances.
•	When an API request is sent from an EC2 instance to AWS services, the IMDS verifies the request authenticity using the instance's identity and associated IAM roles and policies.
•	This ensures that only authorized requests from legitimate EC2 instances are processed by AWS services.

9. What are the various methods for connecting to an EC2 instance and could you list their advantages and disadvantages.
Review the following links to learn more

* https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect.html
* https://aws.amazon.com/blogs/infrastructure-and-automation/securing-your-bastion-hosts-with-amazon-ec2-instance-connect/
* https://aws.amazon.com/blogs/infrastructure-and-automation/toward-a-bastion-less-world/

11. What roles does an Auto-Scaling Group (ASG) play in an application serving architecture?
ans:•	ASGs enable automatic scaling of resources based on demand.
•	They monitor metrics, such as CPU utilization, network traffic, or custom application-specific metrics, and adjust the number of instances in the group accordingly.
•	ASGs ensure that the application can handle varying levels of traffic and workload by automatically scaling up or down the number of instances.
2.	High Availability and Fault Tolerance:
•	ASGs provide high availability and fault tolerance for the application.
•	Instances launched within an ASG are spread across multiple Availability Zones (AZs) within a region.
•	If an instance or an entire AZ becomes unhealthy or unavailable, the ASG automatically replaces the affected instances in a healthy AZ to maintain application availability.
3.	Load Balancing:
•	ASGs work seamlessly with load balancers to distribute incoming traffic across multiple instances.
•	Load balancers, such as the Elastic Load Balancer (ELB) or Application Load Balancer (ALB), are integrated with ASGs to evenly distribute requests and provide better application performance and availability.
4.	Instance Health Monitoring and Recovery:
•	ASGs continuously monitor the health of instances in the group.
•	If an instance becomes unhealthy or fails, the ASG automatically terminates the unhealthy instance and launches a new one to replace it.
•	This ensures that instances are always healthy and the application remains operational.
5.	Version Management and Deployment:
•	ASGs facilitate the deployment of new versions of an application or software.
•	They can be used in conjunction with services like AWS Elastic Beanstalk or AWS CodeDeploy to automate the deployment process.
•	ASGs allow for the rolling updates or blue/green deployment strategies, ensuring minimal downtime and smooth application upgrades.
6.	Cost Optimization:
•	ASGs help optimize costs by automatically adjusting the number of instances based on the demand.
•	During periods of low demand, the ASG scales down the number of instances, reducing costs by minimizing unnecessary infrastructure.
•	Conversely, during high demand, the ASG scales up the number of instances to handle increased traffic and workload.



## Site Reliability Engineering (SRE), Troubleshooting, Observability

1.

2.

3.

4.

5.



## DevOps and Agile Transformation principles and methodology

1.	Agile Methodologies: Agile methodologies, such as Scrum, Kanban, and Lean, provide frameworks for iterative and incremental development, emphasizing adaptive planning, collaboration, and frequent delivery of working software.
2.	DevOps Practices: DevOps does not have a specific methodology, but rather a set of practices. These practices include continuous integration, continuous delivery, infrastructure automation, configuration management, and more, which enable fast, reliable, and automated software delivery.
3.	DevSecOps: DevSecOps extends DevOps principles to include security practices throughout the software development lifecycle, integrating security measures into the continuous delivery pipeline.

4.	SRE (Site Reliability Engineering): SRE combines software engineering and operations principles to ensure reliable, scalable, and efficient systems. It focuses on automation, monitoring, incident response, and postmortems to improve system reliability.


2.

3.

4.

5.



## New commands logs - Enter up to ten new commands you have learnt this week

| Number      | Commands | What does it do and how might you check its effect     |
| :---        |    :----:   | :---  |
| 1  | yum      | it tells linus to run update on package manager   |
| 2  | user mode       | to modify user   |
| 3  | chown       | changing the ownership of a file   |
| 4  | XXXXXXXX       | YYYYYYYY   |
| 5  | XXXXXXXX       | YYYYYYYY   |
| 6  | XXXXXXXX       | YYYYYYYY   |
| 7  | XXXXXXXX       | YYYYYYYY   |
| 8  | XXXXXXXX       | YYYYYYYY   |
| 9  | XXXXXXXX       | YYYYYYYY   |
| 10 | XXXXXXXX       | YYYYYYYY   |

## Glossary of the week - Enter new technical words you have learnt this week and their meanings.

| Number   | Word | Meaning     |
| :---     | :----:   |  :---  |
| 1  | XXXXXXXX       | YYYYYYYY   |
| 2  | XXXXXXXX       | YYYYYYYY   |
| 3  | XXXXXXXX       | YYYYYYYY   |
| 4  | XXXXXXXX       | YYYYYYYY   |
| 5  | XXXXXXXX       | YYYYYYYY   |
| 6  | XXXXXXXX       | YYYYYYYY   |
| 7  | XXXXXXXX       | YYYYYYYY   |
| 8  | XXXXXXXX       | YYYYYYYY   |
| 9  | XXXXXXXX       | YYYYYYYY   |
| 10 | XXXXXXXX       | YYYYYYYY   |

