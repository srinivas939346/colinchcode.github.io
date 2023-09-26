---
layout: post
title: "[python] Email sending and receiving using Python networking"
description: " "
date: 2023-09-26
tags: [python]
comments: true
share: true
---

Sending and receiving emails is a common task in many applications. In Python, there are multiple libraries available for handling email functionalities. In this tutorial, we will explore how to send and receive emails using Python's built-in `smtplib` and `poplib` modules.

## Sending Email using smtplib

The `smtplib` module in Python provides a simple way to send emails using the Simple Mail Transfer Protocol (SMTP). Here's an example of how to send an email:

```python
import smtplib

# Email configuration
sender_email = "your-email@gmail.com"
receiver_email = "recipient-email@gmail.com"
subject = "Hello from Python"
body = "This is the body of the email."

# Connect to the SMTP server
with smtplib.SMTP("smtp.gmail.com", 587) as server:
    # Login to your email account
    server.starttls()
    server.login(sender_email, "your-password")

    # Create the email message
    email_message = f"Subject: {subject}\n\n{body}"

    # Send the email
    server.sendmail(sender_email, receiver_email, email_message)
```

Make sure to replace `"your-email@gmail.com"` and `"recipient-email@gmail.com"` with the appropriate email addresses, and `"your-password"` with the password for the sender's email account.

## Receiving Email using poplib

To retrieve emails from a mail server, we can use the `poplib` module, which implements the Post Office Protocol (POP3). Here's an example:

```python
import poplib

# Email configuration
email = "your-email@gmail.com"
password = "your-password"
pop_server = "pop.gmail.com"

# Connect to the POP3 server
with poplib.POP3_SSL(pop_server) as server:
    # Login to your email account
    server.user(email)
    server.pass_(password)

    # Get the number of emails in the inbox
    num_emails = len(server.list()[1])

    # Retrieve the latest email
    response, lines, size = server.retr(num_emails)

    # Convert the email lines to a string
    email_content = b"\n".join(lines).decode("utf-8")

    # Print the email content
    print(email_content)
```

Again, make sure to replace `"your-email@gmail.com"` and `"your-password"` with the appropriate email credentials.

## Conclusion

With the help of the `smtplib` and `poplib` modules in Python's standard library, sending and receiving emails becomes a straightforward task. By incorporating these functionalities into your applications, you can automate email communication and streamline your workflow.

Remember to handle sensitive information, such as email credentials, securely and responsibly.