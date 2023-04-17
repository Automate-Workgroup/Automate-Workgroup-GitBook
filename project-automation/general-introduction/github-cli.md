---
description: GitHub Command Line Interface
---

# GitHub CLI

## GitHub CLI

For documentation on the GitHub Command Line Interface see here [https://cli.github.com/](https://cli.github.com/)

<figure><img src="../../.gitbook/assets/Screenshot from 2023-04-09 17-09-46.png" alt=""><figcaption></figcaption></figure>

### Clone repo

<figure><img src="../../.gitbook/assets/Screenshot from 2023-04-09 17-48-56.png" alt=""><figcaption></figcaption></figure>

### List Issues in repo

<figure><img src="../../.gitbook/assets/Screenshot from 2023-04-09 17-57-40.png" alt=""><figcaption></figcaption></figure>

### Export issues to a csv file

`gh issue list --limit 1000 --state all | tr ',' ' ' | tr '\t' ',' > issues.csv`

### Extending GitHub CLI with hub

**hub** is _an extension to command-line git_ that helps you do everyday GitHub tasks without ever leaving the terminal.

{% embed url="https://hub.github.com/" %}
