### EC2 and nginx setup
Create a new EC2 instance, but this time go the advanced section and add this script uner user data (this is to set up nginx automatically):
- `sudo apt-get update -y`
- `sudo apt-get upgrade -y`
- `sudo apt-get install nginx -y`
- `sudo systemctl start nginx`
- `sudo systemctl enable nginx`
Paste the IP address into a new tab to see if its working.
Copy app and environmetn folder for nodejs from local host to EC2 instance (used git bash and done this in .ssh folder where my .pem file exists):
- `scp -i eng130.pem -r /C/Users/Mohammed/Desktop/Mohammed/"Sparta Global"/"DevOps course Eng130"/app ubuntu@ec2-63-32-43-180.eu-west-1.compute.amazonaws.com:/home/ubuntu`
- `scp -i eng130.pem -r /C/Users/Mohammed/Desktop/Mohammed/"Sparta Global"/"DevOps course Eng130"/environment ubuntu@ec2-63-32-43-180.eu-west-1.compute.amazonaws.com:/home/ubuntu`

### Nodejs app setup
ssh into EC2 Instance `ssh -i "eng130.pem" ubuntu@ec2-63-32-43-180.eu-west-1.compute.amazonaws.com` (the IP will change each time you create a new instance)
Run these commands after getting into instance:
- `ls` - to make sure that the files have been transfered over. Should see app and environment
- `curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -`
- `sudo apt-get install nodejs -y`
- `sudo nano /etc/nginx/sites-available/default` - Once inside delete everything using `ctrl + k` and paste this instead. Replace `8080` for local host under `proxy_pass`:

```server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;

    index index.html index.htm index.nginx-debian.html;

    server_name _;

    location / {
        proxy_pass http://localhost:8080; #Change this to the port of your application
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}```
- `sudo nginx -t` - to test if nginx is ok
- `sudo systemctl restart nginx`
- `cd app`
- `ls`
- `cd app`
- `ls`
- `nodejs --version` - should see something like this `v12.22.12`
- `npm install`
- `npm start` - should see this response `Your app is ready and listening on port 3000` and once you refresh the page, you should see the app up and running
