# example-cassandra-terraform-astra-provider

Learn how to manage your DataStax Astra infrastructure with terraform! This tutorial can be done with Gitpod so you don't have to worry about any OS inconsistencies with your local machine! Hit the button below to get started!

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Anant/example-cassandra-terraform-astra-provider)


## 1. [Generate an Astra Token](https://docs.datastax.com/en/astra/docs/manage-application-tokens.html)
Generate an admin level token and copy your token value as we will need it for when we run terraform.

## 2. Install Terraform on Gitpod
```bash
brew tap hashicorp/tap
```

```bash
brew install hashicorp/tap/terraform
```

```bash
sudo apt-get install graphviz
```

## 3. Create `astra.tf`

```bash
touch astra.tf
```

## 4. Create a new Astra DB instance

### 4.1 Copy code into `astra.tf`
```
terraform {
    required_providers {
        astra = {
            source = "datastax/astra"
        }
    }
}

variable "token" {}

provider "astra" {
  // This can also be set via ASTRA_API_TOKEN environment variable.
  token = var.token
}

resource "astra_database" "example" {
  name           = "terraform"
  keyspace       = "test"
  cloud_provider = "gcp"
  regions        = ["us-east1"]
}
```

### 4.2 Run `terraform init`

### 4.3 Run `terraform plan` and paste in token when prompted

### 4.4 Run `terraform apply` and paste in token when prompoted. Additionally, type `yes` when prompted to apply changes

## 5. Create a dependency graph
```bash
sudo apt-get install graphviz
```
You can download this to your local and then open it in the browser.

## 6. Destroy newly created Astra DB instance
```bash
terraform destroy
```
