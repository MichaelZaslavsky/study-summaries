# SQL Injection

## What are SQL Injections
SQL Injection occurs when an attacker can inject SQL queries by the input data of an application.\
A successful attack allows an attacker to access and manipulate the backend database.

## What causes SQL Injections
User input is used to to build queries dynamically. If this input is not first validated the query interpreter can be tricked into running arbitrary SQL queries or commands.\
To prevent SQL injection developers should use parameterized queries.

## What are the impacts of SQL Injections
A successful injection could allow an attacker to update/insert/delete data.\
All data could be exposed or even deleted. Furthermore, access to the hosting system could be gained by an attacker, with proper Authentication processing being bypassed.\
As a result, any altered data such as balance and transaction information could cause repudiation issues.

## Example

Developers should never contacatenate user-controllable input with application SQL to form the query ssent to the database.
```C#
string sql = $@"
    SELECT  U.*
    FROM    dbo.Users U
    WHERE   U.FirstName = {firstName}
            AND U.LastName = {lastName};"
```

The SQL Injection can be passed in the firstName or lastName parameters.\
e.g: LastName = "some name OR 1 = 1;"

Instead, use parameterized queries like the following example.\
All popular development frameworks provide support for the secure construction of database queries.
```C#
string sql = @"
    SELECT  U.*
    FROM    dbo.Users U
    WHERE   U.FirstName = @FirstName
            AND U.LastName = @LastName;"
```

## More tips for preventing SQL Injections

- Use allowlist validation on all user input. This ensures all input is checked against an allowed list of input parameters, before they are processed in the code.
- Apply the least privilege principle to all backend database users.
- Consider GET and POST parameters, Cookies, and other HTTP headers.

## More info

Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://owasp.org/www-community/attacks/SQL_Injection
- Identify SQL Injection: https://www.owasp.org/index.php/Testing_for_SQL_Injection_(OTG-INPVAL-005)
- Remediation approaches: https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html
https://www.youtube.com/embed/pypTYPaU7mM

Relevant material published by the Software Assurance Forum for Excellence in Code (SAFECode):\
SAFECode resources: https://safecode.org/courses/injections-101-sql-and-beyond/
