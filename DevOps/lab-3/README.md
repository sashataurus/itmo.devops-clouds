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
        working-directory: ./lab-3
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
        working-directory: ./lab-3
    steps: 
      - uses: actions/checkout@v3
      - run: |
          sudo apt-get update
          sudo apt-get install -y python3
      - run: |
          echo "hi, I'm a bad guy"
          python hi.py
```

Что же такого **"bad"** в этом файле?

1. Тег latest
```
    runs-on: ubuntu-latest
```   
В каждой лабе пишем про это! Тег latest всегда указывает на последнюю версию доступного образа Ubuntu, но если базовый образ обновится, то это может привести к нестабильности конфигурации. 
   
2. defaults несколько раз
```
    defaults:
      run:
        working-directory: ./lab-3
```
Это прописано 2 раза: и для теста, и для деплоя. Лучше вывести это отдельно, чтобы каждый раз не прописывать и не нагромождать код, а еще это удобно в тех случаях, если при смене проекта мы поменяем общую папку.
   
3. Нет шагов, куча-мала!
```
    steps:
      - uses: actions/checkout@v3
      - run: |
          sudo apt-get update
          sudo apt-get install -y python3
          pip install pytest
      - run: pytest test.py
```
Инструкция WORKDIR устанавливает рабочий каталог контейнера, а последующие команды наследуют привязку WORKDIR. Лучше сохранять все исходные файлы в отдельной папке в корневом каталоге, чем размещать их там же, где находятся системные файлы. Это снижает риск случайного повреждения образа при удалении.

## "Good" CI/CD
```
name: good ci/cd

defaults:
  run:
    working-directory: ./lab-3

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
Что стало **"good"**?

1. Определенный базовый образ
```
    runs-on: ubuntu-22.04
```
Мы изменили базовый образ на определенную версию (ubuntu-22.04), и теперь он не сможет обновиться самостоятельно, что не слоает нам зависимости пайплайна.
   
2. defaults вынесен 
```
defaults:
  run:
    working-directory: ./lab-3
```
Здесь мы избавились от ненужных повторений. Теперь defaults вынесен отдельно, и не нужно каждый раз его дублировать.
   
3. шаги
```
WORKDIR /lab-2
```
Добавили рабочий каталог, тем самым избавившись от случайных рисков и добавив ясности и прозрачности (куда класть файлы, чтобы они не потерялись).



---

мемы
