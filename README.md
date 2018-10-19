mage-rpi-zabbix-proxy
=====================

Install and configure zabbix proxy on Raspberry Pi. Reuires *dj-wasabi.zabbix-proxy* role.

This role uses sqlite3 database stored in tmpfs drive to prolong the life of SD card. After reboot the database is automatically restored.


Role Variables
--------------
Variables and its default values
```
# mountpoint for tmpfs filesystem
mage_zabbix_db_folder: /opt/zabbixdb
# file name of zabbix database
mage_zabbix_db_file_name: zabbix.db
# size of tmpfs
mage_zabbix_folder_size: 256m
```
Dependencies
------------

[dj-wasabi.zabbix-proxy](https://galaxy.ansible.com/dj-wasabi/zabbix-proxy)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- hosts: proxy
  roles:
    - role: vaizard.mage-rpi-zabbix-proxy
    - role: dj-wasabi.zabbix-proxy
      become: true
      zabbix_server_host: my.server.cz
      zabbix_version: 4.0

      zabbix_proxy_mode: 0

      zabbix_database_creation: True
      zabbix_database_sqlload: False
      zabbix_proxy_database_long: sqlite3
      zabbix_proxy_database: sqlite3
      zabbix_proxy_dbname: "{{ mage_zabbix_db_folder }}/{{ mage_zabbix_db_file_name }}"

      zabbix_proxy_hostname: proxy1.server.cz
      zabbix_proxy_logfile: "{{ mage_zabbix_db_folder }}/zabbix_proxy.log"
      
      zabbix_proxy_configfrequency: 1800
```

License
-------

MIT