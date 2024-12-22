# Second Semester Exam Documentation 

## Discription
This project demostrates how to set up an EC2 server on AWS, configure the operating system to ubuntu, install a web server, deploy an HTML landing page and configure the networking to allow HTTP traffic.

## How i provisioned the server
1. I Logged in to my AWS account.
2. Navigated to the EC2 dashboard and launched an instance using the Ubuntu 24.04 free tier.
3. I selected a t2.micro instance (free-tier eligible).
4. I created a new security group allowing SSH traffic (port 22) from anywhere for server access.
5. I used a previous private key file that i created before (test server.pem) for SSH access.
6. I connected to the instance using SSH
`ssh -i "test server.pem" ubuntu@52.55.150.34`

Where "52.55.150.34" is my public IP address

## How i set up the web server
1. I updated and upgraded the system packages
    `sudo apt update`
    `sudo apt upgrade`
2. I installed nginx
    `sudo apt install nginx`
3. I started and enabled the nginx server
    `sudo systemctl start nginx`
    `sudo systemctl enable nginx`
4. I verified the web server by checking if my ip address was accessable via browser. http://52.55.150.34

## Html page setup
1. I created a custom HTML file at /var/www/html/index.html
    `sudo vim /var/www/html/index.htm`
2. I pressed i to enable me insert text in the html file
3. I typed in the code currently in the `index.html` file.
4. I pressed the ESC key and typed :wq to exit vim.
5. I Saved and exited the editor. The page was live on http://52.55.150.34


![html page screenshot](<html page screenshot.png>)
## Configuring the sserver
1. To allow http access from anywhere, I clicked on the security tab in my aws console instance page. 
2. I clicked **Edit inbound rules** and clicked the **Add rule** button.
3. Under Type, i selected HTTP, under port range i wrote 80. For source i chose custom and selected 0.0.0.0/0. for description i wrote "Allows port connection to http request".
Then i saved the new inbound rule and refreshed my page.


## Configuring SSL using Let's Encrypt
1. I installed certbot
    `sudo apt install certbot python3-certbot-nginx`
2. I ran certbot to generate an SSL sertificate
    `sudo certbot --nginx`
3. I followed the prompt to configure https
