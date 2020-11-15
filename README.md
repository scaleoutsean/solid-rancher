# Solid Rancher: Notes on Rancher Labs' Kubernetes with NetApp HCI and SolidFire

Solid Rancher is a repo with personal thoughts and notes about the Rancher Kubernetes solution available on NetApp HCI.

## Table of Content

- [Solid Rancher: Notes on Rancher Labs' Kubernetes with NetApp HCI and SolidFire](#solid-rancher-notes-on-rancher-labs-kubernetes-with-netapp-hci-and-solidfire)
  - [Links](#links)
  - [Planning](#planning)
    - [Networking](#networking)
  - [Deployment](#deployment)
    - [Hybrid Cloud Control vs. DIY](#hybrid-cloud-control-vs-diy)
    - [vCenter Role for Rancher Management Cluster](#vcenter-role-for-rancher-management-cluster)
  - [DR, BC, Backup](#dr-bc-backup)
    - [DR](#dr)
    - [BC](#bc)
    - [Backup](#backup)
  - [Is this some sort of official advice from Rancher Labs or NetApp](#is-this-some-sort-of-official-advice-from-rancher-labs-or-netapp)
  - [License and Trademarks](#license-and-trademarks)

## Resources 

External resources referenced in this document:

- [Awesome SolidFire](https://github.com/scaleoutsean/awesome-solidfire)

## Planning

It's best to read the official docs, of course, but you'll likely have to make choicies within limits of what's supported. Not everything is hard-coded or has a default setting.

### Networking

Which networks to use with vDS? Which with vSS? It's likely that a number of approaches could be supported (check with Support if unsure).

Your Rancher Management Cluster must be able to communicate with the vCenter of the cluster in which it is installed, NetApp HCI Management Node (HCC running on it) as well as with Workload Clusters it manages. It may also need to be able to connect to a backup network, another cluster at the DR site, a gateway to connect to your Public Cloud provider, and so on.

## Deployment

### Hybrid Cloud Control vs. DIY

For NetApp HCI customers HCC is the recommended and supported approach to deploy Rancher on NetApp HCI. For SolidFire customers HCC is available per se, but may not be able to deploy Rancher (your compute nodes where Rancher Kuberntes is deployed cannot be managed by HCC, so that task would be impossible to accomplish in the way it's done on NetApp HCI compute nodes).

### vCenter Role for Rancher Management Cluster

For manual (DIY) deployments, you shouldn't use a vCenter administrator account. The Rancher documentation has a list of minimum vCenter privileges required for Rancher v2.x. Feel free to work by it or (as of v2.5.2) you can use PowerCLI to load [this text file](./files/rancher-vcenter-roles-v2.5.2.txt) to your vCenter. Then you'd create a Rancher deployment account with these privileges. See this ([example](https://documentation.commvault.com/commvault/v11_sp19/article?p=115101.htm) of a PS script template.

## DR, BC, Backup

### DR

You can use SolidFire replication (see Awesome SolidFire) to replicate volumes to a remote site.

### BC

On YouTube you can find a video with demonstration of SolidFire failover and failback in a Trident environment. In essence it's a search-and-replace operation for Trident targets combined with a break-reverse-start sequence for storage replication).

Awesome SolidFire has examples of how Target IQNs differ between clusters.

### Backup

Rancher provides its own "snapshot" feature that can backup cluster configuration. I'd use that over VMware or SolidFire snapshots or backups.

For cluster data, you could use application backups or a 3rd party backup software that can backup K8s containers (see Awesome SolidFire, Backup section).

## Is this some sort of official advice from Rancher Labs or NetApp

No.

## License and Trademarks

solid-rancher by scaleoutSean is licensed under the Do What The F\*ck You Want To Public License (see [LICENSE](LICENSE)) except where noted differently.

The Solid Rancher repository image was derived from "Cowboy Hat" by Charles Rondeau and licensed under Public Domain license.

NetApp, ONTAP, SolidFire, SnapMirror and the marks listed at www.netapp.com/TM are trademarks of NetApp, Inc.
Redhat, Kubernetes, and other brands and marks belong to their respective owners.
