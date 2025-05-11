<!--<img src="https://k3s.io/img/k3s-logo-light.svg" width="150" height="150">-->

# Simple K3s Deployment for Homelab
K3s is one of the best solutions I've found for easily deploying a lightweight Kubernetes cluster.

>This guide is a simple, practical walkthrough based on my own experience setting up K3s for a home lab environment. I wrote it to help myself and others get up and running faster and hopefully avoid some of the hiccups and troubleshooting I faced along the way.

Read the Docs for [K3s](https://k3s.io/)!

## Requisites 
In this case I used 3 virtual machines and called them:
- Kube-Master (Control Plane - Master Node)
- Worker-One (Agent - Worker Node One)
- Worker-Two (Agent - Worker Node Two)

## - Step One: Export environment variable
```bash
export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
export PATH=$PATH:/usr/local/bin
```
## - Step Two: K3s Install
> Note: Root privilege is needed to setup and configuration.

Install K3s (On the Master node) 
```bash
curl -sfL https://get.k3s.io | K3S_KUBECONFIG_MODE="644" sh -s -
```
Get the node token from the Master Node
```
sudo cat /var/lib/rancher/k3s/server/node-token
```
## - Step Three: K3s Install (Nodes)
Execute this command in each of the nodes
```bash
curl -sfL https://get.k3s.io | K3S_TOKEN="YOURTOKEN" K3S_URL="https://[your server]:6443" K3S_NODE_NAME="servername" sh - 
```
> Delete the "" on the script

> Replace **YOURTOKEN** for the one provided in the previous command and **[your server]** by the Master Node IP address. Finally replace **servername**. 

### If everything works as expected you should see something like this: 

<img src="https://i.ibb.co/BV6C8gJH/Screenshot-from-2025-04-09-20-40-54.png" alt="Screenshot-from-2025-04-09-20-40-54" border="0">

## - Uninstall K3s server (control plane)
```bash
sudo /usr/local/bin/k3s-uninstall.sh
```
## - Uninstall K3s Agents (worker)
```bash
sudo /usr/local/bin/k3s-agent-uninstall.sh
```
