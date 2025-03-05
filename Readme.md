Setting Up a Web Server on AWS (Ubuntu EC2 + Apache)

In this guide, I'll walk you through the step-by-step process of setting up a web server on AWS. This includes launching an Ubuntu EC2 instance, connecting to it via SSH, and installing Apache to serve web pages.

Step 1: Launching an Ubuntu EC2 Instance on AWS

1. Log in to AWS Management Console

Go to AWS Console.

Sign in to your AWS account.

2. Navigate to the EC2 Dashboard

In the AWS Management Console, search for EC2 in the search bar.

Click on EC2 to open the EC2 Dashboard.

3. Launch a New Instance

Click Launch Instance.

4. Configure Instance Details

Name your instance: (e.g., Ubuntu-Server)

Choose Amazon Machine Image (AMI):

Select Ubuntu Server 22.04 LTS (or your preferred version).

Choose Instance Type:

Select t2.micro (free tier eligible).

5. Configure Key Pair

Create a new key pair or use an existing one.

Download and store the key securely (you will need it to connect via SSH).

6. Configure Network Settings

Enable Allow SSH traffic (Port 22).

Allow HTTP traffic (Port 80) for web access.

7. Configure Storage

Set the storage to at least 8 GB (default).

8. Launch the Instance

Click Launch Instance.

Wait for the instance to initialize (takes a few minutes).

Step 2: Connecting to the Instance via SSH

Once your instance is running, follow these steps to connect:

1. Get the Public IP Address

Go to the EC2 Dashboard.

Click on your running instance.

Copy the Public IP Address.

2. Open a Terminal (or Command Prompt)

Linux/macOS users: Open Terminal.

Windows users: Open PowerShell or use an SSH client like PuTTY.

3. Navigate to the Location of Your Key File

If your .pem key file is in the Downloads folder, move into that directory:

cd ~/Downloads

4. Set Proper Permissions for the Key File

Run this command to ensure the key has the correct permissions:

chmod 400 your-key.pem

(Replace your-key.pem with the actual key file name.)

5. Connect to the EC2 Instance

Run the following SSH command to log in to your server:

ssh -i your-key.pem ubuntu@<Public-IP>

(Replace your-key.pem with the actual key file name and <Public-IP> with your instance's public IP.)

6. Verify Connection

If everything is set up correctly, you should see something like this:

Welcome to Ubuntu 22.04 LTS (GNU/Linux 5.15.0-1036-aws x86_64)

This confirms that you have successfully connected to your Ubuntu EC2 instance via SSH! 🎉

Step 3: Installing and Configuring Apache on Ubuntu EC2

Now that you're connected to your Ubuntu EC2 instance via SSH, let's install and configure Apache to serve web pages.

1. Update the Package List

Before installing any software, update the package list to ensure you have the latest versions:

sudo apt update

2. Install Apache

Run the following command to install Apache:

sudo apt install apache2 -y

(The -y flag automatically confirms the installation.)

3. Start and Enable Apache

Once installed, start the Apache service and enable it to launch automatically at system boot:

sudo systemctl start apache2
sudo systemctl enable apache2

To verify that Apache is running, check its status:

sudo systemctl status apache2

(Press Q to exit the status view.)

4. Allow HTTP Traffic in Firewall (if necessary)

If a firewall is enabled, allow traffic on port 80 (HTTP):

sudo ufw allow 'Apache'

To check the firewall status, run:

sudo ufw status

5. Verify Apache Installation

Open your web browser and enter your EC2 instance's public IP address:

🔗 http://<Public-IP>/

If Apache is installed correctly, you should see the default Apache welcome page that says:

"Apache2 Ubuntu Default Page"