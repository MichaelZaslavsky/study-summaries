# CRLF Injection

## What is CRLF Injection
CRLF refers to carriage return and line feed, which are used for line termination.\
CRLF injection takes place when a user can start a new line by injecting one or both of these characters (e.g. `&%0d%0a`).

## What causes CRLF Injection
A user is can inject a carriage return or line feed in a URL or HTTP parameter which is not sanitized and is therefore processed by the application.

## What are the impacts of CRLF Injection
The vulnerabilities allow an attacker to manipulate server-side files, so an attacker could add new lines to files such as logs.\
An attacker could also abuse CRLF injection to perform HTTP response splitting which returns multiple HTTP responses to the target user and could redirect them to malicious URLs or scripts.

## Examples

1. An attacker may append a CRLF injection to the URL, containing a fake log entry by adding &%0d%0a.\
   The %0d is URL encoding for a carriage return, while %0a is an encoded line feed which together will be interpreted as a new line.

   ```
   https://site.com/index.php?page=home&%0d%0a
   ```

2. An attacker can send a malicious link that will be sent to a victim.
   The malicious link will point to another domain that is specified by the attacker.

## How to prevent CRLF Injection

- Never trust user input!
- Implement application-wide filters.
- Properly sanitizing user inputs and performing encoding on the outputs can prevent this type of attack.
- Remember to consider GET and POST parameters, Cookies, and other HTTP headers.
- Apply HTML encoding to anything sent back to the browser.

## More info

Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://www.owasp.org/index.php/HTTP_Response_Splitting
- Identify HTTP Injection: https://www.owasp.org/index.php/Testing_for_HTTP_Splitting/Smuggling_(OTG-INPVAL-016)
