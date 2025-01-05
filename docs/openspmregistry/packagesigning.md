---
title: Package Signing
parent: Documentation
nav_order: 2
---

# How to sign packages
Yes package signing is supported and yes its a bit more complicated than just publishing a package.
Sorry for that, but it is what it is. We will get through this together.
{: .fs-6 .fw-300 }

## Prerequisites
- You need a metadata file for the package.
- You need to have a private key and a certificate.
- The private key needs to be in PKCS8 format.
- The certificate needs to be in PEM format.
- The certificate needs to be signed by a CA that is trusted by the client.

This can be done via Keychain (in case you are operating on a MacOS System) or manually via openssl command.

## Steps
### 1. Create a metadata file for the package.
The metadata file is a json file that contains the information about the package.
```json
{
  "author": {
    "name": "Wolfgang Reithmeier",
    "email": "w.reithmeier@gmail.com",
    "organization": {
      "name": "wgr1984"
    }
  },
  "description": "spm test library",
  "licenseURL": "https://github.com/wgr1984/spm_test_lib/LCENCE.TXT",
  "readmeURL": "https://github.com/wgr1984/spm_test_lib/README.md",
  "repositoryURLs": [
    "https://github.com/wgr1984/spm_test_lib.git",
    "git@github.com:wgr1984/spm_test_lib.git"
  ]
}
```
save this file as `package-metadata.json`

### 2. Create certs, sign & publish package
- [Create via Keychain](packagesigningkeychain.md)
- [Create manually via commandline](packagesigningmanual.md)

