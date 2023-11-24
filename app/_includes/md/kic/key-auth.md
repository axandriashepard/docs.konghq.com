    {% comment %}This file is intentionally indented as it's included in an <ol> on multiple pages{% endcomment %}
    {% assign key = include.key | default: 'gav' %}
    {%- assign credName = include.credName | default: 'credential' %}
    ```bash
    kubectl create secret generic {{ credName }} \
      --from-literal=key={{ key }} \
      -o json --dry-run=client | \
      jq '.metadata.labels |= {"konghq.com/credentials": "key-auth"}' | \
      kubectl apply -f -
    ```
    The results should look like this:
    ```text
    secret/{{ credName }} created
   ```
