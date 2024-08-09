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
      uses: Aleph-Kim/discord-github-notification@v1.2.0
      with:
        discord-webhook-url: ${{ secrets.DISCORD_WEBHOOK_URL }} # Discord webhook URL stored in secrets
        language: 'english' # Set language to English (default: Korean)
        custom: true # optional
```

For the `on event trigger` available in github action, please refer to the official [GitHub Actions document](https://docs.github.com/en/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows).

---

## 💬 Input Parameters
1. `discord-webhook-url` (required): Enter the Discord webhook URL.
2. `language` (optional): Set the language of the notification message. The default is Korean. You can change it to English.
3. `custom` (optional): Uses a [custom message template](#custom-message-template). It reads the `.github/workflows/messages.json file` from the user's repository.

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

## 📄 Message Template
By default, the message template is defined in the [messages.json file](https://github.com/Aleph-Kim/discord-github-notification/blob/master/messages.json).

---

## Custom Message Template

### Activation Method
Set the `custom parameter` to `true` to read the `.github/workflows/messages.json file` from the user's repository.

### Structure
1. Language key
    1. `korean`
    2. `english`
2. Event-specific message keys
    1. `PR_OPENED` - Event triggered when a new pull request is created
    2. `PR_SYNCHRONIZE` - Event triggered when a pull request is updated (e.g., new commits added)
    3. `PR_REOPENED` - Event triggered when a closed pull request is reopened
    4. `PR_CLOSED` - Event triggered when a pull request is closed
    5. `PR_MERGED` - Event triggered when a pull request is merged
    6. `BRANCH_CREATE` - Event triggered when a new branch is created
    7. `BRANCH_DELETE` - Event triggered when a branch is deleted
    8. `ISSUE_OPENED` - Event triggered when a new issue is created
    9. `ISSUE_CLOSED` - Event triggered when an issue is closed
    10. `PUSH` - Event triggered when new commits are pushed

### Message Format
The following variables must be included in the message:
1. `{title}` - The title of the event (PR, issue, branch, etc.)
2. `{user}` - The name of the user who triggered the event
3. `{url}` - The link related to the event

#### Custom Message Template Example

Ex. A custom message template for sending notifications in english only when a pull request is created or a push event occurs

```json
{
    "english": {
        "PR_OPENED": "NEW PR CREATEDDD!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! {title}\n CREATED BY!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!! {user}\n PR URL!!!!!!!!!!!!!!!!!!!!!!!!!!!! {url}",
        "PUSH": "There's another commit I don't want to read... \ncommit message: {title}\nthe greatest developer in human history: {user}\n{url}"
    },
}

```