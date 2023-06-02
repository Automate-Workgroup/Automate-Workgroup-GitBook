---
description: A Guide to accessing your dework workspace id
---

# How to get your Dework Workspace id

{% hint style="info" %}
Written by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate
{% endhint %}

## Overview

Follow these steps to access your Dework Workspace id

## Step 1 - Inspect the page

To find out what your workspace id is go to the project board in Dework. Right click on the page and select inspect element - like so.

![](<../../.gitbook/assets/image (1) (1) (1) (1) (1).png>)

## Step 2 - Select Network and refresh

Next click on Network and refresh the page.

![](<../../.gitbook/assets/image (3) (1) (1) (1) (1).png>)

## Step 3 - Find and select GraphQL query

Select graphql?op=GetWorkspaceTasksQuery and look on the right for workspace id

![](<../../.gitbook/assets/image (2) (1) (1) (1).png>)

This string - "d815594d-0286-448f-97fe-b157ddb83c69" - is the workspace id for the project board in this example.

