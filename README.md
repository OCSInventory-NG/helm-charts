![Logo-OCS](http://cdn.ocsinventory-ng.org/common/banners/banner300px.png)

# OCS Inventory Helm Chart

## Some Links
  - [ASK question](https://ask.ocsinventory-ng.org)
  - [Website](https://www.ocsinventory-ng.org/?utm_source=github-ocs)
  - [Github](https://github.com/OCSInventory-NG)
  - [OCS Professional](https://ocsinventory-ng.org/?page_id=140&lang=en)

OCS (Open Computers and Software Inventory Next Generation) is an assets management and deployment solution.
Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful.
OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server.

----------

## Assets management

Since 2001, OCS Inventory NG has been looking for making software and hardware more powerful. OCS Inventory NG asks its agents to know the software and hardware composition of every computer or server. OCS Inventory also ask to discover network’s elements which can’t receive an agent. Since the version 2.0, OCS Inventory NG take in charge the SNMP scans functionality.
This functionality’s main goal is to complete the data retrieved from the IP Discover scan. These SNMP scans will allow you to add a lot more informations from your network devices : printers, scanner, routers, computer without agents, …

----------

## Deployment

OCS Inventory NG includes the packet deployment functionality to be sure that all of the softwares environments which are on the network are the same. From the central management server, you can send the packets which will be downloaded with HTTP/HTTPS and launched by the agent on client’s computer. The OCS deployment is configured to make the packets less impactable on the network. OCS is used as a deployment tool on IT stock of more 100 000 devices.

----------

## Get the Chart

### Add Helm repository

```bash
helm repo add ocsinventory https://ocsinventory-ng.github.io/helm-charts
helm repo update
```

### Retrieve the values.yaml 

```bash
wget https://raw.githubusercontent.com/OCSInventory-NG/helm-charts/main/charts/ocsinventory/values.yaml
```

Note : all parameters on values.yaml are explained in the "Values" section of the README

### Installing the Chart

```bash
cd OCSInventory-Helm-Chart
helm -n <namespace> install <release_name> ocsinventory/ocsinventory -f ./values.yaml --create-namespace
```

### Upgrading the Chart

```bash
helm -n <namespace> upgrade <release_name> ocsinventory/ocsinventory -f ./values.yaml
```

### Uninstalling the Chart

```bash
helm uninstall -n <namespace> <release_name>
kubectl delete ns <namespace>
```
