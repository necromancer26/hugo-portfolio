---
title: "IaC Terraform 🌏 on Azure 🔷"
description: "IaC Terraform 🌏 on Azure 🔷"
date: 2023-07-28T22:44:23+01:00
draft: true
---

**Khalil Assef CHETTAOUI 4 ARCTIC 5**
the following Lab has been conducted on a 
*on a MacOS  environment, ZSH as shell, ITerm2 as terminal, homebrew as a package manager*
i hope this documentation provides help for future students with MacOS environment
# Installation ✅
## Installing Terraform on host machine
`brew tap hashicorp/tap`
`brew install hashicorp/tap/terraform`
`terraform -version`
output
```
Terraform v1.3.8
on darwin_arm64

Your version of Terraform is out of date! The latest version
is 1.3.9. You can update by downloading from https://www.terraform.io/downloads.html
```
## Installing Azure Cli
`brew update && brew install azure-cli`
`az version`
output
```
{
  "azure-cli": "2.45.0",
  "azure-cli-core": "2.45.0",
  "azure-cli-telemetry": "1.0.8",
  "extensions": {}
}
```
then we proceed to login through the cli
```
[
  {
    "cloudName": "AzureCloud",
    "homeTenantId": "836cc30b-3430-499a-a9ae-92fd7fea5098",
    "id": "92445f10-b3aa-4eae-90ca-1810e2733e30",
    "isDefault": true,
    "managedByTenants": [],
    "name": "Azure for Students",
    "state": "Enabled",
    "tenantId": "836cc30b-3430-499a-a9ae-92fd7fea5098",
    "user": {
      "name": "khalilassef.chettaoui@esprit.tn",
      "type": "user"
    }
  }
]
```
account list
`az account list --query "[?user.name=='khalilassef.chettaoui@esprit.tn'].{Name:name,ID:id,Default:isDefault}" --output table`
=> Output:
```
Name                ID                                    Default
------------------  ------------------------------------  ---------
Azure for Students  92445f10-b3aa-4eae-90ca-1810e2733e30  True
```
+ Creation service :
`az ad sp create-for-rbac --name terraformSP --role Contributor`
=> Output (error):
`Usage error: To create role assignments, specify both --role and --scopes.`
+ To fix this issue
`az ad sp create-for-rbac --name terraformSP --role Contributor --scopes /subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30`
=> Output :
```
The output includes credentials that you must protect. Be sure that you do not include these credentials in your code or check the credentials into your source control. For more information, see https://aka.ms/azadsp-cli
{
  "appId": "c1f37b0a-4e41-4c3b-8079-51ee9eadd143",
  "displayName": "terraformSP",
  "password": "****************",
  "tenant": "836cc30b-3430-499a-a9ae-92fd7fea5098"
}
```
+ Subscription list:
`az account subscription list`
=> Output:
```
[
  {
    "authorizationSource": "RoleBased",
    "displayName": "Azure for Students",
    "id": "/subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30",
    "state": "Enabled",
    "subscriptionId": "92445f10-b3aa-4eae-90ca-1810e2733e30",
    "subscriptionPolicies": {
      "locationPlacementId": "Public_2014-09-01",
      "quotaId": "AzureForStudents_2018-01-01",
      "spendingLimit": "On"
    }
  }
]
```
defining environment variable on zsh for macos
```
➜ ~ export ARM_SUBSCRIPTION_ID="92445f10-b3aa-4eae-90ca-1810e2733e30"
➜ ~ export ARM_TENANT_ID="836cc30b-3430-499a-a9ae-92fd7fea5098"
➜ ~ export ARM_CLIENT_ID="c1f37b0a-4e41-4c3b-8079-51ee9eadd143"
➜ ~ export ARM_CLIENT_SECRET="****************"
```
# Terraforming the environment 🌱
after creating main.tf variables.tf and output.tf
`terraform init`
=> output
```
Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/random from the dependency lock file
- Reusing previous version of hashicorp/azurerm from the dependency lock file
- Using previously-installed hashicorp/random v3.4.3
- Using previously-installed hashicorp/azurerm v2.99.0

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure...
... 
```
`➜ azure-terraform terraform validate
returns
`Success! The configuration is valid.`
after adding credentials to main.tf and following the documentation it has come to my knowledge that there's a section missing in the provided lab on google classroom
indeed it is not mentioning the importance of this section for the following steps as i was unable to go through `terraform plan` without errors here is the missing section
```
terraform { 
	required_providers { 
	azurerm = { 
		source = "hashicorp/azurerm" 
		version = "~>2.0" 
		} 
	} 
} 
provider "azurerm" { 
	features {} 
	subscription_id = "<azure_subscription_id>" 
	tenant_id = "<azure_subscription_tenant_id>" 
	client_id = "<service_principal_appid>" 
	client_secret = "<service_principal_password>" 
} 
	# Rest of the code goes here
```
after correcting this issue i applied this command that finally worked
`terraform plan`
returning
```
Success! The configuration is valid.

➜ azure-terraform terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.rg will be created
  + resource "azurerm_resource_group" "rg" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = (known after apply)
    }

  # random_pet.rg-name will be created
  + resource "random_pet" "rg-name" {
      + id        = (known after apply)
      + length    = 2
      + prefix    = "rg"
      + separator = "-"
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + resource_group_name = (known after apply)

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if you run "terraform apply" now.
```
with the command terraform apply we apply the changes
`terraform apply`
returning success
```
Terraform used the selected providers to generate the following execution plan.
Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

  # azurerm_resource_group.rg will be created
  + resource "azurerm_resource_group" "rg" {
      + id       = (known after apply)
      + location = "eastus"
      + name     = (known after apply)
    }

  # random_pet.rg-name will be created
  + resource "random_pet" "rg-name" {
      + id        = (known after apply)
      + length    = 2
      + prefix    = "rg"
      + separator = "-"
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + resource_group_name = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

random_pet.rg-name: Creating...
random_pet.rg-name: Creation complete after 0s [id=rg-suited-ibex]
azurerm_resource_group.rg: Creating...
azurerm_resource_group.rg: Creation complete after 2s [id=/subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30/resourceGroups/rg-suited-ibex]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

Outputs:

resource_group_name = "rg-suited-ibex"
```
the ressource group was created with the screenshot
`terraform state list`
returns
```
azurerm_resource_group.rg 
random_pet.rg-name
```
to delete the created ressources 
`terraform destroy`
```
random_pet.rg-name: Refreshing state... [id=rg-suited-ibex]
azurerm_resource_group.rg: Refreshing state... [id=/subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30/resourceGroups/rg-suited-ibex]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  - destroy

Terraform will perform the following actions:

  # azurerm_resource_group.rg will be destroyed
  - resource "azurerm_resource_group" "rg" {
      - id       = "/subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30/resourceGroups/rg-suited-ibex" -> null
      - location = "eastus" -> null
      - name     = "rg-suited-ibex" -> null
      - tags     = {} -> null
    }

  # random_pet.rg-name will be destroyed
  - resource "random_pet" "rg-name" {
      - id        = "rg-suited-ibex" -> null
      - length    = 2 -> null
      - prefix    = "rg" -> null
      - separator = "-" -> null
    }

Plan: 0 to add, 0 to change, 2 to destroy.

Changes to Outputs:
  - resource_group_name = "rg-suited-ibex" -> null

Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

azurerm_resource_group.rg: Destroying... [id=/subscriptions/92445f10-b3aa-4eae-90ca-1810e2733e30/resourceGroups/rg-suited-ibex]
azurerm_resource_group.rg: Still destroying... [id=/subscriptions/92445f10-b3aa-4eae-90ca-...e2733e30/resourceGroups/rg-suited-ibex, 1m10s elapsed]
...
azurerm_resource_group.rg: Destruction complete after 1m20s
random_pet.rg-name: Destroying... [id=rg-suited-ibex]
random_pet.rg-name: Destruction complete after 0s

Destroy complete! Resources: 2 destroyed.
```
# Terraforming an instance of a VM ☁️💻
after creating the main.tf inside a directory that i named terraform-instance as described in the homework we proceed to do terraform init 
which returns a success message
```
Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.
```
we check the syntaxt with `terraform validate` then `terraform plan`
which generates a long success output as shown on the screenshot
the last output of the `terraform apply` is
```
Apply complete! Resources: 11 added, 0 changed, 0 destroyed.

Outputs:

tls_private_key = <sensitive>
```
# Thank you ✨
This has been a very interesting journey, and i'm grateful for all the effort that was put into the tutoring of this course.
I hope the future promotions will find it as fruitful and useful.
**Good Bye**