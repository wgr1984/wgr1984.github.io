---
title: Sign & create via Keychain
parent: Package Signing
nav_order: 1
---

# Sign & create via Keychain_
_Create a self-signed certificate via Keychain_

## Create a Certificate
1. Open Keychain
2. Create new CA certificate

![Create Cert 1](../../assets/images/spm_cert_create_1.jpg)
2a. Overright the default settings
![Create Cert 2](../../assets/images/spm_cert_create_2.jpg)
2b. Change Key Pair Information to ECC and 256 bits
![Create Cert 3](../../assets/images/spm_cert_create_3.jpg)
![Create Cert 4](../../assets/images/spm_cert_create_4.jpg)
2c. Ensure Code Signing is enabled
![Create Cert 5](../../assets/images/spm_cert_create_5.jpg)
3. Save it to keychain

## Sign a Package & Publish
```shell
swift package-registry publish [scope].[Package] [version] \
      --metadata-path package-metadata.json \
      --signing-identity "Test SPM Cert" \
      --vv
```
