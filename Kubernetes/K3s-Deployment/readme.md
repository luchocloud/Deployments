<img src="https://k3s.io/img/k3s-logo-light.svg" width="150" height="150">

# Simple K3s Deployment for Homelab
K3s is one of the best solutions I've found for easily deploying a lightweight Kubernetes cluster.

Read the Docs for [K3s](https://k3s.io/)!

## Requisites 
In this case I used 3 virtual machines and called them:
- Kube-Master (Control Plane - Master Node)
- Worker-One (Agent - Worker Node One)
- Worker-Two (Agent - Worker Node Two)

## - Step One: K3s Install
> Note: Root privilege is needed to setup and configuration.

Install K3s (On the Master node) 
```
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s -
```
Get the node token from the Master Node
```
sudo cat /var/lib/rancher/k3s/server/node-token
```
## - Step Two: K3s Install (Nodes)
Execute this command in each of the nodes
```
curl -sfL https://get.k3s.io | K3S_TOKEN="YOURTOKEN" K3S_URL="https://[your server]:6443" K3S_NODE_NAME="servername" sh - 
```

> Replace **YOURTOKEN** for the one provided in the previous command and **[your server]** by the Master Node IP address. Finally replace **servername** 
