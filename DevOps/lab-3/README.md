# Отчёт по лабораторной работе по DevOps №3
## Содержание:
- ["Bad" CI/CD](#bad-ci/cd)
- ["Good" CI/CD](#good-ci/cd)

## "Bad" CI/CD
```
name: bad ci/cd

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./DevOps/lab-3
    steps:
      - uses: actions/checkout@v3
      - run: |
          sudo apt-get update
          sudo apt-get install -y python3
          pip install pytest
      - run: pytest test.py

  deploy:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./DevOps/lab-3
    steps: 
      - uses: actions/checkout@v3
      - run: |
          sudo apt-get update
          sudo apt-get install -y python3
      - run: |
          echo "hi, I'm a bad guy"
          python hi.py
```
### Запуск :rocket:
![image](https://github.com/user-attachments/assets/e245b6a6-aa8b-4cf7-acc0-54e666749e52)
![image](https://github.com/user-attachments/assets/fc20138d-ce5c-4eb2-8aaf-8c8659affcb5)
![image](https://github.com/user-attachments/assets/3711ec44-b87b-491e-9b3e-db871ee1731a)


Что же такого **"bad"** в этом файле?

**1. Тег latest**
```
    runs-on: ubuntu-latest
```   
В каждой лабе пишем про это! Тег latest всегда указывает на последнюю версию доступного образа Ubuntu, но если базовый образ обновится, то это может привести к нестабильности конфигурации. 
   
**2. defaults несколько раз**
```
    defaults:
      run:
        working-directory: ./DevOps/lab-3
```
Это прописано 2 раза: и для теста, и для деплоя. Лучше вывести defaults отдельно, чтобы каждый раз не прописывать и не нагромождать код, а еще это удобно в тех случаях, если при смене проекта мы поменяем общую папку.
   
**3. Нет имен шагов, куча-мала!**
```
    steps:
      - uses: actions/checkout@v3
      - run: |
          sudo apt-get update
          sudo apt-get install -y python3
          pip install pytest
      - run: pytest test.py
```
Без названий шагов код становится не очень читабельным и не всегда сразу понятно о чем конкретный шаг, всё смешивается. 

**4. Отсутствие needs: test**

Без данной строчки в деплое он будет выполняться параллельно с тестом. Нам нужна зависимость и четкая последовательность.

**5. Установка Python через install**
```
          sudo apt-get install -y python3
```
Вообще это более-менее норм, но в "хороших" практиках мы нашли способ получше)

## "Good" CI/CD
```
name: good ci/cd

defaults:
  run:
    working-directory: ./DevOps/lab-3

on:
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-22.04
    steps: 
      - name: Check out
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.10'
  
      - name: Install pytest
        run: pip install pytest
          
      - name: Run Test
        run: pytest test.py
          
  deploy:
    needs: test
    runs-on: ubuntu-22.04
    steps:
      - name: Check out
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.10'

      - name: Deploy
        run: |
              echo "hi, I'm a good guy"
              python hi.py
```
### Запуск :rocket:
![image](https://github.com/user-attachments/assets/9e7bb28d-9ca2-47e1-8343-5c1d4c0021c6)
![image](https://github.com/user-attachments/assets/585aa468-c113-4107-bc54-6b7174d6b884)
![image](https://github.com/user-attachments/assets/588f2189-68f0-408e-b9b9-d37cce512197)


Что стало **"good"**?

**1. Определенный базовый образ**
```
    runs-on: ubuntu-22.04
```
Мы изменили базовый образ на определенную версию (ubuntu-22.04), и теперь он не сможет обновиться самостоятельно, что не сломет нам зависимости пайплайна.
   
**2. defaults вынесен**
```
defaults:
  run:
    working-directory: ./DevOps/lab-3
```
Здесь мы избавились от ненужных повторений. Теперь defaults вынесен отдельно, и не нужно каждый раз его дублировать.
   
**3. Добавлены имена шагов**
```
    steps:
      - name: Check out
        uses: actions/checkout@v3
```
Теперь для каждого шага прописано свое имя, что повышает читабельность кода и визуально разделяет шаги друг от друга.

**4. Добавление needs: test**
```
  deploy:
    needs: test
```
С добавлением данной строки появилась зависимость деплоя от теста, и теперь они выполняются поочередно. Мы создали четкую последовательность.

**5. Установка Python через actions**
```
        uses: actions/setup-python@v3
```
Данный способ (setup-python) обеспечивает единообразное поведение в разных раннерах и разных версиях Python, а еще он устанавливается на разные ОС. Поэтому он лучше, чем старый способ через install.

---

мемы
