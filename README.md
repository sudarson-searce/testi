# Prerequisites
You’ll need the following:

1.A GCP project

2.gcloud installed, up-to-date, logged in, and connected to your project.
  for cloud sdk installation  - 
  *Refer link -https://cloud.google.com/sdk/install

3. All required Google Cloud APIs enabled

> gcloud components update

> gcloud auth login

> gcloud config set project <my-project>

> gcloud config list
  
4.Make sure you have update version of terraform installed terraform 12.28
 *Refer link - https://releases.hashicorp.com/terraform/0.12.28/terraform_0.12.28_linux_amd64.zip

   1.Download the file and Unzip it

   2.For Linux servers - Move the file to /usr/local/bin
  
5.Remove the hidden files in terraform folder like .terrform

# VPC and Subnets for GKE and Cloud SQL

This script configures a single simple VPC with subnets with secondary ranges inside of a project.

This VPC has three subnets, with the first subnet being given two secondary
ranges.

# Subtitution of values in .tfvars file 

we have to move to the config directory and we have make changes in .tfvars file 

Here we have production.tfvars and prod-backend.tfvars

<!-- Values for production.tfvars file -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| network\_name | The name of the VPC network being created | string | n/a | yes |
| project\_id | The project ID to host the network in | string | n/a | yes |
| region | The region of the network in | string | n/a | yes |
| gke\_subnet | the name of gke subnet | string | n/a | yes |
| vm\_subnet | the name of vm subnet | string | n/a | yes |
| db\_subnet | the name of db subnet | string | n/a | yes |
| subnet01 | the subnet range of gke subnet | string | n/a | yes |
| subnet02 | the subnet range of vm subnet | string | n/a | yes |
| subnet03 | the subnet range of db subnet | string | n/a | yes |
| pods\_cidr\_range | the pods cidr range | string | n/a | yes |
| services\_cidr\_range | the services cidr range | string | n/a | yes |

<!-- Backend configuration forprod-backend.tfvars -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| bucket | The name of the Gcs bucket to store the tfstatefile | string | n/a | yes |
| prefix | The prefix or path of the file to be store in the gcs bucket| string | n/a | yes |

<!--TERRAFORM execution commands-->

## terraform execution commands
*comeback to the main directory and execute the below commands*

1.apply terraform init - terraform init -var-file=config/production.tfvars -backend-config=config/prod-backend.tfvars

2.apply terraform plan - terraform plan -var-file=config/production.tfvars -var-file=config/prod-backend.tfvars

3.apply terraform apply - terraform apply -var-file=config/production.tfvars -var-file=config/prod-backend.tfvars


## Outputs

| Name | Description |
|------|-------------|
| network\_name | The name of the VPC being created |
| network\_self\_link | The URI of the VPC being created |
| project\_id | VPC project id |
| route\_names | The routes associated with this VPC |
| subnets\_flow\_logs | Whether the subnets will have VPC flow logs enabled |
| subnets\_ips | The IP and cidrs of the subnets being created |
| subnets\_names | The names of the subnets being created |
| subnets\_private\_access | Whether the subnets will have access to Google API's without a public IP |
| subnets\_regions | The region where subnets will be created |
| subnets\_secondary\_ranges | The secondary ranges associated with these subnets |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->


