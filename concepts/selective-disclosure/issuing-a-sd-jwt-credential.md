---
description: >-
  Learn about issuing SD-JWT credentials which includes hashing, creating
  disclosures and adding decoy hashes
---

# Issuing a SD-JWT Credential

### **SD-JWT Credential Issuance Process**

1. **Credential Creation**: The issuer first creates the credential, as usual.
2. **Conversion to SD-JWT Credential**: The issuer then transforms the credential into an SD-JWT. This is done by hashing all or only a subset of claims, adding decoy hashes, and preparing disclosures. At the end, the SD-JWT credential can contain plain-text claims next to disclosable ones.
3. **Claim Hashing**: The claim is transformed into a disclosure, which is a plain-text representations of the claim, by concatenating the attribute name and value, then prefixing it with a salt. The salt prevents attackers from guessing plain-text values via dictionary attacks. This is then converted to a base64 string, which will represent the disclosure. For example, the disclosure may look like this (salt + attribute name + value): `[ “dC12Y2xpYi9tYXN0ZXI”, “given_name”, “John” ]`. The disclosure is then put into a hash function, and the result gets included in the SD-JWT.&#x20;
4. **Adding Decoy Hashes:**  At this point, decoy hashes are also added to the SD-JWT. These decoy hashes are essentially dummy values that help conceal the actual number of claims a credential holds. By using decoy hashes, the issuer can prevent potential observers from determining how many claims are contained within the credential based on the number of hashes.
5. **SD-JWT Credential Transfer to Holder**: The issuer sends the SD-JWT and all disclosures to the holder. Because the holder now has the SD-JWT credential as well as all the disclosures, he can read the entire content of the credential. This allows the holder to decide which disclosures to send alongside the SD-JWT in a transaction with a verifier.
6. **Transfer Format**: On transfer, the SD-JWT is shared with the concatenated disclosures using the \~ sign. An example of this format would be:

<pre data-overflow="wrap"><code>eyJraWQiOiI5MmJlMTAzYjRkZmY0OGYxYmE5ODc4ZGQyNmZhZjcxZSIsImN0eSI6ImNyZWRlbnRpYWwtY2xhaW1zLXNldCtqc29uIiwidHlwIjoidmMrc2Qtand0IiwiYWxnIjoiRWREU0EifQ.eyJjcmVkZW50aWFsU2NoZW1hIjp7ImlkIjoiaHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL3dhbHQtaWQvd2FsdGlkLXNzaWtpdC12Y2xpYi9tYXN0ZXIvc3JjL3Rlc3QvcmVzb3VyY2VzL3NjaGVtYXMvVmVyaWZpYWJsZUlkLmpzb24iLCJ0eXBlIjoiRnVsbEpzb25TY2hlbWFWYWxpZGF0b3IyMDIxIn0sImV2aWRlbmNlIjpbeyJkb2N1bWVudFByZXNlbmNlIjpbIlBoeXNpY2FsIl0sInZlcmlmaWVyIjoiZGlkOmVic2k6MkE5Qlo5U1VlNkJhdGFjU3B2czFWNUNkakh2THBRN2JFc2kySmI2TGRIS25ReGFOIiwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJ0eXBlIjpbIkRvY3VtZW50VmVyaWZpY2F0aW9uIl0sInN1YmplY3RQcmVzZW5jZSI6IlBoeXNpY2FsIn1dLCJpc3N1YW5jZURhdGUiOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsImNyZWRlbnRpYWxTdWJqZWN0Ijp7InBlcnNvbmFsSWRlbnRpZmllciI6IjA5MDQwMDgwODRIIiwiZmlyc3ROYW1lIjoiSmFuZSIsIl9zZCI6WyJuNWRYOEVpTUNoQ1hBR0o3elZCM1duQjc4Y3lBVFp3T1hwVkpCTUdOUzhzIiwiemFxMTNsa2lHLTd2am90SFppM0psSmhwS2JtUjFTVnV6Q3pLYVZYOUZRUSIsInhyYjdTOFZsNlctb0dMaVVQcTVlMmplVFpKVk5mYmRtNW9KNjd0VlVQem8iLCJwT0Jmb3hmQndqQUNPbXZ4aTNUSTc0RDN4Y2FwZS1RWVlGeUNPZEpPel9VIiwiRm1ZcmFmbWotUW9lbE1sSkQtVTN2OVgwS3hXTkZwelhwRl9McVc2dkZ0byJdLCJwbGFjZU9mQmlydGgiOiJMSUxMRSwgRlJBTkNFIiwiZ2VuZGVyIjoiRkVNQUxFIiwiZmFtaWx5TmFtZSI6IkRPRSIsImlkIjoiZGlkOmVic2k6MkFFTUFxWFdLWU11MUpIUEFnR2NnYTRkeHU3VGhnZmdOOTVWeUpCSkdaYlNKVXRwIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJjdXJyZW50QWRkcmVzcyI6WyIxIEJvdWxldmFyZCBkZSBsYSBMaWJlcnTDqSwgNTk4MDAgTGlsbGUiXX0sIl9zZF9hbGciOiJzaGEtMjU2IiwiaWQiOiJ1cm46dXVpZDozYWRkOTRmNC0yOGVjLTQyYTEtODcwNC00ZTRhYTUxMDA2YjQiLCJ2YWxpZEZyb20iOiIyMDIxLTA4LTMxVDAwOjAwOjAwWiIsInR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiaXNzdWVkIjoiMjAyMS0wOC0zMVQwMDowMDowMFoiLCJAY29udGV4dCI6WyJodHRwczovL3d3dy53My5vcmcvMjAxOC9jcmVkZW50aWFscy92MSJdLCJpc3N1ZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifQ.5TZ1n6iDHtW3lnKA_7ofSQ-BWyvEr39LThGdIc1OMgUejG6JF6blGkTqcoaQABQJKq6pFgkhjrYcpDG8QcObDA~<a data-footnote-ref href="#user-content-fn-1">WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0</a>~<a data-footnote-ref href="#user-content-fn-2">WyJXeS11VjJDa216SmJ4NGtjeTJQWjF3IiwiZGF0ZU9mQmlydGgiLCIxOTkzLTA0LTA4Il0</a>

</code></pre>



### Issuance in Action

Using either the CLI, Kotlin or REST option, you can start issuing your SD-JWT credential.



{% tabs %}
{% tab title="CLI" %}
[Setup section](../../getting-started/cli-command-line-interface.md), if you never used the SSi-Kit before.\
I will be using `ssikit` as an alias for `./ssikit.sh` in this section.

### &#x20;**DID creation**

\
Creating a did:key for our SD-JWT credential. Please refer to [DIDs section](../../getting-started/cli-command-line-interface/decentralized-identifiers.md) for all options.

```
ssikit did create
```

Example Response

```
walt.id SSI Kit 1.SNAPSHOT (running on Java 18.0.1+10-24)

Creating did:id.walt.cli.did.KeyMethodOption@59c04bee (key: 98de22f79c7e445dbedc0c72a18f6f9a)

Results:


DID created: did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a


DID document (below, JSON):

{
    "assertionMethod" : [
        "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a"
    ],
    "authentication" : [
        "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a"
    ],
    "capabilityDelegation" : [
        "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a"
    ],
    "capabilityInvocation" : [
        "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a"
    ],
    "@context" : "https://www.w3.org/ns/did/v1",
    "id" : "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
    "keyAgreement" : [
        "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6LSdemtq8mkV4nRKqvQvGkvs1JzSm4sCKKWNh6KkVox1vFn"
    ],
    "verificationMethod" : [
        {
            "controller" : "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
            "id" : "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
            "publicKeyBase58" : "FMZP5xZMrXr8cveAR28hr1s5wnybptiz5RddaM7KqnHC",
            "type" : "Ed25519VerificationKey2019"
        },
        {
            "controller" : "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
            "id" : "did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a#z6LSdemtq8mkV4nRKqvQvGkvs1JzSm4sCKKWNh6KkVox1vFn",
            "publicKeyBase58" : "2ybjJpxtPc4gETYePdEyYR6WbcXkVi9MViNeG3ARJYV2",
            "type" : "X25519KeyAgreementKey2019"
        }
    ]
}
```

### &#x20;**Issue VC with SD-JWT format**

\
We will be using the VerifiableId credential template for this example, but you can use whatever template you want. When issuing we specify the format of the VC as SD-JWT, the fields which we want to make selectily discloable and the number of decoy digests we want to include (optiona).

```bash
ssikit vc issue -s did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a \
-i did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a \
-y SD_JWT -t VerifiableId \
--sd credentialSubject \
--sd credentialSubject.dateOfBirth \
--num-decoys 2 \
--interactive vc.txt

```

**Options:**&#x20;

* `-s, --subject-did`: DID of the subject
* `-i, --issuer-did`: DID of the issuer
* `-y, --proof-type`: Either `JWT`, `LD_PROOF` or `SD_JWT`
* `-t, --template`: VC template, e.g VerifiableId
* `--sd, --selective-disclosure`: Path to selectively disclosable fields (if supported by chosen proof type), in a simplified JsonPath format, can be specified multiple times, e.g _credentialSubject.dataOfBirth_
* `--num-decoys`: Number of SD-JWT decoy digests to add (fixed mode), or max num of decoy digests (random mode)
* `--interactive`: Interactively prompt for VC data to fill in
* `vc.txt`: Path to output the generated VC

\
**Example Response**

Receiving a JWT token with disclosures appended via '\~'.

<pre data-overflow="wrap"><code>eyJraWQiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSN6Nk1rdG9wUmdDb29DNUxialJVczZiNlloN1I1bU5GVEVteUxtU1laUWQ1TG0xNGEiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSIsIm5iZiI6MTY4NjU3OTY5NCwiaXNzIjoiZGlkOmtleTp6Nk1rdG9wUmdDb29DNUxialJVczZiNlloN1I1bU5GVEVteUxtU1laUWQ1TG0xNGEiLCJpYXQiOjE2ODY1Nzk2OTQsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDoyZDM1YWFkMC1jY2UyLTQyODYtYWRmNy1jNGY5YTJlNTdmOTYiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDYtMTJUMTQ6MjE6MzRaIiwiaXNzdWVkIjoiMjAyMy0wNi0xMlQxNDoyMTozNFoiLCJ2YWxpZEZyb20iOiIyMDIzLTA2LTEyVDE0OjIxOjM0WiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL3Jhdy5naXRodWJ1c2VyY29udGVudC5jb20vd2FsdC1pZC93YWx0aWQtc3Npa2l0LXZjbGliL21hc3Rlci9zcmMvdGVzdC9yZXNvdXJjZXMvc2NoZW1hcy9WZXJpZmlhYmxlSWQuanNvbiIsInR5cGUiOiJGdWxsSnNvblNjaGVtYVZhbGlkYXRvcjIwMjEifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV0sIl9zZCI6WyJDQVlnNmc2bXJJTkFtdURDMzVKbXFMYy1DT1JBNC1MV2Fua2hKVWdVeHhzIl19LCJqdGkiOiJ1cm46dXVpZDoyZDM1YWFkMC1jY2UyLTQyODYtYWRmNy1jNGY5YTJlNTdmOTYifQ.xHwzXlrx0qS3grAQXWbZAX26Vg8enUegcVGMktl22Tr_ir19GHNidD6ZgEAJzlfmYS08hQDTAuDxsxE5J-ZvCA~<a data-footnote-ref href="#user-content-fn-3">WyJaalF3X3RKTGpZSVB0ZXl3Q0JKT21RIiwiZGF0ZU9mQmlydGgiLCIyMDIzIl0</a>~<a data-footnote-ref href="#user-content-fn-4">WyIyRXNHOV94aEhyNnU5Y2hrUGluX2FRIiwiY3JlZGVudGlhbFN1YmplY3QiLHsiaWQiOiJkaWQ6a2V5Ono2TWt0b3BSZ0Nvb0M1TGJqUlVzNmI2WWg3UjVtTkZURW15TG1TWVpRZDVMbTE0YSIsImN1cnJlbnRBZGRyZXNzIjpbIlZpZW5uYSJdLCJmYW1pbHlOYW1lIjoiQmF1bWFubiIsImZpcnN0TmFtZSI6IlRhbWlubyIsImdlbmRlciI6Ik1hbGUiLCJuYW1lQW5kRmFtaWx5TmFtZUF0QmlydGgiOiJKYW5lIERPRSIsInBlcnNvbmFsSWRlbnRpZmllciI6IjA5MDQwMDgwODRIIiwicGxhY2VPZkJpcnRoIjoiTXVuaWNoIiwiX3NkIjpbImlTVDBnT3ZzQ3pWNW1KX0FjTUtXdG81aWZPcGNwMUlsUXJpMHNUR09WZ1UiXX1d</a>
</code></pre>

### **Parsing the response**

Viewing body of SD-JWT in JSON format

```bash
ssikit vc parse -c vc.txt
```

**Options:**&#x20;

* `-c`: credential content or file path

**Example Responsen**

```json
{
    "type":[
        "VerifiableCredential",
        "VerifiableAttestation",
        "VerifiableId"
    ],
    "@context":[
        "https://www.w3.org/2018/credentials/v1"
    ],
    "id":"urn:uuid:2d35aad0-cce2-4286-adf7-c4f9a2e57f96",
    "issuer":"did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
    "issuanceDate":"2023-06-12T14:21:34Z",
    "issued":"2023-06-12T14:21:34Z",
    "validFrom":"2023-06-12T14:21:34Z",
    "credentialSchema":{
        "id":"https://raw.githubusercontent.com/walt-id/waltid-ssikit-vclib/master/src/test/resources/schemas/VerifiableId.json",
        "type":"FullJsonSchemaValidator2021"
    },
    "credentialSubject":{
        "id":"did:key:z6MktopRgCooC5LbjRUs6b6Yh7R5mNFTEmyLmSYZQd5Lm14a",
        "currentAddress":[
            "Vienna"
        ],
        "familyName":"Baumann",
        "firstName":"Tamino",
        "gender":"Male",
        "nameAndFamilyNameAtBirth":"Jane DOE",
        "personalIdentifier":"0904008084H",
        "placeOfBirth":"Munich",
        "dateOfBirth":"2023"
    },
    "evidence":[
        {
            "documentPresence":[
                "Physical"
            ],
            "evidenceDocument":[
                "Passport"
            ],
            "subjectPresence":"Physical",
            "type":[
                "DocumentVerification"
            ],
            "verifier":"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN"
        }
    ]
}
```
{% endtab %}

{% tab title="REST" %}
coming soon\

{% endtab %}
{% endtabs %}



[^1]: 

[^2]: 

[^3]: disclosure

[^4]: disclosure
