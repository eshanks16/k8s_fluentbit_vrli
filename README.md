# k8s_fluentbit_vrli
FluentBit daemonset for sending k8s logs to vRealize Log Insight

## Purpose
This repository stores details about setting up fluentbit as a Kubernetes Daemonset which pushes logs to vRealize Log Insight syslog port. 

>Note: The Daemonset contains a toleration to allow it to run on control plane nodes.

## Instructions

1. Clone the repository and change directories to k8s_fluentbit_vrli
2. Replace the configuration settings for vRLI in the configmap files.

`Host                 vrli.domain.local`

`Port                 514`


2. Deploy roles/bindings/namespaces

```bash
kubectl apply -f 1-fluentbit-pre.yaml
```

3. Deploy the fluentbit configmap for your CRI
> Note: Only one of these should be deployed. Choose the one that matches your own Container Runtime Interface.

If using CRI or containerd

```bash
kubectl apply -f 2-fluentbit-configmap-containerd.yaml
```

If using Docker

```bash
kubectl apply -f 2-fluentbit-configmap-docker.yaml
```

4. Deploy the Daemonset

```bash
kubectl apply -f 3-fluentbit-daemonset.yaml
```

