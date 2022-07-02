# LDAP Injection

## What is LDAP Injection
An LDAP injection is a vulnerability by which an attacker can influence backend LDAP queries by injecting malicious LDAP statements via user-controllable input.

## What causes an LDAP Injection
User input is used to dynamically build LDAP queries.\
If this input is not first validated, the LDAP query interpreter can be tricked into running arbitrary queries.

## What are the impacts of an LDAP Injection
Sensitive information about users and hosts represented in the LDAP tree could be disclosed, modified, inserted, or deleted.\
LDAP injection could be used to bypass access control and gain access to administrator accounts.\
Sensitive data could be exposed leading to privacy issues.

## Examples
1. Bypass an authentication process through an LDAP Injection.\
   Input values of a login:

    ```
    Username = admin)(&))
    Password = any
    ```

   The submitted input changes the logic of the query. The ampersand in the parentheses "(&)" is interpreted as a "TRUE" statement. Because of this additional true statement - the password condition will be ignored.\
   The vulnerability is exploited by giving access to an account without providing a valid password.\
   This leads the session Cookie to be returned to the browser and the attacker is now logged in as administrator.

2. Information disclosure through an LDAP Injection.\
   The Input value of search users:

   ```
   /search?user=*
   ```

   The submitted input changes the logic of the query so that the wildcard statement queries all users in the LDAP tree.\
   The vulnerability is exploited to gain detailed information about all users in the LDAP tree resulting in a major bridge of security.

## How to prevent LDAP Injection
- User input that is being used as part of an LDAP query should be sanitized first. This includes GET and POST parameters, cookies, and other HTTP headers.
- Always use framework-provided function when available and make use of escaped variables in LDAP queries.
- Use LDAP Injection resistant frameworks, automatic LDAP encoding, and framework provided functions, where possible.
- Perform validation through an allowlist.
- Minimize LDAP binding account privileges by using the Least Privilege principle.

## More info
Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://owasp.org/Top10/A03_2021-Injection/
- Identify LDAP Injection: https://owasp.org/www-project-web-security-testing-guide/stable/4-Web_Application_Security_Testing/07-Input_Validation_Testing/06-Testing_for_LDAP_Injection
- Remediation approaches: https://cheatsheetseries.owasp.org/cheatsheets/LDAP_Injection_Prevention_Cheat_Sheet.html
