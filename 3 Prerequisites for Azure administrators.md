# AZ-104: Prerequisites for Azure administrators
____

### Apply and monitor infrastructure standards with Azure Policy 

#### Overview: 

##### Introduction:

Good IT governance involves planning your initiatives and setting priorities on a strategic level to help manage and prevent issues. 

You need good governance when: 

* You have multiple engineering teams working in Azure
* You have multiple subscriptions in your tenant
* You have regulatory requirements that must be enforced 
* You want to ensure standards are followed for all IT allocated resources 

Azure provides several tools you can use to enforce and validate your standards, while still allowing your engineering teams to create and own their own resources in the cloud. 

In addition to providing IT standards, you need to be able to monitor your resources and make sure they are responsive and performing properly. 

Learning objectives: 

* Apply policies to control and audit resource creation 
* Learn how role-based security can fine-tune access to your resources 
* Understand Microsoft's policies and privacy guarantees
* Learn how to monitor your resources 


##### Define IT compliance with Azure Policy:

Planning out a consistent cloud infrastructure starts with setting up policy. Your policies will enforce your rules for created resources, so your infrastructure stays compliant with your corporate standards, cost requirements, and any service-level agreements (SLAs) you have with your customers. 

--> Azure Policy - is an Azure service you use to create, assign, and manage policies. These policies enforce different rules and effects over your resources so that those resources stay compliant with your corporate standards and service level agreements. Azure Policy meets this need by evaluating your resources for noncompliance with assigned policies. For example, you might have a policy that allows virtual machines of only a certain size in your environment. After this police is implemented, new and existing resources are evaluated for compliance. With the right type of policy, existing resources can be brought into compliance. 

To control cost we don't want anyone to just be able to create virtual machines(VMs). The administrator of our Azure tenant defines a policy that prohibits the creation of any VM with more than 4 CPUs. Once the policy is implemented, Azure Policy will stop anyone from creating a new VM outside the list of allowed stock keeping units (SKUs). Also, if you try to update an existing VM, it will be checked against policy. Finally, Azure Policy will audit all the existing VMs in our organizations to ensure our policy is enforced. It can audit non-compliant resources, alter the resource properties, or stop the resource from being created. You can even integrate Azure Policy with Azure DevOps, by applying any continuous integration and delivery pipeline policies that affect the pre-deployment and post-deployment of your applications. 

> How are Azure Policy and RBAC different? 

At first glance, it might seem like Azure Policy is a way to restrict access to specific resource types similar to role-based access control (RBAC). However, they solve different problems. RBAC focuses on user actions at different scopes. You might be added to the contributor role for a resource group, allowing you to make changes to anything in the resource group. Azure Policy focuses on resource properties during deployment and for already-existing resources. Azure Policy controls properties such as the types of locations of resources. Unlike RBAC, Azure Policy is a default-allow-and-explicit-deny system. 


##### Create a policy 

The process of creating and implementing an Azure Policy begines with creating a policy definition. Every policy definition has conditions under which it is enforced. And, it has an accompanying effect that takes place if the conditions are met. To apply a policy, you will: 

1. Create a policy definition 
2. Assign a definition to a scope of resources 
3. View policy evaluation results

##### What is a policy definition? 

 A policy definition expresses what to evaluate and what action to take. For example, you could ensure all public websites are secured with HTTPS, prevent a particular storage type from being created, or force a specific version of SQL Server to be used. 

##### Apply an Azure policy:


``` Powershell
# Register the resource provider if it's not already registered 

Register-AzResourceProvider -ProviderNamespace 'Microsoft.PolicyInsights'
```
Once registered the provider, you can now create a policy assignment. 
``` Powershell

# Get a reference to the resource group that will be the scope of the assignment 
$rg - Get-AzResourceGroup -Name '<resourceGroupName>'

# Get a reference to the built-in policy definition that will be assigned 
$definition = Get-AzPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Audit VMs that do not use managed disks' }

# Create the policy assignment with the built-in definition against your resource group 
New-AzPolicyAssignment -Name 'audit-vm-manageddisks' -DisplayName 'Audit VMs without managed disks Assignment' -Scope $rg.ResourceId -PolicyDefinition $definition
```

##### Remove a policy assignment 

You can delete a policy requirements through the portal, or through the PowerShell command `Remove-AzPolicyAssignment` 

```PowerShell
Remove-AzPolicyAssignment -Name 'audi-vm-manageddisks' -Scope '/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>'
```
##### Organize policy with initiatives: 

Managing a few policy definitions is easy, but once you have more than a few you will want to organize them. That's where **initiatives** come in. 

Initiatives work alongside policies in Azure Policy. An initiative definition is a set or group of policy definitions to help track your compliance state for a larger goal. Even if you have a single policy, it is recommended to use initiatives if you anticipate increasing the number of policies over time. 

Like a policy assignment, an initiative assignment is an initiative definition assigned to a specific scope. Initiative assignments reduce the need to make several initiative definitions for each scope. This scope could also range from a management group to a resource group. 

##### Manage access, policies, and compliance across multiple Azure subscriptions: 

##### Define standard resources with Azure Blueprints: 

##### Explore your service compliance with Compliance Manager: 

##### Monitor your service health: 

##### Summary: 

