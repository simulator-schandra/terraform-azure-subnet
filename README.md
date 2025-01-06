Azure Subnet Terraform module
=====================================

This module is used to deploy Azure Subnet resource on Azure cloud using Terraform.

Prerequisites
--------------
- [Terraform](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli)
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)

Requirements
------------

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.9.8 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 4.0.1 |


Usage
------

```hcl
terraform {
  required_providers {
    azurerm = {
      source = "hashicorp/azurerm"
      version = "4.0.1"
    }
  }
}

provider "azurerm" {
  features {}
}

module "public_subnet" {
  source                          = "./module/subnet"
  subnet_name                     = ["simulator-sub-pub-1", "simulator-sub-pub-2"]
  rg_name                         = "simulator-rg"
  vnet_name                       = "simulator-vnet"
  subnet_cidr                     = [["10.0.0.0/23"], ["10.0.2.0/23"]]
  default_outbound_access_enabled = true
}

module "private_subnet" {
  source      = "./module"
  subnet_name = ["simulator-sub-pvt-1", "simulator-sub-pvt-2"]
  rg_name     = "simulator-rg"
  vnet_name   = "simulator-vnet"
  subnet_cidr = [["10.0.4.0/23"], ["10.0.6.0/23"]]
}

```

Inputs
------


| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| **rg_name** | Resource group name | `string` | `NA` | yes |
| **vnet_name** | Virtual network name | `string` | `NA` | yes |
| **subnet_name** | Subnet name | `string` | `NA` | yes |
| **subnet_cidr** | Subnet CIDR | `list(string)` | `NA` | yes |
| **default_outbound_access_enabled** | Default outbound internet access for subnet | `bool` | `NA` | no |

Outputs
--------

| Name | Description |
|------|-------------|
| **subnet_ids** | Subnet id's |

Revision History 
----------------

### Contributors

- Created by [Suyash Chandra](https://github.com/suyash1610)