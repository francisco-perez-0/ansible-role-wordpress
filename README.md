## WordPress Ansible Role
======================

This Ansible role installs and configures WordPress with Apache and PHP. It supports both Debian/Ubuntu and RedHat/Rocky Linux families. The role is designed to automate the deployment of a ready-to-use WordPress site, including web server setup, PHP installation, and directory permissions. It can be used in conjunction with the geerlingguy.mysql role for database provisioning.

Requirements
------------
- Ansible 2.9+
- Supported OS: Ubuntu, Debian, Rocky Linux, RedHat
- For database provisioning: [geerlingguy.mysql](https://galaxy.ansible.com/geerlingguy/mysql)
- (Optional) Docker and Molecule for testing

Role Variables
--------------
The following variables can be customized:

- `wordpress_php_version`: PHP version to install (default: "7.4")
- `wordpress_apache_http_port`: Apache HTTP port (default: 80)
- `wordpress_apache_server_name`: ServerName for Apache (default: "localhost")
- `wordpress_apache_log_dir`: Apache log directory (auto-detected by OS family)
- `wordpress_apache_service_name`: Apache service name (auto-detected by OS family)
- `wordpress_dir`: Directory where WordPress will be installed (required)
- `wordpress_db_name`: WordPress database name (required for wp-config.php)
- `wordpress_db_user`: WordPress database user (required for wp-config.php)
- `wordpress_db_password`: WordPress database password (required for wp-config.php)
- `wordpress_db_host`: WordPress database host (required for wp-config.php)
- `skip_wp_config`: If true, skips generating wp-config.php (default: false)

See `defaults/main.yml` and `vars/Debian.yml` or `vars/RedHat.yml` for more details.

Dependencies
------------
- [geerlingguy.mysql](https://galaxy.ansible.com/geerlingguy/mysql) (for MySQL/MariaDB setup)

Example Playbook
----------------
```yaml
- name: Install WordPress with MySQL
  hosts: all
  become: true
  vars:
    wordpress_db_name: wp_db
    wordpress_db_user: wp_user
    wordpress_db_password: wp_pass
    wordpress_db_host: localhost
    wordpress_dir: /var/www/wordpress
  roles:
    - geerlingguy.mysql
    - role: wordpress
      vars:
        wordpress_apache_server_name: mysite.local
        wordpress_apache_http_port: 80
        wordpress_php_version: "7.4"
```

License
-------
MIT

Author Information
------------------
Francisco Pérez <francisco.perez@mikroways.com>
