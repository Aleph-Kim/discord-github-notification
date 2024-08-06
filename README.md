# Discord Github Notification
GitHub Action Marketplace Action to Allow Discord to Receive GitHub Notifications

## Inputs

- `discord-webhook-url`: The Discord webhook URL.

## Example usage

1. Create a new workflow file in your repository (e.g., `.github/workflows/pr-notify.yml`).

```yaml
name: PR Notification

on:
  pull_request:
    types: [opened, synchronize, reopened]

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Send Discord Notification
        uses: owner/discord-pr-notifier@v1.0.0
        with:
          discord-webhook-url: ${{ secrets.DISCORD_WEBHOOK_URL }}
