PostgreSQL is one of the most popular opensource databases, and is very similar to Oracle database.\
The way to manage database infrastructure in the production environment [LINK] is with automation tools like Terraform, Ansible, etc. \
But for development environment, a CentOS server is used. Here is the how to guide for a development environment of PostgreSQL on CentOS Stream 9:

## installation

initializing a database
```
sudo postgresql-setup --initdb --unit postgresql
```
start and enable database
```
sudo systemctl start postgresql
sudo systemctl enable postgresql
```
setup password for default user "postgres", and then login as "postgres":
```
sudo passwd postgres
sudo su - postgres
```
## configuration
edit the config file for local access:
```
sudo vi /var/lib/pgsql/data/pg_hba.conf
```
edit the config file to set port and listening address:
```
sudo vi /var/lib/pgsql/data/postgresql.conf
```
uncomment the following:
```
port = 5432
listen_adresses = '*'
```
restart for the config changes to take effect:
```
sudo systemctl restart postgresql
```
additional configuration for memory management, logging, and firewall rules can be done.
## usage
access SQL environment:
```
psql
```
create and config a new user "devops":
```
CREATE DATABES new_database;
CREATE USER devops WITH PASSWORD 'new_password';
GRANT ALL PRIVILEDGES ON DATABASE new_database TO devops;
```
