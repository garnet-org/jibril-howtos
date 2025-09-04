---
icon: docker
---

# Docker Container

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
docker pull garnetlabs/jibril:v2.6
```

## <mark style="color:$primary;">Run Jibril using Docker</mark> <a href="#run-jibril-using-command-line-arguments" id="run-jibril-using-command-line-arguments"></a>

```
docker run --rm --name=jibril --privileged \
    --pid=host --cgroupns=host --network=host \
    -e TERM=xterm -v /sys:/sys:ro \
    -v /sys/fs/bpf:/sys/fs/bpf:rw \
    -v /etc/jibril/:/etc/jibril:rw \
    -v /var/log/jibril:/var/log/jibril:rw \
    garnetlabs/jibril:v2.6 --config /etc/jibril/config.yaml
```

> This command is an example of how one can run Jibril using its docker image.

{% hint style="info" %}
For Kubernetes, use the [Kubernetes instructions](../kubernetes/).
{% endhint %}
