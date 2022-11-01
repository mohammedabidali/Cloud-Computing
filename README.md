# Cloud-Computing

### What is cloud computing?
Cloud computing is the delivery of computing services over the internet on a metered pay-as-you-go basis. Some examples are virtual machines, databases, and networking.

### Why use the cloud and what are some of the benefits?
if you can't afford to buy the physical infrastructure of your operation, then you can just pay for what you are using through subscriptions on the cloud. It is much cheaper and affordable. 

### Advantages of using the cloud
- Saves money
- Saves space
- Less responsibility (don't have to install security for physical infrastructure, like cameras and security guards. Don't have to worry about power and cooling.)
- Easy to set up

### What is AWS?
AWS stands for Amazon Web Services. AWS provides on-demand cloud computing platforms to individuals, companies, and governments.

### Who is using AWS?
- Netflix
- LinkedIn
- Facebook

### Why use AWs?
- AWS offers a lot of its services as free tires. For example for some of the services you get a free trial period to test out the service and see how it is. While other services have a free 12-month trial or even always free.
- AWS is a global leader - it has a bigger marget share that most of the cloud providers.
- Very simple to use. It is design for developers to get quickly accustomed to the interface.

### IAAS - PAAS - SAAS
![image](https://user-images.githubusercontent.com/89383740/199247851-66513f40-2d0f-4604-a695-57cdd947fcd7.png)

IAAS - Infrastructure as a Service are made of highly scalable and automated computer resources. IaaS is fully self-service for accessing and monitoring computers, networking, storage, and other services. IAAS provides the most control of your infrastructure, in terms of network security and typy of operating system used for your VMs, but this also means a lot more responsibility. Eamples if IAAS, AWS, Microsoft Azure.

PAAS - Platform as a Service. PaaS delivers a framework for developers that they can build upon and use to create customized applications. An example of a PAAS application is gmail.

SAAS - Software as a Service, also known as cloud application services, represents the most commonly utilized option for businesses in the cloud market. SaaS utilizes the internet to deliver applications, which are managed by a third-party vendor, to its users. Examples of SAAS, Salesforce, Netflix.

### What IS CapEx and OpEx?
- Capital expenditure are major purchases for a company or an individual to be used over a long time. This is when you pay for your infrastructure in full. For example when you buy new hardware, or upgrade power in the building etc.
- Operational expenditure is more day-to-day. For example, the cloud is used as a type of OpEx. You use the cloud to pay for services that you use only, and if you stop usng a service, then you no longer have to pay for it.


## Amazon Elastic Compute Cloud (EC2)
EC2 is a virtual server in the AWS Infrastructure. It provides scalable computing capacity and eliminates your need to invest in hardware up front, so you can develop and deploy applications faster.

### Setting up key pair in .ssh folder
- cd .ssh
- nano eng130.pem
- copy over the key pair and then save the file
- chmod 400 eng130.pem

### EC2 instance set-up
Locate and launch an EC2 Instance
EC2 specifications:
- Name and tags: follow this convention - eng130_name
- Application and OS images: browse for `ubuntu 18.04 LTS` image, or just find it in your recent imagies if you have used it before.
- Instance type: keep at default of `t2.micro`
- Key pair: select `eng130`
- Network settings: Allow for both `ssh` and `http` traffic from the internet. Click on edit and change the security name to follow the convention. E.g. `eng130_name_sg`
- Configuration storage: keep it at default of `8GiB`
- Finally click `Launch instance`

### Connecting to EC2 Instance
- Click on your instance and then click connect.
- Click on SSH client tab
- follow the instructions to connect

### Setting up nginx and reverse proxy in EC2 instance
- pwd, whoami, uname -a (to see if its working)
- sudo apt-get update -y
- sudo apt-get upgrade -y
- sudo upt install nginx -y
- Find the IP address of your EC2 instance and paste it into a new browser to see if it worked. (Can find the IP address after clicking `connect` on AWS interface
- sudo systemctl status nginx (to check status of nginx)
- sudo nano /etc/nginx/sites-available/default (change the proxy_pass to port 3000)
- sudp nginx -t (test if nginx is working. Should have this response: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok,
nginx: configuration file /etc/nginx/nginx.conf test is successful
- sudo systemctl restart nginx
