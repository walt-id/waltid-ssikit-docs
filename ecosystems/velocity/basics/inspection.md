# Inspection

The verification process (inspection) is initiated by disclosure exchanges where the Relying Party requests credentials from Holder. These exchanges can be encoded in the following ways:
* deep links - a URI that matches the spec:
    * [velocity-network://inspect?request_uri=[REQUEST_URI]&inspectorDid=[INSPECTOR_DID]&vendorOriginContext=[VENDOR_ORIGIN_CONTEXT]](velocity-network://inspect?request_uri=[REQUEST_URI]&inspectorDid=[INSPECTOR_DID]&vendorOriginContext=[VENDOR_ORIGIN_CONTEXT])
* QR-codes - a visual representation of a deep link

Depending on the  use case, the Relying Party can request either:
* verified credentials
    * requires payment in tokens
    * returns the verification checks (policies) result
* unverified credentials:
    * requires no payment in tokens
    * can be verified later

## Verification policies
The verification checks performed against the credential are the following:
* UNTAMPERED
    * pass - hasn't been tampered
    * fail - has been tampered
    * voucher_reserve_exhausted - a voucher is required for verification
* TRUSTED_ISSUER
    * pass - issuer is trusted
    * fail - issuer is not a member of Velocity
    * self_signed - data attested by the Holder
    * voucher_reserve_exhausted - a voucher is required for verification
* UNREVOKED
    * pass - hasn't been revoked
    * has been revoked
    * voucher_reserve_exhausted - a voucher is required for verification
* UNEXPIRED
    * pass - hasn't expired
    * fail - has expired

More details on credential verification checks can be found at https://docs.velocitynetwork.foundation/docs/developers/developers-guide-disclosure-exchange#credential-verification-checks.

More on credential verification at https://docs.velocitynetwork.foundation/docs/developers/developers-guide-disclosure-exchange.