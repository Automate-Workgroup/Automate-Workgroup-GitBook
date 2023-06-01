---
description: >-
  A Javascript tool to assist and automate content for monthly reports based on
  Dework tasks
---

# Dework Performance Dashboard Automation

{% hint style="info" %}
Developed by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate
{% endhint %}

## Overview

The following tool was built with Vue.js . It makes use of Dework's API to get all task information from a specific workspace. This workspace id can be changed in the code and will be explained in this documentation. Once the task information is accessed it gets curated and processed to prepare it for charts and a chatGPT prompt. The dashboard has 4 charts and a button to create a chatGPT promt. If you click the button the prompt gets copied into your clipboard and you can then just paste it in chatGPT. There are 2 other stats... Total tasks done and documentation made. We will explore in the documentation how to change these stats.&#x20;

{% hint style="info" %}
Disclaimer\
This tool exposes your Discord Auth token, so anyone with access to the webpage is able to view your Discord Auth token. Don't share this tool around if you are using it. If you need to share it, you can integrate Discord login into the tool and let the data get accessed via logged in user tokens. To integrate Discord Login you can look into this documentation - [https://supabase.com/docs/guides/auth/social-login/auth-discord](https://supabase.com/docs/guides/auth/social-login/auth-discord)\

{% endhint %}

## Step 1

Clone this repo - [https://github.com/Andre-Diamond/dework-performance-dashboard](https://github.com/Andre-Diamond/dework-performance-dashboard)\
Set up your working environment - If you dont know how to - Follow this guide -&#x20;
