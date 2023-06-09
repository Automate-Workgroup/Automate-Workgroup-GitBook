---
description: A Guide to deploy your code to Netlify
---

# How to deploy to Neltify

{% hint style="info" %}
Written by : André Diamond

Funded by - Fund 8 Automate, Educate, Communicate

Licence - [Creative Commons : Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
{% endhint %}

## Overview

Follow these steps to deploy your code to Netlify

## Step 1 - Create Netlify account

You can login with GitHub as well. Below is the link to Netlify

{% embed url="https://app.netlify.com/" %}

## Step 2 - Add new site

On the home page click on "Add new site" and select "Import an existing project"

![](<../../.gitbook/assets/image (2).png>)

Next click on the GitHub button and follow the Authorization process

![](<../../.gitbook/assets/image (5) (1).png>)

Next Select the repo you want to add and then click on deploy site

![](<../../.gitbook/assets/image (8).png>)

## Step 3 - Adding your .env variables

After you added your site, go to site settings

![](../../.gitbook/assets/image.png)

Select "Environment variables" and click on "Add a variable" and select "Add a single variaable"

![](<../../.gitbook/assets/image (6).png>)

Now enter the key and value as they are saved in the .env file you created in your code and click "Create variable"

![](<../../.gitbook/assets/image (7).png>)

If you don't know where to find your .env variables or what they are, please have a look here.

{% content-ref url="how-to-get-your-discord-auth-token-in-dework-for-.env-file.md" %}
[how-to-get-your-discord-auth-token-in-dework-for-.env-file.md](how-to-get-your-discord-auth-token-in-dework-for-.env-file.md)
{% endcontent-ref %}

## Step 4 - Re-deploy site

Select Deploys in the left and click on "Trigger deploy" on the right and select "Clear cache and deploy site"

![](<../../.gitbook/assets/image (4).png>)

## Final thoughts

Now that your site is deployed, everytime you make changes to your code and commit to GitHub, Netlify will automatically re-deploy your site with the new code.

