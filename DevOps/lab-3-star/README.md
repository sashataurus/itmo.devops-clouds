# Отчёт по лабораторной работе по DevOps №3⭐
## Содержание:
- [Doppler](#doppler)
- [Запуск](#запуск)
- [Ответы на вопросы](#ответы-на-вопросы)

## Doppler
Мы выбрали облачную платформу Doppler, которая здорово помогла нам управлять секретами. В ней мы создали проект, который синхронизировали с гитхабом:

![image_2024-12-25_02-07-01](https://github.com/user-attachments/assets/30f6b5dc-8222-41b3-af93-6c4aa752102d)

Затем здесь создаем секретик:

![image_2024-12-25_02-10-11](https://github.com/user-attachments/assets/8783cbbe-9959-4aaa-b36e-ce76d5f3dbc1)
(кстати, еще один секретик в том, что мы в штатах :eagle::eagle::eagle:)

Дальше создаем токен, чтобы у пайплайна появился доступ к Doppler:

![image_2024-12-25_02-12-51](https://github.com/user-attachments/assets/f1cc958c-f29b-4688-b09c-81f6a694ffb3)

Затем идем в гитхаб, проверяем, чтобы наши секреты там появились, и добавляем токен как секрет:

![image](https://github.com/user-attachments/assets/65d55f18-9de2-4011-bd06-daef11c866ce)

Дальше нам надо было написать большой могучий код CI/CD файла:

```
name: secrets

defaults:
  run:
    working-directory: ./DevOps/lab-3-star
    
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

Также, чтобы всё работало, нам пришлось покорёжиться. Понадобилось сделать файлики package.json и deploy.sh.

## Запуск🚀:

И вауля! Когда мы увидели галочку, эмоция была одна - слава богу :pray:

![image](https://github.com/user-attachments/assets/72385579-e1cd-434c-9ec2-aa49d1a719b6)
![image](https://github.com/user-attachments/assets/8f31c044-ffc0-4192-9af2-9bd6efe46f05)

## Ответы на вопросы

### Почему наш способ "красивый"?
Через Doppler очень легко подключиться к гитхабу и пайплайнам. Удобно, что все секреты хранятся в одном месте, мы можем легко их обновлять, а также менять их срок действия, не меняя при этом код. Также плюсом является автоматическое шифрование и доступ через токен.

### Почему хранение секретов в CI/CD переменных репозитория не является хорошей практикой?
Все, у кого есть доступ к этому репозиторию, могут менять в нем что-то, что легко может привести к утечкам. Также при необходимости изменений могут возникнуть трудности с обновлением секретов, а если увеличится масштаб проекта, то работать с секретами станет сложнее.

---

Мы, когда в 20 раз засветился красный крестик вместо зеленой галочки:

![Снимок экрана 2024-12-25 045943](https://github.com/user-attachments/assets/d7295afc-ceba-4061-b528-82263f7ea3f0)

