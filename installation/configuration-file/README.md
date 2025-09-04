---
icon: sliders-up
---

# Configuration File

## <mark style="color:yellow;">Defaults: /etc/jibril/config.yaml</mark>

```yaml
#### Github Config File.

run-time:
  log-level: simple
  profiler: false
  health: true
  cardinal: true
  stdout: stdout
  stderr: stderr

#### Cadences.

# Cadences are the intervals at which patterns are detected.
# https://jibril.garnet.ai/installation/configuration-file/cadence-configuration

cadences:
  file-access: 9
  network-peers: 9
  network-flows: 9
  env-vars: 9

#### Caches.

# Caches are both the kernel maps and the in-memory caches for OS resources.
# https://jibril.garnet.ai/installation/configuration-file/cache-configuration

caches:
  rec-tasks: 32
  tasks: 64
  cmds: 32
  args: 32
  files: 32
  dirs: 8
  bases: 16
  task-file: 512
  file-task: 512
  task-ref: 512
  flows: 128
  task-flow: 128
  flow-task: 128
  flow-ref: 128

#### Config.

# This is the old config file syntax used for backward compatibility.

config:
  extension:
    - config
    - data
    - jibril
  plugin:
    - jibril:hold
    - jibril:procfs
    - jibril:printers
    # - jibril:jbconfig
    # - jibril:pause
    # - jibril:attenuator:enabled=true:model=gpt-4o:temperature=0.3:mode=reason
    - jibril:detect
    # - jibril:netpolicy:file=/etc/jibril/netpolicy.yaml
  printer:
    # - simple:printers:voidprinter
    # - jibril:printers:stdout
    # - jibril:printers:stdout:raw=true
    - jibril:printers:varlog
  event:
    # ---- Informational events about network policy applied
    # - jibril:netpolicy:dropip
    # - jibril:netpolicy:dropdomain
    # ---- Informational events about network flows
    # - jibril:detect:flow
    # ---- Detection recipes for file access patterns
    # - jibril:detect:file_example (/tmp/blergh, ...)
    - jibril:detect:capabilities_modification
    - jibril:detect:code_modification_through_procfs
    - jibril:detect:core_pattern_access
    - jibril:detect:cpu_fingerprint
    - jibril:detect:credentials_files_access
    - jibril:detect:filesystem_fingerprint
    - jibril:detect:java_debug_lib_load
    - jibril:detect:java_instrument_lib_load
    - jibril:detect:machine_fingerprint
    - jibril:detect:os_fingerprint
    - jibril:detect:os_network_fingerprint
    - jibril:detect:os_status_fingerprint
    - jibril:detect:package_repo_config_modification
    - jibril:detect:pam_config_modification
    - jibril:detect:sched_debug_access
    - jibril:detect:shell_config_modification
    - jibril:detect:ssl_certificate_access
    - jibril:detect:sudoers_modification
    - jibril:detect:sysrq_access
    - jibril:detect:unprivileged_bpf_config_access
    - jibril:detect:global_shlib_modification
    - jibril:detect:environ_read_from_procfs
    - jibril:detect:binary_self_deletion
    - jibril:detect:crypto_miner_files
    - jibril:detect:auth_logs_tamper
    # ---- Detection recipes for execution patterns
    # - jibril:detect:exec_example (zip executable)
    - jibril:detect:binary_executed_by_loader
    - jibril:detect:code_on_the_fly
    - jibril:detect:credentials_text_lookup
    - jibril:detect:data_encoder_exec
    - jibril:detect:denial_of_service_tools
    - jibril:detect:exec_from_unusual_dir
    - jibril:detect:file_attribute_change
    - jibril:detect:hidden_elf_exec
    - jibril:detect:interpreter_shell_spawn
    - jibril:detect:net_filecopy_tool_exec
    - jibril:detect:net_mitm_tool_exec
    - jibril:detect:net_scan_tool_exec
    - jibril:detect:net_sniff_tool_exec
    - jibril:detect:net_suspicious_tool_exec
    - jibril:detect:net_suspicious_tool_shell
    - jibril:detect:passwd_usage
    - jibril:detect:runc_suspicious_exec
    - jibril:detect:webserver_exec
    - jibril:detect:webserver_shell_exec
    - jibril:detect:crypto_miner_execution
    # ---- Detection recipes for environment variables patterns
    - jibril:detect:dynamic_linker_attacks
    # ---- Detection recipes for network peers patterns
    # - jibril:detect:peer_example (example.com)
    - jibril:detect:adult_domain_access
    # - jibril:detect:algorithmic_domains
    - jibril:detect:algorithmic_domains_light
    - jibril:detect:badware_domain_access
    - jibril:detect:cloud_metadata_access
    - jibril:detect:dyndns_domain_access
    - jibril:detect:fake_domain_access
    # - jibril:detect:gambling_domain_access
    - jibril:detect:gambling_domain_access_light
    # - jibril:detect:general_new_domains
    - jibril:detect:general_new_domains_light
    # - jibril:detect:phishing_domains
    - jibril:detect:phishing_domains_light
    - jibril:detect:piracy_domain_access
    - jibril:detect:plaintext_communication
    # - jibril:detect:threat_domain_access
    - jibril:detect:threat_domain_access_light
    # - jibril:detect:threat_domain_access_medium
    - jibril:detect:tracking_domain_access
    - jibril:detect:vpnlike_domain_access

```

## <mark style="color:yellow;">Run Jibril</mark>

```
sudo -E ./build/loader --config ~/config/default.yaml
```
