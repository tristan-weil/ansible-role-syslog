# Ansible Role: syslog

An Ansible Role that installs and configures a syslog service.

[![Actions Status](https://github.com/tristan-weil/ansible-role-syslog/workflows/molecule/badge.svg?branch=master)](https://github.com/tristan-weil/ansible-role-syslog/actions)

## Role Variables

Available variables are listed below, (see also `defaults/main.yml`).

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| syslog_service_options | [] | a list of <*service option*> |
| syslog_sources | [] | a list of <*source*>, defined globally |
| syslog_destinations | [] | a list of <*destination*>, defined globally |
| syslog_configs_list | [] | a list of <*configuration*>|

### <*service option*>

A *service option* represents a parameter used to the launch of the service.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

### <*source*>

A *source* represents the configuration of a syslog source used to receive logs.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| name          | the name of this configuration |
| drivers       | a list of <*network driver*> or <*unix-dgram driver*> |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

### <*destination*>

A *destination* represents the configuration of a syslog destination used to send logs.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| name          | the name of this configuration |
| drivers       | a list of <*network driver*> or <*file driver*> |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

### <*configuration*>

A *configuration* represents the configuration of a syslog entry.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| name          | the name of this configuration |
| sources       | a list of <*source*>, defined locally |
| destinations  | a list of <*destination*>, defined locally |
| filters       | a list of <*filter*>, defined locally |
| logs          | a list of <*log*>, defined locally |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

#### <*filter*>

A *filter* configures how to filter the log.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| name          | the name of this filter |
| program       | a list of program name to filter |
| facilities    | a list of facilities to listen on |
| levels        | a list of levels to listen on |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

#### <*log*>

A *log* configures how to handle the log.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| sources       | a list of sources' names (they must refer to existing sources) |
| filters       | a list of filters' names (they must refer to existing filters) |
| destinations  | a list of destinations' names (they must refer to existing destinations) |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

#### <*network driver*>

A *network driver* represents a type of source or destination.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| type          | *network*: the type of the driver |
| protocol      | *tcp / udp*: the protocol |
| hostname      | the hostname or IP to send to or receive from |
| port          | the port to listen on |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| ip_version    | 4       | *4 / 6*: the IP protocol version |

#### <*file driver*>

A *file driver* represents a type of source or destination.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| type          | *file*: the type of the driver |
| log_path      | the path of the file

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |
| log_user      | root    | the owner
| log_group     | adm / wheel | the group
| log_mode      | 0600    | the mode
| dir_user      | root    | the owner
| dir_group     | adm / wheel | the group
| dir_mode      | 0700    | the mode

#### <*unix-dgram driver*>

A *network driver* represents a type of source or destination.

Mandatory variables:

| Variable      | Description |
| :------------ | :---------- |
| type          | *unix-dram*: the type of the driver |
| devlog        | the path of the device |

Optional variables:

| Variable      | Default | Description |
| :------------ | :------ | :---------- |

## Example Playbook

    - hosts: 'webservers'
      role: 'syslog'
      syslog_sources:
        - name: 'mynet'
          drivers:
            - type: 'network'
              protocol: 'udp'
              hostname: '127.0.0.1'
              port: 514

      syslog_configs_list:
        - name: 'testinfra1'

          filters:
            - name: 'testinfra_default'
              program:
                - 'testinfra'
              facilities:
                - '*'
              levels:
                - 'notice'

          destinations:
            - name: 'testinfra_default'
              drivers:
                - type: 'file'
                  log_path: '/var/log/testinfra/testinfra.log'
                  log_user: 'testinfra'
                  log_group: 'testinfra'
                  log_mode: '0640'
                  dir_user: 'testinfra'
                  dir_group: 'testinfra'
                  dir_mode: '0750'

          logs:
            - sources:
                - 'src'
                - 'mynet'
              filters:
                - 'testinfra_default'
              destinations:
                - 'testinfra_default'

## Todo

None.

## Dependencies

See [requirements_galaxy.yml](https://github.com/tristan-weil/ansible-role-consul/blob/master/requirements_galaxy.yml)

## Supported platforms

See [meta/main.yml](https://github.com/tristan-weil/ansible-role-consul/blob/master/meta/main.yml)

## License

See [LICENSE.md](LICENSE.md)
