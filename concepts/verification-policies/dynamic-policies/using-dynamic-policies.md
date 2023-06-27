# Using Dynamic Policies

### Verification with a Dynamic Policy

Once a dynamic policy has been saved with a specific name, as explained in [the previous section](creating-dynamic-policies.md), you can use it to verify Verifiable Credentials.

{% tabs %}
{% tab title="CLI" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/cli-command-line-interface.md) to exectute the command successfully.

```bash
ssikit vc verify \
  -p SubjectPolicy='{ "user": "did:key:z6MkgERd8hghGSBndxduiXtUdbYmtbcX9TeNdAL2BAhvXoAp" }' \
  src/test/resources/rego/VerifiableId.json
```

* `-p, --policy`: Verification policy. Can be specified multiple times. By default, SignaturePolicy is used. To specify a policy argument (if required), use the format PolicyName='{"myParam": "myValue", ...}', to specify the JSON object directly, or PolicyName=path/to/arg.json, to read the argument from a JSON file.

{% hint style="info" %}
We can verify a credential with the `SubjectPolicy` and VerifiableId located in `src/test/resources/rego/VerifiableId.json`, which are provided when cloning the project, so no setup is needed.
{% endhint %}
{% endtab %}

{% tab title="REST" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/rest-apis.md) to serve the API.

```bash
curl -X 'POST' \
  'http://127.0.0.1:7003/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "policies": [
        {
            "policy": "MyCustomPolicy",
            "argument": {
                "user": "did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z"
            }
        }
    ],
    "credentials": [
        "eyJraWQiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiN6Nk1rckZ0ellTNVJXNzQ4dnZBakFSWjRDWWpCTXZlVjlMWWZTQUZvdjQzOUJtOFoiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsIm5iZiI6MTY4Nzg2NDU2NCwiaXNzIjoiZGlkOmtleTp6Nk1rckZ0ellTNVJXNzQ4dnZBakFSWjRDWWpCTXZlVjlMWWZTQUZvdjQzOUJtOFoiLCJpYXQiOjE2ODc4NjQ1NjQsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDplMDY3ZDVmYy0zNWFlLTRkMGUtYTk1ZS03MzdmMGUwYzIzM2IiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDYtMjdUMTE6MTY6MDRaIiwiaXNzdWVkIjoiMjAyMy0wNi0yN1QxMToxNjowNFoiLCJ2YWxpZEZyb20iOiIyMDIzLTA2LTI3VDExOjE2OjA0WiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL3Jhdy5naXRodWJ1c2VyY29udGVudC5jb20vd2FsdC1pZC93YWx0aWQtc3Npa2l0LXZjbGliL21hc3Rlci9zcmMvdGVzdC9yZXNvdXJjZXMvc2NoZW1hcy9WZXJpZmlhYmxlSWQuanNvbiIsInR5cGUiOiJGdWxsSnNvblNjaGVtYVZhbGlkYXRvcjIwMjEifSwiY3JlZGVudGlhbFN1YmplY3QiOnsiaWQiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsImN1cnJlbnRBZGRyZXNzIjpbIjEgQm91bGV2YXJkIGRlIGxhIExpYmVydMOpLCA1OTgwMCBMaWxsZSJdLCJkYXRlT2ZCaXJ0aCI6IjE5OTMtMDQtMDgiLCJmYW1pbHlOYW1lIjoiRE9FIiwiZmlyc3ROYW1lIjoiVGFtaW5vIiwiZ2VuZGVyIjoiRkVNQUxFIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJwZXJzb25hbElkZW50aWZpZXIiOiIwOTA0MDA4MDg0SCIsInBsYWNlT2ZCaXJ0aCI6IkxJTExFLCBGUkFOQ0UifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV19LCJqdGkiOiJ1cm46dXVpZDplMDY3ZDVmYy0zNWFlLTRkMGUtYTk1ZS03MzdmMGUwYzIzM2IifQ.tyLqPczrzyRQQNBoR1z5fR9oA50XiT8IX9OpQY_1qLA71eInI71fFOulDsS9WuwfT2FjN5ugjihLaiRVx7OcAg"
    ]
}'
```

**Body**

```json
{
    "policies": [
        {
            "policy": "MyCustomPolicy",
            "argument": {
                "user": "did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z"
            }
        }
    ],
    "credentials": [
        "eyJraWQiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiN6Nk1rckZ0ellTNVJXNzQ4dnZBakFSWjRDWWpCTXZlVjlMWWZTQUZvdjQzOUJtOFoiLCJ0eXAiOiJKV1QiLCJhbGciOiJFZERTQSJ9.eyJzdWIiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsIm5iZiI6MTY4Nzg2NDU2NCwiaXNzIjoiZGlkOmtleTp6Nk1rckZ0ellTNVJXNzQ4dnZBakFSWjRDWWpCTXZlVjlMWWZTQUZvdjQzOUJtOFoiLCJpYXQiOjE2ODc4NjQ1NjQsInZjIjp7InR5cGUiOlsiVmVyaWZpYWJsZUNyZWRlbnRpYWwiLCJWZXJpZmlhYmxlQXR0ZXN0YXRpb24iLCJWZXJpZmlhYmxlSWQiXSwiQGNvbnRleHQiOlsiaHR0cHM6Ly93d3cudzMub3JnLzIwMTgvY3JlZGVudGlhbHMvdjEiXSwiaWQiOiJ1cm46dXVpZDplMDY3ZDVmYy0zNWFlLTRkMGUtYTk1ZS03MzdmMGUwYzIzM2IiLCJpc3N1ZXIiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsImlzc3VhbmNlRGF0ZSI6IjIwMjMtMDYtMjdUMTE6MTY6MDRaIiwiaXNzdWVkIjoiMjAyMy0wNi0yN1QxMToxNjowNFoiLCJ2YWxpZEZyb20iOiIyMDIzLTA2LTI3VDExOjE2OjA0WiIsImNyZWRlbnRpYWxTY2hlbWEiOnsiaWQiOiJodHRwczovL3Jhdy5naXRodWJ1c2VyY29udGVudC5jb20vd2FsdC1pZC93YWx0aWQtc3Npa2l0LXZjbGliL21hc3Rlci9zcmMvdGVzdC9yZXNvdXJjZXMvc2NoZW1hcy9WZXJpZmlhYmxlSWQuanNvbiIsInR5cGUiOiJGdWxsSnNvblNjaGVtYVZhbGlkYXRvcjIwMjEifSwiY3JlZGVudGlhbFN1YmplY3QiOnsiaWQiOiJkaWQ6a2V5Ono2TWtyRnR6WVM1Ulc3NDh2dkFqQVJaNENZakJNdmVWOUxZZlNBRm92NDM5Qm04WiIsImN1cnJlbnRBZGRyZXNzIjpbIjEgQm91bGV2YXJkIGRlIGxhIExpYmVydMOpLCA1OTgwMCBMaWxsZSJdLCJkYXRlT2ZCaXJ0aCI6IjE5OTMtMDQtMDgiLCJmYW1pbHlOYW1lIjoiRE9FIiwiZmlyc3ROYW1lIjoiVGFtaW5vIiwiZ2VuZGVyIjoiRkVNQUxFIiwibmFtZUFuZEZhbWlseU5hbWVBdEJpcnRoIjoiSmFuZSBET0UiLCJwZXJzb25hbElkZW50aWZpZXIiOiIwOTA0MDA4MDg0SCIsInBsYWNlT2ZCaXJ0aCI6IkxJTExFLCBGUkFOQ0UifSwiZXZpZGVuY2UiOlt7ImRvY3VtZW50UHJlc2VuY2UiOlsiUGh5c2ljYWwiXSwiZXZpZGVuY2VEb2N1bWVudCI6WyJQYXNzcG9ydCJdLCJzdWJqZWN0UHJlc2VuY2UiOiJQaHlzaWNhbCIsInR5cGUiOlsiRG9jdW1lbnRWZXJpZmljYXRpb24iXSwidmVyaWZpZXIiOiJkaWQ6ZWJzaToyQTlCWjlTVWU2QmF0YWNTcHZzMVY1Q2RqSHZMcFE3YkVzaTJKYjZMZEhLblF4YU4ifV19LCJqdGkiOiJ1cm46dXVpZDplMDY3ZDVmYy0zNWFlLTRkMGUtYTk1ZS03MzdmMGUwYzIzM2IifQ.tyLqPczrzyRQQNBoR1z5fR9oA50XiT8IX9OpQY_1qLA71eInI71fFOulDsS9WuwfT2FjN5ugjihLaiRVx7OcAg",
        "{\n  \"type\" : [ \"VerifiableCredential\", \"VerifiableAttestation\", \"VerifiableId\" ],\n  \"@context\" : [ \"https://www.w3.org/2018/credentials/v1\", \"https://w3id.org/security/suites/jws-2020/v1\" ],\n  \"id\" : \"urn:uuid:ed0de88b-4df7-458d-9ed6-8caa07a02e2d\",\n  \"issuer\" : \"did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z\",\n  \"issuanceDate\" : \"2023-06-27T11:32:36Z\",\n  \"issued\" : \"2023-06-27T11:32:36Z\",\n  \"validFrom\" : \"2023-06-27T11:32:36Z\",\n  \"credentialSchema\" : {\n    \"id\" : \"https://raw.githubusercontent.com/walt-id/waltid-ssikit-vclib/master/src/test/resources/schemas/VerifiableId.json\",\n    \"type\" : \"FullJsonSchemaValidator2021\"\n  },\n  \"credentialSubject\" : {\n    \"id\" : \"did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z\",\n    \"currentAddress\" : [ \"1 Boulevard de la Liberté, 59800 Lille\" ],\n    \"dateOfBirth\" : \"1993-04-08\",\n    \"familyName\" : \"DOE\",\n    \"firstName\" : \"Tamino\",\n    \"gender\" : \"FEMALE\",\n    \"nameAndFamilyNameAtBirth\" : \"Jane DOE\",\n    \"personalIdentifier\" : \"0904008084H\",\n    \"placeOfBirth\" : \"LILLE, FRANCE\"\n  },\n  \"evidence\" : [ {\n    \"documentPresence\" : [ \"Physical\" ],\n    \"evidenceDocument\" : [ \"Passport\" ],\n    \"subjectPresence\" : \"Physical\",\n    \"type\" : [ \"DocumentVerification\" ],\n    \"verifier\" : \"did:ebsi:2A9BZ9SUe6BatacSpvs1V5CdjHvLpQ7bEsi2Jb6LdHKnQxaN\"\n  } ],\n  \"proof\" : {\n    \"type\" : \"JsonWebSignature2020\",\n    \"created\" : \"2023-06-27T11:32:36Z\",\n    \"verificationMethod\" : \"did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z#z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z\",\n    \"jws\" : \"eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9..P_CJAzsdjsVzL5Zx2hnH3riuq5nhmlIYt8yRc21r1ZiuTMMWQ0Ugo0Ep85gtYjDwCDdS3FNVbDudz-fPqhXMAw\"\n  }\n}"
    ]
}

```

* `policies`: _**\[array]**_ A list of policy definitions to verify against
  * `policy`: _**\[string]**_ The name/id of the policy
  * `argument`: _**\[JSON]**_ The argument needed by the policy (optional)
* `credentials`: _**\[array]**_ An array of credentials in JWT, or LD\_PROOF format
{% endtab %}
{% endtabs %}
