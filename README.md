# LAMP STACK IMPLEMENTATION IN AWS
A LAMP stack is an open-source stack that combines four services that the developers use to create powerful websites and applications. The base layer is the operating system called Linux, the layer for the web server is Apache, the database layer uses MySQL, and PHP is used as the programming language. When used properly, these four layers enable hosting, creating, and maintaining websites and web applications.

## LAMP Stack Architecture
### Linux
Linux is the operating system and the first layer of the architecture. It binds every other layer together. Linux is also an open-source operating system; it can be configured to meet the requirements of other software layers.

### Apache
Apache is used for the web server and is the second layer of the LAMP stack model. Apache uses an HTTP connection to exchange information between the browser and the web server. Apache also calls upon PHP to serve dynamic content to the web server.

### MySQL
MySQL is the third layer in our LAMP stack. MySQL is used for storing and managing information. For example, client data and product data are all stored in the relational, open-source MySQL software. When information is requested, the database is queried and served.

### PHP
Sitting on top of them all is the fourth and final layer. PHP stands for PHP: Hypertext Preprocessor, and it's a scripting language that allows you to dynamically serve content. Dynamic content is content whose values are not constant. They change depending on the circumstances of the function they are trying to accomplish. PHP is also linked to MySQL and the web server, which then is used in tandem to serve content to your browser.
* Visual Representation of the LAMP Stack
![Lamp Stack](./images/0.%20LAMP%20Stack.jpeg)

## How It Works
Whenever you open a website through a browser, the LAMP stack is triggered, and the information it processes goes through the following flow. The web application makes a request from the web browser. The LAMP stack then initiates the Apache web server and MySQL, which use PHP for their communication. 

The Apache web server first receives the request from the web browser, depending on the request (static or dynamic content) it serves it accordingly. If the request is for static content, Apache serves it immediately. However, if it is dynamic content, the PHP component then gets involved and loads the correct PHP file to process that request.

Once the correct PHP file is found, the written functions within it are then used to interpret the request and provide the necessary output. Some PHP functions also utilize the database, so a connection to MySQL is necessary. 

After the PHP function is done, the output is then relayed back to the web server in HTML format. Also, note that sometimes a new entry in the database is made. The Apache web server then serves the dynamic content to the browser.

## How To Set A LAMP Stack On AWS
### STEP 1: Launch An EC2 Instance
The following steps are taken to lauch an EC2 Instance on AWS:

* On the EC2 Dashboard, click on the **Launch Instance button** 

![Launch Instance](./images/0.%20Launch%20Instance1.png)

* Give the EC2 Instance a name of your choice and search for the preferred Virtual Server (i.e Ubuntu)

![Launch Instance2](./images/0.%20Launch%20Instance2.png)

* Select the Amazon Machine Image. Ubuntu server 22.04 was selected.

![Launch Instance3](./images/0.%20Launch%20Instance3.png)

* Create a key pair login, the key pair login was used to SSH into the instance.

![Launch Instance4](./images/0.%20Launch%20Instance4.png)

* Give the key pair a name, select the .pem format and a private key will be sent to the Downloads folder on your computer.

![Launch Instance5](./images/0.%20Launch%20Instance5.png)

* Create a security group and allow SSH traafic from Any IP address as shown below.

![Launch Intance5a](./images/0.%20Launch%20Instance5a.png)

* Click on the Launch Instance buttonn.

![Launch Instance6](./images/0.%20Launch%20Instance6.png)


### STEP 2: Connect To EC2 Using SSH

* On the EC2 Dashboard, click on the Running Insances tab.

![Launch Instance7](./images/0.%20Launch%20Instance7.png)

* Click on the Instance ID of Running Instance.

![Launch Instance8](./images/0.%20Launch%20Instance8.png)

* Click on the Connect button of Instance ID summary.

![Launch Instance9](./images/0.%20Launch%20Instance9.png)

* The highlighted commands in the image below are used to SSH into the EC2 instance.

![Launch Instance10](./images/0.%20Launch%20Instance10.png)

* On your terminal, run the following command to `cd Downloads` to go to the location of the `.pem` private key file.

* Run the code shown below to change file permissions for the .pem private key file:

```bash
sudo chmod 0400 <private-key-name>.pem
```

![SSH Instance1](./images/0.%20SSH%20Instance1.png)

* Finally, connect to the EC2 instance by running the command shown below:

```bash
ssh -i <private-key-name>.pem ubuntu@<Public-IP-address>
```

![SSH Instance2](./images/0.%20SSH%20Instance2.png)

### STEP 3: Installing Apache

* Update the list of packages in the package manager

```bash
sudo apt update
```

![apt update](./images/1.%20apt%20update.png)

* Run apache2 package installation

```bash
sudo apt install apache2
```

![apt install apache2](./images/2.%20install%20apache2.png)

* Run the systemctl status command to check if apache2 is running, if it green then apache2 is running correctly. Your first web server has been launched.

```bash
sudo systemctl status apache2
```

![systemctl status apache2](./images/3.%20systemctl%20status%20apache2.png)

### STEP 4: Updating The Firewall

Before any traffic can be received by the web server, you need to open TCP port 80 which is the default port browsers use to connect to access web pages on the internet. The following steps are taken open TCP port 80:

* Click on Security Groups on the EC2 Dashboard.

* Click on the default security group ID.

![firewall1](./images/4.%20firewall1.png)

* Click on Edit Inbound Rules.

![firewall2](./images/4.%20firewall2.png)

* Add a rule that allows HTTP (port 80) and all IPv4 addresses to connect.

![firewall3](./images/4.%20inbound%20rules.png)

Finally, the server can now be accesssed locally and from any IPv4 addres. To check if you can access the server locally in Ubuntu, run the following command:

```bash
curl http://localhost:80
```

![curl localhost](./images/4.%20curl%20localhost.png)

To check if the Apache HTTP server can respond to requests from the Internet, open your browser and run the following url:

```bash
http://<Public-IP-Address>:80
```

![http ip address](./images/6.%20http-ip%20address.png)

The public ip address can be retrieved by running the following command:

```bash
curl -s http://169.254.169.254/latest/meta-data/public-ipv4
```

![public ip address2](./images/5.%20public%20ip%20address2.png)

It can also be retrieved by clicking on the Instance ID of the Ruunning Instance ash shown below:

![public ip address1](./images/5.%20public%20ip%20address1.png)

### STEP 5: Installing MySql
