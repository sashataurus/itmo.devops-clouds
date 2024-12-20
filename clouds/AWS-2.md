# Лабораторная работа 1. Знакомство с IaaS, PaaS, SaaS сервисами в облаке на примере Amazon Web Services (AWS). Создание сервисной модели. Вариант 2
## Цель работы: 
Знакомство с облачными сервисами. Понимание уровней абстракции над инфраструктурой в облаке. Формирование понимания типов потребления сервисов в сервисной-модели.
## Дано
Для начала импортируем данные, представленные в файле .csv в таблицу Excel. 
![image](https://github.com/user-attachments/assets/b1feae55-b9ba-4ac6-9542-15a4362980c0)

Распределить потребление сервисов по иерархии, чтобы можно было провести анализ от большего к меньшему

## Сервисы
**Amazon Elastic Compute Cloud (Amazon EC2)** — это веб-сервис, который предоставляет безопасную, масштабируемую вычислительную мощность в облаке 

**Amazon DynamoDB Accelerator (DAX)** — это полностью управляемый высокодоступный кэш в оперативной памяти для Amazon DynamoDB, который обеспечивает до 10-кратное повышение производительности

**Amazon DynamoDB** — это доступный облачный бессерверный сервис баз данных. DynamoDB удовлетворяет ваши потребности в масштабировании и преодолении операционных сложностей, связанных с реляционными базами данных.

**AWSDatabaseMigrationSvc**– это сервис миграции, который помогает быстро, безопасно и с нулевой потерей данных перенести рабочие нагрузки баз данных и аналитики на AWS.

**AWS Device Farm** – это сервис для тестирования приложений, который повышает производительность мобильных и веб-приложений. Для этого используются различные браузеры для настольных компьютеров и реальные мобильные устройства, поэтому вам не требуется создавать собственную инфраструктуру для тестов. Это ускоряет процесс тестирования, во время которого Device Farm создает журналы для быстрого выявления ошибок в работе вашего приложения.

**IoTDeviceManagement** - это сервис для надзора и обслуживания подключенных устройств в сети IoT. Сервис включает в себя адаптацию новых устройств, настройку параметров, мониторинг их производительности, обеспечение безопасности, обновление программного обеспечения и утилизацию устройств.

**APNFee** - это закрытый раздел веб‑сайта AWS, позволяющий всем партнерам, входящим в партнерскую сеть AWS (APN), использовать нужные инструменты и материалы для развития бизнеса на AWS независимо от уровня партнерства.

**Amazon Translate** – это сервис нейронного машинного перевода, обеспечивающий быстрый, высококачественный, доступный по стоимости перевод с пользовательскими настройками с одного языка на другой.

**Amazon Transcribe** – это сервис автоматического распознавания речи, который позволяет разработчикам добавлять в свои приложения возможности преобразования речи в текст. В его основе лежит базовая речевая модель, которая обеспечивает высокоточную транскрипцию потоковой и записанной речи. 

**CloudHSM** - это полностью управляемый сервис, который автоматизирует аппаратное обеспечение, исправление программного обеспечения и безопасное управление ключами.

**AWS CodeBuild** - это полностью управляемая служба непрерывной интеграции, которая компилирует исходный код, проводит тесты и создает пакеты программного обеспечения, готовые к развертыванию. Вам не нужно предоставлять, управлять и масштабировать свои собственные серверы сборки. 

**Comprehend** - это сервис для обработки текстовых документов, позволяющий извлекать текст, ключевые фразы, темы и другое; также сервис позволяет защищать конфиденциальную информацию и контролировать доступ к ней.

**Amazon Comprehend Medical** - это служба обработки естественного языка, которая использует машинное обучение, для понимания и извлечения медицинских данных из медицинского текста, таких как рецепты, процедуры или диагнозы.

**AWS Backup** - это полностью управляемая служба резервного копирования, централизуют и автоматизирую резервное копирование данных в службах AWS. Она обеспечивает глобальные возможности резервного копирования, которые могут помочь вам достичь требований к аварийному восстановлению и соблюдению нормативных требований. Вы можете централизованно настраивать политики резервного копирования и отслеживать активность резервного копирования ресурсов AWS.

С помощью AWS документации заполняем пустые столбцы таблицы и получаем:
![image](https://github.com/user-attachments/assets/5172499b-c894-4c10-ab51-82c2c85e1a94)

[Ссылка на гугл таблицу](https://docs.google.com/spreadsheets/d/1yFu9z9Cf-2mM6HBwIiVok4mccW1u31KGRaxcKt66ql4/edit?gid=0#gid=0)

## Выводы
В результате выполнения лабораторной работы были изучены некоторые облачные сервисы AWS и можно сделать вывод, что Amazon предоставляет огромное количество сервисов в различных сферах: машинное обучение, защита данных, разработка программного обеспечения, аналитика, мониторинг и другое.
