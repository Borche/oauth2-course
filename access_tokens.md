# Access tokens
Two types exist:
- Reference tokens
- Structured tokens

## Reference tokens
The token itself is just a reference, a random string, for example a key in a database. Using the key one could identify a row that holds data, but the token doesn't contain any data itself. 

## Structured tokens
Also known as *Self Encoded Tokens*. Contains data in some format. Example of data it usually contains:
- User
- Application
- Expiration
- Time Created
- Scopes
- Authorization Server
- Last Login Time

The most common format is *JWT (JSON Web Token)*.

Do remember, though, that an _application_ shouldn't care about the token's format or if it contains any data. Only _the API_ should care.