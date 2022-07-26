---
slug: transit-secrets-engine
id: qdjd8llld92j
type: challenge
title: Introduction to the Transit Secrets Engine
notes:
- type: text
  contents: |-
    <p>
    Congratulations, you have just been promoted to 00 status and assigned to protect precious MI6 secrets from being leaked to our enemy. Your mission is to learn the encryption capabilites of HashiCorp Vault and determine whether or not it will be beneficial to her majesty.
    </p>


    <center><img src="https://i.gifer.com/5LE3.gif">
tabs:
- title: Vault CLI
  type: terminal
  hostname: server
difficulty: basic
timelimit: 600
---
The first step of your mission is to understand the Transit Secrets Engine of Vault. For your ease Vault is already running in dev mode. The dev server is a built-in, pre-configured server that is not very secure but useful for playing with Vault locally.

<p style="color:rgb(255, 99, 71);"><u>Step 1:</u></p>

To check is Vault is running enter this into the Vault CLI tab. This will show you a list of commands you can run with Vault. You can also run `vault -help`
```
vault
```
<p style="color:rgb(255, 99, 71);"><u>Step 2:</u></p>

Before we can begin with the encryption we need to export the Vault address and Vault token. Run this command in the Vault CLI tab.
```
export VAULT_ADDR='http://127.0.0.1:8200'
export VAULT_TOKEN=root
```
This will configure the Vault client to talk to the dev server.

<p style="color:rgb(255, 99, 71);"><u>Step 3:</u></p>

To verify the server is running run `vault status`.
```
vault status
```
The output should look similar to:
```
Key             Value
---             -----
Seal Type       shamir
Initialized     true
Sealed          false
Total Shares    1
Threshold       1
Version         1.7.0
Storage Type    inmem
Cluster Name    vault-cluster-4d862b44
Cluster ID      92143a5a-0566-be89-f229-5a9f9c47fb1a
HA Enabled      false
```

<p style="color:rgb(255, 99, 71);"><u>Step 4:</u></p>

Now that we have Vault up and running we can move to the encryption part. To perform encryption the Transit secrets engine must be enabled. To check the enabled secrets engines run the following.
```
vault secrets list
```
<p style="color:rgb(255, 99, 71);"><u>Step 5:</u></p>

Here we can see that the Transit secrets engine is not yet enabled. To enable it run
```
vault secrets enable transit
```
<p style="color:rgb(255, 99, 71);"><u>Step 6:</u></p>

The next step is to create a named encryption key.
```
vault write -f transit/keys/my-key
```
After the secrets engine is configured and a user/machine has a Vault token with the proper permission, it can use this secrets engine.

<p style="color:rgb(255, 99, 71);"><u>Step 7:</u></p>

Encrypt some plaintext data using the `/encrypt` endpoint with a named key
```
vault write transit/encrypt/my-key plaintext=$(base64 <<< "my secret data")
```
The returned ciphertext starts with vault:v1:. The first prefix (vault) identifies that it has been wrapped by Vault. The v1 indicates the key version 1 was used to encrypt the plaintext; therefore, when you rotate keys, Vault knows which version to use for decryption.

<p style="color:rgb(255, 99, 71);"><u>Step 8:</u></p>

Decrypt a piece of data using the `/decrypt` endpoint with a named key
```
vault write transit/decrypt/my-key ciphertext=vault:v1:8SDd3WHDOjf7mq69CyCqYjBXAiQQAVZRkFM13ok481zoCmHnSeDX9vyf7w==
```
<p style="color:rgb(255, 131, 206);"><b><u>Note: Remember to replace the above ciphertext with the ciphertext in your Vault CLI tab.</u></b></p>

<p style="color:rgb(255, 99, 71);"><u>Step 9:</u></p>

After decryption your result will be base64-encoded. To get the raw plaintext run:
```
base64 --decode <<< "bXkgc2VjcmV0IGRhdGEK"
```
Note: If you changed the plain text in Step 7 then this encoded string will be different.

Now that you have learned the basic of encryption and using the Transit secrets engine we can move on to the real deal.

