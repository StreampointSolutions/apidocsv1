---
title: Streampoint API Reference

language_tabs:
  - csharp: .NET (C#)
  - python: Python
toc_footers:
  - <a href='mailto:api@streampoint.com'>Contact us for a Developer Account</a>
  - <a href='http://www.streampoint.com'>© 2017 Streampoint Solutions</a>

includes:
  - country
  - exhibitor
  - payment
  - paymenttype
  - person
  - provstate
  - question
  - registrationtype
  - seminar
  - seminarcredittype
  - seminartrack
  - speaker
  - speakerfile


search: true
---

# Introduction
Welcome to the Streampoint API Documentation!

Use the documentation on this site to learn how to implement services to pull registration data from the Streampoint system.  Information on attendee, exhibitor and speaker registrations are available to be requested.  Currently, our API offers read-only access to the system.

To date, we provide language bindings in C# only.  You will find code samples to the right and can switch between languages using the tabs at the top as they become available.  Please note that all code snippets provided are for reference and illustration purposes only. They are to show you how to format requests and what kind of data to expect in return.  Simply using the code as is may not work out of the box.

If you have any questions, feel free to contact us at <a href="mailto:api@streampoint.com">api@streampoint.com</a>
# Getting Started

Streampoint offers REST access to our systems through two endpoints.  Each environment is given separate credentials, use the appropriate keys to access the test and production environments accordingly.  To get started today, please contact <a href="mailto:api@streampoint.com">api@streampoint.com</a> to request a developer account.

###UAT (Testing) Environment:

REST: https://apireststaging.streampoint.com/v1/personal.svc

###Production Environment:

REST: https://apirest.streampoint.com/v1/personal.svc



# Authentication

Authentication to the API is made using HTTP Basic Auth.  Every request your application makes to the Streampoint API must include your API keys for authentication.

## REST Authentication

```csharp
const string token = "TOKEN GOES HERE";
const string baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
const string dataPullEndpoint = "DATA ENDPOINT GOES HERE";

var pullRequest = (HttpWebRequest)WebRequest.Create(baseUrl + dataPullEndpoint);
pullRequest.Method = "GET";
pullRequest.ContentType = "application/json";
pullRequest.KeepAlive = false;
pullRequest.Timeout = 3600000;
pullRequest.Headers.Add("x-auth-token", token);
```

```python
const token = "TOKEN GOES HERE";
const baseUrl = "https://apireststaging.streampoint.com/v1/personal.svc";
const dataPullEndpoint = "DATA ENDPOINT GOES HERE";

pullRequest = curl_init(baseUrl . dataPullEndpoint); 
curl_setopt($pullRequest, CURLOPT_HTTPGET, true);
$header = array();
$header[] = "Content-type: application/json";
$header[] = "x-auth-token: " . token;
curl_setopt($pullRequest, CURLOPT_HTTPHEADER, $header);
curl_setopt($pullRequest, CURLOPT_FORBID_REUSE, true);
curl_setopt($pullRequest, CURLOPT_TIMEOUT, 3600);
curl_setopt($pullRequest, CURLOPT_RETURNTRANSFER, true);
```


Using this implementation, you will need to authenticate by providing an authorization token.

Please refer to the code sample to the right.




