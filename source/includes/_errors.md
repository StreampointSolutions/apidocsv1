# Errors


Error Code | Meaning
---------- | -------
400 | Bad Request -- The server cannot or will not process the request due to an apparent client error (e.g., malformed request syntax, invalid request message framing, or deceptive request routing).
401 | Unauthorized -- Unauthorized: Access is denied due to invalid credentials.
403 | Forbidden -- The request was a valid request, but the server is refusing to respond to it.
404 | Not Found -- The requested resource could not be found but may be available in the future.
405 | Method Not Allowed -- A request method is not supported for the requested resource; for example, a GET request on a form which requires data to be presented via POST, or a PUT request on a read-only resource.
406 | Not Acceptable -- e requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request.
410 | Gone -- Indicates that the resource requested is no longer available and will not be available again. 
429 | Too Many Requests -- The user has sent too many requests in a given amount of time. Intended for use with rate limiting schemes.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- The server is currently unavailable
