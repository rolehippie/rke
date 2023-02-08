# rke

[![Source Code](https://img.shields.io/badge/github-source%20code-blue?logo=github&logoColor=white)](https://github.com/rolehippie/rke) [![General Workflow](https://github.com/rolehippie/rke/actions/workflows/general.yml/badge.svg)](https://github.com/rolehippie/rke/actions/workflows/general.yml) [![Readme Workflow](https://github.com/rolehippie/rke/actions/workflows/readme.yml/badge.svg)](https://github.com/rolehippie/rke/actions/workflows/readme.yml) [![Galaxy Workflow](https://github.com/rolehippie/rke/actions/workflows/galaxy.yml/badge.svg)](https://github.com/rolehippie/rke/actions/workflows/galaxy.yml) [![License: Apache-2.0](https://img.shields.io/github/license/rolehippie/rke)](https://github.com/rolehippie/rke/blob/master/LICENSE) [![Ansible Role](https://img.shields.io/ansible/role/51496)](https://galaxy.ansible.com/rolehippie/rke)

Ansible role to deploy Kubernetes with Rancher Kubernetes Engine.

## Sponsor

Building and improving this Ansible role have been sponsored by my current and previous employers like **[Cloudpunks GmbH](https://cloudpunks.de)** and **[Proact Deutschland GmbH](https://www.proact.eu)**.

## Table of content

- [Default Variables](#default-variables)
  - [rke_addon_default](#rke_addon_default)
  - [rke_addon_extra](#rke_addon_extra)
  - [rke_auth_mode](#rke_auth_mode)
  - [rke_auth_sans](#rke_auth_sans)
  - [rke_auth_strategy](#rke_auth_strategy)
  - [rke_backup_enabled](#rke_backup_enabled)
  - [rke_backup_interval](#rke_backup_interval)
  - [rke_backup_retention](#rke_backup_retention)
  - [rke_binary_checksum](#rke_binary_checksum)
  - [rke_binary_download](#rke_binary_download)
  - [rke_binary_version](#rke_binary_version)
  - [rke_cluster_name](#rke_cluster_name)
  - [rke_config_dir](#rke_config_dir)
  - [rke_config_group](#rke_config_group)
  - [rke_config_mode](#rke_config_mode)
  - [rke_config_owner](#rke_config_owner)
  - [rke_controller_config](#rke_controller_config)
  - [rke_copy_kubeconfig](#rke_copy_kubeconfig)
  - [rke_dns_config](#rke_dns_config)
  - [rke_enable_cri_dockerd](#rke_enable_cri_dockerd)
  - [rke_etcd_config](#rke_etcd_config)
  - [rke_external_domain](#rke_external_domain)
  - [rke_force_update](#rke_force_update)
  - [rke_images_config](#rke_images_config)
  - [rke_ingress_config](#rke_ingress_config)
  - [rke_kubeapi_config](#rke_kubeapi_config)
  - [rke_kubelet_config](#rke_kubelet_config)
  - [rke_kubeproxy_config](#rke_kubeproxy_config)
  - [rke_kubernetes_support](#rke_kubernetes_support)
  - [rke_kubernetes_version](#rke_kubernetes_version)
  - [rke_monitoring_config](#rke_monitoring_config)
  - [rke_network_options](#rke_network_options)
  - [rke_network_password](#rke_network_password)
  - [rke_network_plugin](#rke_network_plugin)
  - [rke_nodes_config](#rke_nodes_config)
  - [rke_provider_config](#rke_provider_config)
  - [rke_registries_config](#rke_registries_config)
  - [rke_s3_access](#rke_s3_access)
  - [rke_s3_bucket](#rke_s3_bucket)
  - [rke_s3_endpoint](#rke_s3_endpoint)
  - [rke_s3_folder](#rke_s3_folder)
  - [rke_s3_region](#rke_s3_region)
  - [rke_s3_secret](#rke_s3_secret)
  - [rke_scheduler_config](#rke_scheduler_config)
- [Discovered Tags](#discovered-tags)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Default Variables

### rke_addon_default

List of default addons to install

#### Default value

```YAML
rke_addon_default: []
```

#### Example usage

```YAML
rke_addon_default:
  - url: https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/operator.yaml
  - name: example
    content:
      apiVersion: v1
      kind: Service
      metadata:
        name: example
        namespace: kube-system
      spec:
        ports:
          - name: http
            port: 8080
        selector:
          app.kubernetes.io/example
  - name: dummy
    state: absent
```

### rke_addon_extra

List of extra addons to install

#### Default value

```YAML
rke_addon_extra: []
```

#### Example usage

```YAML
rke_addon_extra:
  - url: https://raw.githubusercontent.com/rook/rook/master/cluster/examples/kubernetes/ceph/operator.yaml
  - name: example
    content:
      apiVersion: v1
      kind: Service
      metadata:
        name: example
        namespace: kube-system
      spec:
        ports:
          - name: http
            port: 8080
        selector:
          app.kubernetes.io/example
  - name: dummy
    state: absent
```

### rke_auth_mode

Authorization mode

#### Default value

```YAML
rke_auth_mode: rbac
```

### rke_auth_sans

List of SANs for the Kubernetes API

#### Default value

```YAML
rke_auth_sans: []
```

#### Example usage

```YAML
rke_auth_sans:
  - 192.168.1.254
  - kubernetes.example.com
```

### rke_auth_strategy

Authentication strategy

#### Default value

```YAML
rke_auth_strategy: x509
```

### rke_backup_enabled

Enable etcd backups

#### Default value

```YAML
rke_backup_enabled: false
```

### rke_backup_interval

Interval for etcd backups

#### Default value

```YAML
rke_backup_interval: 24
```

### rke_backup_retention

Retention for etcd backups

#### Default value

```YAML
rke_backup_retention: 7
```

### rke_binary_checksum

Checksum of the binary to download

#### Default value

```YAML
rke_binary_checksum: sha256:154d55b3a587edc2da497f621f2b302a393cf70e332001fcd2aad612dd479a41
```

### rke_binary_download

URL to download the release binary

#### Default value

```YAML
rke_binary_download: https://github.com/rancher/rke/releases/download/v{{ rke_binary_version
  }}/rke_linux-amd64
```

### rke_binary_version

Version of the RKE release to use

#### Default value

```YAML
rke_binary_version: 1.4.2
```

### rke_cluster_name

Name of the Kubernetes cluster

#### Default value

```YAML
rke_cluster_name:
```

### rke_config_dir

Path to for configuration and state

#### Default value

```YAML
rke_config_dir: /etc/rke
```

### rke_config_group

#### Default value

```YAML
rke_config_group: root
```

### rke_config_mode

#### Default value

```YAML
rke_config_mode: u=rw,g=r,o=
```

### rke_config_owner

Owner of the copied kubeconfig

#### Default value

```YAML
rke_config_owner: root
```

### rke_controller_config

#### Default value

```YAML
rke_controller_config:
```

### rke_copy_kubeconfig

Copy kubeconfig to these nodes

#### Default value

```YAML
rke_copy_kubeconfig: []
```

#### Example usage

```YAML
rke_copy_kubeconfig:
  - master-01
  - master-02
  - master-03
```

### rke_dns_config

DNS configuration

#### Default value

```YAML
rke_dns_config:
  provider: coredns
  nodelocal:
    ip_address: 169.254.20.10
  upstreamnameservers:
    - 1.1.1.1
    - 8.8.8.8
```

### rke_enable_cri_dockerd

Enable CRI dockerd wrapper

#### Default value

```YAML
rke_enable_cri_dockerd: false
```

### rke_etcd_config

Scheduler configuration

#### Default value

```YAML
rke_etcd_config:
```

### rke_external_domain

External domain to override copied kubeconfigs

#### Default value

```YAML
rke_external_domain:
```

### rke_force_update

Force cluster update even without config changes

#### Default value

```YAML
rke_force_update: false
```

### rke_images_config

System images configuration

#### Default value

```YAML
rke_images_config:
```

#### Example usage

```YAML
rke_images_config:
  etcd: rancher/coreos-etcd:v3.2.24
  alpine: rancher/rke-tools:v0.1.24
  nginx_proxy: rancher/rke-tools:v0.1.24
```

### rke_ingress_config

Ingress configuration

#### Default value

```YAML
rke_ingress_config:
  provider: nginx
  dns_policy: ClusterFirstWithHostNet
```

### rke_kubeapi_config

#### Default value

```YAML
rke_kubeapi_config:
  always_pull_images: true
  audit_log:
    enabled: true
  secrets_encryption_config:
    enabled: true
```

### rke_kubelet_config

#### Default value

```YAML
rke_kubelet_config:
```

### rke_kubeproxy_config

#### Default value

```YAML
rke_kubeproxy_config:
```

### rke_kubernetes_support

Mapping for supported Kubernetes versions

#### Default value

```YAML
rke_kubernetes_support:
  '1.17': v1.17.17-rancher1-3
  '1.18': v1.18.20-rancher1-3
  '1.19': v1.19.16-rancher1-6
  '1.20': v1.20.15-rancher1-4
  '1.21': v1.21.14-rancher1-1
  '1.22': v1.22.17-rancher1-1
  '1.23': v1.23.15-rancher1-1
  '1.24': v1.24.9-rancher1-1
  '1.25': v1.25.5-rancher1-1
```

### rke_kubernetes_version

Kubernetes version to install

#### Default value

```YAML
rke_kubernetes_version: '1.24'
```

### rke_monitoring_config

Monitoring configuration

#### Default value

```YAML
rke_monitoring_config:
  provider: metrics-server
```

### rke_network_options

Network options

#### Default value

```YAML
rke_network_options:
```

### rke_network_password

Weave password

#### Default value

```YAML
rke_network_password: p455w0rd
```

### rke_network_plugin

Network plugin

#### Default value

```YAML
rke_network_plugin: weave
```

### rke_nodes_config

Nodes configuration

#### Default value

```YAML
rke_nodes_config:
```

#### Example usage

```YAML
rke_nodes_config: |
  {% for node in groups['server'] %}
    - hostname_override: {{ node }}
      address: {{ hostvars[host]['ansible_host'] }}
      user: rke
      role:
        - controlplane
        - etcd
  {% endfor %}
  {% for node in groups['worker'] %}
    - hostname_override: {{ node }}
      address: {{ hostvars[host]['ansible_host'] }}
      user: rke
      role:
        - worker
  {% endfor %}
```

### rke_provider_config

Cloud provider configuration

#### Default value

```YAML
rke_provider_config:
```

### rke_registries_config

System images configuration

#### Default value

```YAML
rke_registries_config:
```

#### Example usage

```YAML
rke_registries_config:
  - url: registry.example.com
    user: username
    password: p455w0rd
  - url: registry.foobar.com
    user: username
    password: p455w0rd
    is_default: True
```

### rke_s3_access

Backup S3 access key

#### Default value

```YAML
rke_s3_access:
```

### rke_s3_bucket

Backup S3 bucket

#### Default value

```YAML
rke_s3_bucket:
```

### rke_s3_endpoint

Backup S3 endpoint

#### Default value

```YAML
rke_s3_endpoint:
```

### rke_s3_folder

Backup S3 folder

#### Default value

```YAML
rke_s3_folder:
```

### rke_s3_region

Backup S3 region

#### Default value

```YAML
rke_s3_region:
```

### rke_s3_secret

Backup S3 secret key

#### Default value

```YAML
rke_s3_secret:
```

### rke_scheduler_config

#### Default value

```YAML
rke_scheduler_config:
```

## Discovered Tags

**_rke_**

**_skip_ansible_later_**


## Dependencies

- None

## License

Apache-2.0

## Author

[Thomas Boerger](https://github.com/tboerger)
