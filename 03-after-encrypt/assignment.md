---
slug: after-encrypt
id: 67zrq8bhfmgy
type: challenge
title: Encrypted Web Application and Database
notes:
- type: image
  url: https://i.gifer.com/5LE3.gif
tabs:
- title: Vault CLI
  type: terminal
  hostname: server
- title: Web App
  type: service
  hostname: server
  path: /
  port: 3000
- title: Database
  type: service
  hostname: server
  path: /api/getUsers
  port: 3000
difficulty: basic
timelimit: 600
---
Following the steps of the previous challenge:

<p style="color:rgb(255, 99, 71);"><u>Step 1:</u></p>

To start we need to run `npm start` again. Type this command into the Vault CLI tab.
```
npm start
```
This will start the web app and database. Once the packages are installed the web app is ready to be used.

<p style="color:rgb(255, 99, 71);"><u>Step 2:</u></p>

Navigate to the Web App tab and click `Register`. Enter a username and password and click submit.

<p style="color:rgb(255, 99, 71);"><u>Step 3:</u></p>

<p style="color:rgb(255, 131, 206);"><b><u>Note: Remember to enter a unique username.</u></b></p>

Navigate to the Database tab and hit the refresh button if nothing is shown. You will now see the username you entered along with the encrypted password in JSON format.

<p style="color:rgb(255, 99, 71);"><u>Step 4:</u></p>
Navigate back to the Web App tab and click login. Enter the same username and password. If you entered it correctly it will redirect you to a success page.

Congratulations you have now learned how encryption works. Move to the next challenge to further understand this use-case and the application.