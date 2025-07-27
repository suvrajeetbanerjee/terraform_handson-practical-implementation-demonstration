# 3-tier-vpc

C:\Users\Admin\Desktop\testbabtch\3-tier-architecture>terraform init
Initializing modules...
- autoscaling in modules\autoscaling
Downloading registry.terraform.io/terraform-aws-modules/alb/aws 5.16.0 for autoscaling.alb...
- autoscaling.alb in .terraform\modules\autoscaling.alb
Downloading registry.terraform.io/terraform-in-action/iip/aws 0.1.0 for autoscaling.iam_instance_profile...
- autoscaling.iam_instance_profile in .terraform\modules\autoscaling.iam_instance_profile
- database in modules\database
- networking in modules\networking
Downloading registry.terraform.io/terraform-in-action/sg/aws 0.1.0 for networking.db_sg...
- networking.db_sg in .terraform\modules\networking.db_sg
Downloading registry.terraform.io/terraform-in-action/sg/aws 0.1.0 for networking.lb_sg...
- networking.lb_sg in .terraform\modules\networking.lb_sg
Downloading registry.terraform.io/terraform-aws-modules/vpc/aws 2.64.0 for networking.vpc...
- networking.vpc in .terraform\modules\networking.vpc
Downloading registry.terraform.io/terraform-in-action/sg/aws 0.1.0 for networking.websvr_sg...
- networking.websvr_sg in .terraform\modules\networking.websvr_sg

Initializing the backend...

Initializing provider plugins...
- Reusing previous version of hashicorp/cloudinit from the dependency lock file
- Reusing previous version of hashicorp/aws from the dependency lock file
- Reusing previous version of hashicorp/random from the dependency lock file
- Installing hashicorp/cloudinit v2.2.0...
- Installed hashicorp/cloudinit v2.2.0 (signed by HashiCorp)
- Installing hashicorp/aws v3.63.0...
- Installed hashicorp/aws v3.63.0 (signed by HashiCorp)
- Installing hashicorp/random v3.1.0...
- Installed hashicorp/random v3.1.0 (signed by HashiCorp)

Terraform has made some changes to the provider dependency selections recorded
in the .terraform.lock.hcl file. Review those changes and commit them to your
version control system if they represent changes you intended to make.

Terraform has been successfully initialized!

You may now begin working with Terraform. Try running "terraform plan" to see
any changes that are required for your infrastructure. All Terraform commands
should now work.

If you ever set or change modules or backend configuration for Terraform,
rerun this command to reinitialize your working directory. If you forget, other
commands will detect it and remind you to do so if necessary.

C:\Users\Admin\Desktop\testbabtch\3-tier-architecture>terraform plan

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # module.autoscaling.data.cloudinit_config.config will be read during apply
  # (config refers to values not yet known)
 <= data "cloudinit_config" "config"  {
      + base64_encode = true
      + gzip          = true
      + id            = (known after apply)
      + rendered      = (known after apply)

      + part {
          + content      = (sensitive)
          + content_type = "text/cloud-config"
        }
    }

  # module.autoscaling.aws_autoscaling_group.webserver will be created
  + resource "aws_autoscaling_group" "webserver" {
      + arn                       = (known after apply)
      + availability_zones        = (known after apply)
      + default_cooldown          = (known after apply)
      + desired_capacity          = (known after apply)
      + force_delete              = false
      + force_delete_warm_pool    = false
      + health_check_grace_period = 300
      + health_check_type         = (known after apply)
      + id                        = (known after apply)
      + max_size                  = 3
      + metrics_granularity       = "1Minute"
      + min_size                  = 1
      + name                      = "my-3-tier-architecture-asg"
      + name_prefix               = (known after apply)
      + protect_from_scale_in     = false
      + service_linked_role_arn   = (known after apply)
      + target_group_arns         = (known after apply)
      + vpc_zone_identifier       = (known after apply)
      + wait_for_capacity_timeout = "10m"

      + launch_template {
          + id      = (known after apply)
          + name    = (known after apply)
          + version = (known after apply)
        }
    }

  # module.autoscaling.aws_launch_template.webserver will be created
  + resource "aws_launch_template" "webserver" {
      + arn                    = (known after apply)
      + default_version        = (known after apply)
      + id                     = (known after apply)
      + image_id               = "ami-070a90e0a26a6c7bd"
      + instance_type          = "t2.micro"
      + latest_version         = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = "my-3-tier-architecture"
      + tags_all               = (known after apply)
      + user_data              = (known after apply)
      + vpc_security_group_ids = (known after apply)

      + iam_instance_profile {
          + name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_protocol_ipv6          = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }
    }

  # module.database.aws_db_instance.database will be created
  + resource "aws_db_instance" "database" {
      + address                               = (known after apply)
      + allocated_storage                     = 10
      + apply_immediately                     = (known after apply)
      + arn                                   = (known after apply)
      + auto_minor_version_upgrade            = true
      + availability_zone                     = (known after apply)
      + backup_retention_period               = (known after apply)
      + backup_window                         = (known after apply)
      + ca_cert_identifier                    = (known after apply)
      + character_set_name                    = (known after apply)
      + copy_tags_to_snapshot                 = false
      + db_subnet_group_name                  = (known after apply)
      + delete_automated_backups              = true
      + endpoint                              = (known after apply)
      + engine                                = "mysql"
      + engine_version                        = "8.0"
      + engine_version_actual                 = (known after apply)
      + hosted_zone_id                        = (known after apply)
      + id                                    = (known after apply)
      + identifier                            = "my-3-tier-architecture-db-instance"
      + identifier_prefix                     = (known after apply)
      + instance_class                        = "db.t2.micro"
      + kms_key_id                            = (known after apply)
      + latest_restorable_time                = (known after apply)
      + license_model                         = (known after apply)
      + maintenance_window                    = (known after apply)
      + monitoring_interval                   = 0
      + monitoring_role_arn                   = (known after apply)
      + multi_az                              = (known after apply)
      + name                                  = "pets"
      + nchar_character_set_name              = (known after apply)
      + option_group_name                     = (known after apply)
      + parameter_group_name                  = (known after apply)
      + password                              = (sensitive value)
      + performance_insights_enabled          = false
      + performance_insights_kms_key_id       = (known after apply)
      + performance_insights_retention_period = (known after apply)
      + port                                  = (known after apply)
      + publicly_accessible                   = false
      + replicas                              = (known after apply)
      + resource_id                           = (known after apply)
      + skip_final_snapshot                   = true
      + snapshot_identifier                   = (known after apply)
      + status                                = (known after apply)
      + storage_type                          = (known after apply)
      + tags_all                              = (known after apply)
      + timezone                              = (known after apply)
      + username                              = "admin"
      + vpc_security_group_ids                = (known after apply)
    }

  # module.database.random_password.password will be created
  + resource "random_password" "password" {
      + id               = (known after apply)
      + length           = 16
      + lower            = true
      + min_lower        = 0
      + min_numeric      = 0
      + min_special      = 0
      + min_upper        = 0
      + number           = true
      + override_special = "_%@/'\""
      + result           = (sensitive value)
      + special          = true
      + upper            = true
    }

  # module.autoscaling.module.alb.aws_lb.this[0] will be created
  + resource "aws_lb" "this" {
      + arn                        = (known after apply)
      + arn_suffix                 = (known after apply)
      + dns_name                   = (known after apply)
      + drop_invalid_header_fields = false
      + enable_deletion_protection = false
      + enable_http2               = true
      + id                         = (known after apply)
      + idle_timeout               = 60
      + internal                   = false
      + ip_address_type            = "ipv4"
      + load_balancer_type         = "application"
      + name                       = "my-3-tier-architecture"
      + security_groups            = (known after apply)
      + subnets                    = (known after apply)
      + tags                       = {
          + "Name" = "my-3-tier-architecture"
        }
      + tags_all                   = {
          + "Name" = "my-3-tier-architecture"
        }
      + vpc_id                     = (known after apply)
      + zone_id                    = (known after apply)

      + subnet_mapping {
          + allocation_id        = (known after apply)
          + ipv6_address         = (known after apply)
          + outpost_id           = (known after apply)
          + private_ipv4_address = (known after apply)
          + subnet_id            = (known after apply)
        }

      + timeouts {
          + create = "10m"
          + delete = "10m"
          + update = "10m"
        }
    }

  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] will be created
  + resource "aws_lb_listener" "frontend_http_tcp" {
      + arn               = (known after apply)
      + id                = (known after apply)
      + load_balancer_arn = (known after apply)
      + port              = 80
      + protocol          = "HTTP"
      + ssl_policy        = (known after apply)
      + tags_all          = (known after apply)

      + default_action {
          + order            = (known after apply)
          + target_group_arn = (known after apply)
          + type             = "forward"
        }
    }

  # module.autoscaling.module.alb.aws_lb_target_group.main[0] will be created
  + resource "aws_lb_target_group" "main" {
      + arn                                = (known after apply)
      + arn_suffix                         = (known after apply)
      + deregistration_delay               = "300"
      + id                                 = (known after apply)
      + lambda_multi_value_headers_enabled = false
      + load_balancing_algorithm_type      = (known after apply)
      + name                               = (known after apply)
      + name_prefix                        = "websvr"
      + port                               = 8080
      + preserve_client_ip                 = (known after apply)
      + protocol                           = "HTTP"
      + protocol_version                   = (known after apply)
      + proxy_protocol_v2                  = false
      + slow_start                         = 0
      + tags                               = {
          + "Name" = "websvr"
        }
      + tags_all                           = {
          + "Name" = "websvr"
        }
      + target_type                        = "instance"
      + vpc_id                             = (known after apply)

      + health_check {
          + enabled             = (known after apply)
          + healthy_threshold   = (known after apply)
          + interval            = (known after apply)
          + matcher             = (known after apply)
          + path                = (known after apply)
          + port                = (known after apply)
          + protocol            = (known after apply)
          + timeout             = (known after apply)
          + unhealthy_threshold = (known after apply)
        }

      + stickiness {
          + cookie_duration = (known after apply)
          + cookie_name     = (known after apply)
          + enabled         = (known after apply)
          + type            = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile will be created
  + resource "aws_iam_instance_profile" "iam_instance_profile" {
      + arn         = (known after apply)
      + create_date = (known after apply)
      + id          = (known after apply)
      + name        = (known after apply)
      + path        = "/"
      + role        = (known after apply)
      + tags_all    = (known after apply)
      + unique_id   = (known after apply)
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role will be created
  + resource "aws_iam_role" "iam_role" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "ec2.amazonaws.com"
                        }
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + force_detach_policies = false
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy {
          + name   = (known after apply)
          + policy = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy will be created
  + resource "aws_iam_role_policy" "iam_role_policy" {
      + id     = (known after apply)
      + name   = (known after apply)
      + policy = jsonencode(
            {
              + Statement = [
                  + {
                      + Action   = [
                          + "rds:*",
                          + "logs:*",
                        ]
                      + Effect   = "Allow"
                      + Resource = "*"
                      + Sid      = ""
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + role   = (known after apply)
    }

  # module.networking.module.db_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 3306
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 3306
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.lb_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
              + description      = ""
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.vpc.aws_db_subnet_group.database[0] will be created
  + resource "aws_db_subnet_group" "database" {
      + arn         = (known after apply)
      + description = "Database subnet group for my-3-tier-architecture-vpc"
      + id          = (known after apply)
      + name        = "my-3-tier-architecture-vpc"
      + name_prefix = (known after apply)
      + subnet_ids  = (known after apply)
      + tags        = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all    = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.vpc.aws_eip.nat[0] will be created
  + resource "aws_eip" "nat" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = (known after apply)
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + vpc                  = true
    }

  # module.networking.module.vpc.aws_internet_gateway.this[0] will be created
  + resource "aws_internet_gateway" "this" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + vpc_id   = (known after apply)
    }

  # module.networking.module.vpc.aws_nat_gateway.this[0] will be created
  + resource "aws_nat_gateway" "this" {
      + allocation_id        = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
    }

  # module.networking.module.vpc.aws_route.private_nat_gateway[0] will be created
  + resource "aws_route" "private_nat_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + nat_gateway_id         = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route.public_internet_gateway[0] will be created
  + resource "aws_route" "public_internet_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + gateway_id             = (known after apply)
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route_table.private[0] will be created
  + resource "aws_route_table" "private" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table.public[0] will be created
  + resource "aws_route_table" "public" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[0] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[1] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[2] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[0] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[1] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[2] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[0] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[1] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[2] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[0] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.21.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[1] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.22.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[2] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.23.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[0] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.1.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[1] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.2.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[2] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.3.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[0] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.101.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[1] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.102.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[2] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.103.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_vpc.this[0] will be created
  + resource "aws_vpc" "this" {
      + arn                              = (known after apply)
      + assign_generated_ipv6_cidr_block = false
      + cidr_block                       = "10.0.0.0/16"
      + default_network_acl_id           = (known after apply)
      + default_route_table_id           = (known after apply)
      + default_security_group_id        = (known after apply)
      + dhcp_options_id                  = (known after apply)
      + enable_classiclink               = (known after apply)
      + enable_classiclink_dns_support   = (known after apply)
      + enable_dns_hostnames             = false
      + enable_dns_support               = true
      + id                               = (known after apply)
      + instance_tenancy                 = "default"
      + ipv6_association_id              = (known after apply)
      + ipv6_cidr_block                  = (known after apply)
      + main_route_table_id              = (known after apply)
      + owner_id                         = (known after apply)
      + tags                             = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all                         = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.websvr_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
                  + "10.0.0.0/16",
                ]
              + description      = ""
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 8080
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 8080
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

Plan: 40 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + db_password = (sensitive value)
  + lb_dns_name = (known after apply)

───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

Note: You didn't use the -out option to save this plan, so Terraform can't guarantee to take exactly these actions if
you run "terraform apply" now.

C:\Users\Admin\Desktop\testbabtch\3-tier-architecture>terraform apply

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
  + create
 <= read (data resources)

Terraform will perform the following actions:

  # module.autoscaling.data.cloudinit_config.config will be read during apply
  # (config refers to values not yet known)
 <= data "cloudinit_config" "config"  {
      + base64_encode = true
      + gzip          = true
      + id            = (known after apply)
      + rendered      = (known after apply)

      + part {
          + content      = (sensitive)
          + content_type = "text/cloud-config"
        }
    }

  # module.autoscaling.aws_autoscaling_group.webserver will be created
  + resource "aws_autoscaling_group" "webserver" {
      + arn                       = (known after apply)
      + availability_zones        = (known after apply)
      + default_cooldown          = (known after apply)
      + desired_capacity          = (known after apply)
      + force_delete              = false
      + force_delete_warm_pool    = false
      + health_check_grace_period = 300
      + health_check_type         = (known after apply)
      + id                        = (known after apply)
      + max_size                  = 3
      + metrics_granularity       = "1Minute"
      + min_size                  = 1
      + name                      = "my-3-tier-architecture-asg"
      + name_prefix               = (known after apply)
      + protect_from_scale_in     = false
      + service_linked_role_arn   = (known after apply)
      + target_group_arns         = (known after apply)
      + vpc_zone_identifier       = (known after apply)
      + wait_for_capacity_timeout = "10m"

      + launch_template {
          + id      = (known after apply)
          + name    = (known after apply)
          + version = (known after apply)
        }
    }

  # module.autoscaling.aws_launch_template.webserver will be created
  + resource "aws_launch_template" "webserver" {
      + arn                    = (known after apply)
      + default_version        = (known after apply)
      + id                     = (known after apply)
      + image_id               = "ami-070a90e0a26a6c7bd"
      + instance_type          = "t2.micro"
      + latest_version         = (known after apply)
      + name                   = (known after apply)
      + name_prefix            = "my-3-tier-architecture"
      + tags_all               = (known after apply)
      + user_data              = (known after apply)
      + vpc_security_group_ids = (known after apply)

      + iam_instance_profile {
          + name = (known after apply)
        }

      + metadata_options {
          + http_endpoint               = (known after apply)
          + http_protocol_ipv6          = (known after apply)
          + http_put_response_hop_limit = (known after apply)
          + http_tokens                 = (known after apply)
        }
    }

  # module.database.aws_db_instance.database will be created
  + resource "aws_db_instance" "database" {
      + address                               = (known after apply)
      + allocated_storage                     = 10
      + apply_immediately                     = (known after apply)
      + arn                                   = (known after apply)
      + auto_minor_version_upgrade            = true
      + availability_zone                     = (known after apply)
      + backup_retention_period               = (known after apply)
      + backup_window                         = (known after apply)
      + ca_cert_identifier                    = (known after apply)
      + character_set_name                    = (known after apply)
      + copy_tags_to_snapshot                 = false
      + db_subnet_group_name                  = (known after apply)
      + delete_automated_backups              = true
      + endpoint                              = (known after apply)
      + engine                                = "mysql"
      + engine_version                        = "8.0"
      + engine_version_actual                 = (known after apply)
      + hosted_zone_id                        = (known after apply)
      + id                                    = (known after apply)
      + identifier                            = "my-3-tier-architecture-db-instance"
      + identifier_prefix                     = (known after apply)
      + instance_class                        = "db.t2.micro"
      + kms_key_id                            = (known after apply)
      + latest_restorable_time                = (known after apply)
      + license_model                         = (known after apply)
      + maintenance_window                    = (known after apply)
      + monitoring_interval                   = 0
      + monitoring_role_arn                   = (known after apply)
      + multi_az                              = (known after apply)
      + name                                  = "pets"
      + nchar_character_set_name              = (known after apply)
      + option_group_name                     = (known after apply)
      + parameter_group_name                  = (known after apply)
      + password                              = (sensitive value)
      + performance_insights_enabled          = false
      + performance_insights_kms_key_id       = (known after apply)
      + performance_insights_retention_period = (known after apply)
      + port                                  = (known after apply)
      + publicly_accessible                   = false
      + replicas                              = (known after apply)
      + resource_id                           = (known after apply)
      + skip_final_snapshot                   = true
      + snapshot_identifier                   = (known after apply)
      + status                                = (known after apply)
      + storage_type                          = (known after apply)
      + tags_all                              = (known after apply)
      + timezone                              = (known after apply)
      + username                              = "admin"
      + vpc_security_group_ids                = (known after apply)
    }

  # module.database.random_password.password will be created
  + resource "random_password" "password" {
      + id               = (known after apply)
      + length           = 16
      + lower            = true
      + min_lower        = 0
      + min_numeric      = 0
      + min_special      = 0
      + min_upper        = 0
      + number           = true
      + override_special = "_%@/'\""
      + result           = (sensitive value)
      + special          = true
      + upper            = true
    }

  # module.autoscaling.module.alb.aws_lb.this[0] will be created
  + resource "aws_lb" "this" {
      + arn                        = (known after apply)
      + arn_suffix                 = (known after apply)
      + dns_name                   = (known after apply)
      + drop_invalid_header_fields = false
      + enable_deletion_protection = false
      + enable_http2               = true
      + id                         = (known after apply)
      + idle_timeout               = 60
      + internal                   = false
      + ip_address_type            = "ipv4"
      + load_balancer_type         = "application"
      + name                       = "my-3-tier-architecture"
      + security_groups            = (known after apply)
      + subnets                    = (known after apply)
      + tags                       = {
          + "Name" = "my-3-tier-architecture"
        }
      + tags_all                   = {
          + "Name" = "my-3-tier-architecture"
        }
      + vpc_id                     = (known after apply)
      + zone_id                    = (known after apply)

      + subnet_mapping {
          + allocation_id        = (known after apply)
          + ipv6_address         = (known after apply)
          + outpost_id           = (known after apply)
          + private_ipv4_address = (known after apply)
          + subnet_id            = (known after apply)
        }

      + timeouts {
          + create = "10m"
          + delete = "10m"
          + update = "10m"
        }
    }

  # module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0] will be created
  + resource "aws_lb_listener" "frontend_http_tcp" {
      + arn               = (known after apply)
      + id                = (known after apply)
      + load_balancer_arn = (known after apply)
      + port              = 80
      + protocol          = "HTTP"
      + ssl_policy        = (known after apply)
      + tags_all          = (known after apply)

      + default_action {
          + order            = (known after apply)
          + target_group_arn = (known after apply)
          + type             = "forward"
        }
    }

  # module.autoscaling.module.alb.aws_lb_target_group.main[0] will be created
  + resource "aws_lb_target_group" "main" {
      + arn                                = (known after apply)
      + arn_suffix                         = (known after apply)
      + deregistration_delay               = "300"
      + id                                 = (known after apply)
      + lambda_multi_value_headers_enabled = false
      + load_balancing_algorithm_type      = (known after apply)
      + name                               = (known after apply)
      + name_prefix                        = "websvr"
      + port                               = 8080
      + preserve_client_ip                 = (known after apply)
      + protocol                           = "HTTP"
      + protocol_version                   = (known after apply)
      + proxy_protocol_v2                  = false
      + slow_start                         = 0
      + tags                               = {
          + "Name" = "websvr"
        }
      + tags_all                           = {
          + "Name" = "websvr"
        }
      + target_type                        = "instance"
      + vpc_id                             = (known after apply)

      + health_check {
          + enabled             = (known after apply)
          + healthy_threshold   = (known after apply)
          + interval            = (known after apply)
          + matcher             = (known after apply)
          + path                = (known after apply)
          + port                = (known after apply)
          + protocol            = (known after apply)
          + timeout             = (known after apply)
          + unhealthy_threshold = (known after apply)
        }

      + stickiness {
          + cookie_duration = (known after apply)
          + cookie_name     = (known after apply)
          + enabled         = (known after apply)
          + type            = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile will be created
  + resource "aws_iam_instance_profile" "iam_instance_profile" {
      + arn         = (known after apply)
      + create_date = (known after apply)
      + id          = (known after apply)
      + name        = (known after apply)
      + path        = "/"
      + role        = (known after apply)
      + tags_all    = (known after apply)
      + unique_id   = (known after apply)
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role will be created
  + resource "aws_iam_role" "iam_role" {
      + arn                   = (known after apply)
      + assume_role_policy    = jsonencode(
            {
              + Statement = [
                  + {
                      + Action    = "sts:AssumeRole"
                      + Effect    = "Allow"
                      + Principal = {
                          + Service = "ec2.amazonaws.com"
                        }
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + create_date           = (known after apply)
      + force_detach_policies = false
      + id                    = (known after apply)
      + managed_policy_arns   = (known after apply)
      + max_session_duration  = 3600
      + name                  = (known after apply)
      + name_prefix           = (known after apply)
      + path                  = "/"
      + tags_all              = (known after apply)
      + unique_id             = (known after apply)

      + inline_policy {
          + name   = (known after apply)
          + policy = (known after apply)
        }
    }

  # module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy will be created
  + resource "aws_iam_role_policy" "iam_role_policy" {
      + id     = (known after apply)
      + name   = (known after apply)
      + policy = jsonencode(
            {
              + Statement = [
                  + {
                      + Action   = [
                          + "rds:*",
                          + "logs:*",
                        ]
                      + Effect   = "Allow"
                      + Resource = "*"
                      + Sid      = ""
                    },
                ]
              + Version   = "2012-10-17"
            }
        )
      + role   = (known after apply)
    }

  # module.networking.module.db_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 3306
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 3306
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.lb_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
              + description      = ""
              + from_port        = 80
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 80
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

  # module.networking.module.vpc.aws_db_subnet_group.database[0] will be created
  + resource "aws_db_subnet_group" "database" {
      + arn         = (known after apply)
      + description = "Database subnet group for my-3-tier-architecture-vpc"
      + id          = (known after apply)
      + name        = "my-3-tier-architecture-vpc"
      + name_prefix = (known after apply)
      + subnet_ids  = (known after apply)
      + tags        = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all    = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.vpc.aws_eip.nat[0] will be created
  + resource "aws_eip" "nat" {
      + allocation_id        = (known after apply)
      + association_id       = (known after apply)
      + carrier_ip           = (known after apply)
      + customer_owned_ip    = (known after apply)
      + domain               = (known after apply)
      + id                   = (known after apply)
      + instance             = (known after apply)
      + network_border_group = (known after apply)
      + network_interface    = (known after apply)
      + private_dns          = (known after apply)
      + private_ip           = (known after apply)
      + public_dns           = (known after apply)
      + public_ip            = (known after apply)
      + public_ipv4_pool     = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + vpc                  = true
    }

  # module.networking.module.vpc.aws_internet_gateway.this[0] will be created
  + resource "aws_internet_gateway" "this" {
      + arn      = (known after apply)
      + id       = (known after apply)
      + owner_id = (known after apply)
      + tags     = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + vpc_id   = (known after apply)
    }

  # module.networking.module.vpc.aws_nat_gateway.this[0] will be created
  + resource "aws_nat_gateway" "this" {
      + allocation_id        = (known after apply)
      + connectivity_type    = "public"
      + id                   = (known after apply)
      + network_interface_id = (known after apply)
      + private_ip           = (known after apply)
      + public_ip            = (known after apply)
      + subnet_id            = (known after apply)
      + tags                 = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
      + tags_all             = {
          + "Name" = "my-3-tier-architecture-vpc-us-west-2a"
        }
    }

  # module.networking.module.vpc.aws_route.private_nat_gateway[0] will be created
  + resource "aws_route" "private_nat_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + nat_gateway_id         = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route.public_internet_gateway[0] will be created
  + resource "aws_route" "public_internet_gateway" {
      + destination_cidr_block = "0.0.0.0/0"
      + gateway_id             = (known after apply)
      + id                     = (known after apply)
      + instance_id            = (known after apply)
      + instance_owner_id      = (known after apply)
      + network_interface_id   = (known after apply)
      + origin                 = (known after apply)
      + route_table_id         = (known after apply)
      + state                  = (known after apply)

      + timeouts {
          + create = "5m"
        }
    }

  # module.networking.module.vpc.aws_route_table.private[0] will be created
  + resource "aws_route_table" "private" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-private"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table.public[0] will be created
  + resource "aws_route_table" "public" {
      + arn              = (known after apply)
      + id               = (known after apply)
      + owner_id         = (known after apply)
      + propagating_vgws = (known after apply)
      + route            = (known after apply)
      + tags             = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + tags_all         = {
          + "Name" = "my-3-tier-architecture-vpc-public"
        }
      + vpc_id           = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[0] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[1] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.database[2] will be created
  + resource "aws_route_table_association" "database" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[0] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[1] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.private[2] will be created
  + resource "aws_route_table_association" "private" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[0] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[1] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_route_table_association.public[2] will be created
  + resource "aws_route_table_association" "public" {
      + id             = (known after apply)
      + route_table_id = (known after apply)
      + subnet_id      = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[0] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.21.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[1] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.22.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.database[2] will be created
  + resource "aws_subnet" "database" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.23.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-db-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[0] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.1.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[1] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.2.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.private[2] will be created
  + resource "aws_subnet" "private" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.3.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = false
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-private-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[0] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2a"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.101.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2a"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[1] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2b"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.102.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2b"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_subnet.public[2] will be created
  + resource "aws_subnet" "public" {
      + arn                             = (known after apply)
      + assign_ipv6_address_on_creation = false
      + availability_zone               = "us-west-2c"
      + availability_zone_id            = (known after apply)
      + cidr_block                      = "10.0.103.0/24"
      + id                              = (known after apply)
      + ipv6_cidr_block_association_id  = (known after apply)
      + map_public_ip_on_launch         = true
      + owner_id                        = (known after apply)
      + tags                            = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + tags_all                        = {
          + "Name" = "my-3-tier-architecture-vpc-public-us-west-2c"
        }
      + vpc_id                          = (known after apply)
    }

  # module.networking.module.vpc.aws_vpc.this[0] will be created
  + resource "aws_vpc" "this" {
      + arn                              = (known after apply)
      + assign_generated_ipv6_cidr_block = false
      + cidr_block                       = "10.0.0.0/16"
      + default_network_acl_id           = (known after apply)
      + default_route_table_id           = (known after apply)
      + default_security_group_id        = (known after apply)
      + dhcp_options_id                  = (known after apply)
      + enable_classiclink               = (known after apply)
      + enable_classiclink_dns_support   = (known after apply)
      + enable_dns_hostnames             = false
      + enable_dns_support               = true
      + id                               = (known after apply)
      + instance_tenancy                 = "default"
      + ipv6_association_id              = (known after apply)
      + ipv6_cidr_block                  = (known after apply)
      + main_route_table_id              = (known after apply)
      + owner_id                         = (known after apply)
      + tags                             = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
      + tags_all                         = {
          + "Name" = "my-3-tier-architecture-vpc"
        }
    }

  # module.networking.module.websvr_sg.aws_security_group.security_group will be created
  + resource "aws_security_group" "security_group" {
      + arn                    = (known after apply)
      + description            = "Managed by Terraform"
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
                  + "10.0.0.0/16",
                ]
              + description      = ""
              + from_port        = 22
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = []
              + self             = false
              + to_port          = 22
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 0
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "-1"
              + security_groups  = []
              + self             = true
              + to_port          = 0
            },
          + {
              + cidr_blocks      = []
              + description      = ""
              + from_port        = 8080
              + ipv6_cidr_blocks = []
              + prefix_list_ids  = []
              + protocol         = "tcp"
              + security_groups  = (known after apply)
              + self             = false
              + to_port          = 8080
            },
        ]
      + name                   = (known after apply)
      + name_prefix            = (known after apply)
      + owner_id               = (known after apply)
      + revoke_rules_on_delete = false
      + tags_all               = (known after apply)
      + vpc_id                 = (known after apply)
    }

Plan: 40 to add, 0 to change, 0 to destroy.

Changes to Outputs:
  + db_password = (sensitive value)
  + lb_dns_name = (known after apply)

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

module.database.random_password.password: Creating...
module.database.random_password.password: Creation complete after 0s [id=none]
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Creating...
module.networking.module.vpc.aws_vpc.this[0]: Creating...
module.networking.module.vpc.aws_eip.nat[0]: Creating...
module.networking.module.vpc.aws_eip.nat[0]: Creation complete after 3s [id=eipalloc-06de8d63aafd881c4]
module.autoscaling.module.iam_instance_profile.aws_iam_role.iam_role: Creation complete after 4s [id=terraform-20220217163955284500000001]
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Creating...
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Creating...
module.autoscaling.module.iam_instance_profile.aws_iam_role_policy.iam_role_policy: Creation complete after 3s [id=terraform-20220217163955284500000001:terraform-20220217163959428400000002]
module.autoscaling.module.iam_instance_profile.aws_iam_instance_profile.iam_instance_profile: Creation complete after 4s [id=terraform-20220217163959429900000003]
module.networking.module.vpc.aws_vpc.this[0]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_vpc.this[0]: Creation complete after 15s [id=vpc-0162dce03908f5d48]
module.networking.module.vpc.aws_route_table.private[0]: Creating...
module.networking.module.vpc.aws_subnet.database[2]: Creating...
module.networking.module.vpc.aws_subnet.public[1]: Creating...
module.networking.module.vpc.aws_subnet.public[2]: Creating...
module.networking.module.vpc.aws_subnet.public[0]: Creating...
module.networking.module.vpc.aws_internet_gateway.this[0]: Creating...
module.networking.module.vpc.aws_subnet.database[1]: Creating...
module.networking.module.vpc.aws_route_table.public[0]: Creating...
module.networking.module.vpc.aws_subnet.private[2]: Creating...
module.networking.module.vpc.aws_subnet.private[0]: Creating...
module.networking.module.vpc.aws_route_table.private[0]: Creation complete after 3s [id=rtb-05090e453276d4b08]
module.networking.module.vpc.aws_subnet.database[0]: Creating...
module.networking.module.vpc.aws_route_table.public[0]: Creation complete after 3s [id=rtb-03686dc8ddba2df6b]
module.networking.module.vpc.aws_subnet.private[1]: Creating...
module.networking.module.vpc.aws_subnet.private[2]: Creation complete after 4s [id=subnet-07e4d2c18625ff4b3]
module.networking.module.vpc.aws_subnet.database[2]: Creation complete after 4s [id=subnet-077379721bfd91997]
module.networking.module.vpc.aws_subnet.private[0]: Creation complete after 4s [id=subnet-06a450ceb909b92e7]
module.networking.module.lb_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_subnet.database[1]: Creation complete after 4s [id=subnet-01cb4541b84e2c200]
module.networking.module.vpc.aws_internet_gateway.this[0]: Creation complete after 6s [id=igw-0a710b8fadc3f74dc]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Creating...
module.networking.module.vpc.aws_subnet.database[0]: Creation complete after 4s [id=subnet-0fd7c570d61d0d912]
module.networking.module.vpc.aws_route_table_association.database[2]: Creating...
module.networking.module.vpc.aws_route_table_association.database[0]: Creating...
module.networking.module.vpc.aws_route_table_association.database[1]: Creating...
module.networking.module.vpc.aws_db_subnet_group.database[0]: Creating...
module.networking.module.vpc.aws_subnet.private[1]: Creation complete after 4s [id=subnet-03524fb344f2f8e2c]
module.networking.module.vpc.aws_route_table_association.private[2]: Creating...
module.networking.module.vpc.aws_subnet.public[2]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_subnet.public[1]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_subnet.public[0]: Still creating... [10s elapsed]
module.networking.module.vpc.aws_route_table_association.database[2]: Creation complete after 3s [id=rtbassoc-014542f4df51251ef]
module.networking.module.vpc.aws_route_table_association.private[1]: Creating...
module.networking.module.vpc.aws_route_table_association.database[0]: Creation complete after 3s [id=rtbassoc-06029981a8f56cd18]
module.networking.module.vpc.aws_route_table_association.private[0]: Creating...
module.networking.module.vpc.aws_route_table_association.database[1]: Creation complete after 3s [id=rtbassoc-0d7f0571c4d980198]
module.networking.module.vpc.aws_route.public_internet_gateway[0]: Creation complete after 4s [id=r-rtb-03686dc8ddba2df6b1080289494]
module.networking.module.vpc.aws_route_table_association.private[2]: Creation complete after 4s [id=rtbassoc-015524b78e832ef1b]
module.networking.module.vpc.aws_db_subnet_group.database[0]: Creation complete after 4s [id=my-3-tier-architecture-vpc]
module.networking.module.lb_sg.aws_security_group.security_group: Still creating... [10s elapsed]
module.networking.module.vpc.aws_route_table_association.private[1]: Creation complete after 4s [id=rtbassoc-0e476e2b5158bd802]
module.networking.module.vpc.aws_route_table_association.private[0]: Creation complete after 4s [id=rtbassoc-0e4d5dcdba88ad217]
module.networking.module.lb_sg.aws_security_group.security_group: Creation complete after 10s [id=sg-02f772f316ebcaf07]
module.networking.module.websvr_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_subnet.public[2]: Creation complete after 16s [id=subnet-01d3ba84d537e8fec]
module.networking.module.vpc.aws_subnet.public[0]: Creation complete after 16s [id=subnet-0a7015d3b7e70d113]
module.networking.module.vpc.aws_subnet.public[1]: Creation complete after 16s [id=subnet-0dd7c76dd9f3f0931]
module.networking.module.vpc.aws_route_table_association.public[0]: Creating...
module.networking.module.vpc.aws_route_table_association.public[1]: Creating...
module.networking.module.vpc.aws_nat_gateway.this[0]: Creating...
module.networking.module.vpc.aws_route_table_association.public[2]: Creating...
module.networking.module.vpc.aws_route_table_association.public[2]: Creation complete after 4s [id=rtbassoc-0c7167da629fa5b18]
module.networking.module.vpc.aws_route_table_association.public[0]: Creation complete after 4s [id=rtbassoc-058dab088e20479ee]
module.networking.module.vpc.aws_route_table_association.public[1]: Creation complete after 4s [id=rtbassoc-03ae6949da4e84e80]
module.networking.module.websvr_sg.aws_security_group.security_group: Still creating... [10s elapsed]
module.networking.module.websvr_sg.aws_security_group.security_group: Creation complete after 11s [id=sg-01f3c3ec38a0e553c]
module.networking.module.db_sg.aws_security_group.security_group: Creating...
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [10s elapsed]
module.networking.module.db_sg.aws_security_group.security_group: Still creating... [10s elapsed]
module.networking.module.db_sg.aws_security_group.security_group: Creation complete after 10s [id=sg-0cb4b0fb67e262eaf]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [20s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [30s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [40s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [50s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m0s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m10s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m20s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Still creating... [1m30s elapsed]
module.networking.module.vpc.aws_nat_gateway.this[0]: Creation complete after 1m32s [id=nat-01901220a9d6040bf]
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Creating...
module.networking.module.vpc.aws_route.private_nat_gateway[0]: Creation complete after 5s [id=r-rtb-05090e453276d4b081080289494]
module.autoscaling.module.alb.aws_lb.this[0]: Creating...
module.database.aws_db_instance.database: Creating...
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [10s elapsed]
module.database.aws_db_instance.database: Still creating... [10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [20s elapsed]
module.database.aws_db_instance.database: Still creating... [20s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [30s elapsed]
module.database.aws_db_instance.database: Still creating... [30s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [40s elapsed]
module.database.aws_db_instance.database: Still creating... [40s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [50s elapsed]
module.database.aws_db_instance.database: Still creating... [50s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m0s elapsed]
module.database.aws_db_instance.database: Still creating... [1m0s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m10s elapsed]
module.database.aws_db_instance.database: Still creating... [1m10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m20s elapsed]
module.database.aws_db_instance.database: Still creating... [1m20s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m30s elapsed]
module.database.aws_db_instance.database: Still creating... [1m30s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m40s elapsed]
module.database.aws_db_instance.database: Still creating... [1m40s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [1m50s elapsed]
module.database.aws_db_instance.database: Still creating... [1m50s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [2m0s elapsed]
module.database.aws_db_instance.database: Still creating... [2m0s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [2m10s elapsed]
module.database.aws_db_instance.database: Still creating... [2m10s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Still creating... [2m20s elapsed]
module.database.aws_db_instance.database: Still creating... [2m20s elapsed]
module.autoscaling.module.alb.aws_lb.this[0]: Creation complete after 2m22s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:loadbalancer/app/my-3-tier-architecture/ce7f653a7cb83435]
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Creating...
module.autoscaling.module.alb.aws_lb_target_group.main[0]: Creation complete after 7s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:targetgroup/websvr20220217164424614500000007/97efd61d827e4e29]
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Creating...
module.database.aws_db_instance.database: Still creating... [2m30s elapsed]
module.autoscaling.module.alb.aws_lb_listener.frontend_http_tcp[0]: Creation complete after 4s [id=arn:aws:elasticloadbalancing:us-west-2:878088820643:listener/app/my-3-tier-architecture/ce7f653a7cb83435/1bd6b061d443b221]
module.database.aws_db_instance.database: Still creating... [2m40s elapsed]
module.database.aws_db_instance.database: Still creating... [2m50s elapsed]
module.database.aws_db_instance.database: Still creating... [3m0s elapsed]
module.database.aws_db_instance.database: Still creating... [3m10s elapsed]
module.database.aws_db_instance.database: Still creating... [3m20s elapsed]
module.database.aws_db_instance.database: Still creating... [3m30s elapsed]
module.database.aws_db_instance.database: Still creating... [3m40s elapsed]
module.database.aws_db_instance.database: Still creating... [3m50s elapsed]
module.database.aws_db_instance.database: Still creating... [4m0s elapsed]
module.database.aws_db_instance.database: Still creating... [4m11s elapsed]
module.database.aws_db_instance.database: Creation complete after 4m11s [id=my-3-tier-architecture-db-instance]
module.autoscaling.data.cloudinit_config.config: Reading...
module.autoscaling.data.cloudinit_config.config: Read complete after 0s [id=1478396351]
module.autoscaling.aws_launch_template.webserver: Creating...
module.autoscaling.aws_launch_template.webserver: Creation complete after 4s [id=lt-095ffc74aac2d4d4d]
module.autoscaling.aws_autoscaling_group.webserver: Creating...
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [20s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [30s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [40s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [50s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m0s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m10s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m20s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m30s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Still creating... [1m40s elapsed]
module.autoscaling.aws_autoscaling_group.webserver: Creation complete after 1m49s [id=my-3-tier-architecture-asg]

Apply complete! Resources: 40 added, 0 changed, 0 destroyed.

Outputs:

db_password = <sensitive>
lb_dns_name = "my-3-tier-architecture-1371552020.us-west-2.elb.amazonaws.com"
