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

```
PS C:\Users\Pexabo> crc stop
INFO Stopping kubelet and all containers...
WARN Failed to stop all OpenShift containers.
Shutting down VM...
INFO Stopping the instance, this may take a few minutes...
Stopped the instance
PS C:\Users\Pexabo> crc start
WARN A new version (2.42.0) has been published on https://developers.redhat.com/content-gateway/file/pub/openshift-v4/clients/crc/2.42.0/crc-windows-installer.zip
INFO Using bundle path C:\Users\Pexabo\.crc\cache\crc_hyperv_4.16.7_amd64.crcbundle
INFO Checking minimum RAM requirements
INFO Check if Podman binary exists in: C:\Users\Pexabo\.crc\bin\oc
INFO Checking if running in a shell with administrator rights
INFO Checking Windows release
INFO Checking Windows edition
INFO Checking if Hyper-V is installed and operational
INFO Checking if Hyper-V service is enabled
INFO Checking if crc-users group exists
INFO Checking if current user is in crc-users and Hyper-V admins group
INFO Checking if vsock is correctly configured
INFO Checking if the win32 background launcher is installed
INFO Checking if the daemon task is installed
INFO Checking if the daemon task is running
INFO Checking admin helper service is running
INFO Checking SSH port availability
INFO Loading bundle: crc_hyperv_4.16.7_amd64...
INFO Starting CRC VM for openshift 4.16.7...
INFO CRC instance is running with IP 127.0.0.1
INFO CRC VM is running
INFO Updating authorized keys...
INFO Check internal and public DNS query...
INFO Check DNS query from host...
INFO Verifying validity of the kubelet certificates...
INFO Starting kubelet service
INFO Waiting for kube-apiserver availability... [takes around 2min]
INFO Waiting until the user's pull secret is written to the instance disk...
INFO Starting openshift instance... [waiting for the cluster to stabilize]
INFO Operator network is progressing
INFO 3 operators are progressing: dns, image-registry, ingress
INFO All operators are available. Ensuring stability...
INFO Operators are stable (2/3)...
INFO Operators are stable (3/3)...
INFO Adding crc-admin and crc-developer contexts to kubeconfig...
Started the OpenShift cluster.

The server is accessible via web console at:
  https://console-openshift-console.apps-crc.testing

Log in as administrator:
  Username: kubeadmin
  Password: VTACN-3jBFj-Unph2-V4QEQ

Log in as user:
  Username: developer
  Password: developer

Use the 'oc' command line interface:
  PS> & crc oc-env | Invoke-Expression
  PS> oc login -u developer https://api.crc.testing:6443
PS C:\Users\Pexabo> oc login --token=sha256~Rzq3EM5KHsYV2JICsDD8aqyDags58N0w9V0N7zf-O4M --server=https://api.crc.testing:6443
Logged into "https://api.crc.testing:6443" as "kubeadmin" using the token provided.

You have access to 66 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "default".
PS C:\Users\Pexabo> oc new-project loki
Now using project "loki" on server "https://api.crc.testing:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.43 -- /agnhost serve-hostname

PS C:\Users\Pexabo>
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
