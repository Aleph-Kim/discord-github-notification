# 📢 Discord Github Notification Action

이 GitHub Action은 GitHub 이벤트 발생 시 Discord 웹훅을 통해 알림을 전송하는 기능을 간편하게 제공합니다.

This GitHub Action provides an easy way to send notifications via a Discord webhook when GitHub events occur.    
Please refer to the link below for [English readme](README_EN.md).

## 🧺 준비물

- `discord-webhook-url`: Discord 웹훅 URL

---

## 🚀 사용 방법 예시

1. GitHub 리포지토리의 `.github/workflows` 디렉토리에 새로운 YAML 파일을 만듭니다(예: `discord-notification.yml`).    
아래 예제를 참고하여 파일 내용을 작성하세요.

```yml
name: Discord Notifications

on:
  pull_request: # pr - opened, synchronize, reopened, closed 이벤트 발생 시 discord 알림
    types: [opened, synchronize, reopened, closed]
  create: # branch - 모든 브런치 생성 시 discord 알림
    branches:
      - '*'
  delete: # branch - 모든 브런치 삭제 시 discord 알림
    branches:
      - '*'
  issues: # issues - opened, closed 이벤트 발생 시 discord 알림
    types: [opened, closed]
  push: # push - master 브랜치에 push 이벤트 발생 시 discord 알림
    branches:
      - master

jobs:
  discordNotification:
    runs-on: ubuntu-latest

    steps:
    - name: Discord Github Notification
      uses: Aleph-Kim/discord-github-notification@v1
      with:
        discord-webhook-url: ${{ secrets.DISCORD_WEBHOOK_URL }} # secret key에 저장한 discord webhook url
```

github action에서 사용 가능한 `on 이벤트 트리거`에 대해서는 [GitHub Actions 공식 문서](https://docs.github.com/ko/actions/writing-workflows/choosing-when-your-workflow-runs/events-that-trigger-workflows)를 참고해주세요.

---

## 💬 입력 파라미터
1. `discord-webhook-url` (필수): Discord 웹훅 URL을 입력합니다.
2. `language` (선택): 알림 메시지 언어를 설정합니다. 기본값은 korean입니다. english로 변경 가능합니다.

---

## 🛠 secrets 설정
GitHub 리포지토리의 `Settings` > `Secrets and variables` > `Actions`에서 `New repository secret`을 클릭하고 `DISCORD_WEBHOOK_URL` 이름으로 웹훅 URL을 추가합니다.

---

## 📚 지원 이벤트 및 메시지

### PR (Pull Request) 이벤트
1. `opened`: PR이 생성되었을 때
2. `synchronize`: PR이 동기화되었을 때
3. `reopened`: PR이 다시 열렸을 때
4. `closed`: PR이 닫혔을 때
5. `merged`: PR이 병합되었을 때

### 브랜치 이벤트
1. `create`: 브랜치가 생성되었을 때
2. `delete`: 브랜치가 삭제되었을 때

### 이슈 이벤트
1. `opened`: 이슈가 생성되었을 때
2. `closed`: 이슈가 닫혔을 때

### 푸시 이벤트
1. `push`: 커밋이 푸시되었을 때

---

## 📄 메시지 템플릿
메시지는 [messages.json 파일](https://github.com/Aleph-Kim/discord-github-notification/blob/master/messages.json)에 정의된 템플릿을 사용합니다.