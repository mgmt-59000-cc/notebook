# Initialize a new Azure Cloud Function

Using the Cloud Shell as your "local" development machine, you'll now create the files necessary for an Azure Cloud Function.

Azure Cloud Function Tools (ACFT) will create the default Python code as well as other required files for you.

## Create a new directory for our Cloud Function files
1. `cd ~/clouddrive`
2. `mkdir hello_world && cd hello_world`

## Initialize a new Azure function
Ensure you are at the command line in your `hello_world` directory.

1. Type `func init`
2. Choose `python`
3. Type `func new`
4. Choose `HTTP trigger`
5. For function name, enter `hello_world`
6. Choose `ANONYMOUS` for Auth Level

The default files have been created for you. To see the files, do the following:

1. `ls` to see the files that were created
2. `code .` to open the files for editing