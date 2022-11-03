![image](https://user-images.githubusercontent.com/89383740/199687279-188244da-0e89-4f24-9908-3c9ff6e44f64.png)
1. create Ec2 instance for web server (nodejs)
2. ssh into web app and then run these commands:
- `npm install`
- `npm start`
3. Now check if the app is up and running by pasting the IP address into a new browser.
4. Create new Ec2 instance for database server (mongodb)
5. ssh into database server using a new git bash terminal and then run these commands once you are in:
- `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv D68FA50FEA312927`
- `echo "deb https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list`
- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
- `sudo apt-get install -y mongodb-org=3.2.20 mongodb-org-server=3.2.20 mongodb-org-shell=3.2.20 mongodb-org-mongos=3.2.20 mongodb-org-tools=3.2.20`
- `sudo systemctl status mongod`
6. Configure the mongod.conf to allow access to everyone or to a specific IP address by updating the `bindIP` (0.0.0.0 to allow for everyone):
- `sudo nano /etc/mongod.conf`
7. Make sure its listening on `port 27017`
8. Save and exit the file and then run these commands:
- `sudo systemctl restart mongod`
- `sudo systemctl enable mongod` or `sudo systemctl start mongod`
- `sudo systemctl status mongod`
9. Go back to the bash terminal containing the web server
10. Create a Env variable in the App VM to point to the MongoDB VM:
- export DB_HOST=mongodb://(IP ADDRESS OF THE DB):27017/posts
- `echo $DB_HOST` - to see if the variable has been created
- `node seeds/seed.js` - so you can see the data
- `npm start`
11. Create AMI for the mongodb server on AWS
12. Click on mongodb server and then click on actions, create AMI


### What is DR?
A disaster recovery (DR) plan is a formal document created by an organization that contains detailed instructions on how to respond to unplanned incidents
such as natural disasters, power outages, cyber attacks and any other disruptive events. The plan contains strategies on minimizing the effects of a disaster,
so an organization will continue to operate – or quickly resume key operations.
A good disaster recovery plan should enable rapid recovery from disruptions, regardless of the source of the disruption.

### What is Amazon S3?
Amazon Simple Storage Service (Amazon S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance.
Customers of all sizes and industries can use Amazon S3 to store and protect any amount of data for a range of use cases, such as data lakes, websites, mobile
applications, backup and restore, archive, enterprise applications, IoT devices, and big data analytics. Amazon S3 provides management features so that you
can optimize, organize, and configure access to your data to meet your specific business, organizational, and compliance requirements.

### Benefits of S3
- Budget-friendly - Amazon provides services based on a pay-as-you-go model. This allows us to pay only for the amount of storage and the time that we use on S3
- High scalability - Scalability is the measure to increase or decrease the resource as per need
- High Durability - Durability is the measurement of the likelihood of data loss
- High availability - Availability is the measure of how readily a service can be used
- Hight Security - S3 enables automatic encryption of data as soon as the data uploading process is finished

### Use cases of s3
- Backup and Disaster Recovery
- 
