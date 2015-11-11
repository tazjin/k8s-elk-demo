Kubernetes ELK demonstration
============================

This repository contains files to demonstrate a simple ELK setup on Kubernetes.

## Launching on Kubernetes

1. Ensure `kubectl` is configured to use an appropriate Kubernetes cluster.
2. Launch the ELK ReplicationController: `kubectl create -f elk-rc.yaml`
3. Launcht ELK Service: `kubectl create -f elk-svc.yaml`
4. Watch `kubectl get pods` and `kubectl get svc` until the services is up and
   the public IP becomes available.

## Docker images

There are a few simple Docker images needed for the presentation.

### `docker/elasticsearch`

This image is based of Docker's official `elasticsearch` image with small
configuration changes to listen on external network interfaces.

### `docker/logstash`

This image is based of Docker's official `logstash` image and installs the
[log-courier][] plugin. Configuration is added to use the plugin and to grok
nginx logs.

[log-courier]: https://github.com/driskell/log-courier
