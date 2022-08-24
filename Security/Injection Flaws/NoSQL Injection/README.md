# NoSQL Injection

## What is NoSQL Injection
NoSQL injections occur when an attacker is able to inject malicious code into a NoSQL database.\
This is typically done through JSON and Javascript code.\

## What causes a NoSQL Injection
The application makes use of NoSQL database and does not properly validate user input before using it to query the database.\

## What are the impacts of NoSQL Injection
A successful injection could allow an attacker to update, insert or delete data.\
All data could be exposed or deleted.\
Access to the hosting system could be gained and authentication could be bypassed.

## Example
An attacker may bypass authentication through an interception proxy and submit input values that change the query's logic.\
A NoSQL comparison operator might be passed instead of the normal username and password.\

```
Username: { $ne: "}
Password: { $ne: "}
```

The username and password from the database will be compared to the empty string, resulting in an always true condition.\
As a consequence of the always true comparison, the attacker has logged in as the first user in the database, usually, it is the admin.\
The session cookie is returned to the browser and the attacker is logged in.

## How to prevent NoSQL Injection
- Input should be JavaScript escaped or validated before being used to query the database.
- Apply allowlist validation on all user input, including GET and POST parameters, Cookies, and other HTTP headers.\
  This ensures that all input is checked against an allowlist of input parameters before being processed.
- Use a database ORM instead of raw queries.
- Always validate input parameters. Coerce input to the correct types during validation routines.
- Always apply the least privilege principle to database users.
- Use explicit comparison operators such as $eq in query expressions rather than allowing implicit equality matching.

