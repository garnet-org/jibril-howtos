---
description: Comprehensive Project Summary
icon: shield-quartered
---

# Jibril Runtime Security

## <mark style="color:$primary;">Project Overview</mark>

***

Jibril is a revolutionary runtime security system that transforms kernel event monitoring through a query-driven eBPF approach, providing comprehensive tracking, advanced querying, and innovative detection in a single cohesive framework with minimal performance impact. Unlike traditional event-streaming models that suffer from ring-buffer overruns and data loss, Jibril utilizes in-kernel maps for efficient event storage with on-demand cached data retrieval.

## Core Architectural Innovation

***

### eBPF-Powered Query System

Jibril's query-driven eBPF approach collects kernel behavioral data with minimal overhead, eliminating performance bottlenecks while maintaining monitoring integrity. The system utilizes interconnected hashed key-value maps with strategic caching to prevent query exhaustion, minimizing context switching and reducing overhead.

### Immutable Data Architecture

The system guarantees forensic integrity with tamper-proof capture through data immutability, creating trustworthy evidence for security investigations. Maps feature cryptographic hashing to prevent unauthorized key generation or modification, with any tampering rendering the system "tainted" for detectability (\*feature unavailable in the free version).

### Modular Component Design

Jibril combines an eBPF loader, eBPF programs, and a userland daemon to monitor, detect, and respond to system behaviors with minimal overhead, emphasizing extensibility through plugins, printers, and events.

## <mark style="color:$primary;">Comprehensive Monitoring Capabilities</mark>

***

### Resource Tracking

Jibril delivers complete observability through exhaustive monitoring of: Identity (Users and Groups), Infrastructure (Machines, Hostnames, Namespaces), Storage (Disks, Filesystems, Volumes, Files), Execution (Containers, Processes, Threads), Communication (Protocols, Domains, Ports, Sockets), and Data Movement (Network Flows).

### Action Visibility

The system records every interaction with system resources including: Lifecycle Events (Create, Destroy), Modification Actions (Truncate, Link, Rename, Open, Close), Data Operations (Read, Write, Seek, Execute), and Advanced Interactions (Memory Map, Sync, Lock).

## <mark style="color:$primary;">Detection Mechanisms</mark>

***

### File Access Monitoring

Jibril maintains comprehensive visibility into every interaction between applications and the filesystem, tracking which processes access which files, what operations they perform, and under what context these actions occur. Using eBPF technology, it monitors file access with minimal performance impact while maintaining visibility even into privileged processes.

### Execution Monitoring

The system monitors all program executions, capturing detailed information about every binary that runs, analyzing command-line arguments for malicious patterns, and evaluating execution context including user privileges, timing patterns, and parent-child process relationships.

### Network Peer Monitoring

Jibril maintains a complete record of all network flows, builds sophisticated relationship graphs connecting processes to connections, preserves DNS resolution chains, and analyzes network peer relationships to identify suspicious patterns and lateral movement attempts.

## <mark style="color:$primary;">Performance and Scalability</mark>

***

### High-Performance Architecture

While standard eBPF tools may drop events at enterprise loads exceeding 50,000 events per second, Jibril maintains consistent performance without data loss through its in-kernel storage delivery. The system shows minimal CPU overhead with no missed events.

### Configurable Resource Management

Jibril utilizes various caches to optimize performance and manage system resources efficiently, with configurable cache sizes for tasks, files, network flows, and domains. Cadence configuration controls evaluation intervals for behavioral pattern analysis, with separate settings for file access, network peers, and network flows.

## <mark style="color:$primary;">Advanced Features</mark>

***

### AI-Powered Analysis (The Attenuator)

The Attenuator leverages cutting-edge AI-powered analysis to examine security events, providing additional context, severity classifications, and false positive determination using models like GPT-4o. It operates in three modes: Amend (adds AI verdict), Reason (adds detailed reasoning), and Block (filters false positives).

### Network Policy Enforcement

The Network Policy Plugin allows users to define and enforce traffic policies based on CIDRs and domain resolutions, supporting advanced configurations for alerting, enforcing, and bypassing traffic rules. It can alert on denied traffic, block traffic based on CIDR rules, and control domain resolution with independent rule operation.

### Dynamic Recipe System (Alchemies)

The Alchemies feature introduces a powerful dynamic recipe generation system allowing users to define detection rules in YAML format instead of relying only on built-in hardcoded recipes. The system supports dynamic loading, hot reload capabilities, built-in recipes, validation, and multiple recipe types for file access, execution, and network peer detections.

### Automated Response System (Reactions)

Reactions transform Jibril from a passive monitoring tool into an active security defense system, enabling immediate programmable responses to security detection events including blocking malicious traffic, terminating suspicious processes, collecting forensic evidence, and isolating compromised systems. The system supports both JavaScript (V8 engine) and shell script execution with comprehensive helper functions for logging, network policy enforcement, process management, and file system operations.

## <mark style="color:$primary;">Extensive Detection Library</mark>

***

### File Access Detection Recipes

Comprehensive detection capabilities including: capabilities modification, code modification through procfs, core pattern access, CPU fingerprinting, credentials files access, filesystem fingerprinting, Java debug/instrument library loading, machine fingerprinting, OS fingerprinting, package repository configuration modification, PAM config modification, shell config modification, SSL certificate access, sudoers modification, and more.

### Execution Detection Recipes

Advanced execution monitoring including: binary execution by loader, code-on-the-fly execution, credential text lookup, denial of service tools, execution from unusual directories, file attribute changes, hidden ELF execution, interpreter shell spawning, network tool executions (file copy, MITM, scanning, sniffing), suspicious tool execution, password usage, webserver execution, and crypto miner detection.

### Network Peer Detection Recipes

Sophisticated network analysis including: adult domain access, algorithmic domains, badware domain access, cloud metadata access, dynamic DNS access, fake domain access, gambling domain access, new domains, phishing domains, piracy domain access, plaintext communication, threat domain access, tracking domain access, and VPN-like domain access.

## <mark style="color:$primary;">Deployment Options</mark>

***

### Installation Methods

Jibril supports multiple deployment approaches: systemd service installation for production environments, command-line execution for testing and development, and Kubernetes DaemonSet deployment for containerized environments with comprehensive configuration options.

### Configuration Flexibility

The system uses a comprehensive YAML configuration file controlling log levels, daemon mode, profiling, health checks, extensions, plugins, events, cadences, and cache sizes, allowing complete customization for specific use cases.

### Integration and Extensibility

### Modular Plugin Architecture

Core extensions include config (userland to eBPF context), data (storage and retrieval logic with virtual maps), and jibril (main extension with multiple plugins including hold, procfs, printers, netpolicy, detect, and configuration plugins).

### Output and Integration

Flexible output options include stdout for immediate visibility, varlog for persistent storage, and extensible printer system supporting logs, files, APIs, and external dashboards with authenticated channels.

## <mark style="color:$primary;">Security and Compliance</mark>

***

### Forensic Integrity

Data immutability guarantees forensic integrity with tamper-proof capture, creating trustworthy evidence for security investigations and maintaining complete audit trails.

### Enterprise Ready

Purpose-built for modern enterprise environments, combining kernel-level monitoring depth with negligible performance impact and compliance-ready features, delivering comprehensive protection for security-conscious organizations.

## <mark style="color:$primary;">Conclusion</mark>

***

Jibril redefines runtime security with its revolutionary approach to kernel event management, collecting, storing, and analyzing system activity with unprecedented efficiency, minimal latency, and tamper-resistant architecture. The system provides unwavering reliability under high loads, complete visibility across entire systems, ironclad security with tamper-evident design, and sustainable performance that scales with demand, setting a new standard for modern security operations.
