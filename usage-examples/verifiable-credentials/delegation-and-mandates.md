# Delegation and Mandates

The SSI Kit contains and implementation of Authority Delegation (AD) or Verifiable Mandates (VM) – as referred within EBSI/ESSIF. Together with NETIS and the team of the Faculty of Electrical Engineering and Computer Science of the University of Maribor a concept and resarch paper "_A Comprehensive Novel Model for Self-Sovereign Identity Authority_" to outline a possible solution for archiving AD/VM was created. This was funded and support by eSSIF Lab:

[https://essif-lab.eu/authority-delegation-verifiable-mandates-by-netis/](https://essif-lab.eu/authority-delegation-verifiable-mandates-by-netis/)

![](<../../.gitbook/assets/image (5).png>)

The following example shows how to create and to validate a Verifiable Mandate credential.

### Issuing a Verifiable Mandate Credential

Preliminary to the issuing command, the issuer (in this case an individual who wants to delegate authority to some other individual) needs to have control of an asymmetric key and also to a DID (decentralized identifier). Both can be created via CLI tool that the SSI Kit is providing.

Creating a key (the key-id is used in the next command)

```
./ssikit.sh key gen -a Secp256k1
```

Creating a DID. In this case a did:ebsi is created, which can be registered on the EBSI block chain (see [usage-examples.md](../../ecosystems/ebsi-essif/usage-examples/onboarding-and-dids.md "mention")).

```
./ssikit.sh did create -m ebsi -k <key-id>
```

By having access to the issuer key and DID the following issuing command can be entered. Note that the parameter "--interactive" will prompt for several parameter that needs to be applied for creating the Verifiable Mandate credential. Therefore one must have the DID of the recipient of the delegated authority available.

The parameter "-s" is referring to "subject" and "-i" to "issuer". As the VM is a self-signed credential, the same DID is used in this case.

```
./ssikit.sh vc issue -t VerifiableMandate -i did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX -s did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX --interactive
```

**Output:**

```
Issuing a verifiable credential (using template VerifiableMandate)..

> Grant

ID of holder [did:ebsi:ze2dC9GezTtVSzjHVMQzpkE]: did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd
Role [family]: family
Name [apply_to_bachelors]: apply_to_masters
Location [Spain]: Slovenia

Results:

Issuer "did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX"
⇓ issued a "VerifiableMandate" to ⇓
Holder "did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX"

Credential document (below, JSON):

{
  "@context" : [ "https://www.w3.org/2018/credentials/v1" ],
  "credentialSchema" : {
    "id" : "https://api.preprod.ebsi.eu/trusted-schemas-registry/v1/schemas/0xb77f8516a965631b4f197ad54c65a9e2f9936ebfb76bae4906d33744dbcc60ba",
    "type" : "FullJsonSchemaValidator2021"
  },
  "credentialSubject" : {
    "holder" : {
      "constraints" : {
        "location" : "Slovenia"
      },
      "grant" : "apply_to_masters",
      "id" : "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd",
      "role" : "family"
    },
    "id" : "did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX",
    "policySchemaURI" : "https://raw.githubusercontent.com/walt-id/waltid-ssikit/master/src/test/resources/verifiable-mandates/test-policy.rego"
  },
  "evidence" : [ {
    "evidenceValue" : "",
    "id" : "https://essif.europa.eu/tsr-va/evidence/f2aeec97-fc0d-42bf-8ca7-0548192d5678",
    "type" : [ "VerifiableMandatePresentation" ]
  } ],
  "id" : "urn:uuid:40733519-78c7-4248-a80a-fede7c5ce978",
  "issued" : "2022-05-19T21:39:21.880729594Z",
  "issuer" : "did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX",
  "validFrom" : "2022-05-19T21:39:21.880731854Z",
  "issuanceDate" : "2022-05-19T21:39:21.880731854Z",
  "type" : [ "VerifiableCredential", "VerifiableMandate" ],
  "proof" : {
    "type" : "EcdsaSecp256k1Signature2019",
    "creator" : "did:ebsi:ztZgP4NGDZgoGRqHpaxQkfX",
    "created" : "2022-05-19T21:39:53Z",
    "domain" : "https://api.preprod.ebsi.eu",
    "nonce" : "0f083aa8-4e8e-4bb3-acef-5467fbc077a3",
    "proofPurpose" : "assertion",
    "jws" : "eyJiNjQiOmZhbHNlLCJjcml0IjpbImI2NCJdLCJhbGciOiJFUzI1NksifQ..OPHTDcz6AWSF8SODePIRM9xCCvmOqbOuUk88E6piCALT0QticpiHnfnOZiYZRAvXmXEJ1iDjI6tVrNAq2kKTug"
  }
}

```

Most importantly in the above shown example are the lines 5 to 6,  as they are created by an interactive dialog with the user (issuer of the credential). The user may define **who** gets **which** permissions. In this case the permissions are delegated to the DID:  did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd. This DID is classified as "family-member" and furthermore is granted to "apply for a master degree" on behalf of the issuing party. Additionally the constrain "location" is defined by "Slovenia" instead of the default value "Spain".&#x20;

The credential body is afterwards signed by the private key of the issuer, which generate the JSON LD proof.

### Verifying a Verifiable Mandate Credential

The Auditor (verifying component of the SSI Kit) can simply be called by the "vc verfiy" command. It takes the filename as argument as well as a list of policies. For keeping this example as simple as possible only the "VerifiableMandatePolicy" is used. Note that the VerifiableMandatePolicy takes a list of arguments as well. This is the JSON document, which dynamically setup the verification engine

#### **Verifying successfully a Verifiable Mandate Credential**

```
{ 
  "user": "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd", 
  "action": "apply_to_masters", 
  "location": "Germany"
}  
```

The full command can be seen here:

```
./ssikit.sh vc verify vm.json -p VerifiableMandatePolicy='{"user": "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd", "action": "apply_to_masters", "location": "Slovenia"}'
```

**Output:**

```
Verifying from file "vm.json"...

rego payload: {"data":{"constraints":{"location":"Slovenia"},"grant":"apply_to_masters","id":"did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd","role":"family"},"input":{"user":"did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd","action":"apply_to_masters","location":"Slovenia"},"rego_modules":{"policy.rego":"package app.rbac\n\nimport future.keywords.in\nimport future.keywords.every\n\ndefault allow = false\n\nroles = [\"family\", \"friend\"]\ngrants = {\n    \"family\": [\"apply_to_masters\", \"get_grades\"],\n    \"friend\": [\"get_grades\"]\n}\nconstraints = {\n    \"get_grades\": [\"location\", \"time\"],\n    \"apply_to_masters\": [\"location\"]\n}\n\n# all inputs must contain user and actions\n\nallow {\n    input.user == data.id\n    data.role in roles\n    input.action in grants[data.role]\n\n    input.action == data.grant\n\n    every constraint in constraints[input.action] {\n        data.constraints[constraint] == input[constraint]\n    }\n}\n"},"strict":true}

Results:

VerifiableMandatePolicy:         true
Verified:                        true

```

#### **Failing to verify a Verifiable Mandate Credential**

In this case the constraint "location" is set from "Slovenia" to  "Germany":

```
./ssikit.sh vc verify vm.json -p VerifiableMandatePolicy='{"user": "did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd", "action": "apply_to_masters", "location": "Germany"}'
```

**Output:**

```
Verifying from file "vm.json"...


rego payload: {"data":{"constraints":{"location":"Slovenia"},"grant":"apply_to_masters","id":"did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd","role":"family"},"input":{"user":"did:key:z6MkvUtihkikPAdwzs18AExS4GFr6t4owyHFRrLFdpRScZDd","action":"apply_to_masters","location":"Germany"},"rego_modules":{"policy.rego":"package app.rbac\n\nimport future.keywords.in\nimport future.keywords.every\n\ndefault allow = false\n\nroles = [\"family\", \"friend\"]\ngrants = {\n    \"family\": [\"apply_to_masters\", \"get_grades\"],\n    \"friend\": [\"get_grades\"]\n}\nconstraints = {\n    \"get_grades\": [\"location\", \"time\"],\n    \"apply_to_masters\": [\"location\"]\n}\n\n# all inputs must contain user and actions\n\nallow {\n    input.user == data.id\n    data.role in roles\n    input.action in grants[data.role]\n\n    input.action == data.grant\n\n    every constraint in constraints[input.action] {\n        data.constraints[constraint] == input[constraint]\n    }\n}\n"},"strict":true}

Results:

VerifiableMandatePolicy:         false
Verified:                        false
```
