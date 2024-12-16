## Step 2: Creating a Resource Group

### Declaring a Resource BLock

We will now move on to creating the most fundamental of resources in Azure: the resource group. Resources are logical containers for other resources in Azure. Nothing can exist without the resource group.

Resource declaration in Terraform has a specific syntax and always follows a specific pattern. The first component in a declaration will be a word: either `resource`, `data`, or `module`. For now, we will focus exclusively on `resource` blocks; the others will be covered in future lessons.

The second component of a resource block is a string in snake-case encased in double quotes. The first word in the string is the name of the Terraform provider being used, the rest will be the resource type. In this case, it will be `"azurerm_resource_group"`.

The third component of a resource block is the semantic name of the resource. This is not the name of the resource in Azure, but simply a moniker by which Terraform will refer to the resource in question within the configuration. In actual configurations, it can be anything you choose. It should be descriptive of purpose for ease of understanding. It is always good practice to write your code so that a resource's purpose is clear from its name. For the purposes of this tutorial, however, we will use Microsoft's recommended resource type abbreveation found [here](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-abbreviations), `rg`.

The full opening of this resource declaration would then be:

```terraform
resource "azurerm_resource_group" "rg" {
  ...
}
```

### Providing the Input Values

Note the curly braces: this is how Terraform encapsulates its blocks. We will now proceed with filling in the parameters for the resource group declaration. Each resource declaration (or data reference or module call, more on those in future lessons) will have various input parameters. HashiCorp hosts documentation for resources delcared with the azurerm on its [website](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs). The documentation for a resource group using azurerm version 4.5.0 can be found [here](https://registry.terraform.io/providers/hashicorp/azurerm/4.5.0/docs/resources/resource_group). Note the azurerm provider version at the top of the page. It is essential to match the documentation version with the provider version in your configuration, as a mismatch may lead to attempts at providing invalid parameters or unsupported input values.

As documented on HashiCorp's website, a resource group has four possible input parameters:

- `name` (required): The name of the resource group in Azure. This is different from the symantic name of the resource group in Terraform. This input is of type `string`.
- `location` (required): The Azure region into which the resource group will be deployed. This input is of type `string`.
- `managed_by` (optional): The Azure resource ID of the resource managing this resource group. We will leave this blank for now. This input is of type `string`.
- `tags` (optional): The Azure tag metadata assigned to the resource group. This input is of type `map(string)`.

Let us now fill in the required parameters for our resource group. Assign the value `my-test-rg` to the `name` parameter and the value `eastus2` to the `location` parameter. The final resource group block should look lite this:

```terraform
resource "azurerm_resource_group" "rg" {
  name     = "my-test-rg"
  location = "eastus2"
}
```

Now save your `main.tf` file, but _**do not yet commit your changes**_.

### Creating the Resource Group in Azure

If your code is not aligned after saving the way this is, do not worry, we will fix that in a moment. Open a terminal in your VS Code window and ensure your terminal directory location is the same as your repository's saved location on your workstation (it should be by default). Now type the command `terraform fmt`. This will automatically format all Terraform files in your directory according to HashiCorp's standards for Terraform code.

The previous step, while not essential, is useful as it makes your code much more readable to the human eye. For the purposes of this lesson, we will deploy resources with Terraform into Azure via the command-line interface. The first step would be to authenticate to Azure, either via Azure CLI or PowerShell. The choice for the purpose of this lesson is irrelevant. Do so now via your terminal in VS Code.

Once you have authenticated to Azure you may now initialize Terraform. Do so now with the following command: `terraform init`. This will validate your permissions on the Azure subscription and will load the azurerm provider for Terraform.

The next step would be to run a step called Terraform plan. This command runs "what if" for the Terraform configuration in your working directory. It compares the configuration with the state file (stored locally for this lesson) and calculates what must either be created, destroyed, or modified. Run this now in your terminal with the command: `terraform plan`. You should see a message at the end of the plan telling you that Terraform expects to create 1 resource, destroy 0 resources, and change 0 resources. The details of the resource that can be determined from a plan will also be visible in the plan report.

The final step is to create the resources in Azure with Terraform. The command to do this is `terraform apply`. Type this now into your terminal and execute. You will notice that Terraform first runs a fresh plan, just in case you have changed any configurations since your last plan. It will then prompt you whether or not to run that exact plan. Type `yes` into the terminal and hit \[enter\]. Terraform will create the resource group in Azure and deliver a report summarizing its actions.

Congratulations! You've used Terraform to deploy a resource group into Azure! Commit your changes to the `terraform-basics` branch to move to the next step of the lesson.
