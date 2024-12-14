## Step 1: Understanding Terraform Essentials

_Welcome to Terraform essentials! :wave:_

Terraform is an exceptionally powerful tool for defining infrastructure as code (IaC). Defining cloud infrastructure as code has several benefits, such as:

1. **Consistency and Repeatability**: IaC ensures that the same environment is created every time, reducing the risk of configuration drift and human error.
1. **Version Control**: Infrastructure definitions can be stored in version control systems like Git, allowing for easy tracking of changes, rollbacks, and collaboration.
1. **Automation**: IaC enables the autmoation of infrastructure provisioning and management, saving time and reducing manual intervention.
1. **Scalability**: With IaC, you can easily scale your infrastructure up or down by modifying the code, making it more adaptable to changing needs.
1. **Documentation**: The code itself serves as documentation, providing a clear and up-to-date reference for the infrastructure setup.
1. **Cost Efficiency**: By autmoating and optimizing resource usage, IaC can help reduce costs associated with over-provisioning and manual management.

Terraform is considered by many as the industry-leading IaC tool of choice for a variety of reasons:

1. **Multi-Cloud Support**: It is cloud agnostic, allowing users to provision to both public and private clouds with the same basic syntax, reducing the need to learn multiple frameworks. 
1. **Declarative Language**: Terraform uses HashiCorp Configuration Language (HCL), a declarative language, which makes it easy to define infrastructure in a human-readable format. This simplifies the process of understanding and managing your cloud estate.
1. **State Management**: Terraform maintains a state file that keeps track of the current state of the infrastructure. This allows for efficient updates and ensures that the infrastructure matchces the desired configuration.
1. **Modularity and Reusability**: Terraform supports modules, which are reusable components that can be shared and used across different projects. This promotes best prqactices and reduces duplication of effort.
1. **Community and Ecosystem**: Terraform has a large and active community, which means there are plenty of resources and plugins available. This makes it easier to find solutions and get support.
1. **Extensibility**: Terraform's plugin architecture allows users to extend its functionality by writing custom providers and modules. This makes it highly adaptable to different use cases and environments.

### Installing Prerequisites

To use this learning repository, it is best to open this repository in VS Code and work there. There are a few prerequisites to do so:

- VS Code installed on your device (with at least version 1.9.5).
- Terraform installed on your device (and added to your system's PATH).
- Git installed on your device.
- Git configuration declared on your device via CLI.
- The following VS Code extensions are recommended:
  - HashiCorp Terraform
  - Remote Development
  - GitHub Repositories

Take the time to ensure these are seen to before proceeding.

### Understanding the `Terraform` Block

Terraform uses a specific language framework to define a configuration's essential properties. The first is called `terraform` block. To create a `terraform` block, you must first create a Terraform file. Create a file in your working branch (named `terraform-basics`) named `main.tf`. The `.tf` extension will tell VS Code that this file is a Terraform file and will load all the appropriate extensions to help assist your Terraform coding.

[Terraform providers](https://registry.terraform.io/browse/providers) are the plugins that tell Terraform which different kinds of resources you plan to deploy, telling Terraform which providers to load. The three primary providers used with Azure are `azurerm`, `azapi`, and `azuread`. The `azapi` provider is less used than the others and is more complicated in its syntax. For most lessons, we will be using the `azurerm` or `azuread` providers. This lesson focuses exclusively on the `azurerm` provider. Let's create a properly formatted `terraform` block in your `main.tf` file. Copy the following code into that file:

```terraform
terraform {
  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm
      version = "=4.5.0"
    }
  }
}
```

You will notice that the provider `azurerm` has a specific version listed in the configuration. This is called a version constraint.

### Version Constraints in Terraform

Version constraints in Terraform are used to specify which versions of a provider or module are compatible with your configuration. This ensures that your infrastructure code works with the correct versions and avoids potential issues caused by incompatible changes. There are several types of version constraints you can use:

- **Exact version**: Specifies a single version that must be used. For example, `version = "=4.5.0"` ensures that only version 4.5.0 of the provider is used.
- **Greater than or equal to**: Specifies a minimum version that must be used. For example, `version = ">=4.5.0"` allows any version greater than or equal to 4.5.0.
- **Less than or equal to**: Specifies a maximum version that can be used. For example, `version = "<=4.5.0"` allows any version less than or equal to 4.5.0.
- **Range**: Specifies a range of versions that can be used. For example, `version = ">=4.5.0, <5.0.0"` allows any version from 4.5.0 up to, but not including, 5.0.0.
- **Wildcard**: Specifies a version pattern that can be used. For example, `version = "~>4.5"` allows any version in the 4.5.x series, but not 4.6.0 or higher.

Using version constraints helps maintain stability and predictability in your Terraform configurations by ensuring that only compatible versions of providers and modules are used. For the purposes of this lesson, we will use version 4.5.0 of the `azurerm` provider.

Terraform itself can likewise be bound by version constraints. This is important, especially when developing modules, as some features of Terraform are not available with previous versions. Let's add a version constraint to Terraform now. Edit your `terraform` block in your `main.tf` file so that it looks like this:

```terraform
terraform {
  required_version = ">=1.9.5"

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm
      version = "=4.5.0"
    }
  }
}
```

### Configuring a Provider Block

Terraform also requires a `provider` block to configure where Terraform will deploy its resources. We will now add a `provider` block for `azurerm`. Add this below the `terraform` block to your `main.tf` file:

```terraform
provider "azurerm" {
  features {}
  subscription_id = "<insert-your-subscription-id-here>"
}
```

Your whole file should now look like this:

```terraform
terraform {
  required_version = ">=1.9.5"

  required_providers {
    azurerm = {
      source  = "hashicorp/azurerm
      version = "=4.5.0"
    }
  }
}

provider "azurerm" {
  features {}
  subscription_id = "<insert-your-subscription-id-here>"
}
```

Now, save your changes and commit them all to your `terraform-basics` branch. GitHub will automatically update this README and provide the next set of instructions.
