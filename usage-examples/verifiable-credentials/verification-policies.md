# Verification Policies

\
For verification of verifiable credentials, the SSI-Kit offers a wide range of predefined static and parameterized verification policies, which are ready-to-use and are designed for common use cases. For more complex verification, the creation of custom policies using a policy execution engine such as the Open Policy Agent can be used.

### Static Verification Policies

Predefined and covering a variety of common use cases, enabling developers to verify credentials without having to dive into dynamic or custom policy creation and scripting languages. Some of these policies include `SignaturePolicy`, `JsonSchemaPolicy`, `ValidFromBeforePolicy`, `ExpirationDateAfterPolicy`, and more.&#x20;

[Learn more about Static Verification Policies.](../../concepts/verification-policies/static-policies.md)

### Parameterized Verification Policies

Parameterized policies are a type of policy that requires certain parameters or arguments for their execution.&#x20;

[Learn more about Parameterized Verification Polices.](../../concepts/verification-policies/parameterized-policies.md)

### Dynamic Verification Policies

Dynamic policies offer a more customized approach to credential verification, enabling even the most complex of use-cases. Policies can be created based on different policy engine languages.

[Learn more about Dynamic Verification Policies.](../../concepts/verification-policies/dynamic-policies/)

