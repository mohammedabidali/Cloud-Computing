1. create Ec2 instance for web server (nodejs)
2. ssh into web app and then run these commands:
- npm install
- npm start
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
- sudo nano /etc/mongod.conf
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
