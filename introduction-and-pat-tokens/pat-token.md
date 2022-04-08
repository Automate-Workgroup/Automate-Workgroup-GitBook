---
description: Create Pat token and place in action secret
---

# How to create a PAT token (Personal Access Token)

## Overview

Personal Access Tokens are used to give GitHub Actions the power to do things that only the user can normally do. These tokens usually have an expiry date for safety reasons. Don't share your PAT token with anyone as it gives them direct access to your account.

&#x20;To create a personal access token click on the profile button in the top right and go to settings.

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

You can can call this PAT token in your GitHub actions like so

```
 with:
        token: ${{ secrets.PAT }} # Built in GITHUB_TOKEN permissions are too restrictive, so a personal access token is used here
```
