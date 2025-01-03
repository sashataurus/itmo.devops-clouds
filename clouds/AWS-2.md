# Лабораторная работа 1. Знакомство с IaaS, PaaS, SaaS сервисами в облаке на примере Amazon Web Services (AWS). Создание сервисной модели. Вариант 2
## Цель работы: 
Знакомство с облачными сервисами. Понимание уровней абстракции над инфраструктурой в облаке. Формирование понимания типов потребления сервисов в сервисной-модели.
## Дано:

Слепок данных биллинга от провайдера после небольшой обработки в виде SQL-параметров. Символ % в начале/конце означает, что перед/после него может стоять любой набор символов. Образец итогового соответствия, что желательно получить в конце. В этом же документе

## Необходимо:

Импортировать файл .csv в Excel или любую другую программу работы с таблицами. Для Excel делается на вкладке Данные – Из текстового / csv файла – выбрать файл, разделитель – точка с запятой.

Распределить потребление сервисов по иерархии, чтобы можно было провести анализ от большего к меньшему (напр. От всех вычислительных ресурсов Compute дойти до конкретного типа использования - Выделенной стойка в датацентре Dedicated host usage).

Сохранить файл и залить в соответствующую папку на Google Drive.
## Дано
Для начала импортируем данные, представленные в файле .csv в таблицу Excel. 
![image](https://github.com/user-attachments/assets/b1feae55-b9ba-4ac6-9542-15a4362980c0)

Распределить потребление сервисов по иерархии, чтобы можно было провести анализ от большего к меньшему

## Сервисы
**Amazon Elastic Compute Cloud (Amazon EC2)** — это веб-сервис, который позволяет пользователям арендовать виртуальные серверы для запуска своих приложений и сервисов

**Amazon DynamoDB Accelerator (DAX)** — сервис, который ускоряет работу с базой данных DynamoDB. 

**Amazon DynamoDB** — это полностью управляемая база данных NoSQL, предоставляемая Amazon Web Services (AWS)

**AWSDatabaseMigrationSvc**– это сервис миграции, который упрощает и ускоряет процесс миграции баз данных, делая его более надежным и управляемым

**AWS Database Migration Service Storage** - хранение данных во время перемещения.

**AWS Device Farm** – это сервис для тестирования приложений на различных плотформах, который повышает производительность мобильных и веб-приложений.

**IoTDeviceManagement** - упрощает управление IoT-устройствами, обеспечивая их надежность, безопасность и эффективность на протяжении всего жизненного цикла.

**APNFee** - это закрытый раздел веб‑сайта AWS, позволяющий всем партнерам использовать нужные инструменты и материалы 

**Amazon Translate** – это сервис, обеспечивающий быстрый, высококачественный, доступный по стоимости перевод с пользовательскими настройками с одного языка на другой.

**Amazon Transcribe** – это сервис автоматического распознавания речи

**CloudHSM** - модуль аппаратной безопасности для обеспечения защиты данных в облаке.

**AWS CodeBuild** - это сервис для сборки и тестирования приложений в облаке. 

**Comprehend** - это сервис для обработки текстовых документов

**AWS Backup** - это служба резервного копирования; централизует и автоматизирует резервное копирование данных в службах AWS. 

**Cold/Warm Storage Support** – поддержка "холодного"/"теплого" хранения данных.

С помощью AWS документации заполняем пустые столбцы таблицы и получаем:
![image](https://github.com/user-attachments/assets/799ef6b2-f74c-4036-ae3c-bf8523af0835)


[Ссылка на гугл таблицу](https://docs.google.com/spreadsheets/d/1yFu9z9Cf-2mM6HBwIiVok4mccW1u31KGRaxcKt66ql4/edit?gid=0#gid=0)

## Выводы
В результате выполнения лабораторной работы были изучены некоторые облачные сервисы AWS и можно сделать вывод, что Amazon предоставляет огромное количество сервисов в различных сферах: машинное обучение, защита данных, разработка программного обеспечения, аналитика, мониторинг и другое.
