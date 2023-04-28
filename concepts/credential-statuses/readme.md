# Credential statuses

The `credentialStatus` property is used to identify the status of a verifiable credential.
It is an optional property (meaning when it's missing, the credential is not subject to any status change),
but when specified, it includes the following mandatory fields:
- ___id___ - a URI which identifies a location for the credential's status
- ___type___ - an arbitrary string which identifies the type of the credential status (typically _revocation_ or _suspension_)

Depending on the type, a _credentialStatus_ property can contain additional fields, according to its model specification.

Currently, [SSIKit](https://github.com/walt-id/waltid-ssikit) supports the following _credentialStatus_ methods:
- [SimpleCredentialStatus2022](simple-credential-status-2022/readme.md)
- [StatusList2021Entry](status-list-2021-entry/readme.md)


More details on _credentialStatus_ specification can be found at [Verifiable Credential Data Model - Status](https://www.w3.org/TR/vc-data-model/#status).