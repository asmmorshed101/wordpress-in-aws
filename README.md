# wordpress-in-aws
Here is some commands for hosting a WordPress website in AWS Cloud

Install PHP in EC2 Instance

<pre>
sudo dnf install -y php php-cli php-common php-mysqlnd php-fpm php-mbstring php-pdo php-gd
</pre>

Now Check the Version of PHP to confirm it actually installed

<pre>
php -v
</pre>

Install mysql/mariadb

<pre>
sudo dnf install mariadb105
</pre>

Checking version

<pre>
mysql --version
</pre>

Now Connect with your Database from EC2 instance

<pre>
mysql -h dbendpoint -u admin -p
</pre>

Change the dbendpoint to your DNS endpoint

Now Install wordpress: Download wordpress from here

<pre>
wget https://wordpress.org/latest.tar.gz
</pre>

Now unzip the file

<pre>
tar -xzf filename
</pre>

Now Copy all the file from here to html folder

<pre>
sudo cp -r wordpress/* /var/www/html/
</pre>

Now we need to change the ownership. changes the ownership of the /var/www directory and all its contents to the user ec2-user and the group apache. This is typically done so that the ec2-user can:
Read/write files owned by Apache (/var/www/html).
Collaborate with Apache for web development or deployments.

<pre>
sudo usermod -a -G apache ec2-user
</pre>

The following command is typically used in web server environments to ensure proper permissions for web server processes and users, facilitating collaboration and proper access control.
This command is used to set up a shared web directory where users in the same group (like ec2-user and apache) can collaborate with proper read/write/execute permissions, and new files inherit the group's ownership.

<pre>
sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
</pre>

This command sets file permissions so that the owner and group can read/write, and others can only read, which is ideal for shared web projects like WordPress or Laravel.

<pre>
find /var/www -type f -exec sudo chmod 0664 {} \;
</pre>

Now change the directory and need to be in html file

<pre>
cd /var/www/html
</pre>

Copy the file 

<pre>
cp wp-config-sample.php wp-config.php
</pre>

Here change the hostname, database name, user and password.

Then open this file by the following command

<pre>
sudo vim /etc/httpd/conf/httpd.conf
</pre>

Find out the below code and change None to All

<pre>
  <Directory "/var/www">
    AllowOverride All
    # Allow open access:
    Require all granted
</Directory>
</pre>
Now restart the apache server
<pre>
sudo systemctl restart httpd
</pre>

Now copy the IP address on the EC2 instance and paste on browser. Here you can configure your WordPress Website.

Thank you





