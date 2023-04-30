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
# Title:         Sandbox: influxdb2 | Default Variables               #
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

influxdb2_name: influxdb2

################################
# Paths
################################

influxdb2_paths_folder: "{{ influxdb2_name }}"
influxdb2_paths_location: "{{ server_appdata_path }}/{{ influxdb2_paths_folder }}"
influxdb2_paths_folders_list:
  - "{{ influxdb2_paths_location }}"

################################
# Web
################################

influxdb2_web_subdomain: "{{ influxdb2_name }}"
influxdb2_web_domain: "{{ user.domain }}"
influxdb2_web_port: "8086"
influxdb2_web_url: "{{ 'https://' + influxdb2_web_subdomain + '.' + influxdb2_web_domain }}"

################################
# DNS
################################

influxdb2_dns_record: "{{ influxdb2_web_subdomain }}"
influxdb2_dns_zone: "{{ influxdb2_web_domain }}"
influxdb2_dns_proxy: "{{ dns.proxied }}"

################################
# Traefik
################################

influxdb2_traefik_middleware: "{{ traefik_default_middleware }}"
influxdb2_traefik_certresolver: "{{ traefik_default_certresolver }}"
influxdb2_traefik_enabled: true
influxdb2_traefik_api_enabled: true
influxdb2_traefik_api_endpoint: "`/api`,`/feed`,`/ping`"

################################
# Docker
################################

# Container
influxdb2_docker_container: "{{ influxdb2_name }}"

# Image
influxdb2_docker_image_pull: true
influxdb2_docker_image_tag: "2.7"
influxdb2_docker_image: "influxdb:{{ influxdb2_docker_image_tag }}"

# Ports
influxdb2_docker_ports_defaults: []
influxdb2_docker_ports_custom: []
influxdb2_docker_ports: "{{ influxdb2_docker_ports_defaults
                            + influxdb2_docker_ports_custom }}"

# Envs
influxdb2_docker_envs_default:
  PUID: "{{ uid }}"
  PGID: "{{ gid }}"
  TZ: "{{ tz }}"
#   INFLUXDB_DB: "homeassistant"
  INFLUXDB_ADMIN_USER: "saltman"
  INFLUXDB_ADMIN_PASSWORD: "cPwf4Kx9K7Q8"
  INFLUXDB_USER: "homeassistant"
  INFLUXDB_USER_PASSWORD: "homeassistant"

influxdb2_docker_envs_custom: {}
influxdb2_docker_envs: "{{ influxdb2_docker_envs_default
                           | combine(influxdb2_docker_envs_custom) }}"

# Commands
influxdb2_docker_commands_default: []
influxdb2_docker_commands_custom: []
influxdb2_docker_commands: "{{ influxdb2_docker_commands_default
                               + influxdb2_docker_commands_custom }}"

# Volumes
influxdb2_docker_volumes_default:
  - "{{ influxdb2_paths_location }}:/var/lib/influxdb2"
influxdb2_docker_volumes_custom: []
influxdb2_docker_volumes: "{{ influxdb2_docker_volumes_default
                              + influxdb2_docker_volumes_custom }}"

# Devices
influxdb2_docker_devices_default: []
influxdb2_docker_devices_custom: []
influxdb2_docker_devices: "{{ influxdb2_docker_devices_default
                              + influxdb2_docker_devices_custom }}"

# Hosts
influxdb2_docker_hosts_default: []
influxdb2_docker_hosts_custom: []
influxdb2_docker_hosts: "{{ docker_hosts_common
                            | combine(influxdb2_docker_hosts_default)
                            | combine(influxdb2_docker_hosts_custom) }}"

# Labels
influxdb2_docker_labels_default: {}
influxdb2_docker_labels_custom: {}
influxdb2_docker_labels: "{{ docker_labels_common
                             | combine(influxdb2_docker_labels_default)
                             | combine(influxdb2_docker_labels_custom) }}"

# Hostname
influxdb2_docker_hostname: "{{ influxdb2_name }}"

# Networks
influxdb2_docker_networks_alias: "{{ influxdb2_name }}"
influxdb2_docker_networks_default: []
influxdb2_docker_networks_custom: []
influxdb2_docker_networks: "{{ docker_networks_common
                               + influxdb2_docker_networks_default
                               + influxdb2_docker_networks_custom }}"

# Capabilities
influxdb2_docker_capabilities_default: []
influxdb2_docker_capabilities_custom: []
influxdb2_docker_capabilities: "{{ influxdb2_docker_capabilities_default
                                   + influxdb2_docker_capabilities_custom }}"

# Security Opts
influxdb2_docker_security_opts_default: []
influxdb2_docker_security_opts_custom: []
influxdb2_docker_security_opts: "{{ influxdb2_docker_security_opts_default
                                    + influxdb2_docker_security_opts_custom }}"

# Restart Policy
influxdb2_docker_restart_policy: unless-stopped

# State
influxdb2_docker_state: started
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