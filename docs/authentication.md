# Authentication

Two ways in. Use an API key unless your client speaks OAuth, in which case use OAuth
and never handle a key at all.

## API keys

Create one in the dashboard at [https://prowl.chat](https://prowl.chat). Send it as a Bearer token:

```
Authorization: Bearer prowl_<your_key>
```

Keys start with `prowl_`. A request without the header, with a malformed one, or with a
revoked key gets `401` and a `WWW-Authenticate` header naming where to discover the
authorization server.

**A key is a wallet.** Every call it makes is debited from your balance, so a leaked key
is a leaked budget. Rotate by creating a new key, moving traffic, then revoking the old
one — revocation takes effect on the next call.

**Where to keep it.** An environment variable, a secret manager, or a git-ignored file.
Not in the MCP config you commit, and not in a prompt you paste somewhere.

## OAuth 2.1

Clients that support it can connect without you pasting a key anywhere. Prowl is a
full OAuth 2.1 authorization server with PKCE, dynamic client registration, and
rotating refresh tokens.

Discovery, per RFC 8414 and RFC 9728:

```
GET https://prowl.chat/.well-known/oauth-authorization-server
GET https://prowl.chat/.well-known/oauth-protected-resource/mcp
```

The flow is the standard one: your client registers itself, sends you to a consent page
that names the client and the scope, and exchanges the returned code — with its PKCE
verifier — for an access token starting `prowl_oat_`. Access tokens last an hour;
refresh tokens rotate on every use.

Behind the token is an ordinary API key, which means two useful things. Spend shows up
in the same wallet and the same statistics. And revoking that key in the dashboard kills
the connector immediately, without touching anything OAuth-shaped.

Details worth knowing before you debug something:

- **Codes are single-use.** Replaying one revokes every token issued under that grant —
  including the legitimate one. That is deliberate: a replayed code means the code
  leaked.
- **A reused refresh token does the same.** Rotation exists so that a stolen token is
  detectable; when it is detected, the whole grant dies.
- **A redirect URI must be registered.** An unknown client or an unregistered redirect
  gets a `400` and no redirect at all — Prowl will not bounce a browser to an address it
  does not know.

## Which one to use

| | API key | OAuth 2.1 |
|---|---|---|
| Setup | paste a key into a config | click through a consent screen |
| Best for | servers, CI, your own backend | desktop agents and IDE clients |
| Revoke | delete the key | delete the underlying key, or the grant |
| Expiry | none until revoked | access token 1 hour, refresh rotates |

Both authenticate the same account and spend the same wallet.
