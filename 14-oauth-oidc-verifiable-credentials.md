# A survey of OAuth, OIDC, and Verifiable Credentials (Wallets)

Presented by Richard Provarp

## Old Days

- Example: Yelp asked for your email and password to get your contacts

## OAuth 2.0

- Authorization protocol
- Mechanism to grant access to a resource
- Several authorization grants (flows)
- Internal Use
    - All of your apps can have the same grants
    - Or set of grants
    - No need to update each app as security for login changes
- Bilateral operation: Need to register your application with the service:
    - Name + website
    - Redirect URI
    - Provided with client ID and client secret
- OAuth 2.0 Roles
    - Resource Owner: User or system that owns the data
    - Client: The software accessing the resource
    - Authorization Server: Issues access tokens on behalf of the Resource Owner
    - Resource Server: Server that is protecting the Resource Owners data
- OAuth 2.0 Scopes: Defined per resource
- Access Token
    - The token presented by the Client to the Resource server
    - Can be anything
        - Needs to not be guessable when effectively representing a session key
        - Can be a JWT, or anything else
- Grant Types:
    - Authorization Code Grant: Traditional grant use by traditional web applications
    - Implicit grant: Deprecated
    - Authorization Code Grant with PKCE
    - Resource Owner Credentials Grant Type
    - Client Credential Grant Type
    - Device Authorization Flow
    - Refresh Token Grant

- Authorization Code Grant
    1. Client Identifier & Redirection URI
    2. User authenticates
    3. Authorization Code
    4. Authorization Code & Redirection URI
    5. Access Token
- With PKCE: Proof Key for Code Exchange
- Refresh Token:
    - Can be stored in secure storage on a device
    - Provides a "seamless" login if main token expired

## OIDC (OpenID Connect)

- SSO (Single Sign On) technology built on top of OAuth
- RP (Relying Party, Client)
- OP (OpenID Provider)
- Requires openid scope
- Get a JWT in return
    - Header: Algorithm and Token type
    - Payload:
        - `iss`: The server
        - `sub`: Subject, immutable identifier
        - `aud`: Audience, you
        - `nonce`: One time key
        - `exp`: Expiration
        - `iat`
    - Signature
- Can contain many more claims
    - Name, given_name, family_name, nickname, preferred_username
    - Profiles
    - Picture
    - website, email, email_verified
    - gender, birthdate
    - address
- JWT Signing
    - Symmetric and assymetric algorithms
    - Modern libraries should require declaring which algorithm is used to ensure verification is correct
- OpenID Federation
    - Enables multi-lateral federation
    - Currently being worked on
        - OpenID Federation 1.0 - draft 40 published October 24, 2024
        - Italian R&E federation leading in implementation details for R&E
    - Allows for many to many trust framework
        - like CAF (Canadian Access Federation), or eduGAIN

## Verifiable Credentials

- Also known as Self Sovereign Identity (SSI)
- Wallets contain a lot of stuff
    - Both physical and digital wallets
    - Not all things are the same in either
- W3C Verifiabe Credentials
- Uses
    - Digital driver's license
        - California has their own app, plus Apple & Google
            - Custom app has ability to limit release of attributes (Sacramento only)
        - Accepted by TSA for several states
        - Online verification
    - Diplomas, Degrees, Certificates, and micro-credentials
        - Employer needs to verify academic credential
        - [Digital Credentials Consortium](https://digitalcredentials.mit.edu/)
    - Digital ID & Authentication Council of Canada
        - [https://diacc.ca/](https://diacc.ca/)
        - Advocating for use
- How?
    - Uses OIDC and PKI
    - Flow is such that identity / attribute issuer doesn't know credential has been used
    - Credentials expire
    - Revocation is odd
    - A bunch of different wallet technology
    - Issue for those that don't have tech
    - Trust
- Parties
    - Issuer
        - Issues credential to holder
        - Signs with reference to public key
    - Holder
        - Releases credential to Verifier
        - Signs with reference to public key
    - Verifier
        - Needs to verify credential by validating signatures using public keys
        - Needs to know to TRUST the Issuer
            - Likely buy a service?
- Doesn't require blockchain

## Q&A

- Zero-knowledge proof?
    - Have heard, but not sure how and where they're being used
- If I wanna make a fake university, how hard is it to get a .edu?
    - More difficult, those are controlled by the government; so that is somewhat trustworthy
