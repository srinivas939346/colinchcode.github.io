---
layout: post
title: "[python] Adding custom SSL certificates in Python Requests"
description: " "
date: 2023-10-03
tags: [python]
comments: true
share: true
---

When making HTTP requests in Python using the popular `requests` library, it's important to ensure that the connection is secure. By default, `requests` performs SSL certificate verification to ensure that the server you're communicating with is authentic and trusted.

In some cases, you may need to connect to a server that has a custom SSL certificate, such as a self-signed certificate or a certificate signed by a trusted certificate authority (CA) not included in the Python certificate store. In such scenarios, you need to explicitly provide the SSL certificate to `requests` to establish a secure connection.

Here's how you can add custom SSL certificates in Python Requests:

## 1. Obtaining the SSL certificate

Firstly, you need to obtain the SSL certificate from the server you want to connect to. There are different ways to obtain the certificate, but one common method is using the OpenSSL command-line tool:

```shell
openssl s_client -showcerts -connect <host>:<port> > certificate.crt
```

This command connects to `<host>:<port>` and saves the SSL certificate in PEM format to `certificate.crt`.

## 2. Adding the SSL certificate to Requests

Once you have obtained the SSL certificate, you can add it to your Python code using the `requests` library.

```python
import requests

cert_path = '<path_to_certificate.crt>'

response = requests.get('https://example.com', verify=cert_path)

print(response.text)
```

In the above example, replace `<path_to_certificate.crt>` with the actual file path where you saved the SSL certificate obtained from the server. The `verify` parameter is used to specify the path of the certificate file. This tells `requests` to use the specified certificate for SSL verification.

Note that if you're using a self-signed certificate, you may also need to set the `verify` parameter to `False`, as shown below:

```python
response = requests.get('https://example.com', verify=False)
```

However, disabling certificate verification should be done with caution as it may expose you to potential security risks.

## Conclusion

Adding custom SSL certificates in Python Requests allows you to establish secure connections with servers that have non-traditional or self-signed certificates. By providing the SSL certificate to `requests`, you can ensure secure communication and data integrity.

Remember to use caution when disabling SSL certificate verification and only do so if you're confident about the authenticity of the server you're connecting to.

Happy coding!