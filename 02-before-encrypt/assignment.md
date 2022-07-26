---
slug: before-encrypt
id: fxzwvypleygo
type: challenge
title: Unencrypted Web Application and Database
notes:
- type: text
  contents: Now that you have completed the basics its time for a real life application
    of this process.
tabs:
- title: Vault CLI
  type: terminal
  hostname: server
- title: Web App
  type: service
  hostname: server
  path: /
  port: 3001
- title: Database
  type: service
  hostname: server
  path: /api/getUsers
  port: 3001
- title: Code
  type: code
  hostname: server
  path: /root/internvault
difficulty: basic
timelimit: 600
---
You can see that there are 5 tabs at the top. Vault CLI, Web App, Database, and Code,. You are already familar with the Vault CLI from the previous challenge. The Web App tab shows you a webpage with a Register and Login button. The Database tab shows the documents in the database, it is empty right now because we have not created any users. The Code tab shows the code that is being implemented in the backend.

Lets see how it looks without encryption.

<p style="color:rgb(255, 99, 71);"><u>Step 1:</u></p>

To start type this command into the Vault CLI tab.
```
npm start
```
This will start the webapp and database. Once the packages are installed the webapp is ready to be used.

<p style="color:rgb(255, 99, 71);"><u>Step 2:</u></p>

To register a user, navigate to the Web App tab and click `Register`. Enter a username and password and click submit.

<p style="color:rgb(255, 131, 206);"><b><u>Note: Each username entry must be unique.</u></b></p>

<p style="color:rgb(255, 99, 71);"><u>Step 3:</u></p>
Navigate to the Database tab and hit the refresh button if nothing is shown. You will now see the username you entered along with the unencrypted password in JSON format.

Go to next challenge to actually encrypt data.