# OpenID

OpenID is an extenstion of OAuth2. Its purpose is to let the AS communicate user information to the client. This is done with a ID token. An ID token in OpenID is always a JWT (JSON Web Token).

## Some differences between an access token and an ID token
- An access token should be treated as an opaque string. An application should not be able to read it. However, an ID token is meant to be read and validated by the application.
- An ID token is always in the JWT format. An access token can have any format.

## Usage example 
In order to get an ID token along with the access token from the AS, include the scope `openid` in the URL's query parameter:

```
https://authorization-server.com/auth?
  response_type=code&
  client_id=CLIENT_ID&
  redirect_uri=REDIRECT_URI&
  scope=photos+openid&
  state=XXXXXX&
  code_challenge=YYYYYYYYYY&
  code_challenge_method=S256
```

The request is otherwise identical to that of a normal Authorization Code flow. The response from the AS after calling `/token` will look like it does in a normal flow, but with an *id_token* included as well:

```
{
  "token_type": "Bearer",
  "access_token": "RsTQ8fv2Yj0Ia3as2PqRqf0N2t3J",
  "expires_in": 3600,
  "id_token": "9hRa0dpQrl6vYuIox4wEpAl19f604NmH..."
}
```

## Scopes
- openid
- profile
- email
- address
- phone

## Implicit flow
`&response_type=id_token`
When using this you have to validate the token's signature because the ID token will come in the front channel. Same with hybrid flows.