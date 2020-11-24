# Ansible MongoDB
[![CI](https://github.com/supertarto/ansible-mongodb/workflows/CI/badge.svg?event=push)](https://github.com/supertarto/ansible-mongodb/actions?query=workflow%3ACI)

Install and configure mongodb with Ansible. This role is designed for my small need, it can be improved and don't use everything Mongodb can propose. Tested only with Debian 10 and mongodb 4.2.

## Requirements
None

## Tested plateform
* Debian 10 (Buster)

## Role variables
Define MongoDB version and if we must hold the mongodb package. 
```yml
mongodb_version: "4.2"
mongodb_version_lock: true
```
MongoDB Admin user login, password and role. Only one admin is possible with this role. TODO: Adapt it to allow multiple admin/roles
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
OS specific variables. 
```yml
mongodb_repository: "deb http://repo.mongodb.org/apt/debian {{ ansible_distribution_release }}/mongodb-org/{{ mongodb_version }} main"
mongodb_apt_keyserver: keyserver.ubuntu.com
mongodb_apt_key_id: "E162F504A20CDF15827F718D4B7C549A058F8B6B"

mongodb_package: mongodb-org
mongodb_daemon_name: "mongod"
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
