## Creating a Network Watcher and Virtual Network

In this step, we will create two other resources in Azure: the network watcher and a virtual network.

Network watchers are resources in Azure that allow the collection of flow logs from subnets and NICs with network security groups (NSGs) deployed to them. When a virtual network is created in Azure, Azure will automatically deploy a network watcher if one has not been created in that region on that subscription. Azure has a strict limitation of one network watcher per region per subscription.
