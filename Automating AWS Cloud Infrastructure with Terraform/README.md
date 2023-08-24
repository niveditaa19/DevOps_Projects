Create an EC2 instance, deploy on a custom VPC and custom subnet and assign a public IP address. Deploy in such a way that you won't only SSH into the server and make changes to it, but as well automatically set a webserver to run on it in order to handle web traffic.

What you will need:

**• AWS account • Linux • Any Source Code Editor**

**STEPS**

1.Create a Key Pair
2.Create a VPC
3.Create an Internet Gateway
4.Create a custom Route Table
5.Create a Subnet
6.Associate subnet with Route Table
7.Create a Security Group to allow ports 22, 80 and 443
8.Create a network interface with an IP in a subnet that was created in step 5
9.Assign an Elastic IP address to the network interface created in step 8
10.Create an Ubuntu server and install/enable Apache2

**After adding this main.tf file to your pwd execute the below terraform commands:**

## 1.terraform init : Prepare your working directory for other commands
**Output of this command will look like this :**

**vagrant@ubuntu-bionic:~$ terraform init**

Initializing the backend...

Initializing provider plugins...
- Finding latest version of hashicorp/aws...
- Installing hashicorp/aws v5.13.1...
- Installed hashicorp/aws v5.13.1 (signed by HashiCorp)

Terraform has created a lock file .terraform.lock.hcl to record the provider
selections it made above. Include this file in your version control repository
so that Terraform can guarantee to make the same selections by default when
you run "terraform init" in the future.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands

## 2.terraform validate : Check whether the configuration is valid
**Output of this command would look like this:**

**vagrant@ubuntu-bionic:~$ terraform validate**
Success! The configuration is valid, but there were some validation warnings as shown above.

## 3.terraform fmt :  Reformat your configuration in the standard style
**Output of this command would look like this:**

**vagrant@ubuntu-bionic:~$ terraform fmt**
main.tf

## 4.terraform plan :
**Output of this command would look like this:**
**vagrant@ubuntu-bionic:~$ terraform plan**

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
  + create

Terraform will perform the following actions:

   aws_eip.one will be created
  + resource "aws_eip" "one" {
      + allocation_id             = (known after apply)
      + associate_with_private_ip = "10.0.1.50"
      + association_id            = (known after apply)
      + carrier_ip                = (known after apply)
      + customer_owned_ip         = (known after apply)
      + domain                    = (known after apply)
      + id                        = (known after apply)
      + instance                  = (known after apply)
      + network_border_group      = (known after apply)
      + network_interface         = (known after apply)
      + private_dns               = (known after apply)
      + private_ip                = (known after apply)
      + public_dns                = (known after apply)
      + public_ip                 = (known after apply)
      + public_ipv4_pool          = (known after apply)
      + tags_all                  = (known after apply)
      + vpc                       = true
    }

   aws_instance.web-server-instance will be created
  + resource "aws_instance" "web-server-instance" {
      + ami                                  = "ami-053b0d53c279acc90"
      + arn                                  = (known after apply)
      + associate_public_ip_address          = (known after apply)
      + availability_zone                    = "us-east-1a"
      + cpu_core_count                       = (known after apply)
      + cpu_threads_per_core                 = (known after apply)
      + disable_api_stop                     = (known after apply)
      + disable_api_termination              = (known after apply)
      + ebs_optimized                        = (known after apply)
      + get_password_data                    = false
      + host_id                              = (known after apply)
      + host_resource_group_arn              = (known after apply)
      + iam_instance_profile                 = (known after apply)
      + id                                   = (known after apply)
      + instance_initiated_shutdown_behavior = (known after apply)
      + instance_lifecycle                   = (known after apply)
      + instance_state                       = (known after apply)
      + instance_type                        = "t3.micro"
      + ipv6_address_count                   = (known after apply)
      + ipv6_addresses                       = (known after apply)
      + key_name                             = "terraform-projects"
      + monitoring                           = (known after apply)
      + outpost_arn                          = (known after apply)
      + password_data                        = (known after apply)
      + placement_group                      = (known after apply)
      + placement_partition_number           = (known after apply)
      + primary_network_interface_id         = (known after apply)
      + private_dns                          = (known after apply)
      + private_ip                           = (known after apply)
      + public_dns                           = (known after apply)
      + public_ip                            = (known after apply)
      + secondary_private_ips                = (known after apply)
      + security_groups                      = (known after apply)
      + spot_instance_request_id             = (known after apply)
      + subnet_id                            = (known after apply)
      + tags                                 = {
          + "name" = "web-server"
        }
      + tags_all                             = {
          + "name" = "web-server"
        }
      + tenancy                              = (known after apply)
      + user_data                            = "4996c924ab79a28d9908039da12d51649830e063"
      + user_data_base64                     = (known after apply)
      + user_data_replace_on_change          = false
      + vpc_security_group_ids               = (known after apply)

      + network_interface {
          + delete_on_termination = false
          + device_index          = 0
          + network_card_index    = 0
          + network_interface_id  = (known after apply)
        }
    }

  # aws_internet_gateway.gw will be created
  + resource "aws_internet_gateway" "gw" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "main"
        }
      + tags_all = {
          + "Name" = "main"
        }
      + vpc_id   = (known after apply)
    }

  aws_network_interface.web-server-nic will be created
  + resource "aws_network_interface" "web-server-nic" {
      + arn                       = (known after apply)
      + id                        = (known after apply)
      + interface_type            = (known after apply)
      + ipv4_prefix_count         = (known after apply)
      + ipv4_prefixes             = (known after apply)
      + ipv6_address_count        = (known after apply)
      + ipv6_address_list         = (known after apply)
      + ipv6_address_list_enabled = false
      + ipv6_addresses            = (known after apply)
      + ipv6_prefix_count         = (known after apply)
      + ipv6_prefixes             = (known after apply)
      + mac_address               = (known after apply)
      + outpost_arn               = (known after apply)
      + owner_id                  = (known after apply)
      + private_dns_name          = (known after apply)
      + private_ip                = (known after apply)
      + private_ip_list           = (known after apply)
      + private_ip_list_enabled   = false
      + private_ips               = [
          + "10.0.1.50",
        ]
      + private_ips_count         = (known after apply)
      + security_groups           = (known after apply)
      + source_dest_check         = true
      + subnet_id                 = (known after apply)
      + tags_all                  = (known after apply)
    }

   aws_route_table.my_route_table will be created
  + resource "aws_route_table" "my_route_table" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = [
          + {
              + carrier_gateway_id         = ""
              + cidr_block                 = ""
              + core_network_arn           = ""
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = (known after apply)
              + ipv6_cidr_block            = "::/0"
              + local_gateway_id           = ""
              + nat_gateway_id             = ""
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
          + {
              + carrier_gateway_id         = ""
              + cidr_block                 = "0.0.0.0/0"
              + core_network_arn           = ""
              + destination_prefix_list_id = ""
              + egress_only_gateway_id     = ""
              + gateway_id                 = (known after apply)
              + ipv6_cidr_block            = ""
              + local_gateway_id           = ""
              + nat_gateway_id             = ""
              + network_interface_id       = ""
              + transit_gateway_id         = ""
              + vpc_endpoint_id            = ""
              + vpc_peering_connection_id  = ""
            },
        ]
      + tags             = {
          + "Name" = "routetable"
        }
      + tags_all         = {
          + "Name" = "routetable"
        }
      + vpc_id           = (known after apply)
    }

   aws_route_table_association.a will be created
  + resource "aws_route_table_association" "a" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

   aws_security_group.allow_web_traffic will be created
  + resource "aws_security_group" "allow_web_traffic" {
      + arn                    = (known after apply)
      + description            = "Allow TLS inbound traffic"
      + egress                 = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = false
              + to_port          = 0
            },
        ]
      + id                     = (known after apply)
      + ingress                = [
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = "HTTP"
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = "HTTPS"
              + from_port        = 443
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 443
            },
          + {
              + cidr_blocks      = [
                  + "0.0.0.0/0",
                ]
              + description      = "SSH"
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
        ]
      + name                   = "allow_web_traffic"
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags                   = {
          + "Name" = "allow_web"
        }
      + tags_all               = {
          + "Name" = "allow_web"
        }
      + vpc_id                 = (known after apply)
    }

   aws_subnet.main_subnet will be created
  + resource "aws_subnet" "main_subnet" {
      + arn                                            = (known after apply)
      + assign_ipv6_address_on_creation                = false
      + availability_zone                              = "us-east-1a"
      + availability_zone_id                           = (known after apply)
      + cidr_block                                     = "10.0.1.0/24"
      + enable_dns64                                   = false
      + enable_resource_name_dns_a_record_on_launch    = false
      + enable_resource_name_dns_aaaa_record_on_launch = false
      + id                                             = (known after apply)
      + ipv6_cidr_block_association_id                 = (known after apply)
      + ipv6_native                                    = false
      + map_public_ip_on_launch                        = false
      + owner_id                                       = (known after apply)
      + private_dns_hostname_type_on_launch            = (known after apply)
      + tags                                           = {
          + "Name" = "Main"
        }
      + tags_all                                       = {
          + "Name" = "Main"
        }
      + vpc_id                                         = (known after apply)
    }

   aws_vpc.my_vpc will be created
  + resource "aws_vpc" "my_vpc" {
      + arn                                  = (known after apply)
      + cidr_block                           = "10.0.0.0/16"
      + default_network_acl_id               = (known after apply)
      + default_route_table_id               = (known after apply)
      + default_security_group_id            = (known after apply)
      + dhcp_options_id                      = (known after apply)
      + enable_dns_hostnames                 = (known after apply)
      + enable_dns_support                   = true
      + enable_network_address_usage_metrics = (known after apply)
      + id                                   = (known after apply)
      + instance_tenancy                     = "default"
      + ipv6_association_id                  = (known after apply)
      + ipv6_cidr_block                      = (known after apply)
      + ipv6_cidr_block_network_border_group = (known after apply)
      + main_route_table_id                  = (known after apply)
      + owner_id                             = (known after apply)
      + tags                                 = {
          + "Environment" = "dev"
          + "Terraform"   = "true"
        }
      + tags_all                             = {
          + "Environment" = "dev"
          + "Terraform"   = "true"
        }
    }

Plan: 9 to add, 0 to change, 0 to destroy.
l

## 5.Finally, terraform apply : Create or update infrastructure,it will generate 'terraform.tfstate' file for tracking your infrastructure.
**Output would look like this, combined with the output we got by executing 'terraform plan':**

Do you want to perform these actions?

  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

aws_vpc.my_vpc: Creating...
aws_vpc.my_vpc: Creation complete after 4s [id=vpc-08a1c233751b3534a]
aws_subnet.main_subnet: Creating...
aws_internet_gateway.gw: Creating...
aws_security_group.allow_web_traffic: Creating...
aws_subnet.main_subnet: Creation complete after 2s [id=subnet-0659728e7e3dd8898]
aws_internet_gateway.gw: Creation complete after 3s [id=igw-0ba0693b6c1a24464]
aws_route_table.my_route_table: Creating...
aws_security_group.allow_web_traffic: Creation complete after 6s [id=sg-0ebae3dc05b4e91ef]
aws_network_interface.web-server-nic: Creating...
aws_network_interface.web-server-nic: Creation complete after 1s [id=eni-04578d44d064ad04e]
aws_route_table.my_route_table: Creation complete after 4s [id=rtb-00337a25dadaa16c7]
aws_eip.one: Creating...
aws_route_table_association.a: Creating...
aws_instance.web-server-instance: Creating...
aws_route_table_association.a: Creation complete after 1s [id=rtbassoc-0967a09e1585395cb]
aws_instance.web-server-instance: Still creating... [10s elapsed]
aws_instance.web-server-instance: Creation complete after 16s [id=i-0705151e8203c5720]

## 6. Lastly, if you want to clean up your infrastructure after practice you can execute
  **terraform destroy : Destroy previously-created infrastructure**
   **Output would look like this along with the destroy plan :**
   
   Plan: 0 to add, 0 to change, 9 to destroy.
   
Do you really want to destroy all resources?
  Terraform will destroy all your managed infrastructure, as shown above.
  There is no undo. Only 'yes' will be accepted to confirm.

  Enter a value: yes

aws_eip.one: Destroying... [id=eipalloc-05e2976507743ca47]
aws_route_table_association.a: Destroying... [id=rtbassoc-0967a09e1585395cb]
aws_instance.web-server-instance: Destroying... [id=i-0705151e8203c5720]
aws_route_table_association.a: Destruction complete after 3s
aws_route_table.my_route_table: Destroying... [id=rtb-00337a25dadaa16c7]
aws_route_table.my_route_table: Destruction complete after 1s
aws_eip.one: Destruction complete after 4s
aws_internet_gateway.gw: Destroying... [id=igw-0ba0693b6c1a24464]
aws_internet_gateway.gw: Destruction complete after 1s
aws_instance.web-server-instance: Still destroying... [id=i-0705151e8203c5720, 10s elapsed]
aws_instance.web-server-instance: Still destroying... [id=i-0705151e8203c5720, 20s elapsed]
aws_instance.web-server-instance: Still destroying... [id=i-0705151e8203c5720, 30s elapsed]
aws_instance.web-server-instance: Destruction complete after 33s
aws_network_interface.web-server-nic: Destroying... [id=eni-04578d44d064ad04e]
aws_network_interface.web-server-nic: Destruction complete after 2s
aws_subnet.main_subnet: Destroying... [id=subnet-0659728e7e3dd8898]
aws_security_group.allow_web_traffic: Destroying... [id=sg-0ebae3dc05b4e91ef]
aws_subnet.main_subnet: Destruction complete after 2s
aws_security_group.allow_web_traffic: Destruction complete after 2s
aws_vpc.my_vpc: Destroying... [id=vpc-08a1c233751b3534a]
aws_vpc.my_vpc: Destruction complete after 2s

Destroy complete! Resources: 9 destroyed.

   
   






