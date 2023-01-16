# Client Credential flow

The purpose of this flow (or grant type) is to allow a server/machine to get an access token without any user interaction. Machine to machine communication.

When registering an application at the AS that wants to use this grant type, choose application type "Machine to machine" or "Service account". If none of these exists, choose another type that you know will give you both a *Client ID* and a *Client secret*.

The request in this flow is made directly to the `/token` endpoint:
```
POST https://authorization-server.com/token
  grant_type=client_credentials
  scope=contacts
  client_id=CLIENT_ID
  client_secret=CLIENT_SECRET
```

Note that in the example above the Client ID and Client secret were sent in the request body. However, some authorization servers are configured to receive them in a HTTP header like so:

```
Authorization: Basic <base64(CLIENT_ID:CLIENT_SECRET)>
```

The response will look the same as in other flows, containing the access token. 

```
{
  "token_type": "Bearer",
  "access_token": "RsTQ8fv2Yj0Ia3as2PqRqf0N2t3J",
  "expires_in": 3600,
  "scope": "contacts"
}
```

However, with the client credential grant type, a refresh token will normally not be present. This is  because the refresh token is used to refresh the access token without interupting the user. But since this grant type is mostly used when there is no user involed, there is normally no need for a refresh token.