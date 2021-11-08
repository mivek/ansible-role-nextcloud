Nextcloud
=========

This role installs and configures [Nextcloud](https://nextcloud.com/) on a server. This role does not install dependencies.

Requirements
------------

Nextcloud requires:
- a database: MYSQL, MariaDB, PostgreSQL or SQLite
- a webserver: Apache or Nginx with php-fpm module.
- PHP runtime

A full list of requirements is listed [here](https://docs.nextcloud.com/server/latest/admin_manual/installation/system_requirements.html). 
The list of required PHP modules is available [here](https://docs.nextcloud.com/server/latest/admin_manual/installation/source_installation.html).


Role Variables
--------------
|Name| Default value|Type|Meaning|
|----|----|-----|-------|
|nextcloud_version| 22.2.0| String| The version of nextcloud to install.
|nextcloud_webserver_user| www-data | string | The webserver user this user must have access to the php command.
|nextcloud_webserver_group| www-data | string | The webserver group this group must have access to the php command.
|nextcloud_server_location| /var/www | path | The path of the nextcloud server, the archive will be unarchived in this directory.
|nextcloud_data_directory| /opt/nextcloud/data | path | This directory will hold nextcloud data files and logs.
|nextcloud_settings | [] | List of objects | List of settings for nextcloud. A setting is composed of a name, a value and type. Default type is string.
|nextcloud_apps| []| List | List of application to install on nextcloud.
|nextcloud_trusted_domains| ['localhost'] | List | List of trusted domains to set.
|nextcloud_redis| |object|Parameters to connect to a redis server. The available keys are `host`, `port`, `dbindex`, `password` and `timeout`. See [nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/caching_configuration.html#id2)
|nextcloud_server_web|nginx| string | The webserver nextcloud will ran on. The web server will not be installed.
|nextcloud_server_http_server_name| | string | The domain name nextcloud can be reached. It should also be in the nextcloud_trusted_domains list.
|nextcloud_server_http_use_https| true | boolean | Whether https should be configured and forced.
|nextcloud_server_http_certificate| | path | The path to the certificate
|nextcloud_server_http_certificate_key| | path | The path to the certificate key
|nextcloud_nginx_template| nginx.conf.j2 | path | When the nextcloud_server_web is nginx, the path to the nginx template to use.
|nextcloud_nginx_configuration| /etc/nginx/conf.d/nextcloud.conf | path | The path where the nextcloud nginx configuration should be deployed.
|nextcloud_database |  | Object | Object to represent the database. The accepted keys are `type`, `host`, `name`, `user` and password. The accepted values for the type are: mysql, pgsql, sqlite and oci
|nextcloud_admin| | string | Name of the admin of the nextcloud server
|nextcloud_admin_password| | string | Password of the admin of the nextcloud server
|nextcloud_apps_settings| [] | List of objects | List of settings for nextcloud applications. A setting is compose of the `app_name`, the `setting_name`, the `value` and the `type`.
|nextcloud_php_executable| php | string | The PHP executable to use when running commands.
|nextcloud_backup_directory|  | path | Path of the directory that will store backups.
|nextcloud_backup_cron|  | Object | Object to configure the backup script cron. The keys are `minute`, `hour`, `day`, `month` and `weekday`.

Dependencies
------------

None.

Example Playbook
----------------

A complete example of a full installation with a webserver and a database is available in the [molecule](/molecule/default) directory.
It installs nginx, PHP, PostgreSQL and redis before running the role.
A valid inventory is available [here](molecule/default/inventory/host_vars/instance.yml)

License
-------

BSD

Author Information
------------------

[GitHub](https://github.com/mivek)
