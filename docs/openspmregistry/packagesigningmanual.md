---
title: Sign & create cert manually
parent: Package Signing
nav_order: 2
---

# Sign & create cert manually
Manually create a self-signed certificate via commandline.
{: .warning }
Might be outdated or not working on your system. Recommend to use [Keychain](packagesigningkeychain.md) instead.

### Create a CA
```shell
openssl genpkey -algorithm RSA  -outform der -out ca.key -pkeyopt rsa_keygen_bits:2048
openssl req -x509 -new -nodes -key ca.key -sha256 -days 365  -outform der -out ca.crt -subj "/C=US/ST=State/L=City/O=Organization/OU=OrgUnit/CN=RootCA"
```
### Create a certificate
```shell
openssl ecparam -genkey -name prime256v1  -outform der -out ecdsa.key
openssl pkcs8 -topk8 -inform DER -outform PEM -in ecdsa.key -out ecdsa_temp.pem -nocrypt
openssl asn1parse -in ecdsa_temp.pem -out ecdsa.key.der -noout
KEY=$(openssl dgst -sha1 -binary ecdsa.key.der | xxd -p | tr -d '\n' | sed 's/\(..\)/\1 /g')
echo "Bag Attributes
    friendlyName: SPM_TEST
    localKeyID: $KEY
Key Attributes: <No Attributes>" > ecdsa.pem
cat ecdsa_temp.pem >> ecdsa.pem

openssl pkcs8 -topk8 -inform pem -outform der -in ecdsa.pem -out ecdsa_pkcs8.key -nocrypt
openssl req -new -key ecdsa.key -out ecdsa.csr -subj "/C=US/ST=State/L=City/O=Organization/OU=OrgUnit/CN=CodeSigningCert"

echo "[ v3_code_sign ]
keyUsage = critical, digitalSignature
extendedKeyUsage = codeSigning" > code_signing_ext.cnf

openssl x509 -req -in ecdsa.csr -CA ca.crt -CAkey ca.key -CAcreateserial -outform der -out ecdsa.crt -days 365 -sha256 -extfile code_signing_ext.cnf -extensions v3_code_sign 
```
### Add CA to trusted root
```
cp ca.crt ~/.swiftpm/security/trusted-root-certs/ca.cer
```
### publish with signing
```shell
swift package-registry publish [scope].[Package] [version] \
      --metadata-path package-metadata.json \
      --private-key-path ecdsa_pkcs8.key \
      --cert-chain-paths ecdsa.crt \
      --vv
```