---
title: Sign & create via Keychain
parent: Package Signing
nav_order: 1
---

# Sign & create via Keychain_
Create a self-signed certificate via Keychain

### Create a Certificate
1. Open keychain
2. Go to Certificate Assistant > Create a Certificate Authority
![Create CA 1](../../assets/images/spm_ca_create_1.jpg)
![Create CA 2](../../assets/images/spm_ca_create_2.jpg)
3. Go to Certificate Assistant > Create a Certificate
3.a. Overwrite the default settings (leaf, code signing)
![Create Cert 1](../../assets/images/spm_ca_cert_create_1.jpg)
3.b. Choose previously created CA
![Create Cert 2](../../assets/images/spm_ca_cert_create_2.jpg)
3.c. Change Key Pair Information to ECC and 256 bits
![Create Cert 3](../../assets/images/spm_ca_cert_create_3.jpg)
3.d. Ensure Code Signing is enabled
![Create Cert 4](../../assets/images/spm_ca_cert_create_4.jpg)
4. Save it to keychain

### Add CA to trusted root
1. Export the CA
![Export CA](../../assets/images/spm_cert_export.jpg)
2. Save in as CER in the trusted root dir: `~/.swiftpm/security/trusted-root-certs/`

### Sign a Package & Publish
```shell
swift package-registry publish [scope].[Package] [version] \
      --metadata-path package-metadata.json \
      --signing-identity "Test SPM Cert" \
      --vv
```
