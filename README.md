# SSPPP Azure Key Vault Terraform Module

A Self Service Provisioning Project Placeholder Terraform module to create mysql server compliant with [IT standards](https://confluence.community.veritas.com/x/PRltEQ).

## Usage

```
module "mysql-db" {
  source              = "git::https://stash.veritas.com/scm/bizcloud/ssppp-azure-mysql-terraform-module.git"
  resource_group_name                 = "rg-mysql-dbpass-al"
  virtual_network_name                = "VPO-DPGE-NBU-BIZTOOLS-NBUXDEV-VNET-CENTRAL-US"
  subnet_name                         = "snet-dbpass-al"
  virtual_network_resource_group_name = "RG-VPO-DPGE-NBU-BIZTOOLS-NBUXDEV-Network-CENTRAL-US"
  administrator_login                 = "mysqladmin"
  administrator_login_password        = "mysqlPassword@123"
  firewall_start_ip_address           = "0.0.0.0"
  firewall_end_ip_address             = "0.0.0.0"
}

## Prerequisite Resources

The following resources must already exist in Azure to use this module:

- resource group
- vnet 
- subnet

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.2.0 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | ~> 3.18.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 3.3.2 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_azurerm"></a> [azurerm](#provider\_azurerm) | ~> 3.18.0 |
| <a name="provider_random"></a> [random](#provider\_random) | ~> 3.3.2 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|

| [azurerm_mysql_database.mysql_db](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_database) | resource |
| [azurerm_mysql_firewall_rule.firewall_rules](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_firewall_rule) | resource |
| [azurerm_mysql_server.mysql_server](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/mysql_server) | resource |
| [azurerm_private_endpoint.mysql](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_endpoint) | resource |
| [random_id.mysql](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |
| [azurerm_private_dns_zone.mysql](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_dns_zone)                                           | resource    |
| [azurerm_private_dns_zone_virtual_network_link.mysql](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/private_dns_zone_virtual_network_link) | resource    |

## Inputs

| Name                                                                                                                                                | Description                                                                           | Type     | Default             | Required |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- | -------- | ------------------- | :------: |
| <a name="input_administrator_login"></a> [administrator\_login](#input\_administrator\_login)                                                       | Server Admin name.                                                                    | `string` | n/a                 |   yes    |
| <a name="input_administrator_password"></a> [administrator\_password](#input\_administrator\_password)                                              | Server Admin password.                                                                | `string` | n/a                 |   yes    |
| <a name="input_backup_retention_days"></a> [backup\_retention\_days](#input\_backup\_retention\_days)                                               | Backup retention days.                                                                | `number` | `14`                |    no    |
| <a name="input_geo_redudant_backup_enabled"></a> [geo\_redudant\_backup\_enabled](#input\_geo\_redudant\_backup\_enabled)                           | Enable Geo-Redundant backup.                                                          | `bool`   | `false`             |    no    |
| <a name="input_location"></a> [location](#input\_location)                                                                                          | Azure Location where to provision mysql Server.                                       | `string` | n/a                 |   yes    |
| <a name="input_mysql_server_version"></a> [mysql\_server\_version](#input\_mysql\\_server\_version)                                                 | MySQL Version.                                                                        | `string` | `"8.0"`             |    no    |
| <a name="input_sku_name"></a> [sku\_name](#input\_sku\_name)                                                                                        | MySQL Database Instance Type.                                                         | `string` | `"GP_Gen5_8"`       |    no    |
| <a name="input_storage_mb"></a> [storage\_mb](#input\_storage\_mb)                                                                                  | The max storage allowed for the mysql Server.                                         | `number` | `131072`            |    no    |
| <a name="input_ssl_enforcement_enabled"></a> [ssl\_enforcement\_enabled](#input\_ssl\_enforcement\_enabled)                                         | Specifies if SSL should be enforced on connections.                                   | `bool`   | `true`              |    yes   |
| <a name="input_ssl_minimal_tls_version_enforced"></a> [ssl\_minimal\_tls\_version\_enforced](#input\_ssl\_minimal\_tls\_version\_enforced)          | The minimum TLS version to support on the server.                                     | `string` | `TLS1_2`            |    no    |
| <a name="input_firewall_start_ip_address"></a> [firewall\_start\_ip\_address\](#input\_firewall\_start\_ip\_address)                                | Start ip address of allowed firewall rules.                                           | `string` | n/a                 |    no    |
| <a name="input_firewall_end_ip_address"></a> [firewall\_end\_ip\_address\](#input\_firewall\_end\_ip\_address)                                      | End ip address of allowed firewall rules.                                             | `string` | n/a                 |    no    |
| <a name="input_charset"></a> [charset](#input\_charset)                                                                                             | Charset of the MySQL Database Instance Type.                                          | `string` | `utf8`              |    no    |
| <a name="input_collation"></a> [collation](#input\_collation)                                                                                       | Collation of the MySQL Database Instance Type.                                        | `string` | `utf8_unicode_ci`   |    no    |
| <a name="input_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name)                                                     | Resource Group name where to provision mysql Server.                                  | `string` | n/a                 |   yes    |
| <a name="input_virtual_network_name"></a> [resource\_group\_name](#input\_resource\_group\_name)                                                    | The IT managed Alkira vnet name.                                                      | `string` | n/a                 |   yes    |
| <a name="input_subnet_name"></a> [resource\_group\_name](#input\_resource\_group\_name)                                                             | Subnet name to attach to mysql server.                                                | `string` | n/a                 |   yes    |
| <a name="input_virtual_network_resource_group_name"></a> [resource\_group\_name](#input\_resource\_group\_name)                                     | Resource Group name where Virtual Network is located.                                 | `string` | n/a                 |   yes    |
| <a name="input_db_count"></a> [db\_count](#input\_db\_count)                                                                                        | The number of MySQL Databases that needs to be created on a single MySQL Server.      | `number` | `1`                 |   yes    |

## Outputs

### Outputs

| Name                                                                                                                                                                     | Description                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---------------------------------------------------------------------- |
| <a name="output_mysql_server_fqdn"></a> [MySQL\_server\_fqdn](#output\_MySQ\_server\_fqdn)                                                                               | The FQDN of the MySQ Flexible Server.                                  |
| <a name="output_mysql_server_name"></a> [MySQL\_server\_name](#output\_MySQ\_server\_name)                                                                               | Name of the MySQ Flexible Server.                                      |
| <a name="output_private_dns_zone_name"></a> [private\_dns\_zone\_name](#output\_private\_dns\_zone\_name)                                                                | Private DNS Zone name where MySQ has a record.                         |
| <a name="output_mysql_server_admin_username"></a> [mysql\_server\_admin\_username](#output_mysql_server_admin_username)                                                  | Tags on the Private DNS Zone resource.                                 |
| <a name="output_mysql_db_name"></a> [mysql\_db\_name\_tags](#output\_mysql_\_db\_name)                                                                                   | Tags on the Private DNS Zone resource.                                 |
