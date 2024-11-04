# Test the Azure Cloud Function App "Locally"

You've generated the starter code for an Azure Cloud Function. You can run this code on your "local" machine (which, in this case, is the Cloud Shell VM).

1. `func host start`
2. Note the port number that is running the app (7071)
3. Click the Web Preview icon 📄🔎 in the Cloud Shell toolbar
4. Choose `Configure`
5. Input `7071`
6. Choose `Open and browse`
7. You will see a lot of code in the window (maybe)
8. Edit the URL and append `api/hello_world` at the end
9. Note the message. Now we need to add a querystring parameter and argument to pass data into the function
10. Append `?name=Rob` at the end of the URL and see the change in the response in the browser window
    * Your app is now accepting input and returning output
11. Press Ctrl+C **twice** in the Cloud Shell to stop the app from running "locally"