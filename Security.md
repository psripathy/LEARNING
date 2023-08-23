## XSS
Done by executing script on users browser.

### 1. Stored XSS
  - These attack targets websites that allow user input and store it in the database, e.g. comments.
  - The attacker writes the malicious script inside the input box, for example, a comment box. When the attacker clicks submit, the malicious script is saved as a comment in the website database. When a user opens this website, the malicious script runs on the browser as soon as the comments load.
    
### 2. Reflected XSS
  - The attacker tricks the user into clicking a link that contains the malicious script.
  - The user may receive the malicious link through email, search results, or advertisements on another website.

### Ways to avoid
- Sanitizing user input
- Validate User input before storing into DB


## CSRF

To perform a CSRF attack, a few conditions should be met.
- Cookie-based session handling  - User already logged into a website and it relies on cookies to identify user
- No unpredictable request parameters
