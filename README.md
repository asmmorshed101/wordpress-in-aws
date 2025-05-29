# wordpress-in-aws
Here is some commands for hosting a WordPress website in AWS Cloud

Install PHP in EC2 Instance

```bash
sudo dnf install -y php php-cli php-common php-mysqlnd php-fpm php-mbstring php-pdo php-gd
```

Now Check the Version of PHP to confirm it actually installed

```bash
php -v
```

Install mysql/mariadb

```bash
sudo dnf install mariadb105
```

Checking version

```bash
mysql --version
```

Now Connect with your Database from EC2 instance

```bash
mysql -h dbendpoint -u admin -p
```

Change the dbendpoint to your DNS endpoint

Now Install wordpress: Download wordpress from here

```bash
wget https://wordpress.org/latest.tar.gz
```

Now unzip the file

```bash
tar -xzf filename
```

Now Copy all the file from here to html folder

```bash
sudo cp -r wordpress/* /var/www/html/
```

Now we need to change the ownership. changes the ownership of the /var/www directory and all its contents to the user ec2-user and the group apache. This is typically done so that the ec2-user can:
Read/write files owned by Apache (/var/www/html).
Collaborate with Apache for web development or deployments.

```bash
sudo usermod -a -G apache ec2-user
```

The following command is typically used in web server environments to ensure proper permissions for web server processes and users, facilitating collaboration and proper access control.
This command is used to set up a shared web directory where users in the same group (like ec2-user and apache) can collaborate with proper read/write/execute permissions, and new files inherit the group's ownership.

```bash
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
```

This command sets file permissions so that the owner and group can read/write, and others can only read, which is ideal for shared web projects like WordPress or Laravel.

```bash
find /var/www -type f -exec sudo chmod 0664 {} \;
```

Now change the directory and need to be in html file

```bash
cd /var/www/html
```

Copy the file 

```bash
cp wp-config-sample.php wp-config.php
```

Here change the hostname, database name, user and password.

Then open this file by the following command

```bash
sudo vim /etc/httpd/conf/httpd.conf
```

Find out the below code and change None to All

```bash
  <Directory "/var/www">
    AllowOverride All
    # Allow open access:
    Require all granted
</Directory>
```
Now restart the apache server
```bash
sudo systemctl restart httpd
```

Now copy the IP address on the EC2 instance and paste on browser. Here you can configure your WordPress Website.

Thank you





