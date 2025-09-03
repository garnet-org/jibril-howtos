---
icon: archway
---

# Architecture

## <mark style="color:$primary;">Overview</mark> <a href="#overview" id="overview"></a>

***

Jibril is a modular runtime security tool that combines an eBPF loader, eBPF programs and a userland daemon to monitor, detect and respond to system behaviors causing minimal overhead. Its design emphasizes extensibility through plugins, printers, and events.

## <mark style="color:$primary;">Key Components</mark> <a href="#id-1-key-components" id="id-1-key-components"></a>

***

### eBPF Loader

Jibril is, at the same time, an eBPF object(s) loader and a main extension. This means the Jibril source code can act as multiple applications when needed (generating, from the same source code, applications for different means).&#x20;

* **Binary Generation**\
  Creates optimized binaries incorporating one or more extensions
* **Extensibility**\
  Supports feature expansion through simple source tree additions
* **Core Functionality**\
  Serves dual purpose as primary loader and default extension

> By default, Jibril acts as the eBPF loader and the main Jibril extension (as the application).

### Agent

_Jibril userland agent interprets patterns detected by the in-kernel code and acts accordingly._

* [**Extensions**](../../execution/components.md)\
  Define core features and system integrations.
* [**Plugins**](../../execution/components.md)\
  Execute specialized detection and monitoring functions.
* [**Printers**](../../execution/components.md)\
  Handle output routing to logs, files, and APIs.
* [**Events**](../../execution/components.md)\
  Capture, process, and dispatch system behaviors and conditions.
* [**Caching**](../../installation/configuration-file/cache-configuration.md)\
  Caches immutable data from kernel to improve performance.
* [**Attenuate**](../../customization/attenuator.md)\
  Disallow duplicates for the same workloads using internal mechanisms.\
  Sends events to external LLMs to filter false-positives (or amend them).
* [**React**](../../customization/reactions/)\
  Reacts to specific detections using internal and isolated JavaScript API.\


This modular architecture ensures both flexibility and performance, allowing Jibril to maintain comprehensive visibility while adapting to evolving security requirements.

## <mark style="color:$primary;">Execution Flow</mark> <a href="#id-2-execution-flow" id="id-2-execution-flow"></a>

***

Jibril components follow a structured execution order:

1. **Initialization:** Core libraries and packages are initialized first.
2. **Extensions:** Load features like configuration or data storage logic.
3. **Plugins:** Execute monitoring or detection tasks.
4. **Printers:** Process and output event data.
5. **Events:** Dispatch captured behaviors to active printers.

Each component runs through five lifecycle stages:

1. Init
2. Start
3. Execute
4. Finish
5. Exit

that can be observed in the output informational messages.

## <mark style="color:$primary;">Modular Design</mark> <a href="#id-3-modular-design-plugins-printers-and-events" id="id-3-modular-design-plugins-printers-and-events"></a>

***

### Plugins <a href="#id-31-plugins" id="id-31-plugins"></a>

Plugins add specialized functionality to Jibril, focusing on monitoring, detection, and system analysis. All plugins can be enabled or disabled in the configuration file. Examples include:

* **Hold**\
  Keeps Jibril running until receiving a termination signal (e.g., `SIGSTOP`).
* **Procfs**\
  Reads data from existing processes in `/proc` at the startup (to include existing processes info).
* **Detect**\
  Provides extensive [detection capabilities](../../execution/detections/).

### Printers <a href="#id-32-printers" id="id-32-printers"></a>

Printers define how and where events are output. They are highly configurable and support various endpoints, including:

* **Stdout:** Prints event data directly to the console for immediate visibility.
* **Varlog:** Outputs events to log files in `/var/log` for persistent storage.

### Events <a href="#id-33-events" id="id-33-events"></a>

Events represent system behaviors or states that Jibril monitors and processes. They are the core of Jibril's detection and response capabilities. Some examples:

* **Network Flows**
  * `jibril:detect:flow`\
    Captures detailed information about active network flows.
*   **Network Policy Drops**

    * `jibril:netpolicy:dropip`\
      Flags traffic dropped due to IP-based policies.
    * `jibril:netpolicy:dropdomain`\
      Flags traffic dropped due to DNS resolutions made to blocked domains.

    > NOTE: Need network policy plugin (`jibril:netpolicy`) to be enabled.
* **File Access:**
  * `jibril:detect:capabilities_modification`\
    Detects changes to file capabilities.
  * `jibril:detect:credentials_files_access`\
    Identifies unauthorized access to sensitive credential files.
  * [Read more ...](../../execution/detections/file-access/)
* **Execution Monitoring:**
  * `jibril:detect:hidden_elf_exec`\
    Detects hidden ELF binary execution.
  * `jibril:detect:binary_executed_by_loader`\
    Tracks executions made by ELF loaders.
  * [Read more ...](../../execution/detections/execution/)
* **Network Activity:**
  * `jibril:detect:net_scan_tool_exec`\
    Flags usage of network scanning utilities.
  * `jibril:detect:net_sniff_tool_exec`\
    Identifies execution of network-sniffing tools.
  * [Read more ...](../../execution/detections/network-peers/)

## <mark style="color:$primary;">Configuration-Driven Behavior</mark> <a href="#id-4-configuration-driven-behavior" id="id-4-configuration-driven-behavior"></a>

***

Jibril’s flexibility comes from its configuration file, which governs how components are enabled and interact. Key configurable elements include:

* **Log Levels**\
  Control verbosity, ranging from minimal output (`fatal`) to detailed debugging (`debug`).
* **Daemon Mode**\
  Run Jibril interactively or as a background service.
* **Profiling and Health Checks**\
  Enable profiling or activate health endpoints for system monitoring.
* **Extensions and Plugins**\
  Select which extensions, plugins, and events to load.
* **Printers**\
  Define where and how data should be output.

These options allow Jibril to integrate seamlessly into various operational environments.

## <mark style="color:$primary;">Why Jibril’s Architecture Works</mark> <a href="#id-5-why-jibrils-architecture-works" id="id-5-why-jibrils-architecture-works"></a>

***

### **Flexibility**

* Configurable plugins, printers, and events
* Enable/disable components based on specific needs
* Tailor monitoring scope to organizational requirements

### **Scalability**

* Seamlessly scales from single systems to enterprise deployments
* Consistent performance across diverse environments
* Resource-efficient even in high-density infrastructures

### **Efficiency**

* eBPF-powered kernel-level data collection minimizes overhead
* Structured userland execution optimizes resource utilization
* Maintains minimal footprint even under heavy monitoring loads

### **Comprehensive Visibility**

* Complete coverage across network, file, and process domains
* Unified view of system activity and security events
* Detailed context for accurate threat assessment

### **Enterprise Integration**

* Ready-to-use connectivity with existing security infrastructure
* Flexible output options for dashboards, SIEM systems, and logs
* API-friendly architecture for custom tool integration

## <mark style="color:$primary;">Conclusion</mark> <a href="#conclusion" id="conclusion"></a>

***

Jibril combines the power of eBPF with a modular, extensible framework to deliver advanced runtime security monitoring. Its architecture balances flexibility, efficiency, and ease of use, making it a robust solution for detecting and responding to threats in modern IT environments. Whether monitoring network flows, detecting file access anomalies, or integrating with GitHub workflows, Jibril offers the tools needed to secure your systems effectively.
