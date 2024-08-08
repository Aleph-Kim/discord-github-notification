# 📢 Discord Github Notification Action

This GitHub Action provides an easy way to send notifications via a Discord webhook when GitHub events occur.

## 🧺 Prerequisites

- `discord-webhook-url`: Discord webhook URL

---

## 🚀 Usage Example

1. Create a new YAML file in the `.github/workflows` directory of your GitHub repository (e.g., `discord-notification.yml`).    
Refer to the example below to write the content of the file.

```yml
name: Discord Notifications

on:
  pull_request: # Send Discord notifications for pull request events: opened, synchronize, reopened, closed
    types: [opened, synchronize, reopened, closed]
  create: # Send Discord notifications for all branch creation events
    branches:
      - '*'
  delete: # Send Discord notifications for all branch deletion events
    branches:
      - '*'
  issues: # Send Discord notifications for issue events: opened, closed
    types: [opened, closed]
  push: # Send Discord notifications for push events to the master branch
    branches:
      - master

jobs:
  discordNotification:
    runs-on: ubuntu-latest

    steps:
    - name: Discord Github Notification
      uses: Aleph-Kim/discord-github-notification@v1
      with:
        discord-webhook-url: ${{ secrets.DISCORD_WEBHOOK_URL }} # Discord webhook URL stored in secrets
```

For the `on event trigger` available in github action, please refer to the official [GitHub Actions document](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows).

---

## 💬 Input Parameters
1. `discord-webhook-url` (required): Enter the Discord webhook URL.
2. `language` (optional): Set the language of the notification message. The default is Korean. You can change it to English.

---

## 🛠 Setting Secrets
In your GitHub repository, go to `Settings` > `Secrets and variables` > `Actions`, click on `New repository secret`, and add the webhook URL with the name `DISCORD_WEBHOOK_URL`.

---

## 📚 Supported Events and Messages

### PR (Pull Request) Events
1. `opened`: When a PR is created
2. `synchronize`: When a PR is synchronized
3. `reopened`: When a PR is reopened
4. `closed`: When a PR is closed
5. `merged`: When a PR is merged

### Branch Events
1. `create`: When a branch is created
2. `delete`: When a branch is deleted

### Issue Events
1. `opened`: When an issue is created
2. `closed`: When an issue is closed

### Push Events
1. `push`: When commits are pushed

---

## 📄 Message Templates
Messages use the templates defined in the [messages.json file](https://github.com/Aleph-Kim/discord-github-notification/blob/master/messages.json).
