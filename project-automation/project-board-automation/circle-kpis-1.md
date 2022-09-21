---
description: Circle KPI automation
---

# Add label to newly created issues

## Overview

## Code

```
name: ada-due-label

on:
  issues:
    types: [opened]

jobs:
  automate-issues-labels:
    runs-on: ubuntu-latest
    steps:
      - name: initial labeling
        uses: andymckay/labeler@master
        with:
          add-labels: "ADA Due"
```

## Training

Funded by Automate Communicate Educate

[https://cardano.ideascale.com/c/idea/398131](https://cardano.ideascale.com/c/idea/398131)

## Charging / Budget (Example)

| Task                         | Hours | Charge @ $55 an hour |
| ---------------------------- | ----- | -------------------- |
| Development                  | 4     | $ 220                |
| Testing                      | 2     | $ 110                |
| Implementation in production | 1     | $ 55                 |
| Documentation                | 2     | 110                  |
| **Totals**                   | **7** | **$ 495**            |

## Sign-Off

Where it is in production and who signed it off

{% embed url="https://cc-treasury.github.io/CircleKPIs" %}
Circle KPIs
{% endembed %}

{% embed url="https://github.com/CC-Treasury/CircleKPIs/blob/main/.github/workflows/main.yml" %}
Yml file of GitHub action
{% endembed %}

{% embed url="https://github.com/Catalyst-Circle/Catalyst-Prioritized-Problems/issues" %}
GitHub Issues
{% endembed %}

{% embed url="https://github.com/CC-Treasury/CircleKPIs/tree/gh-pages" %}
gh\_pages branch
{% endembed %}
