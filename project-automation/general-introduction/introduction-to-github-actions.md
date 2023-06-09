---
description: >-
  An introduction to GitHub actions and an example of a simple marketplace
  GitHub action.
---

# Introduction to GitHub Actions

{% hint style="info" %}
Written by : Andre

Funded by : F6  Distributed Auditability

Licence - [Creative Commons : Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
{% endhint %}

### 1. Introduction

We will be covering the bare minimum to get you started. For a more in depth look at how GitHub actions work, have a look [**here.**](https://docs.github.com/en/actions) We will be using GitHub actions that are available on the [Marketplace.](https://github.com/marketplace?category=\&query=\&type=actions\&verification=) This marketplace will be your go to when you need to automate something.

GitHub actions consists of 2 parts. Part 1 is written in JavaScript, we will not be editing this and this works in the background. Part 2 is the part written in Yaml. The Yaml is where we will be doing our editing.

GitHub actions gets triggered by specific events. There are more than 90 events that can trigger a GitHub action. It is also possible to let more than one event trigger your GitHub action. For this introduction we will be using [this GitHub action](https://github.com/rjstone/discord-webhook-notify) that sends a Discord message whenever something happens to a GitHub Issue.

### 2. Creating your GitHub Action Yml file

After you found the action you need on the Marketplace, you need to create the action Yaml file. You can start this by going to the root of your GitHub repo and creating a new file like so.

![Click Add file and then Create new file](<../../.gitbook/assets/Gitbook (1).png>)

Next type the following ".github/workflows/discord.yml" You'll notice as you type, every time you type a forward slash the colour of the text and the typefield changes. You can name your action anything you want, but the directory for GitHub actions always needs to be "/.github/workflows/" like so...

![Be sure to end your filename with .yml](<../../.gitbook/assets/Gitbook (2).png>)

Next copy the code from this codeblock into the body of your new yaml file.

```
name: Export issues   
on:                   
  issues:
    types: [opened, edited, reopened, closed, deleted, labeled, unlabeled]
 # workflow_dispatch:   
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

### 3. Yml file breakdown

* Name - Name of the action
* On - List of triggers that trigger the action
* Jobs - Jobs that run when action is triggered. More then one job can run per trigger and jobs can be dependent on other jobs to complete before they run.

#### 3.1 Triggers

For this action we will be using the "issues" trigger. Every time an issue is \[opened, edited, reopened, closed, deleted, labeled, unlabeled] the GitHub action will trigger. In the yml file there are other triggers as well, but they are inactive because of the # symbol. The # symbol turns anything after it on the line into a comment. Feel free to remove the # symbols to experiment with the other triggers. The "schedule" trigger uses [**cron**](https://crontab.guru/#0\_0\_\*\_\*\_6) to set a specific time for the action to run. To test the cron, remove the # in front of "schedule" and "cron". To run the action manually you can use "workflow\_dispatch". This is how you run the action manually....

![Notice that step 2 is the name of the action](<../../.gitbook/assets/Gitbook (3).png>)

![The name of the action](<../../.gitbook/assets/Gitbook (4) (1).png>)

#### 3.2 Jobs

You can run more than one job per action and some jobs can be set to only run after another job has completed. For this action we will only run one job.

![Change the values of the blue text under "with:" to experiment a bit](<../../.gitbook/assets/Gitbook (4).png>)

Under "steps:" you'll see "uses: rjstone/discord-webhook-notify@v1". You can access the repo of the action by typing the following URL... github.com/rjstone/discord-webhook-notify Be sure to read the documentation in the repo as well and to look at the test.yml in the workflows folder.

You can change the avatar of the discord message, the text in description, details, footer and text. For this example we are pulling data from the created issue that triggered the action. ex. "text: $\{{ github.event.issue.title \}}"

#### 3.3 GitHub Action secret and Discord Webhook

You will need to create a secret that stores your Discord Webhook. To find out how to create a secret, _skip past the PAT token section_ and have a look at the last section that covers secret creation [<mark style="color:blue;">**here**</mark>](pat-token.md)<mark style="color:blue;">**.**</mark>

To get your Discord Webhook code go to Server settings in Discord

![](<../../.gitbook/assets/Gitbook (5) (1).png>)

Then integrations and then View Webhooks.

![](<../../.gitbook/assets/Gitbook (6) (1) (1).png>)

Next up click New Webhook and then Copy Webhook URL.

![](<../../.gitbook/assets/Gitbook (7) (1).png>)

Go ahead and create a Github action secret and paste the Webhook URL in the secret.

## 4. Testing the action

Use workflow dispatch to test your Github action. Click on the issue name after you've run it.

![](<../../.gitbook/assets/Gitbook (7).png>)

Next click here

![](<../../.gitbook/assets/Gitbook (6) (1).png>)

You can expand these fields to have a look at the different steps the action goes through.

![](<../../.gitbook/assets/Gitbook (5).png>)

You will notice when your action runs into an error it will leave a message that tells you at which point it ran into an error.

If you didn't receive any errors, there will be a message in the Discord channel that is connected to the webhook you chose. Go ahead and create a GitHub issue and see if the action triggers and what the message looks like in Discord.
