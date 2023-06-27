---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: true
  pagination:
    visible: true
---

# Dynamic/Custom Policies

SSI Kit supports custom policies, written in any of the supported policy engine languages. A dynamic policy can either be executed on the fly (if all required parameters are provided) or saved under a specific name for later reference in the verify command or REST API.

{% hint style="danger" %}
_Note: To use dynamic policies with Open Policy Agent, setup of the OPA Engine is required. Refer to the_ [_OPA Engine configuration_](../../../usage-examples/open-policy-agent/configure-opa-engine.md) _for more details._
{% endhint %}



### Getting Started

* [Create a dynamic policy ](creating-dynamic-policies.md)- Learn how to create a dynamic policy via CLI or REST
* [Use a dynamic policy](using-dynamic-policies.md) - Learn how to verify a VC using a dynamic policy via CLI or REST
* [Remove a dynamic policy](removing-dynamic-policies.md) - Learn how to remove a dynamic policy via CLI or REST
* [Data classes](dynamic-policies-or-data-classes.md) - Examine data classes used internally.
