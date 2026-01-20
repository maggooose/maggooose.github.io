---
title: Making HTTP request to Sharepoint using Python
date:  2026-01-16 22:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on making HTTP request to SharePoint using a service account.
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

## Use Case
The function below will be used to download file from SharePoint using GET resquest.

```python
#------------------------------------------
# Function to download file from SharePoint
#------------------------------------------
def download_file(con, server_url, site_url, server_relative_path, output_dir='downloaded_files'):
    
    # Ensure output directory exists to download files
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)

    # Assign file name and local path
    filename = os.path.basename(server_relative_path)
    local_path = os.path.join(output_dir, filename)
    
    # Download file from the relative URL of the file in SharePoint folder
    url = f"{server_url}{site_url}_api/web/GetFileByServerRelativeUrl('{quote(server_relative_path)}')/$value"
    resp = con.get(url)
    
    # Check for successful response
    if resp.status_code == 200:
        # Write content to local folder
        with open(local_path, 'wb') as f:
            f.write(resp.content)
        print(f"Downloaded: {local_path}")
        
    else:
        print(f"Failed to download: {server_relative_path}")
        print(f"Reason: {resp.text}")
    return local_path
```

Call the function with the follow arguments.

```python
download_file(conn, service_account_credentials['server'], service_account_credentials['site'], sever_relative_path)
```



