marcelocorreia.tomcat-multi
=========

Configure multiple instances of Apache Tomcat

Requirements
------------

JDK 7+
tomcat7+ installed via default apt-get 
tomcat7+ installed via default apt-get 

Role Variables
--------------

```yml
java_home: /usr/lib/jvm/java-8-oracle
tomcat_instances:
- name: auat-mock
  hostname: da-ci.auat-mock.int.products.bulletproof.net
  port: 18080
  maint_port: 18085
  Xmx: 512

- name: auat
  hostname: da-ci.auat.int.products.bulletproof.net
  port: 28080
  maint_port: 28085
  Xmx: 512

- name: uat
  hostname: da-ci.uat.int.products.bulletproof.net
  port: 38080
  maint_port: 38085
  Xmx: 512

- name: demo
  hostname: da-ci.demo.int.products.bulletproof.net
  port: 48080
  maint_port: 48085
  Xmx: 512
  
```

Example Playbook
----------------

```yml
---
- name: Install Base stuff
  hosts:
    - all
  sudo: yes
  pre_tasks:
    - name: Sets up hostname
      hostname: name="{{ inventory_hostname }}"
      sudo: yes
    - name: update apt repositories
      apt: update_cache=yes
  roles:
    - marcelocorreia.apt
    - ANXS.oracle-jdk
  tags:
    - apt
    - base
  vars_files:
    - variables.yml

- name: Configure tomcat
  hosts:
    - all
  roles:
    - ./roles/tomcat-multi
  tags:
    - tomcat
  vars_files:
    - variables.yml

```

License
-------

MIT

Author Information
------------------

Some useful stuff at:
- [https://github.com/marcelocorreia](https://github.com/marcelocorreia)
- [https://galaxy.ansible.com/list#/users/15516](https://galaxy.ansible.com/list#/users/15516)
- [https://hub.docker.com/u/marcelocorreia/](https://hub.docker.com/u/marcelocorreia/)
- Any issues, pull-request are welcome
