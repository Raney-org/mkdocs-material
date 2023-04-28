---
tags:
  - SALTBOX
---

# Saltbox

## Wordpress

```yaml
wordpress_docker_envs_default:
  TZ: "{{ tz }}"
  WORDPRESS_DB_HOST: "mariadb:3306" <-- edit that
  WORDPRESS_DB_USER: "root"
  WORDPRESS_DB_PASSWORD: "password321"
  WORDPRESS_DB_NAME: "{{ wordpress_name }}"
```

to install another instance of mariadb, you'd run: `#!bash sb install mariadb -e mariadb_name=mariadb2`

## Homeassistant

So this link to a [Homeassistant] tutorial is going to be super helpful I think.

  [Homeassistant]: https://sequr.be/blog/2022/09/home-assistant-container-part-3-mariadb-and-influxdb/

```yaml
##########################################################################
# Title:         Sandbox: Influxdb_web | Default Variables               #
# Author(s):     CHAIR/Raneydazed14                                      #
# URL:           https://github.com/saltyorg/Sandbox                     #
# --                                                                     #
##########################################################################
#                   GNU General Public License v3.0                      #
##########################################################################
---
################################
# Basics
################################

influxdb_web_name: influxdb_web

################################
# Paths
################################

influxdb_web_paths_folder: "{{ influxdb_web_name }}"
influxdb_web_paths_location: "{{ server_appdata_path }}/{{ influxdb_web_paths_folder }}"
influxdb_web_paths_folders_list:
  - "{{ influxdb_web_paths_location }}"

################################
# Web
################################

influxdb_web_web_subdomain: "{{ influxdb_web_name }}"
influxdb_web_web_domain: "{{ user.domain }}"
influxdb_web_web_port: "8086"
influxdb_web_web_url: "{{ 'https://' + influxdb_web_web_subdomain + '.' + influxdb_web_web_domain }}"

################################
# DNS
################################

influxdb_web_dns_record: "{{ influxdb_web_web_subdomain }}"
influxdb_web_dns_zone: "{{ influxdb_web_web_domain }}"
influxdb_web_dns_proxy: false

################################
# Traefik
################################

influxdb_web_traefik_middleware: "{{ traefik_default_middleware }}"
influxdb_web_traefik_certresolver: "{{ traefik_default_certresolver }}"
influxdb_web_traefik_enabled: true
influxdb_web_traefik_api_enabled: true
influxdb_web_traefik_api_endpoint: "`/api`,`/feed`,`/ping`"

################################
# Docker
################################

# Container
influxdb_web_docker_container: "{{ influxdb_web_name }}"

# Image
influxdb_web_docker_image_pull: true
influxdb_web_docker_image_tag: "2.7"
influxdb_web_docker_image: "influxdb:{{ influxdb_web_docker_image_tag }}"

# Ports
influxdb_web_docker_ports_defaults: []
influxdb_web_docker_ports_custom: []
influxdb_web_docker_ports: "{{ influxdb_web_docker_ports_defaults
                               + influxdb_web_docker_ports_custom }}"

# Envs
influxdb_web_docker_envs_default:
  PUID: "{{ uid }}"
  PGID: "{{ gid }}"
  TZ: "{{ tz }}"
#   INFLUXDB_DB: "homeassistant"
  INFLUXDB_ADMIN_USER: "saltman"
  INFLUXDB_ADMIN_PASSWORD: "cPwf4Kx9K7Q8"
  INFLUXDB_USER: "homeassistant"
  INFLUXDB_USER_PASSWORD: "homeassistant"

influxdb_web_docker_envs_custom: {}
influxdb_web_docker_envs: "{{ influxdb_web_docker_envs_default
                              | combine(influxdb_web_docker_envs_custom) }}"

# Commands
influxdb_web_docker_commands_default: []
influxdb_web_docker_commands_custom: []
influxdb_web_docker_commands: "{{ influxdb_web_docker_commands_default
                                  + influxdb_web_docker_commands_custom }}"

# Volumes
influxdb_web_docker_volumes_default:
  - "{{ influxdb_web_paths_location }}:/var/lib/influxdb2"
influxdb_web_docker_volumes_custom: []
influxdb_web_docker_volumes: "{{ influxdb_web_docker_volumes_default
                                 + influxdb_web_docker_volumes_custom }}"

# Devices
influxdb_web_docker_devices_default: []
influxdb_web_docker_devices_custom: []
influxdb_web_docker_devices: "{{ influxdb_web_docker_devices_default
                                 + influxdb_web_docker_devices_custom }}"

# Hosts
influxdb_web_docker_hosts_default: []
influxdb_web_docker_hosts_custom: []
influxdb_web_docker_hosts: "{{ docker_hosts_common
                               | combine(influxdb_web_docker_hosts_default)
                               | combine(influxdb_web_docker_hosts_custom) }}"

# Labels
influxdb_web_docker_labels_default: {}
influxdb_web_docker_labels_custom: {}
influxdb_web_docker_labels: "{{ docker_labels_common
                                | combine(influxdb_web_docker_labels_default)
                                | combine(influxdb_web_docker_labels_custom) }}"

# Hostname
influxdb_web_docker_hostname: "{{ influxdb_web_name }}"

# Networks
influxdb_web_docker_networks_alias: "{{ influxdb_web_name }}"
influxdb_web_docker_networks_default: []
influxdb_web_docker_networks_custom: []
influxdb_web_docker_networks: "{{ docker_networks_common
                                  + influxdb_web_docker_networks_default
                                  + influxdb_web_docker_networks_custom }}"

# Capabilities
influxdb_web_docker_capabilities_default: []
influxdb_web_docker_capabilities_custom: []
influxdb_web_docker_capabilities: "{{ influxdb_web_docker_capabilities_default
                                      + influxdb_web_docker_capabilities_custom }}"

# Security Opts
influxdb_web_docker_security_opts_default: []
influxdb_web_docker_security_opts_custom: []
influxdb_web_docker_security_opts: "{{ influxdb_web_docker_security_opts_default
                                       + influxdb_web_docker_security_opts_custom }}"

# Restart Policy
influxdb_web_docker_restart_policy: unless-stopped

# State
influxdb_web_docker_state: started
```

```yaml
#########################################################################
# Title:            Sandbox: influxdb_web                               #
# Author(s):        CHAIR/Raneydazed14                                  #
# URL:              https://github.com/saltyorg/Sandbox                 #
# --                                                                    #
#########################################################################
#                   GNU General Public License v3.0                     #
#########################################################################
---
- name: Add DNS record
  ansible.builtin.include_tasks: "{{ resources_tasks_path }}/dns/tasker.yml"
  vars:
    dns_record: "{{ lookup('vars', role_name + '_dns_record') }}"
    dns_zone: "{{ lookup('vars', role_name + '_dns_zone') }}"
    dns_proxy: "{{ lookup('vars', role_name + '_dns_proxy') }}"
- name: Remove existing Docker container
  ansible.builtin.include_tasks: "{{ resources_tasks_path }}/docker/remove_docker_container.yml"
- name: Create directories
  ansible.builtin.include_tasks: "{{ resources_tasks_path }}/directories/create_directories.yml"
- name: Create Docker container
  ansible.builtin.include_tasks: "{{ resources_tasks_path }}/docker/create_docker_container.yml"
```