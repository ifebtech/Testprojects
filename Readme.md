**Step 1: Launching an Ubuntu EC2 Instance on AWS**

**1. Log in to AWS Management Console**

-   Go to [AWS Console](https://aws.amazon.com/console/)

-   Sign in to your AWS account.

**2. Navigate to EC2 Dashboard**

-   In the AWS Management Console, search for **EC2** in the search bar.

-   Click on **EC2** to open the EC2 Dashboard.

**3. Launch a New Instance**

-   Click **Launch Instance**.

**4. Configure Instance Details**

-   **Name your instance**: (e.g., Ubuntu-Server)

-   **Choose Amazon Machine Image (AMI)**:

    -   Select **Ubuntu Server 22.04 LTS** (or any preferred version).

-   **Choose Instance Type**:

    -   Select **t2.micro** (free tier eligible).

**5. Configure Key Pair**

-   Create a new key pair or use an existing one.

-   Download and store the key securely (you will need it to connect via
    SSH).

**6. Configure Network Settings**

-   Enable **Allow SSH traffic (Port 22)**.

-   Allow **HTTP traffic (Port 80)** for web access.

**7. Configure Storage**

-   Set the storage to at least **8 GB** (default).

**8. Launch the Instance**

-   Click **Launch Instance**.

-   Wait for the instance to initialize (takes a few minutes).

------------------------------------------------------------------------

**Step 2: Connecting to the Instance via SSH**

Once your instance is running, follow these steps to connect:

**1. Get the Public IP Address**

-   Go to the **EC2 Dashboard**.

-   Click on your running instance.

-   Copy the **Public IP Address** (in your case: 54.221.78.198).

**2. Open a Terminal (or Command Prompt)**

If you\'re on **Linux or macOS**, open the Terminal.\
If you\'re on **Windows**, open **PowerShell** or use an SSH client like
PuTTY.

**3. Navigate to the Location of Your Key File**

If your .pem key file is in the **Downloads** folder, move into that
directory:

bash

CopyEdit

cd \~/Downloads

**4. Set Proper Permissions for the Key File**

Run this command to ensure the key has the correct permissions:

bash

CopyEdit

chmod 400 your-key.pem

*(Replace your-key.pem with the actual key file name.)*

**5. Connect to the EC2 Instance**

Run the following SSH command to log in to your server:

bash

CopyEdit

ssh -i your-key.pem ubuntu@54.221.78.198

*(Replace your-key.pem with the actual key file name.)*

**6. Verify Connection**

If everything is set up correctly, you should see something like this:

bash

CopyEdit

Welcome to Ubuntu 22.04 LTS (GNU/Linux 5.15.0-1036-aws x86_64)

This means you have successfully connected to your Ubuntu EC2 instance
via SSH! 🎉

------------------------------------------------------------------------

**Step 3: Installing and Configuring Apache on Ubuntu EC2**

Now that you\'re connected to your Ubuntu EC2 instance via SSH, the next
step is to install and configure Apache so it can serve web pages.

------------------------------------------------------------------------

**1. Update the Package List**

Before installing any software, it\'s a good practice to update the
package list to ensure you have the latest versions.

Run the following command:

bash

CopyEdit

*sudo apt update*

This will refresh the list of available packages and their versions.

------------------------------------------------------------------------

**2. Install Apache**

Now, install Apache by running:

bash

CopyEdit

*sudo apt install apache2 -y*

The -y flag automatically confirms the installation, so you don't have
to type \"yes\" manually.

------------------------------------------------------------------------

**3. Start and Enable Apache**

Once installed, start the Apache service and enable it to launch
automatically at system boot:

bash

CopyEdit

*sudo systemctl start apache2*

*sudo systemctl enable apache2*

To verify that Apache is running, check its status:

bash

CopyEdit

*sudo systemctl status apache2*

If Apache is running, you should see output similar to this:

bash

CopyEdit

*● apache2.service - The Apache HTTP Server*

*Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor
preset: enabled)*

*Active: active (running) since \...*

Press **Q** to exit the status view.

------------------------------------------------------------------------

**4. Allow HTTP Traffic in Firewall (if necessary)**

If you have a firewall enabled, allow traffic on port **80** (HTTP) so
the web server can be accessed:

bash

CopyEdit

*sudo ufw allow \'Apache\'*

To check the firewall status, run:

bash

CopyEdit

*sudo ufw status*

------------------------------------------------------------------------

**5. Verify Apache Installation**

To confirm that Apache is running, open your web browser and enter your
EC2 instance's **public IP address**:

🔗 **Open:** <http://54.221.78.198/>

If Apache is installed correctly, you should see the **default Apache
welcome page** that says:

**"Apache2 Ubuntu Default Page"**
