# MySQL
MySQL is a popular SQL database. \
Its opensource community version is MariaDB which is reviewd here for a development environment.
Link to MySQL on AWS (production)
## install on premise
```
ansible-galaxy role install geerlingguy.mysql
```
or you can install and configure step by step:
```
sudo yum update -y
sudo yum install mariadb* -y
```
enable and start the database:
```
sudo systemctl enable mariadb
sudo systemctl start mariadb
```
## configuration
configure firewalld and secure installation if needed:
```
firewall-cmd --permanent --add-port=3306/tcp
firewall-cmd --reload

sudo mysql_secure_installation
```
```
mysql -u root -p
```

```
CREATE DATABASE dbname;
CREATE USER 'dbuser'@'%' IDENTIFIED BY 'dbpassword'; (or @'localhost')
GRANT ALL PRIVILEGES ON dbname.* TO 'dbuser'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
The above info is for an infrastructure context only, and is not meant to be a complete DBA guide.
