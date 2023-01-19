# Access Token validation

## Remote token validation (asking the Authorization server)
The simplest way for an API to validate an access token included in an incoming request is to go and ask the AS if it's valid. This method is slower because it requires communication between the API and the AS. If you're using reference tokens (random strings) then this is however the only way to validate the token.

Use the Authorization server's _Token Introspection Endpoint_ to ask if the token is valid.

## Local token validation
Using an JWT library to validate the token. Validate the signature as well as the claims.

Remember that when using local validation, what you're actually validating is the state of the user's permissions when the token was issued, not necessarily when the request comes in. If the user has been deleted, or been removed from some user group or something else has changed, the token might not reflect that. This is why it's important to consider the life time for access tokens in your API.

More scalable than remote validation.

## The best of both worlds
Use an API Gateway in front of your APIs that does local validation. That way, malformated tokens, hacking attempts and expired tokens will get deleted and returned quickly - the requests never reaching the APIs at all.

The requests that do reach the API will have a token validated at the API gateway and be either valid or _revoked_. Revoked meaning it was recently valid, but it's stale now because of changes to the user's permissions, as exemplified above in the Local validation section.

APIs that doesn't handle sensitive data/operations can consider the validation at the API gateway to be enough. APIs that do sensitive operations, such as charging a credit card or placing an order, can individually perform remote validation of the token for extra security.

This solution will result in far fewer of the slow remote requests to the AS. But the possibility to do them is there for those APIs that need it. 

Note: In a smaller API, the middleware can act as the API gateway.