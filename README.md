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
