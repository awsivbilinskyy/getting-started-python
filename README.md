# resources you should create by terraform

prerequisites:
---
to create manually on GCP:
- create manually GCP service account(SA):
- grant Owner and Storage Admin permissions on project level to this SA
- create SA key to be used by terraform for resource provision 

[see this doumentation](https://cloud.google.com/community/tutorials/getting-started-on-gcp-with-terraform) - you need to configure your **provider "google"** correctly

create the repository for Terraform:


create via Terraform next infrastructure:

- VPC Network:
    - [google_compute_network](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_network#example-usage---network-basic)
    - [google_compute_subnetwork](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_subnetwork#example-usage---subnetwork-basic) - this example already have network creation inside
- Cloud NAT
    - [google_compute_router](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_router#example-usage---router-basic)
    - [google_compute_router_nat](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_router_nat#example-usage---router-nat-basic) - this example already has network, subnetwork, compute router, and cloudnat!!!! check this to understand how chain the dependet resources 
- SQL instance with private IP address
    - [google_sql_database_instance](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_database_instance#private-ip-instance) - example has all required, just need to reconfigure with right parameters
- SQL database
    - [google_sql_database](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_database#example-usage---sql-database-basic) - take just database instance from previous step
    - [google_sql_user](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/sql_user#example-usage)
- Cloud Storage Bucket for Application content
    - [google_storage_bucket](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/storage_bucket#example-usage---life-cycle-settings-for-storage-bucket-objects) - mind this example has life-cycle you dont need this, just simple bucket
    - [google_storage_default_object_access_control](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/storage_default_object_access_control#example-usage---storage-default-object-access-control-public)
- Service Account for Application instance
    - [google_service_account](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/google_service_account#example-usage)
- Instance template (with initial startup-script)
    - [google_compute_instance_template](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance_template#example-usage) - example already has SA creation in it. !!! MIND - THIS INSTANCE GROUP SHOULD USE STARTUP_SCRIPT THAT YOU CONFIGURED. however as it will use new database and storage, some variables should be changed.
- Managed Instance Group 
    - [google_compute_region_instance_group_manager](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_region_instance_group_manager#example-usage-with-top-level-instance-template-google-provider)
    - [google_compute_region_autoscaler](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_region_autoscaler#example-usage---region-autoscaler-basic)
- Firewall rules
    - [google_compute_firewall](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_firewall#example-usage---firewall-basic) 
- HTTP Load Balancer
    - [google_compute_backend_service](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_backend_service) - read whole document page
    - [google_compute_url_map](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_url_map) - read whole document page
    - [google_compute_target_http_proxy](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_target_http_proxy#example-usage---target-http-proxy-basic) - example of LB and all dependent resources from above
    - [google_compute_global_forwarding_rule](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_global_forwarding_rule#example-usage---global-forwarding-rule-http) - example of LB forwarding rule and all dependent resources from above
    - [google_compute_health_check](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_health_check#example-usage---health-check-tcp)


# !!! MIND
all above resources are to be created with parameters provided from your technical design documents and task description, configuration parameters for those resources you may get from [deploy.sh](https://github.com/GoogleCloudPlatform/getting-started-python/blob/steps/7-gce/gce/deploy.sh) script from **steps** branch

