# Path Traversal

## What is Path Traversal
Attackers user path traversal to access files or directories stored in the file system of a web server or application, outside of the web root folder.\
To do so, they manipulate the URL path input to the web app using ../ sequences, double URL encoding, or direct file paths.\
Path traversal is an attack with many names! It's also called directory traversal, directory climbing, backtracking, or, simply, dot-dot-slash.\
Though most modern browsers have some level of built-in protection against basic path traversal attacks, Attackers can still get by using variations of the dot-dot-slash technique.

## What are the impacts of Path Traversal
An attacker may access sensitive information, such as user passwords, private documents, etc.

## Example
In case there is an insecure API that allows users to request image files stored in the web server by providing the filename parameter, an attacker can enter an arbitrary file from the server's file system to access sensitive data.\

```
https://myserver.com/loadfile?filename=../../etc/passwd
```

In an insecure site the command above causes the application to read from the following file path "/var/www/myserver/images/../../etc/passwd".\
The two consecutive dot-dot-slash sequences move the attacker up to the root filesystem.\
So the file being read is "/etc/passwd".\
That's how the attacker can see sensitive information.

## How to prevent Path Traversal
- Test for path traversal vulnerabilities.
- Work without user input when using file system calls.
- Use indexes instead of parts of file names when templating or using language files.
- Be sure that users are unable to supply all parts of the path.
- Use chrooted jails and code access policies to restrict unintended access and modification of files.
- When user input must be submitted for file operations, normalize the input before using in-file IO APIs.

## More info
Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://www.owasp.org/index.php/Path_Traversal
- Identify Path Traversal: https://www.owasp.org/index.php/Path_Traversal
- Identify Path Traversal: https://www.owasp.org/index.php/Testing_Directory_traversal/file_include_(OTG-AUTHZ-001)
- Remediation approaches: https://www.owasp.org/index.php/File_System#Path_traversal
