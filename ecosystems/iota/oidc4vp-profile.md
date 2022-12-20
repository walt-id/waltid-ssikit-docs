# OIDC4VP profile for _Login-with-IOTA_
<font size="1">**Authors:** Severin Stampler ([walt.id](https://walt.id))<br />
December 2022
</font>

## Introduction

_Login-with-IOTA_ is defined as a profile of the _OpenID Connect for Verifiable Presentations_ specification [[OIDC4VP](#oidc4vp)], which defines the protocol for authorization using SSI, based on top of OAuth 2.0 [[RFC6749](#rfc6749)] and introduces protocol extensions for the presentation of claims via Verifiable Credentials [[VC_DATA_MODEL](#vc_data_model)].
In this document we will describe the specifics of using the OIDC4VP protocol in the scope of _Login-with-IOTA_ to ensure compatibility with the _IOTA identity framework_ [[IOTA_IDENTITY](#iota_identity)].

## DIDs and Key Material

The _IOTA identity framework_ [[IOTA_IDENTITY](#iota_identity)] defines a custom _DID method_ [[IOTA_DID](#iota_did)], based on the public key of the user account. The key material used is an _EdDSA/Ed25519_ [[RFC8032](#rfc8032)] key pair.


| DID method  | Key algorithm |
|---          |---            |
| [did:iota](#iota_did)    | [EdDSA/Ed25519](#rfc8032) |

To ensure compatibility with the IOTA identity framework [[IOTA_IDENTITY](#iota_identity)], the issuers and holders of verifiable credentials should use a _did:iota_ for issuance and as credential subject.

## Verifiable Credentials and Proof Format

The credentials used by the _IOTA identity framework_ [[IOTA_IDENTITY](#iota_identity)] are in line with the W3C specification for Verifiable Credentials [[VC_DATA_MODEL](#vc_data_model)]. Every type of credential, that is compatible with the W3C specification, should in theory be supported.

**Proofs** for the credentials are created in the linked data format, **ldp_vc** or **ldp_vp**, as described by the _W3C data integrity_ specification [[VC_DATA_INTEGRITY](#vc_data_integrity)], using [[JSON-LD](#json_ld)] as the credential format and the _JCS Ed25519 Signature 2020_ [[JcsEd25519Signature2020](#jcsed25519signature2020)] signature type.

| Format  | Signature type |
|---          |---            |
| [ldp_vc / ldp_vp](#vc_data_integrity)    | [JcsEd25519Signature2020](#jcsed25519signature2020) |

## Authorization flow

The [[OIDC4VP](#oidc4vp)] specification is based on top of OAuth 2.0 [[RFC6749](#rfc6749)], which enables implementers to also build on top of _OpenID Connect_ [[OIDC](#oidc)] and the _Self-issued OpenId Provider_ specification [[SIOPv2](#siopv2)].

This _Login-with-IOTA_ profile of the [[OIDC4VP](#oidc4vp)] specification supports only W3C Verifiable Credentials [[VC_DATA_MODEL](#vc_data_model)].

Like described by [[OIDC4VP](#oidc4vp)], verifiable presentations can be requested by adding the `presentation_definition` parameter to the authorization request. The presentation is returned in the `vp_token` response parameter.

Both, [same-device](#same-device-flow) and [cross-device](#cross-device-flow) flows are supported by this profile. For cross-device scenarios [[OIDC4VP](#oidc4vp)] introduces a new response mode `post`, to support verifier initiated verification.

### Request

The parameters for a _Login-with-IOTA_ authorization request, are a subset of the parameters defined by the [[OIDC4VP](#oidc4vp)] specification:

* `response_type`: _REQUIRED_. this parameter is defined in [[RFC6749](#rfc6749)]. The possible values are determined by the response type registry established by [[RFC6749](#rfc6749)]. This specification introduces the response type `vp_token`. This response type asks the Authorization Server (AS) to return only a VP Token in the Authorization Response.

* `presentation_definition`: _CONDITIONAL_. A string containing a presentation_definition JSON object as defined in Section 4 of [[DIF.PresentationExchange](#difpresentationexchange)].

* `presentation_definition_uri`: _CONDITIONAL_. A string containing a URL pointing to a resource where a `presentation_definition` JSON object as defined in Section 4 of [[DIF.PresentationExchange](#difpresentationexchange)] can be retrieved .

* `nonce`: _REQUIRED_. This parameter follows the definition given in [[OIDC](#oidc)]. It is used to securely bind the verifiable presentation(s) provided by the AS to the particular transaction.

* `state`: _OPTIONAL_. State provided by the authorization client, that is passed through to the response.

A request MUST contain either a `presentation_definition` or a `presentation_definition_uri`. Those two ways to request credential presentations are mutually exclusive. The wallet MUST refuse any request violating this requirement.

#### presentation_definition

The `presentation_definition` parameter must contain a JSON representation of a _Presentation Definition_ object, according to the _DIF Presentation Exchange_ specification [[DIF.PresentationExchange](#difpresentationexchange)].

**Alternatively** the request could contain the `presentation_definition_uri` parameter, containing a URL to a presentation definition object.

The following example shows a presentation definition object, requesting the presentation of a `VerifiableId` credential:

```
{
    "id": "vp token example",
    "input_descriptors": [
        {
            "id": "verifiable id credential",
            "format": {
                "ldp_vc": {
                    "proof_type": [
                        "JcsEd25519Signature2020"
                    ]
                }
            },
            "constraints": {
                "fields": [
                    {
                        "path": [
                            "$.type"
                        ],
                        "filter": {
                            "type": "string",
                            "pattern": "VerifiableId"
                        }
                    }
                ]
            }
        }
    ]
}

```

#### Example request

This is an example authorization request:

```
GET /authorize?
  scope=openid
  &presentation_definition=[...]
  &response_type=vp_token
  &redirect_uri=[...]
  &state=9925f001-9010-4dd3-9a58-5c140c85d824
  &nonce=9925f001-9010-4dd3-9a58-5c140c85d824
  &client_id=[...]
  &response_mode=post
```

### Response

The response parameters depend on the `response_type` defined in the authorization request. Possible response parameters include:

* `vp_token`: The verifiable presentation or array of presentations matching the presentation definition in the request. The required format in this profile is [[`ldp_vp`](#vc_data_integrity)] / [[JSON-LD](#json_ld)]. The JSON data must be URL encoded. See also section 7.3 of [[OIDC4VP](#oidc4vp)].
* `id_token`: The ID token as defined by section 2 of the [[OIDC](#oidc)] core specification.
* `presentation_submission`: The presentation submission object, as defined in [[DIF.PresentationExchange](#difpresentationexchange)], which links the input descriptors of the presentation definition in the request to the corresponding presentation(s) in the `vp_token` response.
* `state`: Optional state parameter passed through from the authorization request.

#### Response types

Depending of the `response_type` given in the authorization request, the response should contain the following parameters, like described in section 6.1 of [[OIDC4VP](#oidc4vp)]:

* If only `vp_token` is used as the `response_type`, the VP Token is provided in the authorization response.
* If `id_token` is used as the `response_type` alongside `vp_token`, the VP Token is provided in the OpenID Connect authentication response along with the ID Token.
* In all other cases, if `vp_token` is not used, but `presentation_definition` parameter is present, the VP Token is provided in the Token Response.

Any combination of `vp_token` with a `response_type` other than `id_token` is undefined.

#### vp_token

The `vp_token` response parameter contains the verifiable presentation or array of verifiable presentations, matching the input descriptors of the presentation definition, specified in the authorization request.

The only supported format of the verifiable presentation in this specification is the [[`ldp_vp`](#vc_data_integrity)] / [[JSON-LD](#json_ld)] format.  The JSON data can be either a single presentation object or an array of JSON objects and must be URL encoded.

#### presentation_submission

The presentation submission object contains the correlations of the input descriptors, specified in the presentation definition of the authorization request, with the verifiable presentations in the VP token of the response. The format of the presentation submission objects is defined in section 6 of [[DIF.PresentationExchange](#difpresentationexchange)].

#### Example responses

This is an example response for the `respones_type=vp_token` request parameter, with the `presentation_submission` and `vp_token` response parameters:

```
HTTP/1.1 302 Found
  Location: https://client.example.org/cb#
    presentation_submission=[...]
    &vp_token=[...]
    &state=9925f001-9010-4dd3-9a58-5c140c85d824
```

An example `vp_token`, containing a presentation with a VerifiableId credential:

```
{
  "type": [
    "VerifiablePresentation"
  ],
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://w3id.org/security/suites/jws-2020/v1"
  ],
  "id": "urn:uuid:73c01e73-6f18-4e8c-a751-ec9f4d25855e",
  "holder": "did:iota:6Nte6ZfQGQ81UZNGBLtDAJnFui8nBgEMjtMKDadYYexS",
  "verifiableCredential": [
    {
      "type": [
        "VerifiableCredential",
        "VerifiableAttestation",
        "VerifiableId"
      ],
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1"
      ],
      "id": "urn:uuid:4be3b79e-16aa-4562-883c-e5e1c11fd623",
      "issuer": "did:iota:z6MkiprkVjgTngmWh6y2cEPDBPWiWpnSxaPiL4HR8vQRoR3h",
      "issuanceDate": "2022-12-20T10:02:57Z",
      "issued": "2022-12-20T10:02:57Z",
      "validFrom": "2022-12-20T10:02:57Z",
      "credentialSchema": {...},
      "credentialSubject": {
        "id": "did:iota:6Nte6ZfQGQ81UZNGBLtDAJnFui8nBgEMjtMKDadYYexS",
        "currentAddress": [...],
        "dateOfBirth": "1993-04-08",
        "familyName": "DOE",
        "firstName": "Jane",
        "gender": "FEMALE",
        "nameAndFamilyNameAtBirth": "Jane+DOE",
        "personalIdentifier": "0904008084H",
        "placeOfBirth": "LILLE,+FRANCE"
      },
      "evidence": [...],
      "proof": {
        "type": "JcsEd25519Signature2020",
        [...]
        "verificationMethod": "did:iota:[...]",
        "signatureValue": "[...]"
      }
    }
  ],
  "proof": {
    "type": "JcsEd25519Signature2020",
    [...]
    "proofPurpose": "authentication",
    "verificationMethod": "did:iota:[...]",
    "signatureValue": "[...]"
  }
}
```

An example `presentation_submission` object:

```
{
  "definition_id": "1",
  "descriptor_map": [
    {
      "format": "ldp_vp",
      "id": "0",
      "path": "$",
      "path_nested": {
        "format": "ldp_vc",
        "id": "0",
        "path": "$.verifiableCredential[0]"
      }
    }
  ],
  "id": "1"
}
```

#### Error response

For creating compliant error responses, please refer to section 6.3 of [[OIDC4VP](#oidc4vp)].

### Same-device flow (Web)

For the same device flow, the verifier or relying party, links directly to the authorization endpoint of the wallet, passing the request parameters, as specified in the [Authorization request](#request) section.

The `response_mode` should be set to `form_post`. After getting the user consent, the wallet will generate the response parameters, as specified in the [Authorization response](#response) section, and performs a HTTP FORM POST action to the `redirect_uri` specified in the authorization request. The relying party can now verify the authorization response and redirect the user to the protected web page.

#### Example request

```
https://wallet.walt-test.cloud/api/siop/initiatePresentation/
  ?scope=openid
  &presentation_definition=[...]
  &response_type=vp_token
  &redirect_uri=https%3A%2F%2Fverifier.walt-test.cloud%2Fverifier-api%2Fverify
  &state=f3265a8c-4dff-4252-8df9-6569286e109a
  &nonce=f3265a8c-4dff-4252-8df9-6569286e109a
  &client_id=https%3A%2F%2Fverifier.walt-test.cloud%2Fverifier-api%2Fverify
  &response_mode=form_post
```

#### Example response

```
POST https://verifier.walt-test.cloud/verifier-api/verify

vp_token=[...]
&presentation_submission=[...]
&state=f3265a8c-4dff-4252-8df9-6569286e109a
```

### Cross-device flow

For the cross-device flow, the verifier or relying party initiates an internally cached authorization session and displays a QR code containing the authorization request URI with the request parameters, as specified in the [Authorization request](#request) section.

The `response_mode` should be set to `post`. The wallet scans the QR code and parses the authorization request. After getting the user consent, the wallet will generate the response parameters, as specified in the [Authorization response](#response) section, and posts the response to the `redirect_uri` specified in the authorization request, via the HTTP POST method. The relying party can now verify the authorization response and update the state of the internally cached authorization session.
Depending on the concrete implementation (for example by polling for the session state), the relying party UI can now be refreshed and redirected to the protected page.

#### Example request

```
openid://
  ?scope=openid
  &presentation_definition=[...]
  &response_type=vp_token
  &redirect_uri=https%3A%2F%2Fverifier.walt-test.cloud%2Fverifier-api%2Fverify
  &state=663667ae-fc5c-4cb8-87ab-1f506ca142e7
  &nonce=663667ae-fc5c-4cb8-87ab-1f506ca142e7
  &client_id=https%3A%2F%2Fverifier.walt-test.cloud%2Fverifier-api%2Fverify
  &response_mode=post
```

#### Example response

```
POST https://verifier.walt-test.cloud/verifier-api/verify

vp_token=[...]
&presentation_submission=[...]
&state=f3265a8c-4dff-4252-8df9-6569286e109a
```

## References

#### [[OIDC4VP](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)]
Terbu, O., Lodderstedt, T., Yasuda, K., Lemmon, A., Looker, T., "OpenID for Verifiable Presentations", September 2022, <https://openid.net/specs/openid-4-verifiable-presentations-1_0.html>

#### [[RFC6749](https://www.rfc-editor.org/info/rfc6749)]
Hardt, D., Ed., "The OAuth 2.0 Authorization Framework", RFC 6749, DOI 10.17487/RFC6749, October 2012, <https://www.rfc-editor.org/info/rfc6749>

#### [[VC_DATA_MODEL](https://www.w3.org/TR/vc-data-model/)]
Sporny, M., Longley, D., Chadwick, D., "Verifiable Credentials Data Model v1.1", March 2022, <https://www.w3.org/TR/vc-data-model/>

#### [[IOTA_IDENTITY](https://wiki.iota.org/identity.rs/introduction/)]
IOTA Foundation, "IOTA Identity Framework Guide", <https://wiki.iota.org/identity.rs/introduction/>

#### [[IOTA_DID](https://wiki.iota.org/identity.rs/specs/did/iota_did_method_spec/)]
Millenaar, J., IOTA Foundation, "IOTA DID Method Specification", <https://wiki.iota.org/identity.rs/specs/did/iota_did_method_spec/>

#### [[RFC8032](https://datatracker.ietf.org/doc/html/rfc8032)]
 Josefsson, S.; Liusvaara, I. (January 2017). Edwards-Curve Digital Signature Algorithm (EdDSA). IRTF. doi:10.17487/RFC8032. ISSN 2070-1721. RFC 8032. <https://datatracker.ietf.org/doc/html/rfc8032>

#### [[VC_DATA_INTEGRITY](https://w3c.github.io/vc-data-integrity/)]
Longley, D., Sporny, M., "Verifiable Credential Data Integrity 1.0", <https://w3c.github.io/vc-data-integrity/>

#### [[JSON_LD](https://www.w3.org/TR/json-ld11/)]
Sporny, M., Longley, D., Kellog, G., Lanthaler, M., Champin, P., Lindström, N., "JSON-LD 1.1", <https://www.w3.org/TR/json-ld11/>

#### [[JCSEd25519Signature2020](https://identity.foundation/JcsEd25519Signature2020/)]
Cohen, G., Steele, O, Decentralized Identity Foundation, "JCS Ed25519 Signature 2020", <https://identity.foundation/JcsEd25519Signature2020/>

#### [[OIDC](https://openid.net/specs/openid-connect-core-1_0.html)]
N. Sakimura, J. Bradley, M. Jones, B. de Medeiros, C. Mortimore, "OpenID Connect Core 1.0 incorporating errata set 1", November 8, 2014, <https://openid.net/specs/openid-connect-core-1_0.html>

#### [[SIOPv2](https://openid.bitbucket.io/connect/openid-connect-self-issued-v2-1_0.html)]
K. Yasuda, M. Jones, T. Lodderstedt, "Self-Issued OpenID Provider v2", September 2022, <https://openid.bitbucket.io/connect/openid-connect-self-issued-v2-1_0.html>

#### [[DIF.PresentationExchange](https://identity.foundation/presentation-exchange/spec/v2.0.0/)]
Buchner, D., Zundel, B., Riedel, M., and K. H. Duffy, "Presentation Exchange 2.0.0", , <https://identity.foundation/presentation-exchange/spec/v2.0.0/>. 