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


## TrueNAS - Migrate data from other NAS via SMB and rsync ##

Copying data via SMB/CIFS requires some workarounds to have all files readable.

Mounting via SMB is done in FreeBSD with ``mount_smbfs``:

    mount_smbfs //myuser@myoldnas/share /mnt/myoldnas
   
**NOTE:** Don't do this, read until the end first!

My first mistake was to just use ``cp`` to copy the files. They now had the current time as creation timestamp, which is most probably not desired. In FreeBSD there is no --preserve option where you can specify which attributes to preserve but only a -p option to preserve all.
So instead using ``cp`` we use ``rsync`` to preserve creation timestamps only:

    rsync ...

However, if file or folder names contain non-ASCII characters ("gelöscht"), these characters are displayed as "?" on the console and the file or folder isn't visible via SMB at all. To fix this, the ``-E`` option of ``mount_smbfs`` needs to be used:

    mount_smbfs -E utf8:utf8 //myuser@myoldnas/share /mnt/myoldnas

Now all files and directories -- also those containing non-ASCII characters -- should be copied with ``rsync`` and also visible when connecting to TrueNAS via SMB.
