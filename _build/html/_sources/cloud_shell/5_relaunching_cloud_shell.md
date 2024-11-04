# Relaunching Cloud Shell

You've configured your Cloud Shell as a virtual machine with persistent storage within Azure. However, it is ephemeral and some of its settings are reset when you shut it down and restart it.

If you are going to work with Python and/or Cloud Functions using Cloud Shell, you **MUST** perform the following steps as soon as you open a new instance of Cloud Shell.

1. **MAKE SURE YOU ARE USING THE 'CLASSIC' VERSION OF CLOUD SHELL**
    * In Cloud Shell, go to Settings and choose **'Go to Classic version'**
    * If the Settings menu shows **'Go to beta version'**, you are in the right place
2. You should see a block of instructions labeled "NOTES FOR MGMT 59000 CLOUD COMPUTING"
    * If you **do** see the block of instructions, move to step 3, below
    * If you **do not** see the block of instructions, return to the [Install AFCT page](function_app:install_afct:download_scripts) and re-run those instructions
3. To develop with Python, activate your virtual environment with `start_venv`
4. To develop or deploy Cloud Functions, install AFCT by typing `install_afct`