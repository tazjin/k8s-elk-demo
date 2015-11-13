Kubernetes ELK demonstration
============================

This repository contains files to demonstrate a simple ELK setup on Kubernetes.

## Launching on Kubernetes

To launch the ELK stack:

1. Ensure `kubectl` is configured to use an appropriate Kubernetes cluster.
2. Launch the ELK ReplicationController: `kubectl create -f elk-rc.yaml`
3. Launch the internal Logstash Service: `kubectl create -f elk-svc-logstash.yaml`
4. Launch the public Kibana Service: `kubectl create -f elk-svc-kibana.yaml`
5. Watch `kubectl get pods` and `kubectl get svc` until the services are up and
   the public IP becomes available.

To launch the demo application:
1. Launch the demo-app ReplicationController: `kubectl create -f demo-rc.yaml`
2. Launch the demo-app public Service: `kubectl create -f demo-svc.yaml`
3. Watch `kubectl get svc` until the service becomes available, then point your
   web browser at it. Logs from this service are sent to Logstash configured
   above.

To demonstrate rolling-updates:
1. Open the `demo-rc.yaml` file.
2. Change all instances of `demo-app-v1` to `demo-app-v2`
3. Change the git-repository revision in volumes from `static-v1` to `static-v2`
4. Start the rolling update:
   `kubectl rolling-update demo-app-v1 demo-app-v2 -f demo-rc.yaml`

## Docker images

There are a few simple Docker images needed for the presentation.

### `docker/elasticsearch`

This image is based of Docker's official `elasticsearch` image with small
configuration changes to listen on external network interfaces.

### `docker/logstash`

This image is based of Docker's official `logstash` image and installs the
[log-courier][] plugin. Configuration is added to use the plugin and to grok
nginx logs.

### `docker/log-courier`

This image is the log-courier client configured to forward logs to the internal
Logstash service. See the configuration file for this service as an example of
KubeDNS usage.

### `docker/nginx`

This image is the nginx web server configured to serve static files from the
volume mounted into the container in the demo-service.

[log-courier]: https://github.com/driskell/log-courier
