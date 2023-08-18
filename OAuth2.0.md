# [OAuth 2.0](https://auth0.com/intro-to-iam/what-is-oauth-2)
    Is an authorization protocol and NOT an authentication protocol

    OAuth defines 4 roles
    
<img src="./images/oauth__flow.png" width="70%" height="10%">
  
## Grant Types in OAuth 2.0

Authorization Code Grant
- The Authorization server returns single use Access Code to the client which is then exchanged for Access token. Best option for **Traditional Web apps** where exchange can happen securely on server side


## Authorization Code Flow with PKCE (Proof Of KeyCode Exchange)

- Used by Single Page Stateless apps / Mobile apps as they cannot use client id which will be stored on browser/

