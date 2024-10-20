# Домашнее задание к занятию " Микросервисы: принципы"-Абрамов Сергей

Вы работаете в крупной компанию, которая строит систему на основе микросервисной архитектуры.
Вам как DevOps специалисту необходимо выдвинуть предложение по организации инфраструктуры, для разработки и эксплуатации.

## Задача 1: API Gateway 

> Предложите решение для обеспечения реализации API Gateway. Составьте сравнительную таблицу возможностей различных программных решений. На основе таблицы сделайте выбор решения.
> 
> Решение должно соответствовать следующим требованиям:
> - Маршрутизация запросов к нужному сервису на основе конфигурации
> - Возможность проверки аутентификационной информации в запросах
> - Обеспечение терминации HTTPS
> 
> Обоснуйте свой выбор.


| Решение | Маршрутизация | Аутентификация | Терминация HTTPS | Бесплатно/Открыто? |
|---|---|---|---|---|
| Kong | + | + | + | Открыто, Apache 2.0 |
| Tyk.io | + | + | + | Открыто, MPL |
| Apache APISIX | + | + | + | Открыто, Apache 2.0 |
| APIGee | + | + | + | Платно |
| Azure API Gateway | + | + | + | Платно |
| NGINX Plus | + | + | + | Платно |
| KrakenD | + | + | + | Двойное лицензирование, нужные нам функции частично в платной версии |

По фукнционалу нам подходят все.

Наиболее оптимальным. с учётом стомиости,   использовать Kong, т.к. это наиболее популярное бесплатное решение, в основе которого используется не менее популярный и хорошо знакомый многим инженерам NGINX, так же его производительность выше че, например у TYK.   


## Задача 2: Брокер сообщений

> Составьте таблицу возможностей различных брокеров сообщений. На основе таблицы сделайте обоснованный выбор решения.
> 
> Решение должно соответствовать следующим требованиям:
> - Поддержка кластеризации для обеспечения надежности
> - Хранение сообщений на диске в процессе доставки
> - Высокая скорость работы
> - Поддержка различных форматов сообщений
> - Разделение прав доступа к различным потокам сообщений
> - Простота эксплуатации
> 
> Обоснуйте свой выбор.

| Параметр | RabbitMQ | Apache Kafka | ActiveMQ | NATS | Redis |
|:---|:---:|:---:|:---:|:---:|:---:|
| Поддержка кластеризации для обеспечения надежности | + | + | + | + | + |
| Хранение сообщений на диске в процессе доставки | + | + | + | + | + |
| Высокая скорость работы | +- | + | - | + | + |
| Поддержка различных форматов сообщений | AMQP, MQTT, STOMP | Только binary через TCP Socket | 10 форматов, включая AMQP, AUTO, MQTT, REST | Только NATS Streaming Protocol | Только RESP |
| Разделение прав доступа к различным потокам сообщений | + | + | + | + | + |
| Простота эксплуатации | + | - | + | + | + |


Как универсальное решение, я бы предложил RabbitMQ - он усреднённый по всем параметрам, очень распространён, и проще найти специалистов, которые с ним работали.

Если брокер нужен только для связи между микросервисами, тогда наверное NATS - он написан специально для этого.
