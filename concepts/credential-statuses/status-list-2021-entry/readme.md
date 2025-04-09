# StatusList2021Entry

_StatusList2021Entry_ is a _credentialStatus_ method by which the status of a verifiable credential can be checked. The basic idea of it is each issued credential has a corresponding position in a bit-string (also called the status list), having a value of either 0 - not revoked, or 1 - revoked. This status list is published by the issuer as a verifiable credential with a type that includes _StatusList2021Credential_.

The _StatusList2021Entry_ credentialStatus contains the following fields:

* _**id**_ - a URL identifying the status information for the verifiable credential
* _**type**_ - `StatusList2021Entry`
* _**statusPurpose**_ - the purpose of the status entry (typically _revocation_ or _suspension_)
* _**statusListIndex**_ - the bit position of the credential within the bit-string
* _**statusListCredential**_ - the URL of the _StatusList2021Credential_ credential that encapsulates the bit-string

e.g.

```json
{
  "id": "https://example.com/credentials/status/3#94567",
  "type": "StatusList2021Entry",
  "statusPurpose": "revocation",
  "statusListIndex": "94567",
  "statusListCredential": "https://example.com/credentials/status/3"
}
```

### StatusList2021Credential

The _StatusList2021Credential_ is a verifiable credential that encapsulates the bit-string information about all the credentials ever issued. The following fields have to be explicitly provided:

* _**id**_ - (optional) the URL to this credential (should match the _statusListCredential_ value from _StatusList2021Entry_)
* _**type**_ - should contain `StatusList2021Credential`
* _**credentialSubject**_
  * _**type**_ - `StatusList2021`
  * _**statusPurpose**_ - the purpose of the status credential (_StatusList2021Entry_ should match this value)
  * _**encodedList**_ - the compressed and base64 encoded value of the bit-string

e.g.

```json
{
  "id": "https://example.com/credentials/status/3",
  "type": ["VerifiableCredential", "StatusList2021Credential"],
  "credentialSubject": {
    "id": "https://example.com/status/3#list",
    "type": "StatusList2021",
    "statusPurpose": "revocation",
    "encodedList": "H4sIAAAAAAAAA-3BMQEAAADCoPVPbQwfoAAAAAAAAAAAAAAAAAAAAIC3AYbSVKsAQAAA"
  },
  "other-verifiable-credential-properties": {}
}
```

\
More details about _StatusList2021Entry_ and _StatusList2021Credential_ can be found at [Verifiable Credentials Status List v2021](https://www.w3.org/TR/2023/WD-vc-status-list-20230427/).
