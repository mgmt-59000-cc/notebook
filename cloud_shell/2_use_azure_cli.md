# Use the Azure CLI in Cloud Shell
The Azure Command Line Interface (CLI) is a program that allows you to interact with Azure resources by issuing text-based commands.

The Azure CLI commands start with the `az` keyword.

You can likely perform most of these functions in the graphical user interface (GUI) located in the [Azure Portal](https://portal.azure.com), but learning the CLI is important too.

1. View a list of your subscriptions with 

```
az account list --output table
```

* You should see a single subscription entitled "Azure for Students"

2. View a list of your resource groups with

```
az group list --output table
```

* You will see a list of **resource groups**
* Note the resource group that was automatically created when you created your Cloud Shell storage

We will use other CLI commands to manipulate Azure resources shortly.