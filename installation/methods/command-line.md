---
icon: square-terminal
---

# Command Line

> Check out Jibril's public recipes repository at [https://github.com/garnet-org/jibril-balag](https://github.com/garnet-org/jibril-balag).

## <mark style="color:$primary;">Obtain Jibril</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```
sudo curl -L -o /usr/bin/jibril https://github.com/garnet-org/jibril-releases/releases/download/v2.6/loader
```

```
sudo chmod +x /usr/bin/jibril
```

```
/usr/bin/jibril --version
```

## <mark style="color:$primary;">Run Jibril using command line</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

Execute jibril directly with the default settings:

```
sudo -E jibril
```

Or create a [configuration file](../configuration-file/#defaults-etc-jibril-config.yaml) and execute jibril with:

```
sudo -E jibril --config ./config.yaml
```
