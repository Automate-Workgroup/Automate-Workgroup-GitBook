---
description: A Guide to accessing your Discord Auth token in Dework
---

# How to get your Discord Auth token in Dework

{% hint style="info" %}
Written by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate
{% endhint %}

## Overview

Follow these steps to access your Discord Auth token

## Step 1 - Inspect the page

To find out what your workspace id is go to the project board in Dework. Right click on the page and select inspect element - like so.

![](<../../.gitbook/assets/image (1) (1) (1).png>)

## Step 2 - Select Network and refresh

Next click on Network and refresh the page.

![](<../../.gitbook/assets/image (3) (1) (1).png>)

## Step 3 - Find and select GraphQL query

Select graphql?op=GetWorkspaceTasksQuery and click on Headers. Look on the right and scroll down until you see authorization. You need to copy the entire string 'Bearer eyJhbGc......'

![](<../../.gitbook/assets/image (4).png>)

