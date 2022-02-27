---
description: Circle KPI automation
---

# Circle KPIs

## Overview

![](<../.gitbook/assets/Untitled (1) (1) (1).png>)

## Reference example:&#x20;

{% embed url="https://cc-treasury.github.io/CircleKPIs" %}

{% embed url="https://github.com/CC-Treasury/CircleKPIs/blob/main/.github/workflows/main.yml" %}

## Code

```
name: Build Dashboard

#on:
#  workflow_dispatch:
on:
  schedule:
  - cron: 0 0 * * 6
jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Check out repository
      uses: actions/checkout@v2
    - name: Check out GitHub Pages branch
      uses: actions/checkout@v2
      with:
        ref: 'gh-pages'
        path: 'out'

    - name: 'Generate Dashboard'
      uses: ethomson/issue-dashboard@v1
      with:
        config: |
          title: 'Catalyst Prioritized Problems Dashboard'
          output:
            format: html
            filename: 'out/index.html'
          setup: |
            userdata.color_func = function(num) {
              if (num < 6) return 'green'
              if (num > 10) return 'red'
              return 'yellow'
            }
            userdata.num = 0
          sections:
          - title: 'Current Status'
            description: 'Current state of Issues'
            widgets:
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:issue created:>{{ date("-30 days") }}'
              title: 'Opened issues this month'
              color: 'red'
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:issue closed:>{{ date("-30 days") }}'
              title: 'Closed issues this month'
              color: 'green'
          - title: 'All time status'
            description: 'Total Issues opened and closed'
            widgets:
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:issue created:<{{ date("1 days") }}'
              title: 'Opened issues'
              color: 'red'
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:issue closed:<{{ date("1 days") }}'
              title: 'Closed issues'
              color: 'green'
          - title: 'Updated Issues'
            description: 'Total issues that received updates'
            widgets:
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue updated:>{{ date("-60 days") }} updated:<{{ date("-30 days") }}'
              title: 'Last month'
              color: 'yellow'
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue updated:>{{ date("-30 days") }}'
              title: 'This month'
              color: 'blue'
          - title: 'Issue comments'
            description: 'Total issues that received comments'
            widgets:
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue comments:>0 updated:>{{ date("-60 days") }} updated:<{{ date("-30 days") }}'
              title: 'Last month'
              color: 'yellow'
            - type: number
              issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue comments:>0 updated:>{{ date("-30 days") }}'
              title: 'This month'
              color: 'blue'
          - title: 'Circles'
            description: 'Issues per group (Some issues involve more than one group)'
            widgets:
            - type: graph
              title: 'Circle groups'
              elements:
              - title: 'General ADA Holders'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"General Voters" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'General ADA Holders (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"General Voters" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'Community Advisors'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Community Advisor" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'Community Advisors (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Community Advisor" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'Funded Proposers'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Funded Proposers" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'Funded Proposers (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Funded Proposers" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'Toolmakers and Maintainers'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Toolmaker and Maintainer" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'Toolmakers and Maintainers (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"Toolmaker and Maintainer" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'Stake Pool Operators'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"SPOs" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'Stake Pool Operators (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"SPOs" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'IOG'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"IOG" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'IOG (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"IOG" created:<{{ date("-30 days") }}'
                color: 'blue'
              - title: 'Cardano Foundation'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"CF" created:<{{ date("1 days") }}'
                color: 'green'
              - title: 'Cardano Foundation (Last Month)'
                issue_query: 'project:Catalyst-Circle/Catalyst-Prioritized-Problems/3 is:open is:issue label:"CF" created:<{{ date("-30 days") }}'
                color: 'blue'
                
        token: ${{ github.token }}

    - name: Publish Documentation
      run: |
        git add .
        git config user.name 'Dashboard User'
        git config user.email 'nobody@nowhere'
        git commit -m 'Documentation update' --allow-empty
        git push origin gh-pages
      working-directory: out
© 2022 GitHub, Inc.
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About

```



## Charging / Budget (Example)

| Task                         | Hours | Charge    |
| ---------------------------- | ----- | --------- |
| Development                  | 4     | $ 160     |
| Testing                      | 2     | $ 80      |
| Implementation in production | 1     | $ 40      |
| **Totals**                   | **7** | **$ 280** |





## Sign-Off

Where it is in production and who signed it off
