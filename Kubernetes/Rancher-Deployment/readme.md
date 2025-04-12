# Install Rancher in 3 different ways
> Rancher is a Kubernetes management tool to deploy and run clusters anywhere and on any provider.

## Option 1: Rancher on a Single Node Using Docker ([Official Docs](https://ranchermanager.docs.rancher.com/getting-started/installation-and-upgrade/other-installation-methods/rancher-on-a-single-node-with-docker))
- **Provision Linux Host**
Provision a single Linux host to launch your Rancher server.
- **Provision Linux Host**
Run the following command for a default installation with Rancher-generated Self-signed Certificate
```
docker run -d --restart=unless-stopped \
  -p 80:80 -p 443:443 \
  --privileged \
  rancher/rancher:latest
```
