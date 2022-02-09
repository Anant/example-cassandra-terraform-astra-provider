# example-cassandra-terraform-astra-provider

Learn how to manage your DataStax Astra infrastructure with terraform! This tutorial can be done with Gitpod so you don't have to worry about any OS inconsistencies with your local machine! Hit the button below to get started!

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/Anant/example-cassandra-terraform-astra-provider)


## 1. [Generate an Astra Token](https://docs.datastax.com/en/astra/docs/manage-application-tokens.html)
Generate an admin level token and copy your token value as we will need it for when we run terraform.

## 2. When prompted in the terminal, type `yes`

## 3. Create a new Astra DB instance

### 3.1 Copy code into `astra.tf`
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

### 3.2 Run `terraform init`

### 3.3 Run `terraform plan`
Paste in token when prompted and visualize the upcoming infrastructure changes.

### 3.4 Run `terraform apply`
Paste in token when prompoted. Additionally, type `yes` when prompted to apply changes. Once the deploy has completed, you can check your Astra dashboard and see the newly created database!

## 4. Create a new keyspace in newly deployed database

### 4.1 Add the following in `astra.tf` to visualize the databases and get id's of active databases
```
data "astra_databases" "databaselist" {
  status = "ACTIVE"
}

output "existing_dbs" {
  value = [for db in data.astra_databases.databaselist.results : db.id]
}
```

### 4.2 Run `terraform plan` to visualize changes and then `terraform apply`

### 4.3 Add the following in `astra.tf` to create a new keyspace to the new Astra database

```
resource "astra_keyspace" "databaselist" {
  name        = "example"
  database_id = data.astra_databases.databaselist.results[0].id
}
```
### 4.4 Run `terraform plan` to visualize changes and then `terraform apply` to create the new keyspace

## 5. Create a dependency graph
```bash
sudo apt-get install graphviz
```

## 6. Destroy newly created Astra DB instance
```bash
terraform destroy
```
