---
title: Features & Roadmap
parent: Documentation
nav_order: 4
---

# Features & Roadmap
Features and roadmap of Open SPM Registry. The project is still in development and will be updated with new features and improvements.
{: .fs-6 .fw-300 }

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
