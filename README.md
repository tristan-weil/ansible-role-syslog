# Ansible Role: syslog

An Ansible Role that installs and configures a syslog service.

**NOTE**: only common parameters for both `syslog-ng` (Linux) and `syslog` (OpenBSD) are available.
The objective of this role is to stay simple.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    syslog_config_name: [mandatory]                 # the name of the configuration
    syslog_config_state: present                    # present|absent
       
    syslog_destination_log_path: [mandatory]         # the path of the log file
    syslog_destination_user: [mandatory]            # the owner of the log file
    syslog_destination_group: [mandatory]           # the group of the log file
    syslog_destination_mode: [mandatory]            # the mode of the log file

    syslog_facility: [mandatory]                    # the syslog facility
    syslog_level: [mandatory]                       # the syslog level
    syslog_program_name: [mandatory]                # the tag/process name

The variables to configure the syslog behaviour.

## Dependencies

None.

## Example Playbook

    - hosts: webservers
      roles:
        - role: t18s.fr_syslog

## Todo

Make it available for OpenBSD.

## License

```
Copyright (c) 2018 Tristan Weil <titou@lab.t18s.fr>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
