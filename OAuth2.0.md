# [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749)
    Is an Authorization protocol and NOT an Authentication protocol

    OAuth defines 4 roles: Resource Owner, Client, Authorization Server, Resource Server
    
<img src="./images/oauth__flow.png" width="70%" height="10%">
  
## Grant Types in OAuth 2.0

> ### Authorization Code Grant
- The Authorization server returns single use Access Code to the client which is then exchanged for Access token. Best option for **Traditional Web apps** where exchange can happen securely on server side

> ### Implicit Grant
- The authorization server may return the Access Token as a parameter in the callback URI or as a response to a form post

> ### Authorization Code Grant with PKCE (Proof of KeyCode Exchange)
- Used by **SPAs & Mobile/Native apps** as they cannot use client id which will be stored on browser/

> ### Resource Owner Credentials Grant Type
- Requires the Client first to acquire the resource owner’s credentials, which are passed to the Authorization server. So used only with **trusted clients**.

> ### Client Credentials Grant Type
- Used for non-interactive apps like **microservices, automated process** etc.
  
> ### Device Authorization Flow
- For use by apps on input-constrained devices, such as **smart TVs**.

## [Authorization Code Flow with PKCE (Proof Of KeyCode Exchange) with Authentication](https://auth0.com/docs/get-started/authentication-and-authorization-flow/authorization-code-flow-with-proof-key-for-code-exchange-pkce)

<img src="./images/auth-sequence-auth-code-pkce.png" width="70%" height="10%">


## JWT (JSON Web) Token

### Token Based Authentication
Basic flow of token-based authentication:

1. The client sends a request to the server with a username/password.
2. The application validates the credentials and generates a secure, signed token for the client.
3. The token is sent back to the client and stored there.
4. When the client needs to access something new on the server, it sends the token through the HTTP header.
5. The server decodes and verifies the attached token. If it is valid, the server sends a response to the client.
6. When the client logs out, the token is destroyed.

JWS (Signed), JWE (Encrypted)

> ### JWT Structure
    1. Header
        The header defines 2 attributes
        - alg: The algorithm used to sign/encrypt the token
        - typ: the content type that is being encrypted or signed
        {
            "alg": "HS256",
            "typ": "JWT"
        }
    2. Payload
    3. Signature

