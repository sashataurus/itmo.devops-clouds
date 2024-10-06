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





## "Bad" Dockerfile

## "Good" Dockerfile

## "Bad Guys" в контейнерах
