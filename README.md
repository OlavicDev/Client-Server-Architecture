# Client-Server-Architecture
## Understanding Client-Server Architecture

Computers connected to the internet operate as clients and servers. Clients are internet-connected devices like computers and phones, using web browsers (e.g., Firefox, Chrome) to access web content. Servers are computers that host webpages, sites, or apps, delivering content to clients upon request.

This setup exemplifies a typical web stack architecture, implemented in various technologies (LAMP, LEMP, MEAN, MERN) for projects ranging from single-page applications to complex portals.
![image](https://github.com/user-attachments/assets/16b72912-e40e-4a76-8489-fb755793e47c)


### Client-Server Architecture in Action

To see client-server architecture in action, use the `curl` command in your terminal:

```
curl -Iv steghub.com
```

In this example, your terminal acts as the client, and steghub.com is the server. The server's IP address is 160.153.133.153 on port 80. You can also use the `ping` command to get the server's IP address and round-trip time, using the ICMP protocol.

### Implementing a Client-Server Architecture with MySQL DBMS

![image](https://github.com/user-attachments/assets/e4c37c58-1dec-4987-be6e-7fb1a2997157)


To demonstrate a basic client-server setup using MySQL RDBMS, follow these steps:

**Creating and Configuring Two Linux-Based Virtual Servers (EC2 Instances in AWS)**

#### Setting up the 'MySQL Server'

1. **Launch an EC2 Instance:**
   - Sign in to the AWS Management Console.
   - Navigate to the EC2 Dashboard.
   - Click "Launch Instance" and choose Ubuntu Server 20.04 LTS.

2. **Configure Instance Details:**
   - Select instance type, network, subnet, and other settings.

3. **Add Storage:**
   - Allocate storage as needed.

4. **Add Tags:**
   - Optionally, add tags for organization.

5. **Configure Security Group:**
   - Allow inbound traffic on ports 80 (HTTP), 22 (SSH), 3306 (MySQL), and 443 (HTTPS) from your IP address.

6. **Review and Launch:**
   - Review the configuration and launch the instance.

#### Setting up the 'MySQL Client'

1. **Launch an EC2 Instance:**
   - Follow the same steps as setting up the 'MySQL Server.'

2. **Configure Security Group:**
   - Allow inbound traffic on ports 80 (HTTP), 22 (SSH), and 443 (HTTPS) from your IP address.

3. **Review and Launch:**
   - Review the configuration and launch the instance.

### Connecting to the MySQL Server

1. **SSH into the MySQL Server:**

   ```
   ssh -i steghub.pem ubuntu@18.208.161.17
   ```

2. **Update Package Repository:**

   ```
   sudo apt update
   sudo apt upgrade
   ```

3. **Install MySQL Server:**

   ```
   sudo apt install mysql-server -y
   ```
![image](https://github.com/user-attachments/assets/729480c0-42be-4cf2-b03f-751be36862c2)


### Connecting to the MySQL Client

1. **SSH into the MySQL Client:**

   ```
   ssh -i steghub.pem ubuntu@54.219.50.131
   ```
   ![image](https://github.com/user-attachments/assets/8f47fd38-11ec-4669-a093-a3b2e86e830a)


2. **Update Package Repository:**

   ```
   sudo apt update
   sudo apt upgrade
   ```

3. **Install MySQL Client:**

   ```
   sudo apt install mysql-client -y
   ```
   ![image](https://github.com/user-attachments/assets/0955f89e-9df8-4710-ae44-697db66cce45)


### Configuring MySQL Server

1. **Allow Remote Connections:**

   ```
   sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
   ```

   Replace `bind-address = 127.0.0.1` with `0.0.0.0`.
   ![image](https://github.com/user-attachments/assets/e1084c00-4100-4dd2-ad9a-02cdae1bcd6b)
   


3. **Access MySQL Shell:**

   ```
   sudo mysql
   ```

4. **Create a User and Database:**

   ```
   CREATE USER 'client'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
   CREATE DATABASE test_db;
   GRANT ALL ON test_db.* TO 'client'@'%' WITH GRANT OPTION;
   FLUSH PRIVILEGES;
   ```
   ![image](https://github.com/user-attachments/assets/dbf17e2b-5393-402e-9fe7-fb5d21d836fb)


5. **Connect to MySQL Server from Client:**

   ```
   sudo mysql -u client -h 18.208.161.17 -p
   ```

6. **Verify Connection:**

   ```
   SHOW DATABASES;
   ```
   ![Uploading image.png…]()


By following these steps, you will have successfully set up a fully functional MySQL Client-Server architecture.
