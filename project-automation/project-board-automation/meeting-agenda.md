---
description: Circle KPI automation
---

# Meeting Agenda Action

## Overview

This GitHub action looks for an open issue with the label "Meeting". It copies the body of the issue and closes the issue. It then creates a new issue with the same body as the old issue, but with an updated title. It uses Cron to have the issues ready for scheduled dates.



## Code

```
#
# First responder duty, powered by imjohnbo/issue-bot
#
name: First Responder
on:
  workflow_dispatch:
  schedule:
  # 22h00 UTC Tue and Sat – https://crontab.guru
  - cron: 0 22 * * 2,6
env: 
  Org: "treasuryguild" 
  Repo: "Treasury-Advisory-Service"
  Labels: "Meeting"
  
jobs:
  first_responder:
    name: New responder duty
    runs-on: ubuntu-latest
    steps:
    
    - name: Find the last open report issue
      id: last-issue
      uses: micalevisk/last-issue-action@v2
      with:
        state: open
        # Find the last updated open issue that has these labels:
        labels: |
          ${{ env.Labels }}
          
    - name: Set env data
      id: propdata
      run: |
        echo "::set-output name=data::$(curl -s https://api.github.com/repos/${{ env.Org }}/${{ env.Repo }}/issues/${{ steps.last-issue.outputs.issue-number }} | jq '.body' | sed 's/\"//g')"
    
    - name: Set env body
      run: |
        echo "iBody=${{ steps.propdata.outputs.data }}" >> "$GITHUB_ENV"
    - name: Get template
      uses: imjohnbo/extract-issue-template-fields@v1
      id: extract
      with:
        path: .github/ISSUE_TEMPLATE/first_responder.md # assignees, labels, and title defined in issue template header
      env: 
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        
    - name: Prepare issue Message
      id: issue-message-creator
      run: |
        text="${{ env.iBody }}"
        text="${text//'%'/%25}"
        text="${text//'\n'/%0A}"
        text="${text//'\r'/%0D}"
        echo "::set-output name=value::$text"
    # Generates and pins new first responder issue, closes previous, writes linking comments, assigns to next person in line, adds to organization project number 550, column name "Duties", milestone number 10
    - name: Todays date
      run: echo "TODAY=$(date -d '2 days' '+ %A, %dth %B, %Y')" >> $GITHUB_ENV
    - name: New first responder issue
      uses: imjohnbo/issue-bot@v3
      with:
        token: ${{ secrets.PAT }} # Built in GITHUB_TOKEN permissions are too restrictive, so a personal access token is used here
        assignees: ${{ steps.extract.outputs.assignees }}
        labels: ${{ steps.extract.outputs.labels }}
        title: Treasury Advisory Service Meeting - ${{ env.TODAY }}
        body: ${{ steps.issue-message-creator.outputs.value }} 
          
        project: 1  # The project-number from organization project https://github.com/orgs/org/projects/project-number
        pinned: false
        close-previous: true
        linked-comments: true
```

## Training

Funded by Automate Educate Communicate

[https://cardano.ideascale.com/c/idea/368678](https://cardano.ideascale.com/c/idea/368678)

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
