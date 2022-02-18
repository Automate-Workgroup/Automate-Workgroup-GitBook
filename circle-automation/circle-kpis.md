---
description: Circle KPI automation
---

# Circle KPIs

## Overview

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



## Charging / Budget

| Task                        | Hours | Charge |
| --------------------------- | ----- | ------ |
| development                 | 4     | 160    |
| testing                     | 2     | 80     |
| implemenation in production | 1     | 40     |
| Totals                      | 7     |        |





## Sign-Off

Where it is in production and who signed it off
