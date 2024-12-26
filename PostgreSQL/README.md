# PostgreSQL
PostgreSQL is one of the most popular opensource databases, and is very similar to Oracle database.\
The way to manage database infrastructure in the production environment is with automation tools like Terraform, Ansible, etc. \
Link to Postgres on AWS (production)

But for development environment, a CentOS server is used. \
Here is the how to guide for a development environment of PostgreSQL on CentOS Stream 9:

## installation on premise
install Ansible, and then install Postgres with an Ansible role:
```
ansible-galaxy role install geerlingguy.postgresql
```
## note:
alternatively, it can be installed manually steb by step e.g. on CentOS
```
sudo yum update
sudo yum install postgresql-server postgresql-contrib
```
initialize the database
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

The above info is for an infrastructure context only. Here is a [DBA guide](https://roadmap.sh/postgresql-dba) though.
