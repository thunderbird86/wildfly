Wildfly
=======

This role installs Wildfly's application runtime.

Role Variables
--------------

It's important to change the bind addresses to localhost or internal network in
production environments. The management user is also intended for
non-production environments, so you must change these variables for production
or undefine them and the user creation task will be skipped. You can also set
the variable `wildfly_management_user_overwrite` to `no` to avoid the user
creation or override and have the correct change status.

Defaults:

    
        wildfly_manage_standalone_data: true
        wildfly_manage_service: true
        wildfly_remove_download_file: true

        wildfly_version: "8.2.1.Final"

        wildfly_user: wildfly
        wildfly_group: wildfly

        wildfly_base_download_url: http://download.jboss.org/wildfly
        wildfly_name: wildfly-{{ wildfly_version }}
        wildfly_download_file: "{{ wildfly_name }}.tar.gz"
        wildfly_download_url: "{{ wildfly_base_download_url }}/{{ wildfly_version }}/\
                               {{ wildfly_download_file }}"
        wildfly_download_dir: /tmp

        wildfly_install_dir: /opt
        wildfly_dir: "{{ wildfly_install_dir }}/{{ wildfly_name }}"
        wildfly_create_symlink: true

        wildfly_console_log_dir: "/var/log/wildfly"
        wildfly_console_log_file: "console.log"
        wildfly_console_log: "{{ wildfly_console_log_dir }}/\
                              {{ wildfly_console_log_file }}"

        wildfly_conf_dir: /etc/wildfly
        wildfly_standalone_config_file: standalone-full-ha.xml
        wildfly_standalone_config_path: "{{ wildfly_dir }}/standalone/configuration/\
                                         {{ wildfly_standalone_config_file }}"
        wildfly_startup_wait: ''
        wildfly_shutdown_wait: ''

        wildfly_node_name: ''
        wildfly_init_dir: /etc/init.d
        wildfly_systemd_dir: /usr/lib/systemd/system

        wildfly_bind_address: 0.0.0.0
        wildfly_management_bind_address: 0.0.0.0
        wildfly_manage_http_port: 9990
        wildfly_manage_https_port: 9993
        wildfly_http_port: 8080
        wildfly_https_port: 8443
        wildfly_bind_address_unsecure: ''
        wildfly_messaging_group_address: ''

        wildfly_management_users: []

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: thunderbird86.wildfly }

Admin User
----------

It's recommended that you create Wildfly's admin user separately as follows:

    $ ansible-playbook main.yml --extra-vars "wildfly_management_user=admin wildfly_management_password=admin"

License
-------

BSD
