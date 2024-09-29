# Отчёт по лабораторной работе по DevOps №1
## Содержание:
- [Установка Nginx на Ubuntu](#установка-nginx-на-ubuntu)
- [Создание локальных сайтов](#создание-локальных-сайтов)
- [Настройка конфигураций](#настройка-конфигураций)
- [Запуск](#запуск)
- [Исправление ошибки](#исправление-ошибки)
- [Запуск 2](#запуск-2)
- [Alias](#alias)

## Установка Nginx на Ubuntu
Oбновляем списки пакетов из репозиториев с помощью `sudo apt update`, затем установливаем Nginx (очень длинный скрин, поэтому не целиком)

![IMG_9217](https://github.com/user-attachments/assets/bd970261-3238-449c-bef9-fd8d6d94d40d)

Затем добавляем программу в автозагрузку и проверяем статус работы веб-сервера. Видим строку `Active: active (running)...`, значит, сервер успешно работает

![IMG_9218](https://github.com/user-attachments/assets/f9dae253-2599-416d-ab8f-d0a716df20ca)

Проверяем наличие сервера в автозагрузке, всё ок

![image](https://github.com/user-attachments/assets/f3105413-f8fc-4bf3-994b-f75137d688ff)

## Создание локальных сайтов
Здесь мы создали директории для хранения наших локальных сайтов с гениальными названиями `lada` и `sasha`, а также файлы `index.html` внутри них. Содержание файлов также имеет гениальный смысл.

![image](https://github.com/user-attachments/assets/dc6c048d-72d8-4dbf-827c-62d2041ca452)

В хосты добавляем домены сайтов: прописываем `sudo nano /etc/hosts` и пишем там IP сервера (один и тот же: 127.0.0.1) и домены `.local`

![IMG_9221](https://github.com/user-attachments/assets/c3759065-2405-4596-a1bd-86ef5d58fe22)

## Настройка конфигураций
Прописываем `sudo nano /etc/nginx/sites-available/lada.conf` (так же с `sasha.conf`), чтобы зайти в файлы конфигураций. Для каждого сайта указываем, что сервер будет получать запросы http на порту 80, а затем перенаправлять на https на порт 443, чтобы обеспечить безопасное соединение. Сайт должен слушать порт 443 с помощью ssl-сертификата, поэтому прописываем пути к файлам ssl. Также сделаем главной страницей index.html

![IMG_9223](https://github.com/user-attachments/assets/9f4309cf-7807-476b-b497-9da236273981)

Далее делаем наши файлы конфигурации активными, то есть создаем символические ссылки на них

![image](https://github.com/user-attachments/assets/2e4c42b6-b778-4c24-b7b5-63c050a7626d)

И самоподписные сертификаты

![image](https://github.com/user-attachments/assets/9fc1275c-22f5-4c75-8319-52e510bf1346)

## Запуск
![image](https://github.com/user-attachments/assets/94dca746-e31a-4fcf-8094-98ad591e733c)
![image](https://github.com/user-attachments/assets/a8726580-be3f-4c64-af8f-e2924610f719)

Нам выдало ошибку, и было настоящее плаки плаки... Пришлось разбираться

## Исправление ошибки
Переосознавая проделанную работу мы поняли, что мы неправильно создали ссылки. Мы указали их на файлы с доменом `.local`, а не `.conf`. Из-за этого вся конфигурация, которую мы писали, не сработала. Тогда мы удалили лишние файлы, которые случайно создались, и заново грамотно создали новые ссылки и сертификаты

![image](https://github.com/user-attachments/assets/a4cef904-dc03-45af-84cb-8414c087c5c8)
![image](https://github.com/user-attachments/assets/a60ab50a-5afe-4906-bd80-65a9c598888f)

## Запуск 2
Для повторного запуска нам понадобилась команда `sudo nginx -s reload`. И ура! Всё сработало, как надо, и кот смог спеть правильную песню

![IMG_9229 (2)](https://github.com/user-attachments/assets/18ca4f23-819c-4514-b975-de87c7acba44)
![image](https://github.com/user-attachments/assets/1e9ab690-9f7d-4b6a-9744-7bfe9c6b6838)

## Alias
Котику было грустно одному, поэтому мы решили добавить ему собаку

Покажем пример, как мы сделали это для каталога `lada.local`. Внури него мы создаем каталог `gav`, внутри которого создаем файл `html`. Затем используем alias и добавляем псеводнимы путей к папке gav

![image](https://github.com/user-attachments/assets/6c9590ec-3af8-4539-baa9-4a2955befc69)

![image](https://github.com/user-attachments/assets/68c6b83e-c224-4674-906c-6167ee172f16)

Всё, теперь они кайфуют вместе! Всем спасибо, всем пока :heart:

![image](https://github.com/user-attachments/assets/da07e7bf-166d-44b4-bea7-4894ed6269ce)
