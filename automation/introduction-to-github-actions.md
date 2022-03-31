---
description: >-
  An introduction to GitHub actions and an example of a simple marketplace
  GitHub action.
---

# Introduction to GitHub Actions

### 1. Introduction

We will be covering the bare minimum to get you started. For a more in depth look at how GitHub actions work, have a look [here.](https://docs.github.com/en/actions) We will be using GitHub actions that are available on the [Marketplace.](https://github.com/marketplace?category=\&query=\&type=actions\&verification=) This marketplace will be your go to when you need to automate something.&#x20;

GitHub actions consists of 2 parts. Part 1 is written in JavaScript, we will not be editing this and this works in the background. Part 2 is the part written in Yaml. The Yaml is where we will be doing our editing.&#x20;

GitHub actions gets triggered by specific events. There are more than 90 events that can trigger a GitHub action. It is also possible to let more than one event trigger your GitHub action. For this introduction we will be using [this GitHub action](https://github.com/rjstone/discord-webhook-notify) that sends a Discord message whenever something happens to a GitHub Issue.

### 2.  Creating your GitHub Action Yml file

After you found the action you need on the Marketplace, you need to create the action Yaml file. You can start this by going to the root of your GitHub repo and creating a new file like so.

![Click Add file and then Create new file](../.gitbook/assets/Gitbook.png)

Next type the directory and name you want to save this file as. The directory for GitHub actions always needs to be "/.github/workflows/" like so...

![Be sure to end your filename with .yml](<../.gitbook/assets/Gitbook (1).png>)

Next copy the code from this codeblock into the body of your new yaml file.

```
name: Export issues
on:
  issues:
    types: [opened, edited, reopened, closed, deleted, labeled, unlabeled]
  #workflow_dispatch:
 # schedule:
    # run every 8 hours
  #  - cron:  '0 0,8,16 * * *'
jobs:
  issue:
    runs-on: ubuntu-latest
    name: discord
    steps:
     - name: Test Custom
       uses: rjstone/discord-webhook-notify@v1
       with:
         severity: info
         username: CustomUsername
         color: '#ff00aa'
         avatarUrl: https://github.githubassets.com/images/modules/logos_page/Octocat.png
         description: ${{ github.event.issue.number }}
         details: ${{ github.event.issue.body }}
         footer: This is a footer.
         text: ${{ github.event.issue.title }}
         webhookUrl: ${{ secrets.DISCORD_WEBHOOK }}

 
```

### 3. Editing your Yml file
