# Ansible Role: Pantheon

### Description
Ansible role that will install (& uninstall), configure and runs [Pantheon](https://pegasys.tech/solutions/): an enterprise Java Ethereum Client

### Table of Contents
  - [Supported Platforms](#supported-platforms)
  - [Dependencies](#dependencies)
  - [Role Variables](#role-variables)
  - [Example Playbook](#example-playbook)
  - [License](#license)
  - [Author Information](#author-information)

### Supported Platforms
```
* MacOS
* Debian
* Ubuntu
* Redhat(CentOS/Fedora)
* Amazon
```

### Dependencies

* JDK 11 or greater

### Role Variables:

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file. By and large these variables are configuration options. Please refer to the Pantheon [docs](https://docs.pantheon.pegasys.tech/en/stable/) for more information

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `pantheon_version` | ___unset___ | Version of Pantheon to install and run  __REQUIRED__ |
| `pantheon_user` | pantheon | Pantheon user |
| `pantheon_group` | pantheon | Pantheon group |
| `pantheon_download_url` | https://bintray.com/consensys/pegasys-repo/download_file?file_path=pantheon-{{ pantheon_version }}.tar.gz | The download tar.gz file used. You can use this if you need to retrieve pantheon from a custom location such as an internal repository. |
| `pantheon_install_dir` | /opt/pantheon | Path to install to  |
| `pantheon_config_dir` | /etc/pantheon | Path for default configuration |
| `pantheon_data_dir` | /opt/pantheon/data | Path for data directory|
| `pantheon_log_dir` | /var/log/pantheon | Path for logs |
| `pantheon_profile_file` | /etc/profile.d/pantheon-path.sh | Path to allow loading Pantheon into the system PATH |
| `pantheon_managed_service` | true | Enables a systemd service (or launchd if on Darwin) |
| `pantheon_launchd_dir` | /Library/LaunchAgents | The default launchd directory  |
| `pantheon_systemd_dir` | /etc/systemd/system/ | The default systemd directory |
| `pantheon_host_ip` | "" | The host IP that Pantheon uses for the P2P network. This specifies the host on which P2P listens |
| `pantheon_default_ip` | "{{ default(ansible_host) \| default('127.0.0.1') }}" | The fallback default for `pantheon_host_ip` |
| `pantheon_network` | mainnet | The network that this node will join. Other values are 'ropsten', 'rinkeby', 'goerli', 'dev'|
| `pantheon_sync_mode` | FAST | Specifies the synchronization mode. Other values are 'FULL' |
| `pantheon_log_level` | INFO | The log level to use. Other log levels are 'OFF', 'FATAL', 'WARN', 'INFO', 'DEBUG', 'TRACE', 'ALL' |
| `pantheon_p2p_port` | 30303 | Specifies the P2P listening ports (UDP and TCP). Ports must be exposed appropriately |
| `pantheon_rpc_http_enabled` | true | Enabled the HTTP JSON-RPC service |
| `pantheon_rpc_http_host` | 0.0.0.0 | Specifies the host on which HTTP JSON-RPC listens |
| `pantheon_rpc_http_api` | ["ADMIN","DEBUG","NET","ETH","MINER","WEB3"] | Comma-separated APIs to enable on the HTTP JSON-RPC channel. When you use this option, the `pantheon_rpc_http_enabled` option must also be enabled |
| `pantheon_rpc_ws_enabled` | true | Enabled the WebSockets service |
| `pantheon_rpc_ws_host` | 0.0.0.0 | Specifies the host on which WebSockets listens |
| `pantheon_rpc_ws_port` | 8546 | Specifies Websockets JSON-RPC listening port (TCP). Port must be exposed appropriately |
| `pantheon_metrics_host` | 0.0.0.0 | Specifies the host on which Prometheus accesses Pantheon metrics. The metrics server respects the `pantheon_whitelist` option |
| `pantheon_metrics_port` | 9545 | Specifies the port on which Prometheus accesses Pantheon metrics |
| `pantheon_bootnodes` | [] | List of comma-separated enode URLs for P2P discovery bootstrap. When connecting to MainNet or public testnets, the default is a predefined list of enode URLs |
| `pantheon_host_whitelist` | ["*"] | Comma-separated list of hostnames to allow access to the JSON-RPC API. By default, access from localhost and 127.0.0.1 is accepted. |
| `pantheon_cmdline_args` | "" | Command line args that are passed in as overrides |
| `pantheon_env_opts` | "" | Environmental variable PANTHEON_OPTS that gets passed to the JVM. eg: -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 |


### Example Playbook

1. Default setup:
Install the role from galaxy
```
ansible-galaxy install pegasyseng.pantheon
```

Create a requirements.yml with the following:
```
---
- hosts: localhost
  connection: local
  force_handlers: True

  roles:
  - role: pegasyseng.pantheon
    vars:
      pantheon_version: 1.2.0

```

Run with ansible-playbook:
```
ansible-playbook -v /path/to/requirements.yml
```


2. Install via github

```
ansible-galaxy install git+https://github.com/PegaSysEng/ansible-role-pantheon.git
```

Create a requirements.yml with the following:
```
---
- hosts: localhost
  connection: local
  force_handlers: True

  roles:
  - role: ansible-role-pantheon
    vars:
      pantheon_version: 1.2.0

```

Run with ansible-playbook:
```
ansible-playbook -v /path/to/requirements.yml
```


### License

Apache


### Author Information

Pegasys Tech, 2019
