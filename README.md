ansible-logstash
================
[![Build Status](https://travis-ci.org/cyverse/ansible-logstash.svg?branch=master)](https://travis-ci.org/cyverse/ansible-logstash)

Installs logstash on a remote host.

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
| logstash_clean_cfg_dir             |  no      | false                     |         | Determines whether the cfg dir will be cleaned prior to uploading new ones.|
| logstash_cfg_dir                   |  no      | "/etc/logstash/conf.d"  |         | Logstash's config directory. |
| logstash_cfg_template_glob         |  no      |                         |         | Optionally specify a glob pattern to a directory containing template config files.[1] |
| logstash_cfg_file_glob             |  no      |                         |         | Optionally specify a glob pattern to a directory containing static config files.[1] |
| logstash_base_dir                  |  no      | "/opt/logstash"         |         | Logstash's install location. |
| logstash_plugins                   |  no      |                         |         | A list of objects representing logstash plugins to be installed. The `plugin` key is required, while the `version` key is optional. |
| logstash_geoip                     |  no      | false                   |         | When true, installs the GeoLiteCity GeoIP database. |

| logstash_elasticsearch_host        |  no      | "localhost:9200"        |         | The host name and port for the elasticsearch instance to forward messages to. |
| ls_conf_dir                        |  no      | "/etc/logstash/conf.d"  |         | |

[1] - http://docs.ansible.com/ansible/playbooks_loops.html#id4

Dependencies
------------

* [cyverse.geoip](https://galaxy.ansible.com/cyverse/geoip/)

License
-------

BSD

Author Information
------------------

Jonathan Strootman - jstroot@cyverse.org

