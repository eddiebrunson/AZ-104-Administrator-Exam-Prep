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

Access management occurs at Azure subscription level. This control allows an organization to configure each division of the company in a specific fashion based on their responsibilities and requirements. Planning and keeping rules consistent across subscriptions can be challenging. 

Management groups allow you to order your Azure resources hierarchically into collections, which provide a further level of classification that is above the level of subscriptions. All subscriptions within a management group automatically inherit the conditions applied to the management group. Management groups five you enterprise-grade management at a large scale no matter what type of subscriptions you might have.

![Root Management group](/images/managementgroup.png)

##### Important facts about management groups 

* Any Azure AD user in the organization can create a management group. The creator is given an Owner role assignment. 
* A single Azure AD organization can support 10,000 management groups. 
* A management group tree can support up to six levels of depth not including the Root level or subscription level. 
* Each management group can have many children. 
* WHen your organization creates subscriptions, they are automatically added to the root management group. 

##### Define standard resources with Azure Blueprints: 

Adhering to security or compliance requirements, whether government or industry requirements, can be difficult and time-consuming. To help you with auditing, traceability, and compliance of your deployments, use Azure Blueprint artifacts and tools. 

Just as a blueprint allows an engineer or an architect to sketch a project's design parameters, Azure Blueprints enables cloud architects and central information technology groups to define a repeatable set of Azure resources that implements and adheres to an organization's standards, patterns, and requirements. Azure Blueprints makes it possible for development teams to rapidly build and deploy new environments with the trust they're building within organizational compliance using a set of built-in components, such as networking, to speed up development delivery. 


Azure Blueprints is a declarative way to orchestrate the deployment of various resource templates and other artifacts, such as: 

* Role assignments 
* Policy assignments 
* Azure Resource Manager templates 
* Resource groups 

> Azure Blueprints are also useful in Azure DevOps scenarios, where blueprints are associated with specific build artifacts and release pipelines and can be tracked more rigorously. 

The process of implementing Azure Blueprint consists of the following high-level steps: 

1. Create an Azure Blueprint 
2. Assign in blueprint
3. Track the blueprint assignments 

--> How is it different from Resource Manager templates?

The Azure Blueprints service is designed to help with environment setup. This setup often consists of a set of resource groups, policies, role assignments, and Resource Manager template deployments. 

Nearly everything that you want to include for deployment in Blueprints can be accomplished with a Resource Manager template. A Resource Manager template is a document stored inside Azure Templates Service. The template gets used for deployments of one or more Azure resources, but once those resources deploy, there's no active connection or relationships to the template. 

--> How it's different from Azure Policy

A policy is default-allow and explicit-deny system focused on resource properties during deployment and for already existing resources. It supports cloud governance by validating that resources within a subscription adhere to requirements and standards. 

Including a policy in a blueprint enables the creation of the right pattern or design during assignment of the blueprint. The policy inclusion makes sure that only approved or expected changes can be made to the environment to protect ongoing compliance to the intent of the blueprint. 

A policy can be included as one of many artifacts in a blueprint definition. Blueprints also support using parameters with polices and initiatives. 

##### Explore your service compliance with Compliance Manager: 

Governing your own resources and how they are used is only part of the solution when using a cloud provider. You also have to understand how the provider manages the underlying resources you are building on. 

Microsoft takes this management seriously and provides full transparency with four sources: 

1. Microsoft Privacy Statement 
2. Microsoft Trust Center
3. Service Trust Portal
4. Compliance Manager 

--> The Microsoft privacy statement explains what personal data Microsoft processes, how Microsoft processes it, and for what purposes. 

--> Trust Center is a website resource containing information and details about how Microsoft implements and supports security, privacy, compliance, and transparency in all Microsoft cloud products and services. 

--> The Service Trust Portal (STP) host the Compliance Manager service, and is the Microsoft public site for publishing audit report and other compliance-related information relevant to Microsoft's cloud services. 

--> Compliance Manager is a workflow-based risk assessment dashboard within the Service Trust Portal that enables you to track, assign, and verify your organization's regulatory compliance activities related to Microsoft professional services and Microsoft cloud services such as Microsoft 365, Dynamics 365, and Azure. 

##### Monitor your service health: 

##### Summary: 

