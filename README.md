## Authentication vs Authentication

- Authentication means confirmation of your identity, and Authorization means allowing access to the system.
- Authentication is a type of process which ascertains that somebody is what they claim they’re. And Authorization refers to a set

![Alt Text](https://media.geeksforgeeks.org/wp-content/uploads/20190606141632/Untitled-Diagram-2019-06-06T141540.818.png)

* Authentication: Refers to proving correct identity 
* Authorization: Refers to allowing a certain action

## Authentication Methods

         - Basic : Sender places a username:password into the request header. The username and password are encoded with Base64
                  Encoding technique that converts the username and password into a set of 64 characters to ensure safe transmission.
                  Example :Authorization: Basic bG9sOnNlY3VyZQ==

         - Bearer : Client must send this token in the Authorization header when making requests to protected resources
                    Bearer authentication scheme was originally created as part of OAuth 2.0 in RFC-6750 but is sometimes also used on its own.
                    Example:  Authorization: Bearer <token>

        - API Keys :  A unique generated value is assigned to each first time user,Every call user need to pass security key to get access.
                      API key should send in the Authorization header
                      Example: Authorization: Apikey 1234567890abcdef

         - OAuth : OAuth is a standard that apps can use to provide client applications with “secure delegated access”.
                   OAuth works over HTTPS and authorizes devices, APIs, servers, and applications with access tokens rather than credentials.

## Token type :
    
    - JWT :JWT Tokens are actually a full JSON Object that has been base64 encoded and then signed with either a symmetric shared key or using a public/private key pair.
    
    - Opaque Tokens: opaque token has a format that is not intended to be read by you.opaque token is simply a primary key that references a database entry which has the     data. Fast key value stores like Redis or any cache
    

## JWT:
JSON Web Tokens are an open, industry standard RFC 7519 method for representing claims securely between two parties.


![Alt Text](https://backstage.forgerock.com/docs/am/7/oauth2-guide/images/oauth2-jwt-bearer-authn.svg)


![Alt Text](https://research.securitum.com/wp-content/uploads/sites/2/2019/10/jwt_ng1_en.png)

The issuer returns a signed JWT to the client. The JWT must contain, at least, the following claims in the payload:

         - iss. Specifies the unique identifier of the JWT issuer. This could also be the client, or a third party.

         - sub. Specifies the principal who is the subject of the JWT. Must be set to the client ID.

         - aud. Specifies the authorization server that is the intended audience of the JWT. Must be set to the authorization server's token endpoint. For example,            https://openam.example.com:8443/openam/oauth2/realms/root/access_token.

         - exp. Specifies the expiration time,providing a JWT with an expiry time greater than 30 minutes causes AM to return a JWT expiration time is unreasonable error message.

         - jti. Specifies a random, unique identifier for the JWT.


### What problem JWT solve :

HTTP is a stateless protocol, when a user makes a request that requires authentication to  web application they will have to pass in their credentials so we can implement a state mechanism, which brings us to sessions

 - Server side session : Server creates a session object on authenication which contains a unique session id, session expiry date, information about the user such as the user id, and any other information you may want to store.

                                    { 
                                            "id": "qw1e34rt5y", 
                                            "userId": "abcdxxxaasa",  
                                            "username": "vkhan", 
                                            "loginAttempts": 1,
                                            "expiryDate": "2021-07-08T23:28:56.782Z"
                                    }
  ### Issue with session managment 
                  Problem : If application scale up load balancer can forward call to any server and session management happened in one server 
                  Solution :  use Redis cache and save all session into Redis so all server can access it.

                  Problem :Redis cache single point of failure , if raids down all session gone
                  Solution use sticky session on load balancer 
                  
  When request JWT to the server then  server will then create a token with a secret key and send it back. The browser stores this token and sends it in the Authorization header   of every subsequent request.

### Understand JWT in debug
- https://jwt.io/

------------------------------------
## OAuth 2.0

The OAuth 2.0 authorization framework is a protocol that allows a user to grant a third-party web site or application access to the user's protected resources.

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

- Resource owner - The user who authorizes an application to access their account. The application’s access to the user’s account is limited to the “scope” of the authorization granted (e.g. read or write access).

- Scope - A permission.

- JWT - A JSON Web Token is a method for representing claims securely between two parties as defined in RFC 7519.


### Role
 
- Resource Owner − Resource owner is defined as an entity having the ability to grant access to their own data hosted on the resource server. When the resource owner is a person, it is called the end-user. 
- 
- Client Application − Client is an application making protected resource requests to perform actions on behalf of the resource owner.

- Resource Server − Resource server is API server that can be used to access the user's information. It has the capability of accepting and responding to protected resource requests with the help of access tokens.

- Authentication Server − The authentication server gets permission from the resource owner and distributes the access tokens to clients, to access protected resource hosted by the resource server.


### Scopes
Scopes are what you see on the authorization screens when an app requests permissions. They’re bundles of permissions asked for by the client when requesting a token. These are coded by the application developer when writing the application.


### OAuth 2.0 Flows
         1. Authorization Code Flow
         2. Implicit Flow
         3. Resource Owner Password Credentials Flow
         4. Client Credentials Flow
         5. Refresh Token Flow

- https://darutk.medium.com/diagrams-and-movies-of-all-the-oauth-2-0-flows-194f3c3ade85


-------------------------------------------
## OKTA

Okta is one trusted platform to secure every identity, from customers to your workforce. Okta connects any person with any application on any device. It's an enterprise-grade, identity management service, built for the cloud, but compatible with many on-premises applications.

- https://developer.okta.com/docs/guides/

------------------------------------
## SAML
Security Assertion Markup Language (SAML) is an open standard that allows identity providers (IdP) to pass authorization credentials to service providers (SP). What that jargon means is that you can use one set of credentials to log into many different websites.

- https://developer.okta.com/docs/concepts/saml/

------------------------------------
### The Difference among OAuth 2.0 vs OpenID Connect vs SAML

- OAuth 2.0: If you’ve ever signed up to a new application and agreed to let it automatically source new contacts via Facebook or your phone contacts, then you’ve likely used   OAuth 2.0. This standard provides secure delegated access. That means an application can take actions or access resources from a server on behalf of the user, without them having to share their credentials. It does this by allowing the identity provider (IdP) to issue tokens to third-party applications with the user’s approval.

- OpenID Connect: If you’ve used your Google to sign in to applications like YouTube, or Facebook to log into an online shopping cart, then you’re familiar with this authentication option. OpenID Connect is an open standard that organizations use to authenticate users. IdPs use this so that users can sign in to the IdP, and then access other websites and apps without having to log in or share their sign-in information. 

- SAML: You’ve more likely experienced SAML authentication in action in the work environment. For example, it enables you to log into your corporate intranet or IdP and then access numerous additional services, such as Salesforce, Box, or Workday, without having to re-enter your credentials. SAML is an XML-based standard for exchanging authentication and authorization data between IdPs and service providers to verify the user’s identity and permissions, then grant or deny their access to services.


- https://www.okta.com/identity-101/whats-the-difference-between-oauth-openid-connect-and-saml/


### The Difference Between JWT and OAUTH

-  https://github.com/vaquarkhan/vaquarkhan/wiki/JWT-vs-OAuth

### The Difference Between SAML 2.0 and OAuth 2.0

- https://www.ubisecure.com/uncategorized/difference-between-saml-and-oauth/

### The Difference Between LDAP and SAML SSO

- https://jumpcloud.com/blog/difference-ldap-saml-sso#:~:text=When%20it%20comes%20to%20their,cloud%20and%20other%20web%20applications.
- 
------------------------------------

## Springboot 



 ### Code-example

![Alt Text](https://ih0.redbubble.net/image.475329521.8750/ra%2Clongsleeve%2Cx925%2C101010%3A01c5ca27c6%2Cfront-c%2C210%2C180%2C210%2C230-bg%2Cf8f8f8.lite-1.jpg)



No                  |  url
------------------- | -------------
1                   | - https://github.com/vaquarkhan/okta-spring-boot-saml-example
2                   | - https://github.com/rwinch/spring-security-saml2-okta
3                   | - https://github.com/vaquarkhan/sso-okta-spring-boot
4                   | - https://github.com/vaquarkhan/facebook-oauth2-login-using-spring-boot
5                   | - https://github.com/vaquarkhan/spring-boot-security-oauth2-google
6                   | - https://github.com/vaquarkhan/okta-spring-logout-example
7                   | - https://github.com/oktadeveloper/okta-spring-boot-oauth-example
8                   | - https://github.com/oktadeveloper/okta-spring-boot-authz-server-example
9                   | - https://github.com/oktadeveloper/okta-spring-boot-app-with-auth-example
10                  | - https://github.com/oktadeveloper/okta-spring-boot-oauth2-pkce-example
10                  | - https://github.com/oktadeveloper/okta-spring-security-authentication-example


------------------------------------


- https://aws.amazon.com/premiumsupport/knowledge-center/cognito-okta-saml-identity-provider/
- https://dzone.com/articles/tldr-database-authentication-spring-security-saml
- https://dzone.com/articles/get-started-with-spring-boot-saml-and-okta
- https://aws.amazon.com/premiumsupport/knowledge-center/cognito-okta-saml-identity-provider/
- https://spring.io/projects/spring-security-saml
- https://spring.io/projects/spring-security-kerberos
- https://spring.io/projects/spring-security-oauth
- https://developer.okta.com/blog/2019/10/30/java-oauth2
- https://developer.okta.com/blog/2019/05/22/java-microservices-spring-boot-spring-cloud
- https://oauth2.thephpleague.com/
- https://www.tutorialspoint.com/oauth2.0
- https://www.deviantart.com/developers/authentication
- https://developer.okta.com/blog/2017/06/21/what-the-heck-is-oauth
- http://www.passportjs.org/docs/
- https://developer.okta.com/blog/2019/10/21/illustrated-guide-to-oauth-and-oidc
- https://www.ubisecure.com/about/resources/saml-oauth-openid-connect/?utm_source=ubisecure&utm_medium=blog
- https://developer.okta.com/docs/concepts/saml/
- https://www.okta.com/blog/2021/04/okta-amazon-web-services-aws-automate-aws-sso-with-okta-workflows/
