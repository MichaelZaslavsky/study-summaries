# Code Injection

## What is Code Injection?
It's a general term given to vulnerabilities that allow a user to inject code that gets interpreted and executed by the application.\
Code injection is limited to the capabilities of the injected language.\
It can happen both on the server and on the client side.

## What causes Code Injection?
These vulnerabilities occur when untrusted input is used in a context where it can be treated as actual code.\
The input is not properly validated or encoded before being used.

## What are the impacts of Code Injection
It could allow privilege escalation and command injection on the system.\
This could lead to the server falling into an attacker's hands.\
An attacker could modify parts of the application and retrieve sensitive information.\
Also, malware could be installed on the application serves leading to attacks such as cookie theft, site defacement, or phishing.

## Example
Let's assume a Math app that allows users to perform calculations on the input.\
The calculation is performed using an unsafe eval function.

```JavaScript
$calc = "5X5 + 2";
print eval('return '.$calc,';');
```

An attacker manipulates a calculation and enters a string that will result in command execution.

```JavaScript
$calc = "system('ls')";
print eval('return '.$calc.';');
```

As a consequence, the ls command is executed and the directory contents are returned to the attacker.

## Preventing Code Injection
- Developers should never trust user input!
- Use parameterized queries and apply least privilege, such as a read-only user on both the client and the server side.
- Apply application-wide filters or sanitization on all user-provided input through filtering, encoding, and allowlist validation. Libraries exist for this, in different frameworks.\
And remember to check not only GET and POST parameters, but Cookies and other HTTP headers as well.
- If possible, don't let functions execute or interpret user input directly.

## More info

Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://owasp.org/www-community/attacks/Code_Injection
- Identify Code Injection: https://www.owasp.org/index.php/Testing_for_Code_Injection_(OTG-INPVAL-012)
