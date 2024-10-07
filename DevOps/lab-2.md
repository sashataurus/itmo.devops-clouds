# Отчёт по лабораторной работе по DevOps №2
## Содержание:
- [Установка Docker на Ubuntu](#установка-docker-на-ubuntu)
- ["Bad" Dockerfile](#bad-dockerfile)
- ["Good" Dockerfile](#good-dockerfile)
- ["Bad Guys" в контейнерах](#bad-guys-в-контейнерах)

## Установка Docker на Ubuntu
Ниже описываем все шаги, как мы скачивали Docker:

`sudo apt update` - обновляем списки пакетов из репозиториев

`sudo apt install apt-transport-https ca-certificates curl software-properties-common` - установливаем пакеты, которые необходимы для работы пакетного менеджера apt по протоколу HTTPS

`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -` - добавляем GPG-ключ репозитория Docker

`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"` - добавляем репозиторий Docker

`sudo apt update` - ещё раз обновляем пакеты

`apt-cache policy docker-ce` - переключаемся в репозиторий Docker, чтобы его установить

`sudo apt install docker-ce` - устанавливаем Docker

`sudo systemctl status docker` - проверяем работоспособность программы

Всё хорошо!

![image_2024-10-06_18-24-22](https://github.com/user-attachments/assets/0efa1b27-76cd-4ab5-8255-02d8abf6e7c2)

`docker run hello-world` - проверяем доступ к образам Docker

С нами поздоровались, значит, всё супер!

![IMG_9390](https://github.com/user-attachments/assets/fe63c78f-46fc-4794-a7cb-63527827c2e1)

## "Bad" Dockerfile
![IMG_9391](https://github.com/user-attachments/assets/6c452e40-1917-4160-ab08-4c5d511bdea9)

Что же такого "bad" в этом файле?

1. `FROM ubuntu:latest`
   
   Тег latest всегда указывает на последнюю версию доступного образа Ubuntu, но если базовый образ обновится, то написанный Dockerfile может перестать работать: появятся проблемы с совместимостью и непрезсказуемое поведение в работе с контейнерами.
   
2. `RUN`

   пппп
   
3. `чтото`
   
   п


## "Good" Dockerfile
![IMG_9392](https://github.com/user-attachments/assets/8d00bf7f-2b54-4c22-b84d-b8d3a095f69d)



## "Bad Guys" в контейнерах
