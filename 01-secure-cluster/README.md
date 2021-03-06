# 01-secure-cluster

## Prerequisites

:cloud: :rocket: Have fun!

### Updating/Install Terraform and Skaffold
1. Determine terraform version with `terraform version`
1. Update `terraform` if necessary
    - `. hack/utils.sh && download-terraform 0.11.5 && sudo mv -v terraform /usr/local/bin/`
1. Download `skaffold`
    - `. hack/utils.sh && download-skaffold && sudo mv -v skaffold /usr/local/bin/`

### Permissions

Ensure you have the `roles/owner` permission on the GCP project you are using for this lab

## Setup
1. Look through each of the files in the `tf/` folder carefully
    1. READ THE COMMENTS :)
    1. `backend.tf`
    1. `provider.tf`
    1. `therestofthem.tf`

## Step one (CREATING THE CLUSTER)

1. Replace variables in `backend.tf` and `variables.tf`
1. `terraform init`
1. `terraform plan`
1. `terraform apply`
1. `gcloud container clusters get-credentials <cluster-name> --zone=<yourmasterzone>`

```sh
$ kubectl get cs
NAME                 STATUS    MESSAGE              ERROR
controller-manager   Healthy   ok
scheduler            Healthy   ok
etcd-1               Healthy   {"health": "true"}
etcd-0               Healthy   {"health": "true"}
```

## Step two (SECURING THE CLUSTER)

1. From the `tf/` directory: `grep -R TODO .`
1. Complete the `TODO` items using the [provider documentation][tf-provider-google]

## Step three (DEPLOY A WORKLOAD TO THE CLUSTER)

1. `cd ../`
1. `replace-email your.email@domain.com`
1. `skaffold dev`
1. open a new tab
1. `cd terraform-lab/containers/webapp`
1. edit `main.go` and change the smiley to something else
1. go back to your other tab after you press save
1. watch magic

## Lastly (DESTROY THE CLUSTER)

:fire: `terraform destroy`

[tf-provider-google]: https://www.terraform.io/docs/providers/google/index.html
