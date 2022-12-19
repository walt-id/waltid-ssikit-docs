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

**Proofs** for the credentials are created in the linked data format, **ldp_vc**, as described by the _W3C data integrity_ specification [[VC_DATA_INTEGRITY](#vc_data_integrity)], using [[JSON-LD](#json_ld)] as the credential format and the _JCS Ed25519 Signature 2020_ [[JcsEd25519Signature2020](#jcsed25519signature2020)] signature type.

| Format  | Signature type |
|---          |---            |
| [ldp_vc](#vc_data_integrity)    | [JcsEd25519Signature2020](#jcsed25519signature2020) |

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



#### vp_token

### Same-device flow



### Cross-device flow



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

#### [[DIF.PresentationExchange](https://identity.foundation/presentation-exchange)]
Buchner, D., Zundel, B., Riedel, M., and K. H. Duffy, "Presentation Exchange 2.0.0", , <https://identity.foundation/presentation-exchange>. 