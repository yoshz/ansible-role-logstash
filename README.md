# Ansible Role: Logstash

An Ansible Role that installs Logstash on Debian/Ubuntu.

## Role Variables

Example:

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

## Example Playbook

    - hosts: search
      roles:
        - { role: logstash }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
