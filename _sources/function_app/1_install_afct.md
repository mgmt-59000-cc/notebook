# Set Up Cloud Shell for Cloud Function Development

Although you have the Azure CLI already installed, there is another package that must be installed in order to create and deploy Azure Cloud Functions. This is called **Azure Functions Cloud Tools** or AFCT.

## Download Scripts to Help With Installation
I have written a script that will modify your Cloud Shell to provide commands needed for this course.

1. **MAKE SURE YOU ARE USING THE 'CLASSIC' VERSION OF CLOUD SHELL**
    * In Cloud Shell, go to Settings and choose **'Go to Classic version'**
    * If the Settings menu shows **'Go to beta version'**, you are in the right place

Execute the remaining commands on the Cloud Shell command line IN ORDER and wait for each to finish before moving on.

2. `cd ~/clouddrive`
3. `git clone https://github.com/robpurdue/afct`
4. `cd afct`
5. `chmod +x *.sh`
6. `./setup_shell.sh`

Once these commands are completed, you can proceed with the installation of Azure Functions Cloud Tools (AFCT).

## Install AFCT
The terminal should display the new commands for you to use.

1. Enter `install_afct` on the command line *this will take a few minutes*

You will be returned to the command prompt. AFCT is now installed.

## Returning to Cloud Shell
Once you end your Cloud Shell session, your AFCT installation will be deleted.

The next time (and every subsequent time) you visit Cloud Shell, you MUST

1. Ensure you are using 'Classic version' (as described above)
2. Run `install_afct`