# Blob Storage Function App
Follow the steps in this section to write a Cloud Function App that is triggered when a new file is uploaded to blob storage.

This is a common scenario in several cloud pipelines. Think of all the functionality you might want to perform on files as they are uploaded:

* Format file contents for consistency
* Sort files based on contents
* Scan files for vulnerabilities
* Extract file contents and store elsewhere (a database, etc.)
* Rename files
* ...and so on

This demo app will show you how to create the necessary resources to marry a function app with blob storage, and then execute the logic of that function app when a new blob is uploaded.

In this application, you will simply copy an uploaded file to a new directory. It's a simple application, but there are several steps that must be executed to build the functionality.