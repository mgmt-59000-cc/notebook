# Set up Git on Azure Cloud Shell

Git is source control management software that allows you to manage, back up, and collaborate while you are doing development work. Git is automatically installed on the Azure Cloud Shell.

## Configure Git on Azure Cloud Shell

Configure Git so it can automatically add your user details to the commits you will make to your repositories. You should only need to do this one time, but you can re-run these commands anytime you need.

1. Input the following commands on the Azure Cloud Shell command line, replacing the information as needed with your personal details.

```
git config --global user.name "Your Name"
```

You will *not* see any kind of feedback from the command prompt after you issue this command.

2. Use your school email address here (@purdue.edu):

```
git config --global user.email "youremail@purdue.edu"
```

Again, the command prompt will be empty after this command.

3. Finally, confirm that Git on your Azure Cloud Shell uses `main` as the default branch name.
```
git config --global init.defaultBranch main
```

You will again not see a confirmation message.