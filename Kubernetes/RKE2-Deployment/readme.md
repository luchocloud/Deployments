# RKE2 Installation on Linux

RKE2 is a Kubernetes distribution designed for security, performance, and ease of use.

> This guide is a straightforward and hands-on walkthrough based on my own experience setting up RKE2 for a home lab environment. I put it together to make things easier for myself and anyone going down the same path and hopefully help you dodge some of the headaches and troubleshooting I ran into.

## Server Node Installation ([Official Docs](https://docs.rke2.io/install/quickstart))

- Run the installer

```
curl -sfL https://get.rke2.io | sh -
```
- Enable and start the rke2-server service

```
systemctl enable rke2-server.service
systemctl start rke2-server.service
```
- Configure the environmet to interact with the cluster (Allows use of Kubectl and run Kubernetes commands anywhere)

```
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
export PATH=$PATH:/var7lib/rancher/rke2/bin
```
- Extract the *node-token* for the agent installation

```
cat /var/lib/rancher/rke2/server/node-token
```

## Linux Agent (Worker) Node Installation

- Run the installer

```
curl -sfL https://get.rke2.io | INSTALL_RKE2_TYPE="agent" sh -
```
- Enable the rke2-agent service

```
systemctl enable rke2-agent.service
```
- Configure the rke2-agent service

```
mkdir -p /etc/rancher/rke2/
nano /etc/rancher/rke2/config.yaml
```
- Edit the *config.yaml* file

```
server: https://<DNS name or IP address of the master node>:9345
token: <Token conpied from *node-token file*>
```
- Start the service

```
systemctl start rke2-agent.service
```
- Check the pods and follow logs in case of any errors

```
kubectl get pods
journalctl -u rke2-agent -f
```