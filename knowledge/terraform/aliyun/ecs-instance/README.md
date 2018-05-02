Alicloud ECS Instance Terraform Module In VPC
terraform-alicloud-ecs-instance
=====================================================================

A terraform module to provide ECS instances in Alicloud VPC. Its input variables contains VSwitch, Security Group, ECS Disks and ECS Instances.

- It assumes you have one VPC and VSwitch and you want to put the new instances to the VPC. If not, you can launch a new one by module [terraform-alicloud-vpc](https://github.com/alibaba/terraform-alicloud-vpc)
- It assumes you have several security groups in the VPC and you want to join the new instances into them. If not, you can launch one or more groups by module [terraform-alicloud-security-group](https://github.com/alibaba/terraform-alicloud-security-group)
- If you have no idea some parametes, such as instance type, availability zone and image id,
  the module will provide default values according to some input parameters, such as `image_name_regex`, `cpu_core_count`, `memory_size` and so on.

`Note`: If you specify the `vswitch_id`, the `availability_zone` would be ignore when launching ECS instances.
`Note`: We have deprecated ECS instance field `io_optimized` from `terraform-provider-alicloud`. If you happened some I/O optimized issues, please download and update provider package from [terraform-provider-alicloud release](https://github.com/alibaba/terraform-provider/releases).

----------------------

Usage
-----
You can use this in your terraform template with the following steps.

1. Adding a module resource to your template, e.g. main.tf


        module "tf-instances" {
            source = "alibaba/ecs-instance/alicloud"

            alicloud_access_key = "${var.alicloud_access_key}"
            alicloud_secret_key = "${var.alicloud_secret_key}"
            region = "${var.region}"

            vswitch_id = "${var.vswitch_id}"
            group_ids = "${var.group_ids}"

            disk_category = "cloud_ssd"
            disk_name = "my_module_disk"
            disk_size = "50"
            number_of_disks = 2

            instance_name = "my_module_instances"
            host_name = "my_host"
            internet_charge_type = "PayByTraffic"
            number_of_instances = "2"

            key_name = "${var.key_name}"

        }

2. Setting values for the following variables, either through terraform.tfvars or environment variables or -var arguments on the CLI

- alicloud_access_key
- alicloud_secret_key
- region
- key_name
- vswitch_id
- group_ids


Authors
-------
Created and maintained by He Guimin(@xiaozhu36, heguimin36@163.com)

Reference
---------
* [Terraform-Provider-Alicloud Github](https://github.com/alibaba/terraform-provider)
* [Terraform-Provider-Alicloud Release](https://github.com/alibaba/terraform-provider/releases)
* [Terraform-Provider-Alicloud Latest Docs](http://47.95.33.19:4567/docs/providers/alicloud/)


