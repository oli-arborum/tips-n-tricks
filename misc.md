Miscellaneous
=============

## Zabbix with docker-compose ##

Use docker-compose file ``docker-compose_v3_alpine_mysql_latest.yaml`` from https://github.com/zabbix/zabbix-docker

Remove all containers except for ``zabbix-server``, ``zabbix-web-nginx-mysql``, ``mysql-server``, ``zabbix-agent``, ``db_data_mysql``.

Specifying a profile is necessary for ``zabbix-agent`` to launch:

    docker-compose --profile full up -d

Adjustments based on <https://mpolinowski.github.io/devnotes/2020-07-15--zabbix-docker-installation>:
* Enter name of agent "``zabbix-agent``" in GUI (Host > Zabbix server > Configuration > Agent > DNS Name), switch to "Connect to DNS" and click "Update"
* execute ``zabbix_server -R config_cache_reload`` in ``zabbix-server`` container

**NOTE:** Do not use the IP address of the ``zabbix-agent`` container as it does not survive a restart of container!
