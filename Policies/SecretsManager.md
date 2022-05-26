# Secrets Manager
Secrets Manager enables you to replace hardcoded credentials in your code, including passwords, with an API call to Secrets Manager to retrieve the secret programmatically. This helps ensure the secret can't be compromised by someone examining your code, because the secret no longer exists in the code. Also, you can configure Secrets Manager to automatically rotate the secret for you according to a specified schedule. This enables you to replace long-term secrets with short-term ones, significantly reducing the risk of compromise.

## Features
- Programmatically retrieve encrypted secret values at runtime 
- Store different types of secrets
- Encrypt your secret data using KMS
- Automatically rotate your secrets
- Databases with fully configured and ready-to-use rotation support
- Control access to secrets using resource based policies

---------------
[Go Home](../README.md)