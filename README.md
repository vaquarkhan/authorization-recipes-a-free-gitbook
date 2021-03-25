## OAuth2-Okta-SAML

The OAuth 2.0 authorization framework is a protocol that allows a user to grant a third-party web site or application access to the user's protected resources.

------------------------------------
## JWT:
JSON Web Tokens are an open, industry standard RFC 7519 method for representing claims securely between two parties.


![Alt Text](https://backstage.forgerock.com/docs/am/7/oauth2-guide/images/oauth2-jwt-bearer-authn.svg)

### Token 
![Alt Text](https://research.securitum.com/wp-content/uploads/sites/2/2019/10/jwt_ng1_en.png)
The issuer returns a signed JWT to the client. The JWT must contain, at least, the following claims in the payload:

         - iss. Specifies the unique identifier of the JWT issuer. This could also be the client, or a third party.

         - sub. Specifies the principal who is the subject of the JWT. Must be set to the client ID.

         - aud. Specifies the authorization server that is the intended audience of the JWT. Must be set to the authorization server's token endpoint. For example,            https://openam.example.com:8443/openam/oauth2/realms/root/access_token.

         - exp. Specifies the expiration time,providing a JWT with an expiry time greater than 30 minutes causes AM to return a JWT expiration time is unreasonable error message.

         - jti. Specifies a random, unique identifier for the JWT.




### Understand JWT in debug
- https://jwt.io/

------------------------------------


### OAuth Terminology

- Access token - A token used to access protected resources.

- Authorization code - An intermediary token generated when a user authorizes a client to access protected resources on their behalf. The client receives this token and exchanges it for an access token.

- Authorization server - A server which issues access tokens after successfully authenticating a client and resource owner, and authorizing the request.
Client - An application which accesses protected resources on behalf of the resource owner (such as a user). The client could be hosted on a server, desktop, mobile or other device.

- Grant - A grant is a method of acquiring an access token, following are grant type.
            - Authorization code grant
            - Implicit grant
            - Client credentials grant
            - Resource owner password credentials grant
            - Refresh grant

![Alt Text]https://oauth2.thephpleague.com/images/grants.min.svg)

Grant flow (courtesy: oauth2.thephpleague.com).


- Resource server - A server which sits in front of protected resources (for example “tweets”, users’ photos, or personal data) and is capable of accepting and responding to protected resource requests using access tokens.
- 
- Resource owner - The user who authorizes an application to access their account. The application’s access to the user’s account is limited to the “scope” of the authorization granted (e.g. read or write access).

- Scope - A permission.
- 
- JWT - A JSON Web Token is a method for representing claims securely between two parties as defined in RFC 7519.

------------------------------------



- https://oauth2.thephpleague.com/
- 
