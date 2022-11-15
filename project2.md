# LEMP STACK IMPLEMENTATION

## *I started by creating a new EC2 instance of the t2.micro family with Ubunti 20.04 LTS (HVM) image.*

### Step 1 - Install Ngnix Web Server
 The first thing I did after creating the EC2 instance was to install the Ngnix web server.

1. Updated the server's package index

 `sudo apt update` 

 Then I installed Ngnix

 `sudo apt install nginx`


 2. I confirmed Ngnix installation status

 `sudo systemctl status nginx`

 