---
icon: list-tree
---

# Systemd Service

> Check out Jibril's public recipes repository at [https://github.com/garnet-org/jibril-balag](https://github.com/garnet-org/jibril-balag).

## <mark style="color:$primary;">Obtain Jibril</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```
sudo curl -L -o /usr/bin/jibril https://github.com/garnet-org/jibril-balag/releases/download/v2.5/loader
```

```
sudo chmod +x /usr/bin/jibril
```

```
/usr/bin/jibril --version
```

## <mark style="color:$primary;">Run Jibril as a Systemd Service</mark> <a href="#run-jibril-as-a-systemd-service" id="run-jibril-as-a-systemd-service"></a>

Jibril can be run as a systemd service.

This is the recommended way to run Jibril in staging/production environments. The following steps will guide you through the installation and configuration of Jibril as a systemd service.

### Install the Service <a href="#install-the-service" id="install-the-service"></a>

To install the service, run:

```
sudo -E /usr/bin/jibril --systemd install
```

This command will create:

1. [`/etc/systemd/system/jibril.service`](systemd-config.md)
2. [`/etc/jibril/config.yaml`](../../configuration-file/)
3. [`/etc/jibril/netpolicy.yaml`](../../../execution/network-policy.md)
4. `/etc/jibril/recipes/*.yaml`

The systemd service will be installed, but not enabled yet.

> All the recipes automatically installed in `etc` directory are already [builtin in Jibril ](../../../customization/alchemies/builtin-recipes.md)- with a few other [private recipes](../../../customization/alchemies/builtin-recipes.md#private-recipes). If you chose to execute [Jibril with the alchemies plugin](../../../customization/alchemies/) (allowing you to define your own detection recipes), make sure to have the [alchemies directory](../../../customization/alchemies/create-recipes.md) configured to `/etc/jibril/recipes/`directory AND to have those **recipes disabled** in the [configuration file](../../configuration-file/).
>
> **OR, just use the builtin detection recipes and don't worry about that directory.**

### Edit the Configuration File <a href="#edit-the-configuration-file" id="edit-the-configuration-file"></a>

Edit the configuration file at `/etc/jibril/config.yaml`. The default configuration enables Jibril with most of its plugins and the detection events.

{% hint style="info" %}
<mark style="color:red;">The default configuration should be changed for production environments.</mark>

<mark style="color:red;">Fine-tune the config to enable only the necessary plugins, printers and events.</mark>
{% endhint %}

### Enable the Service <a href="#enable-the-service" id="enable-the-service"></a>

After editing the configuration file, enable the service by running:

```
sudo -E jibril --systemd enable-now
```

This will enable the service to start at boot time AND start the service immediately.

### Check the Service Status <a href="#check-the-service-status" id="check-the-service-status"></a>

To check the status of the service, run:

```
sudo systemctl status jibril
```

### Check the Logs <a href="#check-the-logs" id="check-the-logs"></a>

The `varlog` printer is enabled by default in the configuration file. This means that the JSON events are printed to `/var/log/jibril.out`, while Jibril stdout and stderr are redirected to systemd journal.

To check the logs, run:

```
sudo journalctl -u jibril
```

and to check the events, run:

```
sudo cat /var/log/jibril.out | jq
```

### Disable the Service <a href="#disable-the-service" id="disable-the-service"></a>

God forbid, but if you need to disable the service, run:

```
sudo -E jibril --systemd disable-now
```

This will disable the service from starting at boot time AND stop the service immediately.
