mage-rpi-zabbix-proxy
=====================

[![Build Status](https://travis-ci.org/vaizard/mage-rpi-zabbix-proxy.svg?branch=master)](https://travis-ci.org/vaizard/mage-rpi-zabbix-proxy)

Install and configure Zabbix proxy on Raspberry Pi.

This role uses sqlite3 database stored in tmpfs drive to prolong the life of SD card. After reboot the database is automatically restored.

**...to update configuration file** set `mage_zabbix_conf_overwrite` to **true**

Role Variables
--------------
Variables and its default values
```
# latest release file from https://www.zabbix.com/download
mage_zabbix_debfile: zabbix-release_4.0-2+stretch_all.deb

# set this to true to overwrite existing proxy conf file
mage_zabbix_conf_overwrite: false
# set this to true to overwrite existing database
mage_zabbix_db_overwrite: false

# mountpoint for tmpfs filesystem
mage_zabbix_db_folder: /opt/zabbixdb
# file name of zabbix database
mage_zabbix_db_file_name: zabbix.db
# size of tmpfs volume
mage_zabbix_folder_size: 256m

# proxy settings
mage_zabbix_mode: 0
mage_zabbix_server_hostname: my.server.cz
mage_zabbix_server_port: 10051
mage_zabbix_hostname: proxy.xyz
mage_zabbix_trapper_port: 10051
mage_zabbix_pidfile: /var/run/zabbix/zabbix_proxy.pid

# logs
mage_zabbix_log_file: /opt/zabbixdb/zabbix.log
mage_zabbix_log_file_size: 10
mage_zabbix_log_level: 3

# database
mage_zabbix_db_host: localhost
mage_zabbix_db: "{{ mage_zabbix_db_folder }}/{{ mage_zabbix_db_file_name }}"

# data buffering
mage_zabbix_data_buffer_time: 6
mage_zabbix_data_buffer_time_outage: 72

mage_zabbix_heartbeat: 60
mage_zabbix_configfrequency: 1800
mage_zabbix_sendfrequency: 45

# fping location
mage_zabbix_fping: /usr/bin/fping
mage_zabbix_fping_6: /usr/bin/fping6

# TLS settings
# TODO

mage_zabbix_libdir: /usr/lib/zabbix
mage_zabbix_moduledir: "{{ mage_zabbix_libdir }}/modules"


```
Dependencies
------------

none

Example Playbook
----------------

```
- hosts: testvag
  roles:
    - role: vaizard.mage_rpi_zabbix_proxy
      mage_zabbix_conf_overwrite: true
      mage_zabbix_server_hostname: myserver.cz
      mage_zabbix_hostname: myproxy.home.cz
```

TODO
----

- [ ] Allow every option in conf file to be configured
- [ ] Finish all TLS settings (now only PSK is available)
- [ ] Write tests
- [ ] ???


License
-------

MIT