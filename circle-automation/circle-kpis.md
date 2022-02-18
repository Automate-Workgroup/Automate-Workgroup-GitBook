---
description: Circle KPI automation
---

# Circle KPIs



![](<../.gitbook/assets/2022-02-18 (1).png>)

Reference example:&#x20;

[https://cc-treasury.github.io/CircleKPIs/](https://cc-treasury.github.io/CircleKPIs/)&#x20;

{% embed url="https://github.com/CC-Treasury/CircleKPIs/blob/main/.github/workflows/main.yml" %}

```
jobs:
  create_issue:
    name: Create team sync issue
    runs-on: ubuntu-latest
    permissions:
      issues: write
```



