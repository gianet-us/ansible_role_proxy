ansible_role_proxy
==================

Complete Proxy Server Role based on Traefik. This role installs and configures Traefik as a reverse proxy on Debian and Ubuntu systems.

Requirements
------------

This role requires Ansible 2.12 or higher. The target system should be Debian or Ubuntu.

Role Variables
--------------

The following variables are defined in `defaults/main.yml`:

| Variable | Description | Default Value |
|----------|-------------|---------------|
| `traefik_name` | Name of the service and user | `traefik` |
| `traefik_version` | Traefik version to install | `v3.6.7` |
| `traefik_opt` | Installation directory | `/opt/{{ traefik_name }}` |
| `traefik_etc` | Configuration directory | `/etc/{{ traefik_name }}` |
| `traefik_conf_d` | Dynamic configuration directory | `{{ traefik_etc }}/conf.d` |
| `traefik_global_checkNewVersion` | Check for new versions | `false` |
| `traefik_global_sendAnonymousUsage` | Send anonymous usage data | `false` |
| `traefik_entrypoints` | Dictionary defining Traefik entrypoints | `{ web: { address: ':80' }, websecure: { address: ':443' } }` |
| `traefik_api` | Enable Traefik API | `false` |
| `traefik_api_dashboard` | Enable Traefik Dashboard | `false` |
| `traefik_api_insecure` | Enable insecure API access | `false` |
| `traefik_providers_file` | Enable file provider | `true` |
| `traefik_providers_file_directory` | Directory for dynamic configuration files | `/etc/traefik/conf.d/` |
| `traefik_providers_file_watch` | Watch for changes in dynamic configuration | `true` |
| `traefik_log_level` | Log level | `ERROR` |
| `traefik_log_format` | Log format | `common` |
| `traefik_metrics_prometheus` | Enable Prometheus metrics | `false` |
| `traefik_routing_http` | HTTP routing configuration dictionary | `{}` |
| `traefik_routing_tcp` | TCP routing configuration dictionary | `{}` |
| `traefik_routing_udp` | UDP routing configuration dictionary | `{}` |
| `traefik_routing_tls` | TLS routing configuration dictionary | `{}` |

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: proxy_servers
  roles:
     - role: ansible_role_proxy
       vars:
         traefik_api_dashboard: true
         traefik_routing_http:
           routers:
             my-router:
               rule: "Host(`example.com`)"
               service: my-service
           services:
             my-service:
               loadBalancer:
                 servers:
                   - url: "http://1.1.1.1:8080"
```

License
-------

GPL-3.0-only

Author Information
------------------

+ Luciano Giacchetta
+ Giacchetta Networks LLC
+ https://gianet.us/engineering/ansible_role_proxy
