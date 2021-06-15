<a href="https://newerton.com" target="_blank" rel="noopener noreferrer">
<img width="100%" src="https://github.com/newerton/codeeducation-repo-images/blob/main/istio.jpg?raw=true" alt="Istio.io"></a>


<h3 align="center">
  Service Mesh with Istio
</h3>

---

## Getting Started

### Documentation

You can find for more details on [istio.io](https://istio.io/) website.

### Requeriments

Docker installed

- Linux: [Install Docker Engine](https://docs.docker.com/engine/install/)

- Windows: [Install Docker Desktop on Windows](https://docs.docker.com/docker-for-windows/install/)


- Mac: [Install Docker Desktop on Mac](https://docs.docker.com/docker-for-mac/install/)

Kubernets with K3D

- K3D: [Installation](https://k3d.io/#installation)

For Windows 10

- WSL2: [Enable and Install the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10)

## Install Istio and Addons

Create cluster

```console
k3d cluster create -p "8000:30000@loadbalancer" --agents 2
```

Set context

```console
kubectl config use-context k3d-k3s-default
```

Install Istio

- [Download Istio](https://istio.io/latest/docs/setup/getting-started/#download)

```console
curl -L https://istio.io/downloadIstio | sh -
```
Access folder

```console
cd istio-[version]
```

Add the istioctl client to your path (Linux or macOS):

```console
export PATH=$PWD/bin:$PATH
```

Install Istio with profile DEFAULT [Instalation Configuration Profile](https://istio.io/latest/docs/setup/additional-setup/config-profiles/)

```console
istioctl install
```

Add a namespace label to instruct Istio to automatically inject Envoy sidecar proxies when you deploy your application later

```console
kubectl label namespace default istio-injection=enabled
```

Apply [Addons](https://github.com/istio/istio/tree/release-1.10/samples/addons) (Grafana, Jaeger, Kiali and Prometheus)

Prometheus

```console
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/addons/prometheus.yaml
```

Jaeger

```console
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/addons/jaeger.yaml
```

Grafana

```console
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/addons/grafana.yaml
```
Kiali

```console
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.10/samples/addons/kiali.yaml
```

Access the Kiali dashboard
```console
istioctl dashboard kiali
```