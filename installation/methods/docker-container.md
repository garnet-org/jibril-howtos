---
icon: docker
---

# Docker Container

> Check out Jibril's public recipes repository at [https://github.com/garnet-org/jibril-balag](https://github.com/garnet-org/jibril-balag).

## <mark style="color:$primary;">Create a Config File</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```sh
mkdir /etc/jibril
```

```
vi /etc/jibril/config.yaml
```

> Use the [default configuration file ](../configuration-file/)as a reference to create the initial config file.

## <mark style="color:$primary;">Obtain Jibril</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```
docker pull garnetlabs/jibril:v2.5
```

## <mark style="color:$primary;">Run Jibril using Docker</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```
docker run --rm --name=jibril --privileged \
    --pid=host --cgroupns=host --network=host \
    -e TERM=xterm -v /sys:/sys:ro \
    -v /sys/fs/bpf:/sys/fs/bpf:rw \
    -v /etc/jibril/:/etc/jibril:rw \
    -v /var/log/jibril:/var/log/jibril:rw \
    garnetlabs/jibril:v2.5 --config /etc/jibril/config.yaml
```

> This command is an example of how one can run Jibril using its docker image.

{% hint style="info" %}
For Kubernetes, use the [Kubernetes instructions](../kubernetes/).
{% endhint %}

## <mark style="color:$primary;">Optional</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

### Want to try the [attenuator.md](../../customization/attenuator.md "mention") feature ?

```
docker run --rm --name=jibril --privileged \
    --pid=host --cgroupns=host --network=host \
    -e AI_TOKEN=$AI_TOKEN \
    -e AI_MODEL=o3 \
    -e AI_TEMPERATURE=1 \
    -e TERM=xterm -v /sys:/sys:ro \
    -v /sys/fs/bpf:/sys/fs/bpf:rw \
    -v /etc/jibril/:/etc/jibril:rw \
    -v /var/log/jibril:/var/log/jibril:rw \
    garnetlabs/jibril:v2.5 \
    --config /etc/jibril/config.yaml
```

#### Make sure your [configuration-file](../configuration-file/ "mention") `/etc/jibril/config,yaml` is set as:

```yaml
log-level: info
stdout: stdout
stderr: stderr
chop-lines: false
no-health: false
profiler: false
cardinal: true
daemon: false
notify: false
extension:
  - config
  - data
  - jibril
plugin:
  - jibril:hold
  - jibril:procfs
  - jibril:printers
  - jibril:attenuator:enabled=true:mode=reason
  - jibril:detect
printer:
  - jibril:printers:stdout
event:
  - jibril:detect:hidden_elf_exec
  - jibril:detect:plaintext_communication
```

#### Execute a test

Execute a simple test trying to get something from a paste-bin like URL

```
curl https://gist.githubusercontent.com/tempadmin2023/sysconfig-update/raw/critical_patch.sh
```

#### Observe the AI verdict

Observe the event + the verdict given by the AI model.

```json
{
  "uuid": "51960584d144e7a2ed1746b2a48207234f84412048c55662f9712f3851cfc7e5",
  "timestamp": "2025-08-12T17:51:18Z",
  "note": "plaintext_communication_suffix",
  "metadata": {
    "kind": "plaintext_communication",
    "name": "plaintext_communication_suffix",
    "format": "network_peers",
    "version": "1.0",
    "description": "Access to pastebin services",
    "importance": "critical",
    "documentation": "https://garnet.gitbook.io/jibril/detections/network-peers/plaintext_communication",
    "tactic": "command_and_control",
    "technique": "application_layer_protocol",
    "subtechnique": "web_protocols"
  },
  "background": {
    "files": {
      "root": {
        "abs_path": "/",
        "dirs": [
          {
            "abs_path": "/etc",
            "base_name": "etc",
            "dirs": [
              {
                "abs_path": "/etc/ca-certificates",
                "base_name": "ca-certificates",
                "dirs": [
                  {
                    "abs_path": "/etc/ca-certificates/extracted",
                    "base_name": "extracted",
                    "files": [
                      {
                        "abs_path": "/etc/ca-certificates/extracted/tls-ca-bundle.pem",
                        "base_name": "tls-ca-bundle.pem",
                        "actions": ["open", "read", "close"]
                      }
                    ]
                  }
                ]
              },
              {
                "abs_path": "/etc/ssl",
                "base_name": "ssl",
                "files": [
                  {
                    "abs_path": "/etc/ssl/openssl.cnf",
                    "base_name": "openssl.cnf",
                    "actions": ["open", "read", "close"]
                  }
                ]
              }
            ],
            "files": [
              {
                "abs_path": "/etc/gai.conf",
                "base_name": "gai.conf",
                "actions": ["open", "read", "close"]
              },
              {
                "abs_path": "/etc/host.conf",
                "base_name": "host.conf",
                "actions": ["open", "read", "close"]
              },
              {
                "abs_path": "/etc/ld.so.cache",
                "base_name": "ld.so.cache",
                "actions": ["mmap", "open", "close"]
              },
              {
                "abs_path": "/etc/ld.so.preload",
                "base_name": "ld.so.preload",
                "actions": ["open", "close"]
              },
              {
                "abs_path": "/etc/nsswitch.conf",
                "base_name": "nsswitch.conf",
                "actions": ["open", "read", "close"]
              },
              {
                "abs_path": "/etc/passwd",
                "base_name": "passwd",
                "actions": ["open", "read", "close"]
              }
            ]
          },
          {
            "abs_path": "/usr",
            "base_name": "usr",
            "dirs": [
              {
                "abs_path": "/usr/bin",
                "base_name": "bin",
                "files": [
                  {
                    "abs_path": "/usr/bin/curl",
                    "base_name": "curl",
                    "actions": ["mmap", "open", "close", "execve"]
                  }
                ]
              },
              {
                "abs_path": "/usr/lib",
                "base_name": "lib",
                "dirs": [
                  {
                    "abs_path": "/usr/lib/locale",
                    "base_name": "locale",
                    "files": [
                      {
                        "abs_path": "/usr/lib/locale/locale-archive",
                        "base_name": "locale-archive",
                        "actions": ["mmap", "open", "close"]
                      }
                    ]
                  },
                  {
                    "abs_path": "/usr/lib/systemd",
                    "base_name": "systemd",
                    "files": [
                      {
                        "abs_path": "/usr/lib/systemd/resolv.conf",
                        "base_name": "resolv.conf",
                        "actions": ["open", "read", "close"]
                      }
                    ]
                  }
                ],
                "files": [
                  {
                    "abs_path": "/usr/lib/ld-linux-x86-64.so.2",
                    "base_name": "ld-linux-x86-64.so.2",
                    "actions": ["mmap", "open", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libbrotlicommon.so.1.1.0",
                    "base_name": "libbrotlicommon.so.1.1.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libbrotlidec.so.1.1.0",
                    "base_name": "libbrotlidec.so.1.1.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libc.so.6",
                    "base_name": "libc.so.6",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libcap.so.2.76",
                    "base_name": "libcap.so.2.76",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libcom_err.so.2.1",
                    "base_name": "libcom_err.so.2.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libcrypto.so.3",
                    "base_name": "libcrypto.so.3",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libcurl.so.4.8.0",
                    "base_name": "libcurl.so.4.8.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libgcc_s.so.1",
                    "base_name": "libgcc_s.so.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libgssapi_krb5.so.2.2",
                    "base_name": "libgssapi_krb5.so.2.2",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libidn2.so.0.4.0",
                    "base_name": "libidn2.so.0.4.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libk5crypto.so.3.1",
                    "base_name": "libk5crypto.so.3.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libkeyutils.so.1.10",
                    "base_name": "libkeyutils.so.1.10",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libkrb5.so.3.3",
                    "base_name": "libkrb5.so.3.3",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libkrb5support.so.0.1",
                    "base_name": "libkrb5support.so.0.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libm.so.6",
                    "base_name": "libm.so.6",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libnghttp2.so.14.28.5",
                    "base_name": "libnghttp2.so.14.28.5",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libnghttp3.so.9.3.0",
                    "base_name": "libnghttp3.so.9.3.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libnss_mymachines.so.2",
                    "base_name": "libnss_mymachines.so.2",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libnss_resolve.so.2",
                    "base_name": "libnss_resolve.so.2",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libpsl.so.5.3.5",
                    "base_name": "libpsl.so.5.3.5",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libresolv.so.2",
                    "base_name": "libresolv.so.2",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libssh2.so.1.0.1",
                    "base_name": "libssh2.so.1.0.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libssl.so.3",
                    "base_name": "libssl.so.3",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libunistring.so.5.2.0",
                    "base_name": "libunistring.so.5.2.0",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libz.so.1.3.1",
                    "base_name": "libz.so.1.3.1",
                    "actions": ["mmap", "open", "read", "close"]
                  },
                  {
                    "abs_path": "/usr/lib/libzstd.so.1.5.7",
                    "base_name": "libzstd.so.1.5.7",
                    "actions": ["mmap", "open", "read", "close"]
                  }
                ]
              },
              {
                "abs_path": "/usr/share",
                "base_name": "share",
                "dirs": [
                  {
                    "abs_path": "/usr/share/zoneinfo",
                    "base_name": "zoneinfo",
                    "dirs": [
                      {
                        "abs_path": "/usr/share/zoneinfo/America",
                        "base_name": "America",
                        "files": [
                          {
                            "abs_path": "/usr/share/zoneinfo/America/Sao_Paulo",
                            "base_name": "Sao_Paulo",
                            "actions": ["open", "read", "close"]
                          }
                        ]
                      }
                    ]
                  }
                ]
              }
            ]
          }
        ]
      }
    },
    "flows": {
      "ip_version": 4,
      "protocols": [
        {
          "proto": "TCP",
          "pairs": [
            {
              "nodes": {
                "local": {
                  "address": "192.168.250.5",
                  "name": "rugged",
                  "names": ["192.168.250.5", "rugged.lab", "rugged"]
                },
                "remote": {
                  "address": "185.199.108.133",
                  "name": "gist.githubusercontent.com",
                  "names": ["185.199.108.133", "gist.githubusercontent.com"]
                }
              },
              "port_matrix": [
                {
                  "src_port": 40842,
                  "dst_port": 443,
                  "phase": {
                    "direction": "both",
                    "initiated_by": "local",
                    "status": "ended",
                    "ended_by": "local"
                  }
                }
              ]
            }
          ]
        }
      ]
    },
    "ancestry": [
      {
        "start": "2025-08-11T20:34:40Z",
        "exit": "running",
        "retcode": 0,
        "uid": 0,
        "pid": 1,
        "ppid": 0,
        "comm": "systemd",
        "cmd": "systemd",
        "exe": "/usr/lib/systemd/systemd",
        "args": "/sbin/init",
        "envs": "TERM=linux"
      },
      {
        "start": "2025-08-11T20:34:45Z",
        "exit": "running",
        "retcode": 0,
        "uid": 0,
        "pid": 627,
        "ppid": 1,
        "comm": "sshd",
        "cmd": "sshd",
        "exe": "/usr/bin/sshd",
        "args": "sshd: /usr/bin/sshd -D [listener] 0 of 10-100 startups",
        "envs": ""
      },
      {
        "start": "2025-08-12T17:50:45Z",
        "exit": "running",
        "retcode": 0,
        "uid": 0,
        "pid": 227519,
        "ppid": 627,
        "comm": "sshd-session",
        "cmd": "sshd-session",
        "exe": "/usr/lib/ssh/sshd-session",
        "args": "sshd-session: rafaeldtinoco [priv]",
        "envs": ""
      },
      {
        "start": "2025-08-12T17:50:46Z",
        "exit": "running",
        "retcode": 0,
        "uid": 1000,
        "pid": 227522,
        "ppid": 227519,
        "comm": "sshd-session",
        "cmd": "sshd-session",
        "exe": "/usr/lib/ssh/sshd-session",
        "args": "sshd-session: rafaeldtinoco@pts/9",
        "envs": ""
      },
      {
        "start": "2025-08-12T17:50:46Z",
        "exit": "running",
        "retcode": 0,
        "uid": 1000,
        "pid": 227523,
        "ppid": 227522,
        "comm": "bash",
        "cmd": "bash",
        "exe": "/usr/bin/bash",
        "args": "-bash",
        "envs": "HOME=/home/rafaeldtinoco ...",
      },
      {
        "start": "2025-08-12T17:51:15Z",
        "exit": "2025-08-12T17:51:15Z",
        "retcode": 0,
        "uid": 1000,
        "pid": 227674,
        "ppid": 227523,
        "comm": "curl",
        "cmd": "curl",
        "exe": "/usr/bin/curl",
        "args": "curl https://gist.githubusercontent.com/tempadmin2023/sysconfig-update/raw/critical_patch.sh",
        "envs": "SHELL=/bin/bash ...",
      }
    ]
  },
  "flow": {
    "ip_version": 4,
    "proto": "TCP",
    "local": {
      "address": "192.168.250.5",
      "name": "rugged",
      "names": ["192.168.250.5", "rugged.lab", "rugged"],
      "port": 40842
    },
    "remote": {
      "address": "185.199.108.133",
      "name": "gist.githubusercontent.com",
      "names": ["185.199.108.133", "gist.githubusercontent.com"],
      "port": 443
    },
    "service_port": 443,
    "flags": {
      "ingress": true,
      "egress": true,
      "incoming": false,
      "outgoing": true,
      "started": true,
      "ongoing": true,
      "ended": true,
      "terminator": true,
      "terminated": false
    },
    "phase": {
      "direction": "both",
      "initiated_by": "local",
      "status": "ended",
      "ended_by": "local"
    }
  }
}
```
