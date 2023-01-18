# Azure Journey - Learning Experience.

## Welcome

This Bootcamp is for training IT personnel based on the content of the course AZ-900: Azure Fundamentals.

This bootcamp is suitable for IT personnel who are just beginning to work with Azure.

This audience wants to learn about our offerings and get hands-on experience with the product. This bootcamp primarily uses the Azure portal and command line interface to create resources and does not require scripting skills. Students in this course will gain confidence to take other role-based courses and certifications, such as Azure Developers. This course combines lecture, demonstrations, and hands-on labs. This course will also help prepare someone for the AZ-900 exam.

## Requirements

- **[Azure Account](https://docs.google.com/document/d/1XEkiGWUC4_AzngZQLQnVt8yWCb3dft1HzXglUnJcJzM/edit)** 
- **[Azure Devops Account](https://docs.google.com/document/d/12tL1KMNMq3IPNkeSPOVNTpzk0irfMFLNu68BLeUn-sI/edit?usp=sharing)** 
- **Hands-on Labs**

  - Install Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

- **Install VS Code**

```azurecli-interactive
brew install xcodegen
xcode-select --install
```

- **Install Powershell**

```azurecli-interactive
brew install --cask powershell
```

- **Install Azure CLI**

```azurecli-interactive
brew update && brew install azure-cli
```

## About the AZ-900 BOOTCAMP

This bootcamp should help you understand what to expect on the exam and includes a summary of the topics the exam might cover and links to additional resources.

Exam AZ-900: Microsoft Azure Fundamentals – Skills Measured

| STUDY AREAS | WEIGHTS|
| --- | --- |
| Describe cloud concepts | 25-30% |
| Describe Azure architecture and services | 35-40% |
| Describe Azure management and governance | 30-35% | 

## Describe cloud concepts (25–30%)

### [Describe cloud computing](M1/01/README.md)

  * Define cloud computing
  * Describe the shared responsibility model
  * Define cloud models, including public, private, and hybrid
  * Identify appropriate use cases for each cloud model
  * Describe the consumption-based model
  * Compare cloud pricing models

### [Describe the benefits of using cloud services](M1/02/README.md)

  * Describe the benefits of high availability and scalability in the cloud
  * Describe the benefits of reliability and predictability in the cloud
  * Describe the benefits of security and governance in the cloud
  * Describe the benefits of manageability in the cloud

### [Describe cloud service types](M1/03/README.md)

  * Describe infrastructure as a service (IaaS)
  * Describe platform as a service (PaaS)
  * Describe software as a service (SaaS)
  * Identify appropriate use cases for each cloud service (IaaS, PaaS, SaaS)

## Describe Azure architecture and services (35–40%)

### [Describe the core architectural components of Azure](M2/01/README.md)

  * Describe Azure regions, region pairs, and sovereign regions
  * Describe availability zones
  * Describe Azure datacenters
  * Describe Azure resources and resource groups
  * Describe subscriptions
  * Describe management groups
  * Describe the hierarchy of resource groups, subscriptions, and management groups

### [Describe Azure compute and networking services](M2/02/README.md)

  * Compare compute types, including container instances, virtual machines (VMs), and functions
  * Describe VM options, including Azure Virtual Machines, Azure Virtual Machine Scale Sets, availability sets, and Azure Virtual Desktop
  * Describe resources required for virtual machines
  * Describe application hosting options, including the Web Apps feature of Azure App Service, containers, and virtual machines
  * Describe virtual networking, including the purpose of Azure Virtual Networks, Azure virtual subnets, peering, Azure DNS, Azure VPN Gateway, and Azure ExpressRoute
  * Define public and private endpoints

### [Describe Azure storage services](M2/03/README.md)

  * Compare Azure storage services
  * Describe storage tiers
  * Describe redundancy options
  * Describe storage account options and storage types
  * Identify options for moving files, including AzCopy, Azure Storage Explorer, and Azure File Sync
  * Describe migration options, including Azure Migrate and Azure Data Box

### [Describe Azure identity, access, and security](M2/04/README.md)

  * Describe directory services in Azure, including Microsoft Azure Active Directory (Azure AD), part of Microsoft Entra and Azure Active Directory Domain Services (Azure AD DS)
  * Describe authentication methods in Azure, including single sign-on (SSO), multifactor authentication, and passwordless
  * Describe external identities and guest access in Azure
  * Describe Conditional Access in Microsoft Azure Active Directory (Azure AD), part of Microsoft Entra
  * Describe Azure role-based access control (RBAC)
  * Describe the concept of Zero Trust
  * Describe the purpose of the defense in depth model
  * Describe the purpose of Microsoft Defender for Cloud

## Describe Azure management and governance (30–35%)

### [Describe cost management in Azure](M3/01/README.md)

  * Describe factors that can affect costs in Azure
  * Compare the Pricing calculator and the Total Cost of Ownership (TCO) calculator
  * Describe the Azure Cost Management and Billing tool
  * Describe the purpose of tags

### [Describe features and tools in Azure for governance and compliance](M3/02/README.md)

  * Describe the purpose of Azure Blueprints
  * Describe the purpose of Azure Policy
  * Describe the purpose of resource locks
  * Describe the purpose of the Service Trust Portal

### [Describe features and tools for managing and deploying Azure resources](M3/03/README.md)

  * Describe the Azure portal
  * Describe Azure Cloud Shell, including Azure CLI and Azure PowerShell
  * Describe the purpose of Azure Arc
  * Describe Azure Resource Manager and Azure Resource Manager templates (ARM templates)

### [Describe monitoring tools in Azure](M3/04/README.md)

  * Describe the purpose of Azure Advisor
  * Describe Azure Service Health
  * Describe Azure Monitor, including Log Analytics, Azure Monitor alerts, and Application Insights