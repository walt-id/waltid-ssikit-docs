---
description: >-
  Onboarding Emma to a Virtual Company, issuing custom credentials, and
  utilizing dynamic verification policies.
noIndex: true
---

# Advanced VC

In this tutorial, we will expand on the ["My First VC" tutorial](my-first-vc.md) by now onboarding Emma to a virtual company. During the onboarding, Emma will receive an EmployeeID credential, which will be based on a custom credential template using the status property. With that, you learn about two more concepts; Custom credential templates and the status property. The credential will also have Emma's role as a property, which can then be checked with a dynamic verification policy, another new concept.

**Where we start:**

Using the walt.id SSI-Kit's REST API, we'll streamline access control within the company by

* [**Establishing a Digital Identity (DID)**](advanced-vc.md#establishing-a-digital-identity-did): The company will be set up as the issuer through its own Digital Identity (DID).
* [**Creating an EmployeeID Template**](advanced-vc.md#creating-an-employeeid-template): This template will be used for generating verifiable credentials for employees.
* [**Issuing a Verifiable Credential to Emma**](advanced-vc.md#issuing-a-verifiable-credential-to-emma): Emma, an employee, will be issued a Verifiable Credential, making her the holder.
* [**Authenticating with Door Access System**](advanced-vc.md#authenticating-with-door-access-system): The system, acting as the Verifier, will:
  * Confirm Emma's employment status
  * Assess her role within the company
  * Grant or deny access to specific areas on the company campus based on the above.

### Running the SSI-Kit

Make sure you have Docker or a JDK 16 build environment including Gradle installed on your machine

{% tabs %}
{% tab title="Docker" %}
Pull the docker container directly from docker hub and run the project

```
docker run -p 7000-7004:7000-7004 -itv $(pwd)/data:/app/data waltid/ssikit serve -b 0.0.0.0
```

This will create a folder called data in your current directory as storage for the VC, DIDs, Keys and other things which need to be stored in order to provide all the functionality.
{% endtab %}

{% tab title="Local" %}
1. Clone the project

```
git clone https://github.com/walt-id/waltid-ssikit.git
```

2\. Change the folder

```
cd waltid-ssikit/
```

3\. Run the project

The first time you run the command you will be asked to built the project. You can confirm the prompt.

```
./ssikit.sh serve
```
{% endtab %}
{% endtabs %}

Now with the SSI-Kit up and running, we can create the DID for the company, establishing its Digital Identity.

### **Establishing a Digital Identity (DID)**

{% tabs %}
{% tab title="REST API" %}
You have two options for creating a DID: executing a curl command or visiting the swagger docs. The custodian endpoint should be visible in the terminal after you have run the serve command, visit the endpoint to see the swagger docs.

```bash
curl -X 'POST' \
  'http://localhost:7002/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "{method}"
}'
```

**Body Parameters**\
`method`: _**\[string]**_ method of the did. Value can be one of `key`, `web`, `ebsi`, `iota`, `cheqd`, `jwk`\
\
**Example**

```bash
curl -X 'POST' \
  'http://localhost:7002/did/create' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "method": "key"
}'
```
{% endtab %}
{% endtabs %}

Create one DID for the company using the command above. In case you don't have done the My First VC tutorial and still have the DID for Emma, create another one for her. Make sure to save both, as we will be needing them later for the issuance of the EmployeID. You can also use [the list DID endpoint ](../getting-started/rest-apis/custodian-api/did-management.md#list-did)to see all previously created DIDs.

### **Creating an EmployeeID Template**

The SSI-Kit supports the creation of [credential templates](../concepts/credential-templates.md), which are blueprints that establish reusable data structures based on which credentials can be issued.

Let's create one for an EmployeeID. The template will include the following properties:

* `id`: Identifier for the employee
* `name`: Name of the employee
* `role`: Role or designation in the company
* `joiningDate`: Date of joining the company

```json
{
  "type": ["VerifiableCredential", "EmployeeID"],
  "credentialSubject": {
    "id": "",
    "name": "",
    "role": "",
    "joiningDate": ""
  }
}
```

#### Saving the credential template

{% tabs %}
{% tab title="API" %}
```bash
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/templates/{id}' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{credentialTemplate}'
```

**Path Parameters**

* `id`: The name for the credential template, which we will later reference during issuance. e.g. EmployeeID

**Body**\
Use the JSON structure from above as the body.\
\
**Example**

```bash
curl -X 'POST' \
  'http://127.0.0.1:7001/v1/templates/EmployeeID' \
  -H 'accept: text/plain' \
  -H 'Content-Type: application/json' \
  -d '{
    "type": ["VerifiableCredential", "EmployeeID"],
    "credentialSubject": {
        "id": "",
        "name": "",
        "role": "",
        "joiningDate": ""
    }
}'
```
{% endtab %}
{% endtabs %}

We can streamline the process of issuing a credential to Emma by utilizing the EmployeeID credential template. However, we also have the opportunity to further simplify the process using an additional feature: prefilling credential properties. This will be particularly beneficial as Emma likely won't be the only one receiving the Engineer role assignment. By creating a template where the Engineer role is prefilled, we can improve the issuance process.

#### EngineerEmployeeID Template

```
{
    "type": ["VerifiableCredential", "EmployeeID"],
    "credentialSubject": {
        "id": "",
        "name": "",
        "role": "Engineer",
        "joiningDate": ""
    }
}
```

You can now also save this template and use it later for the issuance of our VC, or use the one we created before and provide the value for the role attribute during issuance.

### **Issuing a Verifiable Credential to Emma**

In order to issue Emma's EmployeeID VC, we will use one of the credential templates. Additionally, we will include a credential status so that we have the option to revoke the credential if Emma leaves the company without needing to remove it from her ownership. For more information on credential status and the types we support, read [our guide](../concepts/credential-statuses/).

{% tabs %}
{% tab title="API" %}
```bash
curl -X 'POST' \
  'http://localhost:7001/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "templateId": "{template type}",
  "config": {
    "issuerDid": "{issuerDid}",
    "subjectDid": "{subjectDid}",
    "proofType": "{proofType}",
    "statusType": "{statusType}"
  },
  "credentialData": {
    "id": "{subjectDID}",
    "name": "{name}",
    "role": "{role}",
    "joiningDate": "{joiningDate}"
  }
}'
```

**Body Parameters**

* `templateId`: _**\[string]**_ The identifier of the template used for issuing a Verifiable Credential. In our case this would be the EmployeeID or EngineerEmployeeID template.
* `config`: _**\[object]**_ Contains configuration parameters for the issuance process.
  * `issuerDid`: _**\[string]**_ The DID of the entity issuing the credential (University).
  * `subjectDid`: _**\[string]**_ The DID of the entity receiving the credential (Emma).
  * `proofType`: _**\[string]**_ Specifies the format and cryptographic algorithm used for the digital signature of the Verifiable Credential. E.g. LD\_PROOF
  * `statusType`: _**\[statusType]**_ Specifies if the credential should be issued with status and the type of the status. Options `StatusList2021Entry` or `SimpleCredentialStatus2022`
* `credentialData`: _**\[object]**_ Contains the actual data of the credential being issued.
  * `credentialSubject`: _**\[object]**_ Holds the information about the employee as described in the EmployeeID credential template.

{% hint style="info" %}
The `id` in the credential subject we don't need to provide as this will be prefilled automatically with the DID of Emma.
{% endhint %}

**Example EmployeeID:**

```bash
curl -X 'POST' \
  'http://localhost:7001/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "templateId": "EmployeeID",
  "config": {
    "issuerDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "subjectDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "proofType": "LD_PROOF",
    "statusType": "StatusList2021Entry"
  },
  "credentialData": {
    "name": "Emma",
    "role": "Engineer",
    "joiningDate": "2023-06-28"
  }
}'
```

**Example EngineerEmployeeID:**

```bash
curl -X 'POST' \
  'http://localhost:7001/v1/credentials/issue' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "templateId": "EngineerEmployeeID",
  "config": {
    "issuerDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "subjectDid": "did:key:z6MkmE21F2dAHkM71tnYdBEGaSvnPpxBFZYi2wtzYbTwqvgK",
    "proofType": "LD_PROOF",
    "statusType": "StatusList2021Entry"
  },
  "credentialData": {
    "name": "Emma",
    "joiningDate": "2023-06-28"
  }
}'
```
{% endtab %}
{% endtabs %}

Now we can use the issued VC in the company campus verification system.

### **Authenticating with Door Access System**

To successfully authorize access, our authentication system needs to verify four crucial elements regarding the Verifiable Credential presented during the verification process:

1. Confirm the signature of the Verifiable Credential to ensure it's legitimate.
2. Ascertain the credential's validity by validating its current status, ensuring it has not expired or been revoked.
3. Verify that the issuer is indeed our company, thereby eliminating any fraudulent issuers.
4. Evaluate whether the role of the employee, as indicated on the credential, authorizes them to access the desired area.

To facilitate successful verification, we will use Verification Policies. For the initial two cases, which are relatively common, we can utilize our built-in policies, namely `SignaturePolicy` and `CredentialStatusPolicy`. These policies essentially verify that the signature is authentic and that the status is still valid.

For the additional cases, we will create custom policies, leveraging the Open Policy Agent (OPA) Engine and the REGO language. You can learn more about it [here](../concepts/verification-policies/dynamic-policies/).

{% hint style="info" %}
Please install the Open Policy Agent as described [here](../usage-examples/open-policy-agent/configure-opa-engine.md), to ensure seamless verification.
{% endhint %}

#### Creating Custom Policies - IsCompany

```
package system

default main = false

main {
    input.credentialData.issuer == {issuerDID}
}
```

{% hint style="info" %}
Make sure to replace {issuerDID} with the DID of your issuer (company)
{% endhint %}

\
**Creating Custom Policies - IsRole**

This custom policy holds greater flexibility, as it accepts an argument containing a 'role' property. This property is then cross-verified with the role present in the Verifiable Credential. Alternatively, the role can be hardcoded, and the policy can be renamed accordingly, such as `IsEngineer`, similar to the `IsCompany` policy.

```
package system

default main = false

main {
    input.parameter.role == input.credentialData.credentialSubject.role
}
```

#### Saving the policies

{% tabs %}
{% tab title="API" %}
```bash
curl -X 'POST' \
  'http://127.0.0.1:7003/v1/create/{{policyName}}?update=true&downloadPolicy=true' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "IsCompany",
    "description": "Test",
    "input": {},
    "policy": "package system

default main = false

main {
    input.credentialData.issuer == \"did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z\"
}",
}
",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}'
```

**Path parameters:**

* `policyName`: _**\[string]**_ Name of the policy, e.g. IsCompany

**Query parameters:**

* `update`: _**\[boolean]**_ Specifies if existing policy with same name should be overridden (if mutable)
* `downloadPolicy`: _**\[boolean]**_ When using an URL to reference the to created policy. Downloads and/or saves the policy definition locally, rather than keeping the reference to the original URL\\

**Body**

```json
{
    "name": "MyCustomPolicy",
    "description": "Test",
    "input": {},
    "policy": "package system

               default main = false

               main {
                 input.credentialData.issuer == \"did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z\"
    }",
    "dataPath": "$",
    "policyQuery": "data.system.main",
    "policyEngine": "OPA",
    "applyToVC": true,
    "applyToVP": true
}
```

* `name`: _**\[string]**_ Policy name, must not conflict with existing policies
* `description`: _**\[string]**_ Optional policy description
* `input`: _**\[JSON]**_ Input JSON object for rego query, which can be overridden/extended on verification. Can be a JSON string or JSON file
* `policy`: _**\[URL, REGO]**_ Whole Policy or URL to policy definition.
* `dataPath`: _**\[JSON path]**_ JSON path to the data in the credential which should be verified, default: "$" (whole credential object)
* `policyQuery`: _**\[string]**_ The query string in the policy engine language. Defaults to\
  "data.system.main".
* `policyEngine`: _**\[string]**_ Policy engine type, default: OPA. Options, OPA
* `applyToVC`: _**\[boolean]**_ Apply/Don't apply to verifiable credentials (default: apply)
* `applyToVP`: _**\[boolean]**_ Apply/Don't apply to verifiable presentation (default: don't apply)
{% endtab %}
{% endtabs %}

Using the endpoint above, you can save both policies.

#### Verifying the credential with all policies

{% tabs %}
{% tab title="API" %}
Now with the custom policies created, we will use those and the two predefined ones to verify Emma's credential and enable access.

```bash
curl -X 'POST' \
  'http://127.0.0.1:7003/v1/verify' \
  -H 'accept: application/json' \
  -H 'Content-Type: text/plain' \
  -d '{
    "policies": [
        {
            "policy": "SignaturePolicy"
        },
        {
            "policy": "CredentialStatusPolicy"
        },
        {
            "policy": "IsRole",
            "argument": {"role": "Engineer"}
        },
        {
            "policy": "IsCompany"
        }
    ],
    "credentials": [{
  "type" : [ "VerifiableCredential", "EngineerEmployeeID" ],
  "@context" : [ "https://www.w3.org/2018/credentials/v1", "https://w3id.org/security/suites/jws-2020/v1" ],
  "id" : "urn:uuid:ae9cf1f3-8609-4685-9928-5073b6990af4",
  "issuer" : "did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z",
  "issuanceDate" : "2023-06-28T13:55:15Z",
  "issued" : "2023-06-28T13:55:15Z",
  "validFrom" : "2023-06-28T13:55:15Z",
  "credentialSubject" : {
    "id" : "did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z",
    "name" : "Emma",
    "role" : "Engineer",
    "joiningDate" : "2023-06-28"
  },
  "credentialStatus" : {
    "id" : "http://127.0.0.1:7001/v1/credentials/status/revocation#2",
    "statusListCredential" : "http://127.0.0.1:7001/v1/credentials/status/revocation",
    "statusListIndex" : "2",
    "statusPurpose" : "revocation",
    "type" : "StatusList2021Entry"
  },
  "proof" : {
    "type" : "JsonWebSignature2020",
    "created" : "2023-06-28T13:55:15Z",
    "verificationMethod" : "did:key:z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z#z6MkrFtzYS5RW748vvAjARZ4CYjBMveV9LYfSAFov439Bm8Z",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFZERTQSJ9.._uFLlXHpNgFsUJFwahcIh_VeLsps8n5ZaifMMvAMqmOkESWN1eoJNNkGfAYY_R185ia-qkKRKwb2rsNzPUcvAA"
  }
}]
}
'
```

**Body**

```json
{
    "policies": [
        {
            "policy": "SignaturePolicy"
        },
        {
            "policy": "CredentialStatusPolicy"
        },
        {
            "policy": "IsRole",
            "argument": {"role": "Engineer"}
        },
        {
            "policy": "IsCompany"
        }
    ],
    "credentials": [
      {... credential ... }
    ]
}

```

* `policies`: _**\[array]**_ A list of policy definitions to verify against
  * `policy`: _**\[string]**_ The name/id of the policy
  * `argument`: _**\[JSON]**_ The argument needed by the policy (optional)
* `credentials`: _**\[array]**_ An array of credentials in JWT, or LD\_PROOF format
{% endtab %}
{% endtabs %}

Congratulations, you've reached the finish line! 🎉 You have skillfully utilized an array of features to bring this use case to life. Now, you have the opportunity to explore further and deepen your understanding of the concepts introduced today. Happy building!

### Next Steps

* [Credential Templates](../concepts/credential-templates.md) - Dive deeper into credential templates and what you can do with them
* [Credential Status](../concepts/credential-statuses/) - Learn more about the credential status property and what is enables.
* [Verification Policies](../usage-examples/verifiable-credentials/verification-policies.md) - Explore our pre-build templates and learn more about how to build and leverage custom ones using OPA (Open Policy Agent) and the Rego language.
