---
description: Circle KPI automation
---

# Circle KPIs



![](<../.gitbook/assets/2022-02-18 (1).png>)

## Reference example:&#x20;

{% embed url="https://cc-treasury.github.io/CircleKPIs" %}

{% embed url="https://github.com/CC-Treasury/CircleKPIs/blob/main/.github/workflows/main.yml" %}

## Code

```
jobs:
  create_issue:
    name: Create team sync issue
    runs-on: ubuntu-latest
    permissions:
      issues: write
```



