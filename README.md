# Security Groups Terraform module for Yandex.Cloud

## Features

* Create Security Group and rules in your VPC
* Output Security Group ID for referencing

Use `ingress_rules_with_cidrs` to add rules with IP address ranges.

Use `ingress_rules_with_sg_ids` to add rules with other SGs as a traffic source.

Use `self` to add rule "self_security_group" for communication within a SG.


### How to configure Terraform for Yandex.Cloud 

- Install [YC CLI](https://cloud.yandex.com/docs/cli/quickstart)
- Add environment variables for terraform auth in Yandex Cloud:
  
```
export YC_TOKEN=$(yc iam create-token)
export YC_CLOUD_ID=$(yc config get cloud-id)
export YC_FOLDER_ID=$(yc config get folder-id)
``` 

### Type

The *type* should always be lowercase as shown below.

#### Allowed `<type>` values:

* **breaking: msg** (a commit that has the text BREAKING CHANGE: at the beginning of its optional body or footer section introduces a breaking API change)
* **chore: msg** (updating build/env/packages, etc; no production code change)
* **ci: msg** (changes to our CI configuration files and scripts )
* **docs: msg** (changes to documentation)
* **feat: msg** (new feature for the user)
* **fix: msg** (bug fix for the user, not a fix to build scripts)
* **refactor: msg** (refactoring production code, eg. renaming a variable)
* **security: msg** (fix security vulnerabilities)
* **style: msg** (formatting, missing semi colons, etc; no functional code change)
* **test: msg** (adding missing tests, refactoring tests; no production code change)

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0.0 |
| <a name="requirement_yandex"></a> [yandex](#requirement\_yandex) | > 0.8 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_yandex"></a> [yandex](#provider\_yandex) | 0.90.0 |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [yandex_vpc_security_group.this](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group) | resource |
| [yandex_vpc_security_group_rule.egress_rules](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group_rule) | resource |
| [yandex_vpc_security_group_rule.ingress_nlb_hc_rule](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group_rule) | resource |
| [yandex_vpc_security_group_rule.ingress_rules_with_cidrs](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group_rule) | resource |
| [yandex_vpc_security_group_rule.ingress_rules_with_sg_ids](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group_rule) | resource |
| [yandex_vpc_security_group_rule.ingress_self_rule](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/resources/vpc_security_group_rule) | resource |
| [yandex_client_config.client](https://registry.terraform.io/providers/yandex-cloud/yandex/latest/docs/data-sources/client_config) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_egress_rules"></a> [egress\_rules](#input\_egress\_rules) | Security group egress rules with CIDRs.<br>  Example:<pre>egress_rules = [<br>  {<br>    protocol       = "ANY"<br>    description    = "To the internet"<br>    v4_cidr_blocks = ["0.0.0.0/0"]<br>  },<br>  ]</pre> | `any` | n/a | yes |
| <a name="input_folder_id"></a> [folder\_id](#input\_folder\_id) | Folder ID where the resources will be created | `string` | `null` | no |
| <a name="input_ingress_rules_with_cidrs"></a> [ingress\_rules\_with\_cidrs](#input\_ingress\_rules\_with\_cidrs) | Security group rules with CIDRs as a source.<br>  Example:<pre>ingress_rules_with_cidrs = [<br>  {<br>    description    = "ssh"<br>    port           = 22<br>    protocol       = "ANY"<br>    v4_cidr_blocks = ["0.0.0.0/0"]<br>  },<br>  {<br>    description    = "ICMP"<br>    v4_cidr_blocks = ["0.0.0.0/0"]<br>    from_port      = 0<br>    to_port        = 65535<br>  },<br>  ]</pre> | `any` | n/a | yes |
| <a name="input_ingress_rules_with_sg_ids"></a> [ingress\_rules\_with\_sg\_ids](#input\_ingress\_rules\_with\_sg\_ids) | Security group rules with other SG-id as a source.<br>  Example:<pre>ingress_rules_with_sg_ids = [<br>  {<br>    protocol          = "ANY"<br>    description       = "Communication with web SG"<br>    security_group_id = "xxx222xxx"<br>  },<br>  ]</pre> | `any` | n/a | yes |
| <a name="input_labels"></a> [labels](#input\_labels) | Set of key/value label pairs to assign. | `map(string)` | `null` | no |
| <a name="input_name"></a> [name](#input\_name) | Security group name | `string` | n/a | yes |
| <a name="input_network_id"></a> [network\_id](#input\_network\_id) | Existing network where resources will be created | `string` | `null` | no |
| <a name="input_nlb_hc"></a> [nlb\_hc](#input\_nlb\_hc) | Allow to communicate with NLB health check servers | `bool` | `false` | no |
| <a name="input_self"></a> [self](#input\_self) | Allow to communicate inside security group | `bool` | `true` | no |
| <a name="input_self_from_port"></a> [self\_from\_port](#input\_self\_from\_port) | Allow to communicate within security group with port from | `number` | `null` | no |
| <a name="input_self_port"></a> [self\_port](#input\_self\_port) | Allow to communicaten within security group with port | `number` | `null` | no |
| <a name="input_self_protocol"></a> [self\_protocol](#input\_self\_protocol) | Allow to communicate within security group with protocol | `string` | `"ANY"` | no |
| <a name="input_self_to_port"></a> [self\_to\_port](#input\_self\_to\_port) | Allow to communicate within security group with port to | `number` | `null` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_id"></a> [id](#output\_id) | Security group ID |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
