<h1>
    <img src="https://raw.githubusercontent.com/kgretzky/pwndrop/master/media/pwndrop-logo-512.png" align="left" height="120px" alt="pwndrop logo"/>
    <span>Pwndrop in Kubernetes</span>
</h1>

**Using [pwndrop](https://github.com/kgretzky/pwndrop) on Kubernetes.**
**Based on [linuxserver](https://docs.linuxserver.io/images/docker-pwndrop/) Docker image.**
## Overview
Use this Helm-chart to run pwndrop on k8s (k3s) clusters.

**pwndrop** is a self-deployable file hosting service for sending out red teaming payloads or securely sharing your private files over HTTP and WebDAV.

If you've ever needed to quickly set up an nginx/apache web server to host your files and you were never happy with the limitations of `python -m SimpleHTTPServer`, **pwndrop** is definitely for you!

## Features
* `env` vars for Docker container in `values.yaml`
* Port forwarding (LoadBalancer, NodePort or Ingress-controller port streaming)

```yaml
service:
  type: ClusterIP
  ports:
    - name: http
      port: 80
      targetPort: 8080
      protocol: TCP
    - name: https
      port: 443
      targetPort: 4443
      protocol: TCP
```
You can change (customize) ports in `values.yaml`.
## Installation
### Prerequisites
* Kubernetes or k3s
* Helm install
* `kubectl` configured to authenticate to a Kubernetes cluster with a valid `kubeconfig` file
* Docker on local machine (if you need custom Docker image)
### CLI
1. Clone repo.
```bash
git clone https://github.com/3ayazaya/pwndrop-k8s
cd pwndrop-k8s/charts
```
2. Change `values.yaml` if need in `charts` folder.
3. Install Helm-chart with pwndrop in k8s (k3s) cluster.

```bash
helm install pwndrop pwndrop -f pwndrop/values.yaml -n <namespace> --create-namespace
```
### Helm
1. Add a chart repository.
```bash
helm repo add shmel https://charts.shmel.xyz
```

2. Download `values.yaml` if need.

```bash
helm show values shmel/pwndrop > values.yaml
```
3. Change `values.yaml` if need.
4. Install Helm-chart with pwndrop in k8s (k3s) cluster.

```bash
helm install pwndrop shmel/pwndrop -f values.yaml -n <namespace> --create-namespace
```