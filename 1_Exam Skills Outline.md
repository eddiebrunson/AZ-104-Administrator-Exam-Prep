# Exam Skills Outline 
___ 

### Microsoft Certified: Azure Administrator Associate – Skills Measured

> This document contains the skills measured on the exams associated with this certification. It does not include any upcoming or recent changes that have been made to those skills. For more information about upcoming or recent changes, see the associated exam details page(s).

> NOTE: The bullets that appear below each of the skills measured are intended to illustrate how we are assessing that skill. This list is not definitive or exhaustive.
> NOTE: In most cases, exams do NOT cover preview features, and some features will only be added to an exam when they are GA (General Availability).

### Exam AZ-104: Microsoft Azure Administrator
#### Manage Azure identities and governance (15-20%)
##### Manage Azure AD objects
 create users and groups
 manage user and group properties
 manage device settings
 perform bulk user updates
 manage guest accounts
 configure Azure AD Join
 configure self-service password reset
 NOT: Azure AD Connect; PIM
##### Manage role-based access control (RBAC)
 create a custom role
 provide access to Azure resources by assigning roles
o subscriptions
o resource groups
o resources (VM, disk, etc.)
 interpret access assignments
 manage multiple directories
Manage subscriptions and governance
  configure Azure policies
 configure resource locks
  apply tags
 create and manage resource groups
 o move resources o remove RGs
  manage subscriptions
 configure Cost Management
 configure management groups
Implement and manage storage (10-15%)
Manage storage accounts
   configure network access to storage accounts
 create and configure storage accounts
 generate shared access signature
 manage access keys
 implement Azure storage replication
 configure Azure AD Authentication for a storage account
Manage data in Azure Storage
Configure Azure files and Azure blob storage
   export from Azure job
 import into Azure job
 install and use Azure Storage Explorer
 copy data by using AZCopy
   create an Azure file share
 create and configure Azure File Sync service
 configure Azure blob storage
 configure storage tiers for Azure blobs
Deploy and manage Azure compute resources (25-30%)
 Configure VMs for high availability and scalability
   configure high availability
 deploy and configure scale sets
Automate deployment and configuration of VMs
   modify Azure Resource Manager (ARM) template
 configure VHD template

  deploy from template
 save a deployment as an ARM template
 automate configuration management by using custom script extensions
Create and configure VMs
Create and configure containers
Create and configure Web Apps
   configure Azure Disk Encryption
 move VMs from one resource group to another
 manage VM sizes
 add data discs
 configure networking
 redeploy VMs
   create and configure Azure Kubernetes Service (AKS)
 create and configure Azure Container Instances (ACI)
 NOT: selecting an container solution architecture or product; container registry settings
   create and configure App Service
 create and configure App Service Plans
 NOT: Azure Functions; Logic Apps; Event Grid
Configure and manage virtual networking (30-35%)
Implement and manage virtual networking
   create and configure VNET peering
 configure private and public IP addresses, network routes, network interface, subnets,
and virtual network
Configure name resolution
Secure access to virtual networks
   configure Azure DNS
 configure custom DNS settings
 configure a private or public DNS zone
   create security rules
 associate an NSG to a subnet or network interface
 evaluate effective security rules

  deploy and configure Azure Firewall
 deploy and configure Azure Bastion Service
 NOT: Implement Application Security Groups; DDoS
Configure load balancing
Monitor and troubleshoot virtual networking
 monitor on-premises connectivity
 use Network Performance Monitor
 use Network Watcher
Integrate an on-premises network with an Azure virtual network
   configure Application Gateway
 configure an internal load balancer
 configure load balancing rules
 configure a public load balancer
 troubleshoot load balancing
 NOT: Traffic Manager and FrontDoor and PrivateLink
    troubleshoot external networking
 troubleshoot virtual network connectivity
   create and configure Azure VPN Gateway
 create and configure VPNs
 configure ExpressRoute
 configure Azure Virtual WAN
Monitor and back up Azure resources (10-15%)
Monitor resources by using Azure Monitor
   configure and interpret metrics
 o analyze metrics across subscriptions
  configure Log Analytics
 o implement a Log Analytics workspace o configure diagnostic settings
  query and analyze logs
 o create a query
o save a query to the dashboard o interpret graphs
  set up alerts and actions
 o create and test alerts

o create action groups
o view alerts in Azure Monitor
o analyze alerts across subscriptions
 configure Application Insights
 NOT: Network monitoring
Implement backup and recovery
 configure and review backup reports
 perform backup and restore operations by using Azure Backup
 create a Recovery Services Vault
o use soft delete to recover Azure VMs
 create and configure backup policy
 perform site-to-site recovery by using Azure Site Recovery
 NOT: SQL or HANA