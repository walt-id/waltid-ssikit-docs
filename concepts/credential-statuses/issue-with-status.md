# Issue with a _credentialStatus_

In order to issue a verifiable credential with a _credentialStatus_, the `statusType` property of the
`proofConfig` object should be provided (e.g. '_SimpleCredentialStatus2022_', '_StatusList2021Entry_', etc.).
If no _statusType_ is provided, the credential will be issued without any _credentialStatus_ property.

### Rest API interface

e.g. Issue a _UniversityDegree_ credential having a `StatusList2021Entry` _credentialStatus_ using the REST API
interface issue endpoint: `https://signatory.ssikit.walt.id/v1/credentials/issue`. The request-body is presented below.

```json
{
    "templateId": "UniversityDegree",
    "config":
    {
        "issuerDid": "did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X>",
        "subjectDid": "did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK",
        "statusType": "StatusList2021Entry"
    }
}
```

### Command-line interface

e.g. Issue a _UniversityDegree_ credential having a `StatusList2021Entry` _credentialStatus_ using the command-line
interface issue command: `ssikit vc issue -h`

```shell
ssikit vc issue \ 
-t UniversityDegree \ 
-i did:key:z6MkiWE3zZaTkDYLBwrPeZ94bXC9CnDVVeRcX12tncBh9q2X \
-s did:key:z6MkoHRK9dK81gFrGzwo6kygHW8KRoECGhLk5QJgNPYdzCTK \
--status-type StatusList2021Entry
```