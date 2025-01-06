---
title: Authorization
parent: Documentation
nav_order: 3
---

# Authorization / Authentication / Login
Important feature of every package registry is the authorization and authentication.
This is needed to ensure only authorized users can publish and retrieve packages.
Open SPM Registry supports different methods to authenticate against the registry.
{: .fs-6 .fw-300 }

## No Auth
_just for testing purposes or proxied through external auth provider_

Add auth block to `config.yml` and set `auth.enabled` to `false`
```yaml
  auth:
    enabled: false
```
now you can publish and retrieve packages without any authentication

## Basic Auth
_in case just basic security is needed, not recommended for public registries_

Add `auth` block to `config.yml` and set `auth.type` to `basic`
```yaml
  auth:
    type: basic
    users:
      - username: admin
        password: 937e8d5fbb48bd4949536cd65b8d35c426b80d2f830c5c308e2cdec422ae2244
```
{: .note }
Passwords are stored as sha256 hashes, therefore you need to hash your password before adding it to the config.

afterward you can login with
```shell
swift package-registry login --username [username] --password sha265([password])
```

## Use OIDC provider
Add `auth` block to `config.yml` and set `auth` to the name of the provider e.g. Auth0

⚠️ Important currently only grant type `password` or `code` is supported.
```yaml
  auth:
    name: auth0
    type: oidc
    grant_type: [password|code]
    issuer: (e.g. https://.....auth0.com/)
    client_id: ******
    client_secret: ******
```
### Code ([Authorization Code](https://oauth.net/2/grant-types/authorization-code/){:target="_blank"})

_recommended for public auth providers eg. Auth0, Google, etc_

in case of `code` grant type you need to set the redirect url in the provider to `https://server:port/callback`

Excecute
```shell
swift package-registry login https://server:port --token #####
```
with the code you get from the browser invoke:
`https://server:port/login`

### Password ([Resource Owner Password Credentials](https://oauth.net/2/grant-types/password/){:target="_blank"})

_not recommended for public auth providers, only in case provider should be hidden / not exposed to the users and trusted_

In case of `password` grant type also go to `https://server:port/login` and enter your credentials

{: .warning }
- Be aware the password is transmitted in clear text (well base64 encoded) to this server
- Therefor it is recommended to use `https` at least for the connection.
- Login will be CSRF protected though
> {: .note }
> DO NOT USE `swift package-registry login https://server:port --username [username] --password [password]` (it will not work)

once obtained token login similar to [`code` grant type](#code-authorization-code)
```shell
swift package-registry login https://server:port --token #####
```