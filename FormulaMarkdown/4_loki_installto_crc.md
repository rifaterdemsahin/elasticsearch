# Installing Loki on CRC

This guide will walk you through the steps to install Loki on CodeReady Containers (CRC).

## Prerequisites

Before you begin, ensure you have the following:

- CodeReady Containers installed and running
- `oc` CLI tool installed and configured
- Sufficient resources allocated to CRC

## Steps

### 1. Create a New Project

First, create a new project for Loki:

```sh
oc new-project loki
```

### 2. Add the Loki Helm Repository

Add the Loki Helm repository to your Helm configuration:

```sh
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
```

### 3. Install Loki

Install Loki using Helm:

```sh
helm install loki grafana/loki-stack --namespace=loki
```

### 4. Verify the Installation

Check the status of the Loki pods to ensure they are running:

```sh
oc get pods -n loki
```

You should see output similar to:

```
NAME                            READY   STATUS    RESTARTS   AGE
loki-0                          1/1     Running   0          2m
loki-promtail-xxxxx             1/1     Running   0          2m
```

### 5. Access Loki

To access Loki, you can port-forward the Loki service to your local machine:

```sh
oc port-forward svc/loki 3100:3100 -n loki
```

You can now access Loki at `http://localhost:3100`.

## Conclusion

You have successfully installed Loki on CRC. You can now start using Loki to collect and query logs from your applications.

For more information, refer to the [Loki documentation](https://grafana.com/docs/loki/latest/).
