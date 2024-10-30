# Set Up Cloud Shell for Cloud Function Development

Although you have the Azure CLI already installed, there is another package that must be installed in order to create and deploy Azure Cloud Functions. This is called **Azure Functions Cloud Tools** or AFCT.

(function_app:install_afct:download_scripts)=
## Download Scripts to Help With Installation
I have written a script that will modify your Cloud Shell to provide commands needed for this course.

1. **MAKE SURE YOU ARE USING THE 'CLASSIC' VERSION OF CLOUD SHELL**
    * In Cloud Shell, go to Settings and choose **'Go to Classic version'**
    * If the Settings menu shows **'Go to beta version'**, you are in the right place

Execute the remaining commands on the Cloud Shell command line IN ORDER and wait for each to finish before moving on.

```
cd ~/clouddrive
git clone https://github.com/robpurdue/afct
cd afct
chmod +x *.sh
./setup_shell.sh
```

You can now proceed with the installation of Azure Functions Cloud Tools (AFCT).

## Install AFCT
The terminal should display the new commands for you to use.

1. Enter `install_afct` on the command line *this will take a few minutes*

2. Once the software loads, you **MUST** reload your Cloud Shell settings by entering the following command
```
source ~/.bashrc
```
You will be returned to the command prompt. AFCT is now installed.