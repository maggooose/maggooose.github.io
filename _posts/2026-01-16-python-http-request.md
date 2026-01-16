---
title: Making HTTP request to Sharepoint
date:  2026-01-16 22:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on making HTTP request to SharePoint using service account.
---

## Imports
In order to make HTTP request to SharePoint using a service account, the request and request_ntlm libraries will need to be installed first as both are third-party libraries.

The request library is used for making standard HTTP request like GET or POST, while requests_ntlm is a plugin that adds supports for NTLM (NT LAN Manager) authentication, which is commonly used in Microsoft Windows-based networks.

Using the HttpNtlmAuth with a request.Session() object leads to better performance as it helps to handle connection pooling efficiently as NTLM authenticates connections rather than individual requests.

Both libraries will be installed using pip, the standard package manager for Python, through the command prompt.

```shell
pip install request requests_ntlm
```

After installation, import the request library.

```python
import requests
from requests_ntlm import HttpNtlmAuth
```

## Code 
Create a dictionary to store the service account credentials and the SharePoint url.

```python
#-----------------------------
# Service Account Credentials
#-----------------------------
service_account_credentials = {
    'user': ' ',
    'password': ' ',
    'server': 'https://ishare.ap.company.com/', # replace company with actual company domain
    'site': ' ', # specify the folder location
    'domain': ' ',} # specify the company domain
```

Create a function to enable connection to SharePoint and esablish a connection to SharePoint.

```python
#----------------------------------
# Function to connect to SharePoint
#----------------------------------
def get_connection(user, password, server_url, site_url, domain):
    try:
        url = server_url + site_url
        con = requests.session()
        con.auth = HttpNtlmAuth(username=f'{domain}\\{user}',password=password)
        con.verify = False
        con.headers = {'Accept': 'application/json'}
        con.get(url)
        return con
    except Exception as e:
        send_error_email(f"SharePoint connection error. \nError message received: {str(e)}")
```

```python
#----------------------------
# Establish iShare Connection
#----------------------------
conn = get_connection(service_account_credentials['user'], 
                      service_account_credentials['password'], 
                      service_account_credentials['server'], 
                      service_account_credentials['site'],
                      service_account_credentials['domain'])
```

## Use Case (to be updated)

Reading excel files from SharePoint folder.
