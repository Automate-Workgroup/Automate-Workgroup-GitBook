---
description: >-
  A Guide to accessing your Discord Auth token in Dework to save in your .env
  file after you cloned a GitHub project.
---

# How to get your Discord Auth token in Dework for .env file

{% hint style="info" %}
Written by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate

Licence - [Creative Commons : Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
{% endhint %}

## Overview

Follow these steps to access your Discord Auth token

## Step 1 - Inspect the page

To find out what your workspace id is go to the project board in Dework. Right click on the page and select inspect element - like so.

![](<../../.gitbook/assets/image (1) (1) (1) (1) (1).png>)

## Step 2 - Select Network and refresh

Next click on Network and refresh the page.

![](<../../.gitbook/assets/image (3) (1) (1) (1) (1).png>)

## Step 3 - Find and select GraphQL query

Select graphql?op=GetWorkspaceTasksQuery and click on Headers. Look on the right and scroll down until you see authorization. You need to copy the entire string 'Bearer eyJhbGc......'

![](<../../.gitbook/assets/image (4) (1) (1).png>)

## Step 4 - Create .env file and add Auth token

&#x20;In the root folder of your code create a .env file and save your Auth token as follows.

![](<../../.gitbook/assets/image (2) (1).png>)

Here is an example of how the Auth token is used in the code. Notice how we use the name we assigned to the token in the .env file. In this case we use "import.meta.env.VITE\_DEWORK\_AUTH" to call the environment variable.

![](<../../.gitbook/assets/image (3).png>)

## !!! Important !!!&#x20;

One more very important thing to do is to update your .gitignore file. You need to add ".env" on a new line. This will exclude your .env file when commiting to GitHub. This is very important as you don't want to share your Auth tokens with the world. These tokens basically give people access to your account. Here is an example of the ".env" added to the .gitignore file.

![](<../../.gitbook/assets/image (6) (1).png>)

You will also need to add your Discord Auth tokens on Netlify when you deploy your site. You can see how to do that in the link below.

{% content-ref url="how-to-deploy-to-netlify.md" %}
[how-to-deploy-to-netlify.md](how-to-deploy-to-netlify.md)
{% endcontent-ref %}

## Closing

That covers everything needed to find and use your Discord Auth token. Below you will find 2 projects that makes use of this Auth token.

{% content-ref url="../project-board-automation/dework-performance-dashboard-automation.md" %}
[dework-performance-dashboard-automation.md](../project-board-automation/dework-performance-dashboard-automation.md)
{% endcontent-ref %}

{% content-ref url="../project-board-automation/dework-csv-exporter-automation.md" %}
[dework-csv-exporter-automation.md](../project-board-automation/dework-csv-exporter-automation.md)
{% endcontent-ref %}
