# Set Up Cloud Shell
Azure Cloud Shell is a virtual machine that you can access through a web browser. You have options for a Linux (Bash) or Windows (PowerShell) machine.

**In this course we will use the Linux (Bash) version of Azure Cloud Shell.**

## Create an Azure Resource Group and Storage for your Cloud Shell files
The first time you run Cloud Shell you must create cloud storage space for the files you will use in Cloud Shell. Fortunately, Cloud Shell will do some of the work for you.

### Open the Cloud Shell
1. Visit the [Azure Portal](https://portal.azure.com)
    * Log in with your USERNAME@purdue.edu account
2. Click the "Cloud Shell" icon at the top of the screen

```{image} images/cloud_shell.png
:alt: Screenshot of the Azure Portal toolbar
:align: center
:width: 500px
```

3. Choose `Bash`
4. Choose `Mount storage account`
    * Choose `Azure for Students` under subscription
5. Choose `We will create a storage account for you` and click `Next`
6. Once Cloud Shell opens, go to Settings and choose `Go to Classic version`
```{image} images/cloud_shell_settings.png
:alt: Screenshot of Cloud Shell settings menu
:align: center
:width: 150px
```
7. Once you have loaded Cloud Shell in the Classic version, your screen should look similar to the following:
```{image} images/cloud_shell_classic_version.png
:alt: Screenshot of Cloud Shell Classic Version
:align: center
:width: 500px
```

You are now ready to continue.

# Demo: Creating a File in Cloud Shell

Practice using Linux command line commands to view and create directories and files.

1. `ls` lists files (note `clouddrive` is there)
2. `cd clouddrive`
3. `ls` (empty - no files)

## Create a new directory

Create a new directory, make it the working directory, and create a new file named `dummy.md`

```
mkdir dummy && cd dummy
touch dummy.md
```

1. Type `ls` to see the files in the working directory

## View the file you created in Storage browser
1. In Azure portal (web), from the hamburger menu choose `Storage accounts`
2. Click the Storage account named something similar to `cs210030000974e3518` *this was automatically created for you*
3. Choose `Storage browser`
4. Choose `File shares`
5. Click the only folder that appears
6. Open the directory you created `dummy`
7. Note `dummy.md`
8. In Cloud Shell, `touch dummy2.md`
9. Refresh the Storage browser
    * You should see the new file `dummy2.md` already listed