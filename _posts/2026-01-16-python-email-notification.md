---
title: Sending Email Notifcation using Python
date:  2026-01-16 17:00:00 +0800
categories: [Knowledge, Python]
tags: [python, documentation, knowledge]     # TAG names should always be lowercase
description: A guide on using smtplib library for email notifications.
---

## Imports
In order to send email notification using Python, the smtplib library will need to be imported.

The smtplib library is a built in Python module and it is already included within the standard Python installation. No further pip installation is required.

```python
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
```

## Code 
Create a function to to set up the email content and SMTP connection.

```python
#---------------------
# Set up email content
#---------------------
def send_error_email(error_message):
    subject = 'Notification: Datasource Pipeline Failure'
    body = 'An error occurred during the execution of the datasource pipeline, please investigate the issue.' + f"\n\n{error_message}"
    sender_email = 'NoReply@company.com'
    list_of_recipients = ['user@company.com']

    # Create a multipart message
    message = MIMEMultipart()
    message['Subject'] = subject
    message['From'] = sender_email
    message['To'] = ', '.join(list_of_recipients)

    # Attach the email body
    message.attach(MIMEText(body))

    # Set up the SMTP connection
    smtp_server = 'mailrelay-internal.company.com'
    smtp_port = 25

    # Connect to the email server and send the email
    server = smtplib.SMTP(smtp_server, smtp_port)
    server.sendmail(sender_email, list_of_recipients, message.as_string())
    server.quit() 
```

## Use Case
The send_error_email function can be used to send email notification to developers whenever an error occurs in the script.

First, create a number that will sum up two numbers.

```python
#-----------------------------
# Function to sum up 2 numbers
#-----------------------------
def calculator(num1, num2):
    try:
        sum = num1 + num2
        return sum
    except Exception as e:
        send_error_email(f"Error message received from calculator function:\n{str(e)}")
```

Next, call the function.
```python
# This will return the right result
calculator(10, 20) 

# This will raise an exception and trigger the email notification
calculator(10, '20') 
```
