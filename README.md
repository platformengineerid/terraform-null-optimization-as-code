<img src="https://www.densify.com/wp-content/uploads/densify.png" width="300">

# Densify
This module is the interface between Densify machine learning analytics and Terraform templates. 
It enables two operations:
- auto-tagging of cloud instances and containers based on Densify’s optimization analysis (making them “self-aware”)
-	automated optimization of instance families/sizes, and container resource requests/limits (making them “self-optimizing”) 

This integration is based on densify.auto.tfvars, which is automatically generated by Densify and contains operational intelligence, analysis findings, and optimization recommendations for each cloud instance or container in scope. This module unpacks data from this structure, making it available to Terraform as variables, enabling precise specification of resources to optimally match the learned patterns of behavior. 
The result is next-generation resource optimization with the elimination of hard-coded resource specifications.

- [Requirements](#requirements)
- [Usage](#usage)
- [Examples](#examples)
- [Inputs](#inputs)
- [Outputs](#outputs)
- [License](#license)

## Requirements
- Densify account, which is provided with a Densify subscription or free trial (www.densify.com/trial)


## Usage

```hcl
module "optimization-as-code" {
  source  = "densify-dev/optimization-as-code/null"
  
  densify_recommendations = "${var.densify_recommendations}"
  densify_fallback = "${var.densify_fallback}"
  densify_unique_id = "${var.name}"
}
```
## Examples 
* [AWS EC2](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/aws-ec2)
* [AWS RDS](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/aws-rds)
* [Azure VM](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/azure-vm)
* [GCP Instance](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/gcp-instance)
* [Kubernetes Pod](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/k8s-pod)
* [Kubernetes Replication Controller](https://github.com/densify-dev/terraform-null-optimization-as-code/tree/master/examples/k8s-replication-controller)

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| densify_recommendations | Map variable containing recommendations from Densify | Map | - | Yes |
| densify_fallback | The map default values used if Densify recommendations are not available | Map | - | Yes |
| densify_unique_id | The unique identifier of the system to be updated | String | - | Yes |

## Outputs

| Name | Description |
|------|-------------|
| Current_type | Current instance size and family |
| recommended_type | Densify recommended instance size and family |
| savings_estimate | The potential monthly savings from modifying the current instance to the Densify recommended instance |
| predicted_uptime | The predicted percentage of CPU utilization hours over the duration of a month |
| recommend_ri_coverage | Densify recommends purchasing reserved instance coverage for this instance |
| current_cpu_request | Current CPU request for Kubernetes |
| recommended_cpu_request | Recommended CPU request for Kubernetes |
| current_cpu_limit | Current CPU limit for Kubernetes |
| recommended_cpu_limit | Recommended CPU limit for Kubernetes |
| current_mem_request | Current memory request for Kubernetes |
| recommended_mem_request | Recommended memory request for Kubernetes |
| current_mem_limit | Current memory limit for Kubernetes |
| recommended_mem_limit | Recommended memory limit for Kubernetes |
| instance_type | The instance size and family to be implemented, which is either the current size or the Densify recommendation, depending on the automation policy and the approval status (if approval is enabled) |
| cpu_request | The CPU request to be implemented, which is either the current size or the Densify recommendation, depending on the automation policy and the approval status (if approval is enabled) |
| cpu_limit | The CPU limit to be implemented, which is either the current size or the Densify recommendation, depending on the automation policy and the approval status (if approval is enabled) |
| mem_request | The memory request to be implemented, which is either the current size or the Densify recommendation, depending on the automation policy and the approval status (if approval is enabled) |
| mem_limit | The memory limit to be implemented, which is either the current size or the Densify recommendation, depending on the automation policy and the approval status (if approval is enabled) |
| min_group_current | The current minimum group size of the ASG |
| min_group_recommended | The recommended minimum group size of the ASG |
| max_group_current | The current maximum group size of the ASG |
| max_group_recommended | The recommended maximum group size of the ASG |
| min_group | The minimum group size to be implemented, which is either the current minimum group size or the Densify recommended minimum group size depending on the automation policy and approval status (if approval is enabled) |
| max_group | The maximum group size to be implemented, which is either the current maximum group size or the Densify recommended maximum group size depending on the automation policy and approval status (if approval is enabled) |
| avg_inst_count_recommended | The predicted average number of instances running in the ASG if the recommendations are implemented |
| current_desired_capacity | The current desired number of instances running in the ASG |
| desired_capacity | The desired capacity to be implemented, which is either the current desired capacity or the recommended average instance count (rounded down) depending on the automation policy and approval status (if approval is enabled) |

## License

Apache 2 Licensed. See LICENSE for full details.
