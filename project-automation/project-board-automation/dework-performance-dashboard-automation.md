---
description: >-
  A Javascript tool to assist and automate content for monthly reports based on
  Dework tasks
---

# Dework Performance Dashboard Automation

{% hint style="info" %}
Developed by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate

Licence - [Creative Commons : Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
{% endhint %}

Live demo

{% embed url="https://dework-performance-dashboard.netlify.app" %}

## Overview

The following tool was built with Vue.js . It makes use of Dework's API to get all task information from a specific workspace. This workspace id can be changed in the code and will be explained in this documentation. Once the task information is accessed it gets curated and processed to prepare it for charts and a chatGPT prompt. The dashboard has 4 charts and a button to create a chatGPT promt. If you click the button the prompt gets copied into your clipboard and you can then just paste it in chatGPT. There are 2 other stats... Total tasks done and documentation made. We will explore in the documentation how to change these stats. The dework spaces used in this documentation can be found here - [https://app.dework.xyz/test-157/main-project-2951](https://app.dework.xyz/test-157/main-project-2951). The tasks on the bounty boards have links to github commits if you want to dive deeper into some of the changes made to prep the code for this documentation.&#x20;

{% hint style="info" %}
Disclaimer\
This tool exposes your Discord Auth token, so anyone with access to the webpage is able to view your Discord Auth token. Don't share this tool around if you are using it. If you need to share it, you can integrate Discord login into the tool and let the data get accessed via logged in user tokens. To integrate Discord Login you can look into this documentation - [https://supabase.com/docs/guides/auth/social-login/auth-discord](https://supabase.com/docs/guides/auth/social-login/auth-discord)\

{% endhint %}

## Step 1 - Fork Repo

Fork this repo - [https://github.com/Andre-Diamond/dework-performance-dashboard](https://github.com/Andre-Diamond/dework-performance-dashboard)\
and set up your working environment - If you dont know how to - Follow this guide&#x20;

{% content-ref url="../general-introduction/how-to-fork-a-github-repo.md" %}
[how-to-fork-a-github-repo.md](../general-introduction/how-to-fork-a-github-repo.md)
{% endcontent-ref %}

## Step 2 - Find your Workspace ID

To find out what your workspace id is follow these guidelines&#x20;

{% content-ref url="../general-introduction/how-to-get-your-dework-workspace-id.md" %}
[how-to-get-your-dework-workspace-id.md](../general-introduction/how-to-get-your-dework-workspace-id.md)
{% endcontent-ref %}

## Step 3 - Change Workspace id in code

You can change the workspace and workgroup name in the code in the Home.vue file. Right at the top of the file you will find these 2 variables

![](<../../.gitbook/assets/image (3).png>)

## Step 4 - Deploy the webpage

Deploy the site using your favourite provider. If you have never deployed a site before follow these guidelines.

{% content-ref url="../general-introduction/how-to-deploy-to-netlify.md" %}
[how-to-deploy-to-netlify.md](../general-introduction/how-to-deploy-to-netlify.md)
{% endcontent-ref %}

## Step 5 - Extra things to note

You can also add some extra stats yourself.

![](<../../.gitbook/assets/image (11).png>)

Scroll down to line 167 in the Home.vue file. This will update the number for tasks that have the documentation tag. To use this remove the 2 slashes. If you dont have tasks with that label it wont run the page. To capture a different label change "documentation" in "everyTask.tags\["documentation"].tasks" to the label you want to capture. To avoid bugs, try using one word labels or if its 2 words connect them with a dash like so "tool-development". Do these label changes in dework and then make the changes to the code.

Scroll down to line 440 and change the text "Documentation made" to what ever label you want to capture.

![](<../../.gitbook/assets/image (24).png>)

## Charging

| Task               | Hours | Charge @ $55 an hour |
| ------------------ | ----- | -------------------- |
| Coding             | 17    | 55                   |
| Dework space setup | 1     | 55                   |
| Documentation      | 1     | 55                   |
|                    |       |                      |
| Totals             | 19    | 1045                 |

## Where is this in production

Governance Guild is using it to assist with monthly reports. Link to the repo below.

{% embed url="https://github.com/Governance-Services-Guild/Governance-Guild-Dework-Dashboard" %}

Unfortunately we can't share the link to the page yet as the Discord token is still exposed. As soon as its updated to a more sharable version we will share a link here. Here is a Screenshot of the tool in action.

![](<../../.gitbook/assets/image (29).png>)

