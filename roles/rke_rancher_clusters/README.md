ansible-role-rke_rancher_clusters
==================

Create a new Kubernetes Cluster with RKE and deploys Rancher on it

Requirements
------------

Only uses python and ansible.


Role Variables
--------------

```yaml
---
### Helm Settings
helm_binary_version: v3.2.4
helm_binary_download_url: "https://get.helm.sh/helm-{{ helm_binary_version }}-linux-amd64.tar.gz"
helm_binary: "./helm"
helm_home: ".helm"
helm_rancher_repo: rancher-stable
helm_rancher_repo_url: "https://releases.rancher.com/server-charts/stable"
helm_rancher_version: v2.4.5
# You only need to configure these "helm_certmanager_*" values if you enable
# Let's Encrypt support in the "Rancher Cluster Settings" section!
helm_certmanager_version: 0.16.0
helm_certmanager_jetstack_repo: jetstack
helm_certmanager_jetstack_repo_url: https://charts.jetstack.io

### Kubectl Settings
kubectl_binary_version: v1.18.0
kubectl_binary_download_url: "https://storage.googleapis.com/kubernetes-release/release/{{ kubectl_binary_version }}/bin/linux/amd64/kubectl"
kubectl_binary: "./kubectl-{{ kubectl_binary_version }}"

### RKE Cluster Settings
rke_binary_version: v1.1.4
rke_binary_download_url: "https://github.com/rancher/rke/releases/download/{{ rke_binary_version }}/rke_linux-amd64"
rke_cluster_bin: "./rke-{{ rke_binary_version }}"
rke_cluster_kube_config: "kube_config_config-{{ inventory_hostname }}.yml"
rke_cluster_config: "config-{{ inventory_hostname }}.yml"
rke_kubernetes_version: v1.18.6-rancher1-1
rke_ssh_user: centos     # due to https://bugzilla.redhat.com/show_bug.cgi?id=1527565
rke_ssh_agent_auth: true
rke_network_interface: eth0
rke_cluster_group_inventory_name: "{{ groups['rke_' + inventory_hostname] }}"

### Rancher Cluster Settings
# General Rancher Settings
rancher_hostname: ""
rancher_admin_password: ""
rancher_admin_initial_password: admin
rancher_telemetry: out
# Lets Encrypt Configuration
# Enable Cert-Manager for Let's Encrypt support
rancher_certmanager_enabled: false
rancher_letsencrypt_email: me@example.com
rancher_certmanager_crd_url: "https://github.com/jetstack/cert-manager/releases/download/v{{ helm_certmanager_version }}/cert-manager.crds.yaml"
# Officially signed or self-signed Configuration
rancher_tls_crt: ""
rancher_tls_key: ""
rancher_tls_cacerts: ""
# rancher_tls_self_signed needs to be true if the Rancher TLS cert is self-signed, then also the
# full CA chain needs to be provided via rancher_tls_cacerts. 
# See https://rancher.com/blog/2020/transport-layer-security-p2 for more information
rancher_tls_self_signed: false
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
