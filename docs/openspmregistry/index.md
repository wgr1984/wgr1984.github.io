---
title: Open SPM Registry
nav_order: 2
---

# About
Simple, fast and as feature complete as possible version
of [Swift Package Manager Registry](https://github.com/swiftlang/swift-package-manager/blob/main/Documentation/PackageRegistry/Registry.md){:target="_blank"}.
(at least in terms of API)
{: .fs-6 .fw-300 }

## Usage
- Getting started: [Click here]()
- Installation: [Click here]()
- Full API Documentation: [Click here]()
- Docker Image: [Click here]()
- Source Code: [Click here]()

## Features
### Listing / Browsing

| State | Feature               | API                                                                           |
|:------|:----------------------|:------------------------------------------------------------------------------|
| ✅     | Listing / Browsing    | `GET /{scope}/{package}`                                                      |
| ✅     | Info of Package       | `GET /{scope}/{package}/{version}`                                            |
| ✅     | Retrieval of Package  | `GET /{scope}/{package}/{version}.zip`                                        |
| ✅     | Retrieval of Manifest | `GET /{scope}/{package}/{version}/Package.swift[?swift-version=[e.g. 5.7.0]]` |

### Publishing

| State | Feature         | API                                                                                                                                                                          |
|:------|:----------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ✅     | Publishing      | `PUT /{scope}/{package}/{version}`<br/>ℹ️ currently only synchronous mode is supported                                                                                       |
| ✅     | Package Signing | e.g. `swift package-registry publish [scope].[Package] [version] --metadata-path package-metadata.json --vv --private-key-path ecdsa_pkcs8.key --cert-chain-paths ecdsa.crt` |

### Management

| State | Feature              | API                                           |
|:------|:---------------------|:----------------------------------------------|
| ✅     | Storage              | currently Filesystem only                     |
| ✅     | Docker Image Support | `docker pull wgr1984/openspmregistry`         |
| ✅     | User Management      | No auth, Basic Auth, Oauth password and token |
                                                                                   
## Roadmap

- Publishing
    - Package Validity checking (checksum, manifest, etc)
    - asynchronous mode support 
    - base64 format (not sure if needed)
- Management API
  - Delete packages
  - Browser UI to e.g. list packages
  - Upload Binary Files (e.g. .zip), needed for binary targets
- Storage
    - DB support (e.g. mysql, postgres)
    - Online storage (e.g S3, cloud drive)
    - Proxying / Cacheing support of other registries
  
- User Management / Access Control 
  - Permissions / roles
  - Scope restrictions
  - Audit logging
  
## Repository

Source code is available at 🔗 [https://github.com/wgr1984/openspmregistry](https://github.com/wgr1984/openspmregistry){:target="_blank"} check it out and contribute!

## Alternatives

There are other Swift Package Manager Registries available, e.g.:
- [Artifactory (Pro version required)](https://jfrog.com/artifactory/){:target="_blank"}
- [Gitea](https://docs.gitea.com/usage/packages/swift){:target="_blank"} / [Forgejo](https://forgejo.org/docs/latest/user/packages/swift/){:target="_blank"}
- [AWS CodeArtifact](https://aws.amazon.com/codeartifact/){:target="_blank"}

For sure these project are more general purpose projects and better suited for your needs.
This project is focused providing a microservice for Swift Package Manager Registry as lightweight as possible.
If this is what you are looking for, you are at the right place 🙂

## Contributing

Please feel free to contribute to this project. Just open issues, feature requests or pull requests.

## Donations

If you like this project and want to support me, [buy me a coffee](https://buymeacoffee.com/wreithmeiep){:target="_blank"} ☕️
