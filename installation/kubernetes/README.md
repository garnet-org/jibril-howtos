---
icon: box-open
---

# Kubernetes

## <mark style="color:$primary;">Deploy Jibril on Kubernetes</mark>

To deploy Jibril as a DaemonSet on Kubernetes clusters, use the [`setup-k8s.sh`](kubernetes-script.md) script. This script automatically creates a **Deployment** file with the necessary **ConfigMap**, **DaemonSet**, and related resources.

{% hint style="info" %}
Make sure to use `--dry-run` so it does not apply the deployment automatically.
{% endhint %}

{% hint style="success" %}
Currently almost all development-like Kubernetes distributions (Minikube, Microk8s, ...) are supported, as long as compute nodes are virtual-machines or real hosts.
{% endhint %}

{% hint style="danger" %}
Container based compute nodes distributions, like [Kind](https://kind.sigs.k8s.io/), will make resource consumption bigger and is unsupported for now).
{% endhint %}
