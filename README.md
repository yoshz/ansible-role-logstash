logstash
========

An Ansible Role for configuring Logstash on Debian/Ubuntu.


Requirements:
-------------

None.


Role Variables
--------------

Example configuration:

    logstash_config:
      input:
        syslog: |
          file {
            type => "syslog"
            path => [ "/var/log/syslog" ]
          }
      output:
        redis: |
          redis {
            host => "127.0.0.1"
            data_type => "list"
            key => "logstash"
          }
      filter:
        syslog: |
          multiline {
            type => "syslog"
            pattern => "\t"
            what => "previous"
            add_tag => [ "multilined" ]
          }


Example Playbook:

    - hosts: search
      roles:
        - { role: logstash }


License
-------

MIT
