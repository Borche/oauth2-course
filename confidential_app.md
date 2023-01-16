# Confidential App example

Application redirects to AS (using PKCE):

```
https://authorization-server.com/auth?
  response_type=code&
  client_id=CLIENT_ID&
  redirect_uri=REDIRECT_URI&
  scope=photos&
  state=XXXXXX&
  code_challenge=YYYYYYYYYY&
  code_challenge_method=S256
```

*User logs in at AS (Login Page) and agrees to give App requested permissions (Consent Page).*

AS redirects back to App:

```
https://example-app.com/redirect?code=AUTH_CODE&state=XXXXXX
```

Then the app will request a token from the AS:

```
POST https://authorization-server.com/token
  grant_type=authorization_code&
  code=AUTH_CODE&
  redirect_uri=REDIRECT_URI&
  code_verifier=VERIFIER_STRING&
  client_id=CLIENT_ID&
  client_secret=CLIENT_SECRET
```

Assuming everything is OK, the AS with respond with an access token and potentially also a refresh token (depends on AS config):

```
{
  "token_type": "Bearer",
  "access_token": "RsTQ8fv2Yj0Ia3as2PqRqf0N2t3J",
  "expires_in": 3600,
  "scope": "photos",
  "refresh_token": "7hRa0dpQrl6vYuIox4wEpAl19f604NmH"
}
```

If you received a refresh token, you can refresh the access token like this:

```
POST https://authorization-server.com/token
  grant_type=refresh_token&
  refresh_token=REFRESH_TOKEN&
  client_id=CLIENT_ID&
  client_secret=CLIENT_SECRET
```