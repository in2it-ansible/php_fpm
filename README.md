PHP FPM
=======

[![Build Status](https://travis-ci.org/in2it-ansible/php_fpm.svg?branch=master)](https://travis-ci.org/in2it-ansible/php_fpm)

A stand-alone PHP-FPM server running on Debian 9 ("Stretch") that will listen on a port instead of a socket.

Requirements
------------

No specific requirements necessary

Role Variables
--------------

These are the variables defined in `defaults/main.yml` which can be overridden in `vars/main.yml`:

- **php_timezone:** Sets the system timezone (default: UTC)
- **php_apt_list:** The APT repository for PHP (default: "deb https://packages.sury.org/php/ {{ ansible_lsb.codename }} main")
- **php_apt_keyid:** The GPG Key ID for the APT repository (default: AC0E47584A7A714D)
- **php_apt_key:** The location of the APT GPG key for this APT repo (default: https://packages.sury.org/php/apt.gpg)
- **php_version:** The PHP version you want to use (default: 7.3)
- **php_app_path:** The location where your PHP files are kept (default: /var/www/app)
- **php_fpm_port:** The port PHP-FPM listens on (default: 9000)
- **php_log_level:** The log level you want to have (default: warn)
- **package:** A list of PHP packages you want to install (default: most common ones)

The following variables are used in `templates/php_fpm.conf`:

- **ansible_host:** The hostname or IP address of the hosts used for the web server (see Example Inventory)

Dependencies
------------

No known dependencies

Example Inventory
-----------------

    [all]
    php ansible_host=192.168.1.1
    
    [php]
    php

Example Playbook
----------------

    - name: Provision boxes
      hosts: all
      become: true
      roles:
        - { role: all, tags: [ 'common', 'all' ] }
        
    - name: Set up the PHP server
      hosts: php
      become: true
      roles:
        - { role: php-fpm, tags: [ 'php', 'fpm', 'web' ] }

License
-------

MIT

Author Information
------------------

Michelangelo van Dam (michelangelo+github@in2it.be)
