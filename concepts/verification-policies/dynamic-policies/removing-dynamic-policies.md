# Removing Dynamic Policies

#### Removing a Dynamic Policy

{% tabs %}
{% tab title="CLI" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/cli-command-line-interface.md) to exectute the command successfully.

```bash
ssikit vc policies remove -n MyCustomPolicy
```

* `-n, --name`: name of the dynamic policy to remove
{% endtab %}

{% tab title="REST" %}
Please refer to the [SSI-Kit setup section](../../../getting-started/rest-apis.md) to serve the API.

```bash
curl -X 'DELETE' \
  'http://127.0.0.1:7003/v1/delete/{{name}}' \
  -H 'accept: */*'

```

**Path parameters:**&#x20;

* `policyName`: _**\[string]**_ Name of the policy to delete
{% endtab %}
{% endtabs %}
