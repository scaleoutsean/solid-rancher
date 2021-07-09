---
layout: default
title: ez-rancher
parent: Deploy
nav_order: 1 
---

As indicated earlier, unless the official "Rancher on NetApp HCI" documentation or NetApp Support tell us differently, Management Clusters should be deployed with HCC. In this section we'll therefore primarily look at other environments such as NetApp SolidFire/eSDS.

In the case you are now wondering what's the difference between a NetApp HCI environment and non-HCI environment with SolidFire, in this context a short answer could be "NetApp HCI is deployed with NDE", which also means that:

- Compute nodes are NetApp HCI H-Series nodes
- Compute nodes run vSphere ESXi hypervisor

**NOTE**: Best do not enable node auto-replace on nodes that participate in node pools that use Trident. Rancher considers replaceable nodes to be ephermal which means PVs attached to those nodes disappear together with the node to which they're attached. I have't tested how this affects Trident-provisioned PVs (maybe changing Trident delete policy would help preserve such PVs.)

## Deploy Rancher in NetApp SolidFire and eSDS Environments

SolidFire and eSDS users should have mNode and HCC available in their environment, but may not be able to deploy Rancher with it. 

The reason is the compute nodes where Rancher Kubernetes is deployed cannot be managed by HCC, so we cannot use HCC to do this the way it's done on NetApp HCI clusters.

### NetApp Trident Helm Chart for Workload Clusters

ez-rancher deploys it by default. You can also add it later. The chart can be found [here](https://github.com/NetApp/ez-rancher-trident-installer).

### Deploy Rancher Management Cluster using ez-rancher

ez-rancher doesn't make networking or other choices for you, so good planning is essential.

ez-rancher can be downloaded [here](https://github.com/NetApp/ez-rancher). Edit config file according to the instructions and run the tool. It takes 15-20 minutes to complete.

YouTube videos of the process (edited to less than 3 minutes each):

- Deploy Management Cluster with ez-rancher: [https://youtu.be/m54PM9dJujE](https://youtu.be/m54PM9dJujE)
- Deploy Workload Cluster with ez-rancher: [https://youtu.be/2CavtI4Hdh8](https://youtu.be/2CavtI4Hdh8)

