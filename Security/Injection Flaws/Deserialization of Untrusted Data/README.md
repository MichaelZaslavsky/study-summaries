# Deserialization of Untrusted Data

## What is Insecure Deserialization
Serialization is when data structures or object states are translated into a format that can be stored.\
Deserialization is the opposite process. It involves extracting a data structure from a series of bytes.\
Insecure Deserialization occurs when untrusted data is used to abuse the logic flow of an application, execute arbitrary code or inflict a denial of service (DoS) when it is being deserialized.

## What causes Insecure Deserialization
The cause of Insecure Deserialization is the fact that developers often trust data provided by a sanitized object more than classical user input.

## What are the impacts of Insecure Deserialization
Insecure Deserialization could be used to execute arbitrary code, abuse the logic flow of an application or even inflict a Denial of Service.\
SQL Injection, Cross-Site Scripting, or Remote Code Execution could result due to insecure deserialization. It depends on how the serialized object is used.

## Example
Let's assume an online shop that uses serialization to save the shopping cart of a user.\
The user saves the state of the shopping cart and receives the following serialized object from the website.\

```
{"productId": 5, "amount": "3", "price": "39.99"}
```

The user may alter the serialized object and change the price to 1.\

```
{"productId": 5, "amount": "3", "price": "1.00"}
```

In case the application does not check the serialized object, the new price will be used.\
Insecure Deserialization occurs when the object is loaded, and serialized by the application, and the data is used without validation.\
The user will only have to pay the price from the deserialized object.

## How to prevent Insecure Deserialization
- Sanitize the data of a serialized object as untrusted user input through filtering or validation.
- Implement integrity checks such as digital signatures on any serialized object. This will prevent tampering.
- Isolate and run code that is deserialized in a low privilege environment.

## More info
Relevant material published by the Open Web Application Security Project (OWASP):

- Vulnerability overview: https://www.owasp.org/index.php/Deserialization_of_untrusted_data
- Remediation approaches: https://cheatsheetseries.owasp.org/cheatsheets/Deserialization_Cheat_Sheet.html
