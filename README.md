# Solid Rancher: Notes on Rancher Kubernetes with NetApp HCI and SolidFire

- [Solid Rancher: Notes on Rancher Kubernetes with NetApp HCI and SolidFire](#solid-rancher-notes-on-rancher-kubernetes-with-netapp-hci-and-solidfire)
  - [vCenter Role for Rancher Management Cluster](#vcenter-role-for-rancher-management-cluster)
  - [Is this some sort of official advice from Rancher Labs or NetApp](#is-this-some-sort-of-official-advice-from-rancher-labs-or-netapp)
  - [License and Trademarks](#license-and-trademarks)

## vCenter Role for Rancher Management Cluster

For manual DIY deployment, you shouldn't use the administrator account. The Rancher documentation has a list of minimum vCenter privileges required for Rancher v2.x. Feel free to work by it or (as of v2.5.2) you can use PowerCLI to load [this text file](./files/rancher-vcenter-roles-v2.5.2.txt) to your vCenter. Then you'd create a Rancher deployment account with these privileges. 

## Is this some sort of official advice from Rancher Labs or NetApp

Hell no.

## License and Trademarks

solid-rancher by scaleoutSean is licensed under the Do What The F*ck You Want To Public License (see [LICENSE](LICENSE)) except where noted differently.

The Solid Rancher repository image was derived from "Cowboy Hat" by Charles Rondeau and licensed under Public Domain license.

NetApp, ONTAP, SolidFire, SnapMirror and the marks listed at www.netapp.com/TM are trademarks of NetApp, Inc.
Redhat, Kubernetes, and other brands and marks belong to their respective owners.
