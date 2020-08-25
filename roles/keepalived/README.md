keepalived
==================

Install keepalived daemonset on an existing K8s cluster

Requirements
------------

Only uses python and ansible.


Role Variables
--------------

```yaml
---
# Custom K8s cluster vIP HA setup
# Useful when you want built-in HA for your custom K8s cluster ingress controller without external LB
keepalived_enabled: false
# Specify if the keepalived setup should only use a private IP.
# If so, set "keepalived_private_only" to "true"
# and leave all "*_public_*" configuration options down here empty.
keepalived_private_only: false
# Specify if the keepalived setup should only use IPv4.
# If so, set "keepalived_ipv4_only" to "true"
# and leave all "*_ipv6" configuration options down here empty.
keepalived_ipv4_only: false
# Specify a node selector labels if keepalived containers should only run on certain nodes
# If left empty, the daemonset will deploy a replica per node. For example "vip_public" and "vip_private":
keepalived_private_node_selector: "vip_private"
keepalived_public_node_selector: "vip_public"
# Specify a node toleration label if keepalived containers should be running on tainted certain nodes
keepalived_private_node_toleration: ""
keepalived_public_node_toleration: "public_ingress"
# Specify where the custom K8s cluster is running. Currently supported environments are:
# - "local": Local keepalived setup
# - "cloudscale": Keepalived setup with cloudscale floating IP
keepalived_setup_env: "local"
# If "keepalived_setup_env" is set to "cloudscale", a cloudscale API token needs to be provided.
keepalived_cloudscale_api_token: "{{ cloudscale_api_token }}"
# Keepalived service Docker image
keepalived_image: "puzzle/keepalived:2.0.20"
# Keepalived IP address configuration
keepalived_private_failover_track_interface_ip: eth0
keepalived_private_failover_ip:
  - vip: "192.0.2.254"
    router_id: 1
    master: rancher01
    password: my-top-secret-password1-here
keepalived_public_failover_track_interface_ip: eth0
keepalived_public_failover_ip:
  - vip: "198.51.100.254"
    router_id: 2
    master: rancher01
    password: my-top-secret-password2-here
keepalived_public_failover_track_interface_ipv6: eth0
keepalived_public_failover_ipv6:
  - vip: "2001:db8::ffff"
    router_id: 3
    master: rancher01
    password: my-top-secret-password3-here
```

Dependencies
------------

* none

License
-------

GPLv3

Author Information
------------------

* Sebastian Plattner (plattner@puzzle.ch)
