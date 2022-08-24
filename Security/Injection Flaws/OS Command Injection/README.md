# OS Command Injections

## What are OS Command Injections
An "OS Command Injection" is a vulnerability that allows arbitrary commands to be executed on the operating system of the application.

## What causes OS Command Injections
This vulnerability can happen when user-controlled input, through parameters, cookies, HTTP headers, etc, is passed to the system shell without any prior validation.

## What are the impacts of OS Command Injections
Injected commands will run with the privileges of the vulnerable application.\
Sensitive data could be displayed on the application output.\
Customer data could get exposed.\
Files or database records could be manipulated or deleted, and, services could even be started or stopped.\
In a worst-case scenario, all the files of the application could be deleted.

## Example
An attacker may pass to a system shell a malicious URL, such as deleting the whole www directory.

```
http://site.com/action/delete?fileToDelete=a.txt;`rm -rf /var/www`
```

In the URL above, the attacker passes a shell command to the parameter value of a request.\
The application might append the GET parameter to the command string and the malicious command is executed.\
This will cause all the web application files to be deleted.\
Which leads to the web application being unavailable.

## How to prevent OS Command Injections
- Use framework-specific API calls instead of OS commands.
- If it is not possible to use a framework, validate all user-controlled output against an allowlist before passing it to the shell.\
  This validation should include POST and GET parameters, Cookies, and HTTP headers.
- Apply the principle of least privilege to the application.

## More info
Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://www.owasp.org/index.php/Command_Injection
- Identify OS Command Injection: https://www.owasp.org/index.php/Testing_for_Command_Injection_(OTG-INPVAL-013)
