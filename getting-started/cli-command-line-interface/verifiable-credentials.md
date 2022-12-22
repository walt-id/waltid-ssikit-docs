---
description: VC related operations like issuing, verifying and revoking VCs.
---

# Verifiable Credentials

VC related operations like issuing, verifying and revoking VCs.

Commands:

* [Issues and save VC](verifiable-credentials.md#issues-and-save-vc.) - using **issue** command
* [Present VC](verifiable-credentials.md#present-vc) - using **present** command
* [Verify VC or VP](verifiable-credentials.md#verify-vc-or-vp) - using **verify** command&#x20;
* [List verification policies](verifiable-credentials.md#manage-verification-policies) - using **policies** command&#x20;
* [Import VC to custodian store](verifiable-credentials.md#import-vc-to-custodian-store) - using **import** command&#x20;
* [VC templates](verifiable-credentials.md#vc-templates) - using **templates** command &#x20;
* [List VCs](verifiable-credentials.md#list-vcs) - using **list** command&#x20;

All commands have the help option available:

* `<your-command> -h`
* or `<your-command> --help`

E.g. `vc issue -h`

![](<../../.gitbook/assets/image (15).png>)

### Issues and save VC

Use the `issue` command to issue a W3C Verifiable Credential with either a JWT or a JSON\_LD signature.

options:&#x20;

* `-t, --template TEXT` specify the VC template. To create your own template, have a look [here](verifiable-credentials.md#import-vc-to-custodian-store-1)  \[Required]
* `-i, --issuer-did TEXT` DID of the issuer (associated with signing key). \[Required]
* `-s, --subject-did TEXT` DID of the VC subject (receiver of VC). \[Required] \
  e.g.
  * `vc issue -s did:key:z6MkpuUYdpaZPcpnEWnkE8vb7s2u2geTZJden1BwGXsdFUz3 -i did:ebsi:zZ5apnsHPUXNqjWELjNZhYW -t OpenBadgeCredential`, returns a credential document (JSON format)

![](<../../.gitbook/assets/image (14).png>)

* `-v, --issuer-verification-method TEXT` KeyId of the issuers' signing key
* `-y, --proof-type [JWT|LD_PROOF]` Proof type to be used \[LD\_PROOF]
* `-p, --proof-purpose TEXT` Proof purpose to be used \[assertion]
* \--interactive Interactively prompt for VC data to fill in&#x20;
* \--ld-signature, --ld-sig \[Ed25519Signature2018|Ed25519Signature2020|EcdsaSecp256k1Signature2019|RsaSignature2018|JsonWebSignature2020|JcsEd25519Signature2020]&#x20;
* \--ecosystem \[DEFAULT|ESSIF|GAIAX|IOTA] Specify ecosystem, for specific defaults of issuing parameters

### Present VC

Use present command to present a VC or VP to a verifier.

`-i, --holder-did TEXT` DID of the holder (owner of the VC)&#x20;

`-v, --verifier-did TEXT` DID of the verifier (recipient of the VP)&#x20;

`-d, --domain TEXT` Domain name to be used in the LD proof&#x20;

`-c, --challenge TEXT` Challenge to be used in the LD proof

### Verify VC or VP&#x20;

use verify command to verify&#x20;

`-p, --policy VALUE` Verification policy. Can be specified multiple times. By default, SignaturePolicy is used.

### List verification policies&#x20;

To see available verification policies, use `vc policies` command

![](<../../.gitbook/assets/image (10).png>)

### Import VC to custodian store&#x20;

Import DID to custodian store

Options:&#x20;

* `-k, --key-id TEXT` Specify key ID for imported did, if left empty, only public key will be imported
* `-f, --file TEXT` Load the DID document from the given file
* `-d, --did TEXT` Try to resolve DID document for the given DID

&#x20;

### VC templates&#x20;

Learn about VC template related functions like the listing and exporting of templates, as well as how to create/import your own custom VC template.

* `list` List VC Templates.

&#x20;`vc template list`  result

![](<../../.gitbook/assets/image (6).png>)

* `export <template-name>` Export VC Template.

e.g.  `vc templates export VerifiableId`

![](<../../.gitbook/assets/image (11).png>)

#### Import VC template to custodian store

* `import <customCredentialPath.json>`



Options:&#x20;

* `-n, --name <Name>` Name of the template



Arguments:&#x20;

* `credential path` the last argument of the command references the path to the custom credential, which should be imported



e.g `vc templates import MyCustomCredential custom.json`&#x20;



**custom.json**

```json
{
  "type": [
    "VerifiableCredential",
    "MyCustomCredential" // name of the credential
  ],
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.gov/credentials/3732",
  "issuer": {
    "id": "did:example:456"
  },
  "issued": "2020-03-10T04:24:12.164Z",
  "credentialSubject": { //custom credential subject
    "id": "",
    "firstName": "",
    "lastName": "",
    "country": "Austria"
  }
}

```



**Output of the command**

<figure><img src="../../.gitbook/assets/Screenshot on 2022-12-22 at 08-18-42.png" alt=""><figcaption></figcaption></figure>

### List VCs&#x20;



&#x20;

