# project-flow-close-issue-on-pr-merge

## 개요

이 액션은 PR이 머지될 때, 연관된 이슈를 Close 합니다.

---

## ✨ 기능 설명

- 브랜치 이름에서 이슈 번호를 추출합니다.
- 해당 이슈를 Close 합니다.

## 🧾 입력값

| 이름           | 필수 여부 | 기본값 | 설명                                     |
| -------------- | --------- | ------ | ---------------------------------------- |
| `github_token` | 예        | –      | GitHub Token (예: PAT 또는 GITHUB_TOKEN) |

---

## ⚠️ 사용 주의사항

### 브랜치 명에 이슈 번호가 포함되어야 합니다.

브랜치 이름에 이슈 번호가 포함되어 있어야 액션이 정상적으로 작동합니다.  
예: `feature/#12`, `bugfix/issue-34` 등.  
브랜치 명에 이슈 번호가 없으면 이 액션은 오류를 발생시킵니다.

### github.event.pull_request.merged == true 조건을 추가해주세요.

github pull request event로 closed를 사용합니다. 이 때 머지로 인한 closed인지 단순 close인지 구분이 되지 않을 수 있습니다. 그래서 명확히 머지가 될 때 액션을 실행하기 위해서 아래 예시처럼 if문을 추가해주세요.

---

## 🔁 사용 예시

```yaml
on:
  pull_request:
    types: [closed]

jobs:
  close-issue:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Run Close Issue on PR Merge
        uses: jinhokim98/project-flow-close-issue-on-pr-merge@v1
        with:
          github_token: ${{ secrets.SECRET_GITHUB_TOKEN }}
```

## Overview

This action closes the related issue when a pull request is merged.

---

## ✨ Features

- Extracts the issue number from the branch name.
- Closes the related issue when the PR is merged.

## 🧾 Inputs

| Name           | Required | Default | Description                              |
| -------------- | -------- | ------- | ---------------------------------------- |
| `github_token` | ✅ Yes   | –       | GitHub Token (e.g., PAT or GITHUB_TOKEN) |

---

## ⚠️ Usage Notes

### Branch Name Must Contain Issue Number

The branch name must contain the issue number for the action to work properly.  
For example: `feature/#12`, `bugfix/issue-34`, etc.  
If the branch name does not include an issue number, this action will throw an error.

### Add `github.event.pull_request.merged == true` Condition

The GitHub Pull Request event uses `closed`, which could be triggered by either a manual close or a merge. To ensure the action only runs when a PR is merged, you need to add the following condition:

```yaml
if: github.event.pull_request.merged == true
```

🔁 Usage Example

```yaml
on:
  pull_request:
    types: [closed]

jobs:
  close-issue:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Run Close Issue on PR Merge
        uses: jinhokim98/project-flow-close-issue-on-pr-merge@v1
        with:
          github_token: ${{ secrets.SECRET_GITHUB_TOKEN }}
```
