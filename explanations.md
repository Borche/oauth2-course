# Abbreviations & Explanations

PKCE = Proof Key for Code Exchange\
AS = Authorization server

PKCE Code Verifier (Secret) = Random string 43-128 characters long
PKCE Code Challenge (Public) = `base64url(sha256(code_verifier))`