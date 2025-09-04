---
description: Learn How to Enable Alchemies Plugin
icon: square-check
---

# Enable Alchemies

## <mark style="color:yellow;">Enabling the Alchemies Plugin</mark>

To use the alchemies feature, add it to your [config.yaml](../../installation/configuration-file/) file:

```yaml
plugin:
  # Or enable only built-in recipes (default behavior) only
  - jibril:alchemies

  # Enable the alchemies plugin with external recipe directory and builtin recipes
  - jibril:alchemies:builtin=true:path=/path/to/your/recipes/

  # Disable built-in recipes while using external ones
  - jibril:alchemies:builtin=false:path=/path/to/your/recipes/
```

## <mark style="color:yellow;">Plugin Options</mark>

* **`path`**: Directory path containing custom YAML recipe files.
* **`builtin`**: Enable/disable built-in recipes (default: true).

{% hint style="warning" %}
The directory path must be a valid path to a directory and is not recursive.
{% endhint %}

### Example Configuration

Example of a [config.yaml](../../installation/configuration-file/) file with the alchemies plugin configured:

```yaml
#### Standalone Config File.

run-time:
  log-level: info
  profiler: false
  health: true
  cardinal: true
  stdout: stdout
  stderr: stderr

#### Cadences.

cadences:
  file-access: 9
  network-peers: 9
  network-flows: 9
  env-vars: 9

#### Caches.

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

#### Old Config.

# This is the old config file being used for backward compatibility.
# It will be removed in the future.

config:
  extension:
    - jibril
  plugin:
    # Enable alchemies with custom recipe directory
    - jibril:alchemies:path=/etc/jibril/alchemies/
    - jibril:detect
  printer:
    - jibril:printers:stdout
  event:
    # Events will be automatically enabled based on recipes
    - jibril:detect:file_example
    - jibril:detect:exec_example
    - jibril:detect:peer_example
```
