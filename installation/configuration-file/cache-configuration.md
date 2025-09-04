---
description: Adjust Jibril Cache to avoid Miss Detections
icon: line-columns
---

# Cache Configuration

## <mark style="color:yellow;">Jibril Cache Configuration</mark>

Jibril, utilizes various caches to optimize performance and manage system resources efficiently. The configuration of these caches is crucial for tailoring Jibril to specific operational environments, balancing detection capabilities with resource footprint. As outlined in Jibril's architecture, its flexibility and scalability heavily rely on how these components are configured.

This document details the available cache options in the `config.yaml` file, their purpose, and provides sizing examples for different scenarios.

## <mark style="color:yellow;">Cache Options</mark>

Jibril's caches are designed to store transient data related to system activities, such as tasks, file operations, and network flows. Properly sizing these caches ensures that Jibril can maintain a low resource footprint while providing comprehensive monitoring.

### <mark style="color:yellow;">Task-Related Caches</mark>

These caches store information about running processes and their execution context.

* `rec-tasks`\
  Holds data for recent tasks for short-term historical analysis.
* `tasks`\
  Stores information about OS processes observed by Jibril.
* `cmds`\
  Caches the command lines used to start tasks.
* `args`\
  Stores the arguments passed to commands.

### <mark style="color:yellow;">File-Related Caches</mark>

These caches manage data related to file system access and modifications.

* `files`\
  Caches information about accessed files.
* `dirs`\
  Stores data related to accessed directories.
* `bases`\
  Caches base paths for files.
* `task-file`\
  Maps tasks to the files they accessed.
* `file-task`\
  Maps files to the tasks that accessed them.
* `task-ref`\
  Tracks references to tasks.

### <mark style="color:yellow;">Flow-Related Caches (Network)</mark>

These caches store information about network communications.

* `flows`\
  Caches network flow data.
* `task-flow`\
  Maps tasks to the network flows they are associated with.
* `flow-task`\
  Maps network flows back to the tasks responsible for them.
* `flow-ref`\
  Tracks references to network flows.

### <mark style="color:yellow;">Domain-Related Caches (Network)</mark>

These caches store information related to network domain resolutions and peer connections.

Domain-related caches are included in the old config section for backward compatibility.

## <mark style="color:yellow;">Cache Size Examples</mark>

The [config.yaml](./) file provides options that allows Jibril to be adapted to various environments, from resource-constrained devices to high-traffic servers. By not information those options, Jibril will use the [default values](cache-configuration.md#id-1.-average-default).

### <mark style="color:yellow;">1. Average (Default)</mark>

This is the default set of values and good for most of the use cases.

```yaml
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
```

{% hint style="success" %}
The "Average" configuration provides ample cache space for common system activities. It can handle a moderate number of concurrent processes, file operations, and network flows without excessive memory consumption. Under heavy workloads, missed detections might occur for detection recipes that depend on file accesses (but this can be mitigated by fine-tuning these parameters). This aligns with Jibril's goal of maintaining efficiency by using eBPF for kernel-level data collection and a structured userland execution model.
{% endhint %}

### <mark style="color:yellow;">2. Small Devices</mark>

This configuration significantly reduces cache sizes to minimize Jibril's memory footprint, making it suitable for embedded systems or environments with limited resources.

```yaml
caches:
  rec-tasks: 16
  tasks: 32
  cmds: 16
  args: 16
  files: 16
  dirs: 4
  bases: 8
  task-file: 256
  file-task: 256
  task-ref: 256
  flows: 64
  task-flow: 64
  flow-task: 64
  flow-ref: 64
```

{% hint style="success" %}
For small devices, minimizing memory usage is paramount. While smaller caches might lead to more cache misses and some missed detections, the trade-off is acceptable if other detection recipes come into play. This demonstrates Jibril's adaptability to different deployment scales.
{% endhint %}

### <mark style="color:yellow;">3. Heavy I/O</mark>

This configuration increases cache sizes, particularly for file and flow-related data, to reduce miss-detections and improve performance on systems with high disk and network activity.

```yaml
caches:
  rec-tasks: 64
  tasks: 128
  cmds: 64
  args: 64
  files: 64
  dirs: 16
  bases: 32
  task-file: 1024
  file-task: 1024
  task-ref: 1024
  flows: 256
  task-flow: 256
  flow-task: 256
  flow-ref: 256
```

{% hint style="warning" %}
On systems with heavy I/O (thousands of different file creations or modifications per second), larger caches are beneficial. Increasing cache sizes makes Jibril practically infallible in terms of losing detections, at the cost of consuming more memory. This quid-pro-quo is unavoidable if missing file access-related detections is unacceptable. Unlike other projects, Jibril allows you to choose (instead of quietly dropping events like most, if not all, other eBPF-based tools). This configuration prioritizes comprehensive monitoring and detection accuracy in demanding environments, aligning with Jibril's capability to handle large-scale deployments.
{% endhint %}

### Conclusion

Configuring Jibril's caches appropriately is a key aspect of deploying the agent effectively. By understanding the purpose of each cache and selecting a sizing strategy that matches the system's workload and resource availability, users can ensure optimal performance and robust runtime detection. Jibril's eBPF-based architecture, combined with this configurable caching mechanism, allows for deep visibility into system behavior while maintaining efficiency.
