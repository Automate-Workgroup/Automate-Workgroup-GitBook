---
description: Circle KPI automation
---

# Circle KPIs

{% hint style="info" %}
Developed by : André Diamond

Funded by - Fund 6 Distributed Auditability

Licence - [Creative Commons : Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
{% endhint %}

## Overview

This GitHub action tracks the status of issues on a Project Board. It produces and updates the necessary files in your gh\_pages branch to create a dashboard that can be customized in the yml file as well as the css file if you want to change the style of the dashboard. The documentation on this GitHub action can be found [here](https://ethomson.github.io/issue-dashboard/documentation/) if you want to dig a little deeper. You'll find that this dashboard is very customizable. You need to create a gh\_pages branch in your repo. You will need to copy the dashboard.js and dashboard.css files from [this directory](https://github.com/ethomson/issue-dashboard/tree/gh-pages/examples) into the gh\_pages branch where this action will publish to.

![Example Dashboard](<../../.gitbook/assets/Untitled (1) (1) (1).png>)

In the workflow directory in your main branch you will create the yml file for your Github action. You can copy the complete yml at the bottom of this page and go through the following steps to setup the action as you see fit.

1. Be sure to ad workflow dispatch so you can test your action. For this action you would also most likely set up a cron schedule. There are four actions happening here. First your repo gets checked, second the gh\_pages branch gets checked and a working directory gets set to 'out', third the dashboard gets generated and fourth the dashboard gets published. After checking out your repo the action looks for a branch called "gh\_pages". If it doesn't exist be sure to create it. Files in the gh\_pages branch get published to github pages by default. This GitHub action produces and updates the necessary files in this branch every time it runs.

![](../../.gitbook/assets/image\_2022-05-12\_155200551.png)

2\. Next up is generating the dashboard. There are 2 parts here. The config and the widgets. In the config section you set the output path and filename of the HTML file that gets generated. You can also set up variables as well as a function that you can use later in the action. Our first widget on this dashboard is a number widget. It starts with a title, description and then the type of widget. Each widget has its own "key value" pairs that you can change to display the data you want. The issue\_query field is used to pull the data from the issues in the repo. In the issue\_query field after the "repo:" you basically enter your organization or profile name and then after the "/" the name of the repo. After that you will notice "is:issue" and "created:>\{{ date("-30 days") \}}" This is to pull all issues that were created in the last 30 days. For more info on GitHub queries go to this [link](https://docs.github.com/en/search-github/searching-on-github/searching-issues-and-pull-requests). There are quite a few queries you can use in this field to find the data you are looking for.

![Config and widgets](../../.gitbook/assets/image\_2022-05-13\_075243514.png)

3\. The next widget we have is the graph widget. You will notice 2 new queries in the issue\_query field. "is:open" and "label: "General Voters". These queries are looking for OPEN issues with the label "General Voters". If you want to use the function you created in the config section to change the color of the graphs you can enter this into the color field instead ...

color: '\{{ userdata.color\_func(value) \}}'

![Graph Widget](../../.gitbook/assets/image\_2022-05-13\_082442201.png)

4\. The github.token authenticates the widgets to have access to the issues in the repo. The data gets generated and pushed to the gh\_pages branch into the "out" working directory that we mentioned in the top section where we checked out the gh\_pages section the first time. I haven't used all the features of the GitHub action. There is also table widgets and string widgets and a few other features. Again, be sure to check out the official documentation [here.](https://ethomson.github.io/issue-dashboard/documentation/)

![Publish Dashboard](../../.gitbook/assets/image\_2022-05-13\_083554921.png)

Below is the complete yml file for the GitHub action.

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

## Training

Funded by Distributed Auditability

[https://cardano.ideascale.com/c/idea/58679](https://cardano.ideascale.com/c/idea/58679)

## Charging / Budget (Example)

| Task                         | Hours | Charge @ $55 an hour |
| ---------------------------- | ----- | -------------------- |
| Development                  | 4     | $ 220                |
| Testing                      | 2     | $ 110                |
| Implementation in production | 1     | $ 55                 |
| Documentation                | 2     | 110                  |
| **Totals**                   | **7** | **$ 495**            |

## Sign-Off

Where it is in production

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
