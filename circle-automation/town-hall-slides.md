---
description: Town Hall Slides Automation
---

# Town Hall Slides

## Overview

This GitHub action pulls data from an issue template markdown file, creates an issue with that data and places the issue in the project board and column of your choice.

The complete code for this GitHub action can be found at the bottom of this page. You'll have to edit the following parts to make it work for your repository and align with what you are trying to achieve.

1. Below you can see an example of the issue template file. Note that the action won't work if the label field is empty. Also note the path this file is stored in.&#x20;

![Issue template](<../.gitbook/assets/Untitled (3) (1).png>)

Below is where you edit the path that points to your issue template file. Notice that you start the path from ".github/..."

```
    - name: Get template
      uses: imjohnbo/extract-issue-template-fields@v1
      id: extract
      with:   # below is the path to the template issue markdown file
        path: .github/ISSUE_TEMPLATE/town_hall_slides.md # assignees, labels, and title defined in issue template header
      env: 
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

2\. Next you need to identify the project number. Go to your project board and look at the URL bar in your browser. The last digit is your project number. Also note the name of the column you want the issue to reside in.

![](<../.gitbook/assets/Untitled (2) (1).png>)

At the bottom of the yaml file you'll notice the fields where you can edit  the project number and column name.

```
          - [ ] Prepare Town Hall slides for Wednesday
        project: 1  # The project-number from https://github.com/orgs/org/projects/project-number
        column: In progress
        pinned: false
        close-previous: true
        linked-comments: true
```

3\. The following fields that need editing is all the fields that has to do with time. When you want this issue to be created and what date you want displayed in the issue title. Below is the cron field, this determines when your GitHub action will run. To find out how to edit this field to get the timeslot you need, use this [link](https://crontab.guru/#0\_0\_\*\_\*\_6).

```
  schedule:
  # At 00:00 on Wednesday. – https://crontab.guru
  - cron: 0 0 * * 3   # cron sets the time the workflow gets activated
```

Next up is the date you want displayed in your Issue title. Line 2 creates an env variable "DAY" to use later in your workflow. Note that the '7 days' ads the number of days to todays date. So the result will be today +7 days. You can do some more reading on the  format here [https://python.plainenglish.io/manipulating-date-time-data-with-the-datetime-module-4ac93f9db1c3](https://python.plainenglish.io/manipulating-date-time-data-with-the-datetime-module-4ac93f9db1c3)

```
    - name: Issue date
      run: echo "DAY=$(date -d '7 days' '+ %A, %dth %B, %Y')" >> $GITHUB_ENV  # Create env variable "DAY" to use later in workflow
```

4\. Notice below how the "DAY" env variable gets used and the outputs from the imjohnbo/extract-issue-template-fields@v1 action. The token $\{{ secrets.PAT \}} is a secret you have to make yourself. The built in GITHUB\_TOKEN is not strong enough so you need to create a personal access token.

```
   with:
        token: ${{ secrets.PAT }} # Built in GITHUB_TOKEN permissions are too restrictive, so a personal access token is used here
        assignees: ${{ steps.extract.outputs.assignees }} # Extracts info from issue template markdown file
        labels: ${{ steps.extract.outputs.labels }}
        title: Town Hall Slides - ${{ env.DAY }}
        body: |
          ### Townhall slides - ${{ env.DAY }}
```

5\. To create a personal access token click on the profile button in the top right and go to settings.

![](<../.gitbook/assets/Untitled (8).png>)

Next click on the developer settings in the bottom left.

![](<../.gitbook/assets/Untitled (5).png>)

Click on Personal access tokens and then click on Generate new token. You'll be taken to this page where you need to select scopes.

![](<../.gitbook/assets/Untitled (7).png>)

After you click generate token you will get to this page. Copy the token code. Click on the blue squares next to the token code to copy.

![](<../.gitbook/assets/Untitled (4).png>)

Next up go to the repo settings.

![](<../.gitbook/assets/Untitled (6).png>)

Click on secrets and then on actions.

![](<../.gitbook/assets/Untitled (3).png>)

Click on New repository secret (top right), then on the next page paste the code you copied into the value field and type PAT into the Name field. Click Ad secret.

![](<../.gitbook/assets/Untitled (2).png>)

Your action is ready to test. You'll notice in the complete yaml file on line 6 there is a # before workflow\_dispatch:      &#x20;

Remove the # to manually run the action in GitHub actions. Indentation is very important in yaml so make sure the workflow\_dispatch: starts at the same indent as schedule:

Play around with the values and see what you can conjure up.

## Reference Example

[Project board with the Town Hall Issue](https://github.com/Catalyst-Circle/Catalyst-Circle-Coordination/projects/1)

[Automatically open/close issue for town hall slides on every Wednesday](https://github.com/Catalyst-Circle/Catalyst-Circle-Coordination/blob/main/.github/workflows/slides.yml)

## Code

This is the complete yaml file. Copy and edit the fields as shown above.

```
#
# Townhall Slides, powered by imjohnbo/issue-bot
# 
name: Townhall slides
on:
  # workflow_dispatch:    # use workflow_dispatch in the actions tab to test your workflows
  schedule:
  # At 00:00 on Wednesday. – https://crontab.guru
  - cron: 0 0 * * 3   # cron sets the time the workflow gets activated

jobs:
  town_hall_slides:
    name: Slides template
    runs-on: ubuntu-latest   
    steps:

    - name: Get template
      uses: imjohnbo/extract-issue-template-fields@v1
      id: extract
      with:   # below is the path to the template issue markdown file
        path: .github/ISSUE_TEMPLATE/town_hall_slides.md # assignees, labels, and title defined in issue template header
      env: 
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

    # Generates and pins new town hall slides issue, closes previous, writes linking comments, adds to project number 1, column name "In progress"
    - name: Issue date
      run: echo "DAY=$(date -d '7 days' '+ %A, %dth %B, %Y')" >> $GITHUB_ENV  # Create env variable "DAY" to use later in workflow
    - name: New Slide issue
      uses: imjohnbo/issue-bot@v3
      with:
        token: ${{ secrets.PAT }} # Built in GITHUB_TOKEN permissions are too restrictive, so a personal access token is used here
        assignees: ${{ steps.extract.outputs.assignees }} # Extracts info from issue template markdown file
        labels: ${{ steps.extract.outputs.labels }}
        title: Town Hall Slides - ${{ env.DAY }}
        body: |
          ### Townhall slides - ${{ env.DAY }}
          
          * Previous Town Hall - https://github.com//Catalyst-Circle/Catalyst-Circle-Coordination/issues/{{ previousIssueNumber }}
          * CC Admin meeting - 
          
          - [ ] Prepare Town Hall slides for Wednesday
        project: 1  # The project-number from https://github.com/orgs/org/projects/project-number
        column: In progress
        pinned: false
        close-previous: true
        linked-comments: true
```

## Training

Funded by Open Source Training

[https://cardano.ideascale.com/c/idea/368678](https://cardano.ideascale.com/c/idea/368678)

## Charging/Budget

| Task                         | Hours | Charge |
| ---------------------------- | ----: | ------ |
| Development                  |     2 | 80     |
| Testing                      |     4 | 160    |
| Implementation in production |     1 | 40     |
| Totals                       |     7 | 280    |

## Sign-off

Where it is in production:

{% embed url="https://github.com/Catalyst-Circle/Catalyst-Circle-Coordination/blob/main/.github/workflows/slides.yml" %}
Main Yaml file
{% endembed %}

{% embed url="https://github.com/Catalyst-Circle/Catalyst-Circle-Coordination/blob/main/.github/ISSUE_TEMPLATE/town_hall_slides.md" %}
Issue template file
{% endembed %}

{% embed url="https://github.com/Catalyst-Circle/Catalyst-Circle-Coordination/projects/1" %}
Project board where the issue resides
{% endembed %}

Signed off by:
