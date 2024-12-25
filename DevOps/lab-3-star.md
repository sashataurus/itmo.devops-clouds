# Отчёт по лабораторной работе по DevOps №3⭐
## Содержание:
- [Doppler](#doppler)

## Doppler
Мы выбрали облачную платформу Doppler, которая здорово помогла нам управлять секретами. В ней мы создали проект, который синхронизировали с гитхабом:

![image_2024-12-25_02-07-01](https://github.com/user-attachments/assets/30f6b5dc-8222-41b3-af93-6c4aa752102d)

Затем здесь создаем секретик:

![image_2024-12-25_02-10-11](https://github.com/user-attachments/assets/8783cbbe-9959-4aaa-b36e-ce76d5f3dbc1)
(кстати, еще один секретик в том, что мы в штатах🤫🤫🤫)

Дальше создаем токен, чтобы у пайплайна появился доступ к Doppler:

![image_2024-12-25_02-12-51](https://github.com/user-attachments/assets/f1cc958c-f29b-4688-b09c-81f6a694ffb3)

Затем идем в гитхаб, проверяем, чтобы наши секреты там появились, и добавляем токен как секрет:

![image](https://github.com/user-attachments/assets/65d55f18-9de2-4011-bd06-daef11c866ce)

Дальше нам надо было написать большой могучий код CI/CD файла:

```
name: secrets

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-22.04
    steps:
      - name: Check out
        uses: actions/checkout@v3
      - name: Install Doppler CLI
        uses: dopplerhq/cli-action@v3
      - name: Upload Secrets
        run: |
          doppler secrets upload --project "$DOPPLER_PROJECT" --config "$DOPPLER_CONFIG" --silent <(echo "$GITHUB_SECRETS" |
          jq 'del(.github_token, .DOPPLER_TOKEN, .DOPPLER_PROJECT, .DOPPLER_CONFIG) |
          with_entries( .key |= ascii_upcase )')
        env:
          DOPPLER_TOKEN: ${{ secrets.DOPPLER_TOKEN }}
          DOPPLER_PROJECT: ${{ secrets.DOPPLER_PROJECT }}
          DOPPLER_CONFIG: ${{ secrets.DOPPLER_CONFIG }}
          GITHUB_SECRETS: ${{ toJson(secrets) }}
      - name: Install dependencies
        run: npm install
      - name: Build app
        run: npm run build
      - name: Deploy is executable
        run: chmod +x ./deploy.sh
      - name: Deploy app
        env:
          DEPLOY_PATH: ${{ secrets.SECRET_DEPLOY }}
        run: ./deploy.sh $DEPLOY_PATH
```

