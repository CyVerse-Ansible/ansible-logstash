ansible-logstash
================
[![Build Status](https://travis-ci.org/CyVerse-Ansible/ansible-logstash.svg?branch=master)](https://travis-ci.org/CyVerse-Ansible/ansible-logstash)

Installs logstash on a remote host.

* TODO: Update role to update `/etc/default/logstash` with specific variables.
  * This is to allow setting some alternative CLI flags for logstash.

Requirements
------------

Ansible 2.x
Requires become.

Role Variables
--------------

|   Variable                         | required | default                 | choices | comments                                               |
|------------------------------------|----------|-------------------------|---------|--------------------------------------------------------|
| logstash_version                   |  no      | "2.3"                   |         | The version of Logstash to install |
| logstash_install                   |  no      | true                    |         | A flag used to control whether the role should perform installation steps. |
| logstash_clean_cfg_dir             |  no      | false                   |         | Determines whether the cfg dir will be cleaned prior to uploading new ones.|
| logstash_restart_on_change         |  no      | true                    |         | Determines whether the cfg dir will be cleaned prior to uploading new ones.|
| logstash_cfg_dir                   |  no      | "/etc/logstash/conf.d"  |         | Logstash's config directory. |
| logstash_cfg_templates             |  no      | "[]"                    |         | A list of paths to template and copy to the `cfg_dir`. See the ansible `template` command for details. |
| logstash_cfg_files                 |  no      | "[]"                    |         | A list of paths to copy to the `cfg_dir`. See the ansible `copy` command for details. |
| logstash_cfg_template_glob         |  no      |                         |         | Optionally specify a glob pattern to a directory containing template config files.[1] |
| logstash_cfg_file_glob             |  no      |                         |         | Optionally specify a glob pattern to a directory containing static config files.[1] |
| logstash_base_dir                  |  no      | "/opt/logstash"         |         | Logstash's install location. |
| logstash_plugins                   |  no      |                         |         | A list of objects representing logstash plugins to be installed. The `plugin` key is required, while the `version` key is optional. |
| logstash_geoip                     |  no      | false                   |         | When true, installs the GeoLiteCity GeoIP database. |

[1] - http://docs.ansible.com/ansible/playbooks_loops.html#id4

Dependencies
------------

* [cyverse.geoip](https://galaxy.ansible.com/cyverse/geoip/)

Example Playbooks
-----------------
    - hosts: systems
      vars:
      roles:
         - role: cyverse.logstash

To deploy Logstash configuration files and templates:

    - hosts: systems
      vars:
         logstash_cfg_file_glob: "/path/to/config/files/*.conf"
         logstash_cfg_template_glob: "/path/to/config/jinja/templates/*.conf"
      roles:
         - role: cyverse.logstash

Sometimes, you may want to run multiple Logstash instances, with differing configurations on the 
same host. This role does not currently automate the creation of separate services, but you can 
deploy the configuration files for separate instances by specifying a custom `conf.d` directory.

To deploy Logstash config files/templates to a different Logstash configuration directory:

    - hosts: systems
      vars:
         logstash_cfg_file_glob: "/path/to/config/files/*.conf"
         logstash_cfg_template_glob: "/path/to/config/jinja/templates/*.conf"
         logstash_cfg_dir: "/etc/logstash/alternative-dir/conf.d"
      roles:
         - role: cyverse.logstash
License
-------

BSD

Author Information
------------------

Jonathan Strootman - jstroot@cyverse.org

