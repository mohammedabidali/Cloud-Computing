Create a new EC2 instance, but this time go the advanced section and add this script uner user data (this is to set up nginx automatically):
- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
- `sudo apt-get install nginx -y`
- `sudo systemctl start nginx`
- `sudo systemctl enable nginx`
Paste the IP address into a new tab to see if its working.
Copy app and environmetn folder for nodejs from local host to EC2 instance:
- `scp -i eng130.pem -r /C/Users/Mohammed/Desktop/Mohammed/"Sparta Global"/"DevOps course Eng130"/environment ubuntu@ec2-63-32-43-180.eu-west-1.compute.amazonaws.com:/home/ubuntu`
