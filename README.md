# Linux Server Configuration Project

## Server Details
IP address : 54.93.200.82
SSH port : 2200

## Configuration steps 
### 1. Create an instance in AWS Lightsail 

Go to AWS Lightsail and create a new account / sign in with your account.

Click `Create instance` and choose `Linux/Unix`,`OS only` `Ubuntu 16.04LTS`

Choose a payment plan (the cheapest plan is enough for now and it's free for first month)

Click `Create` button to create an instance.

### 2. Set up SSH key

Go to `account` page from your AWS account. You will find your SSH key there.

Download your SSH key, the file name will be like `LightsailDefaultPrivateKey-*.pem`

Navigate to the directory where your file is stored in your terminal.

Run `chmod 600 LightsailDefaultPrivateKey-*.pem` to restrict the file permission. 

Change name to `lightsail_key.rsa`.

Run a command `ssh -i lightsail_key.rsa ubuntu@54.93.200.82` in your terminal.

### 3. Change SSH port from 22 to 2200

Edit `/etc/ssh/sshd_config` file by `sudo nano /etc/ssh/sshd_config`

Change port from `22` to `2200`

Save the change by `Control + X ` and exit from nano with `Y`

Restart SSH with ` sudo service ssh restart`

### 4. Set up Uncomplicated Fire Wall (UFW)

Configure UDW to allow only incoming request from port2200(SSH), port80 (HTTP) and port123 (NTP).

`sudo ufw status ` -- utf should be inactive

`sudo ufw default deny incoming` -- deny all incoming requests

`sudo ufw default deny outgoing`-- allow all outgoing requests

`sudo ufw allow 2200/tcp` -- allow incoming ssh request

`sudo ufw allow 80/tcp` -- allow all http request

`sudo ufw allow 123/udp` -- allow ntp request

`sudo ufw deny 22` -- deny incoming request for port 22

`sudo ufw enable` -- enable ufw

`sudo uff status` -- check current status of ufw

Go to AWS page and set up relevant ports from `networking` tab.

