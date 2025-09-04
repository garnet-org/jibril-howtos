---
icon: heart
layout:
  width: default
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
  metadata:
    visible: false
---

# Welcome

<h2 align="center">The Lightweight Runtime Security Agent</h2>

<figure><img src=".gitbook/assets/jibril-logo-simpler.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/garnet.png" alt="" width="188"><figcaption></figcaption></figure>

Jibril is a cutting-edge runtime monitoring and threat detection engine, designed to deliver real-time insights with minimal impact on systems performance. Powered by eBPF, it remains efficient even under heavy event loads exceeding hundreds of thousands of events per second–delivering real-time protection for modern environments from dev to prod.

| <h4><a href="information/theory-behind/new-era.md"><mark style="color:$warning;"><strong>Workload Visibility</strong></mark></a></h4> | <h4><a href="customization/alchemies/"><mark style="color:$warning;">YAML Detection Recipes</mark></a></h4>                | <h4><a href="execution/network-policy.md"><mark style="color:$warning;">Network Policies</mark></a></h4>   |
| ------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| <h4><a href="customization/reactions/configuration.md"><mark style="color:$warning;">GitOps Ready</mark></a></h4>                     | <h4><a href="information/theory-behind/architecture.md"><mark style="color:$warning;">Low Resources Impact</mark></a></h4> | <h4><a href="customization/reactions/"><mark style="color:$primary;">Programable Reactions</mark></a></h4> |
| <h4><a href="information/theory-behind/security-model.md"><mark style="color:$warning;">Deep Cause Context</mark></a></h4>            | <h4><a href="customization/attenuator.md"><mark style="color:$warning;">Incidents Filtered by AI</mark></a></h4>           |                                                                                                            |

{% hint style="info" %}
**Key Benefits**

* **High Performance -** Maintains efficiency even under extensive event loads exceeding hundreds of thousands of events per second.
* **Lower Overhead -** Significantly less overhead than traditional eBPF tools through in-kernel storage delivery and query-driven architecture.
* **Complete Context -** Each detection event provides comprehensive context for deep forensic analysis with tamper-proof data integrity.
* **Detection -** 100+ built-in detection rules available with 2M+ tracked bad reputation domains across multiple threat categories.
* **Seamless Integration -** Flexible output options for SIEM systems, logs, files, and APIs with authenticated channels.
* **Reduced Noise -** AI-powered Attenuator filters false positives and enhances events using private and public LLM models including GPT-4o.
{% endhint %}
