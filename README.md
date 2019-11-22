# Ansible MongoDB
[![Build Status](https://travis-ci.org/supertarto/ansible-mongodb.svg?branch=master)](https://travis-ci.org/supertarto/ansible-mongodb)

Install and configure mongodb with Ansible. This role is designed for my small need, it can be improved and don't use everything Mongodb can propose.

## Requirements
None

## Tested plateform
* Debian 9 (Stretch)
* Debian 10 (Buster)

## Role variables
Define if we use PyMongo.
```yml
mongodb_use_pymongo: true
```
Define MongoDB version and if we must hold the mongodb package. 
```yml
mongodb_version: "4.2"
mongodb_version_lock: true
```
MongoDB Admin user login, password and role.
```yml
mongo_admin_user: "admin"
mongo_admin_pass: "ChangeIT!"
mongo_admin_roles: "userAdminAnyDatabase"
```
When are the password updated (can be "on_create" or "always"). The host attached to the users.
```yml
mongodb_user_update_password: "on_create"
mongodb_login_host: "localhost"
```
MongoDB users. You can define a user name, a database name, a password et roles.
```yml
mongodb_users: []
# Exemples
#  - name: "User1"
#    database: "database1"
#    password: "ChangeIT!"
#    roles:
#      - readWrite
```
Variables used in the mongodb.conf file.
```yml
mongodb_db_path: "/var/lib/mongodb"
mongodb_journal_enabled: true
mongodb_systemlog_path: "/var/log/mongodb/mongod.log"
mongodb_systemlog_destination: "file"
mongodb_systemlog_log_append: true
mongodb_systemlog_log_rotate: "reopen"
mongodb_net_port: "27017"
mongodb_net_bind_ip: "127.0.0.1"
mongodb_security_authorization: "enabled"
```
## Examples
```yml
hosts: all
roles:
    - role: supertarto.mongodb

vars:
    mongodb_user_update_password: "on_create"
    mongo_admin_roles: userAdminAnyDatabase
    mongo_admin_pass: "ChangeIT!"
    mongo_admin_user: admin
    mongodb_security_authorization: 'enabled'

mongodb_users:
   - name: "user1"
     database: "database1"
     password: "ChangeIT!"
     roles:
       - readWrite
```
## Installation
```
ansible-galaxy install supertarto.mongodb
```
## License
GPL V3.0
