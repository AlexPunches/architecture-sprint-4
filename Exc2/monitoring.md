# Мотивация

Мониторинг необходим прямо сейчас потому что мы не знаем точно, где мы теряем заказы.    
Еще мы не знаем какие нагрузки испытывают наши сервисы и БД.   

Необхдимо это все выяснить, чтобы составить план развития архитектуры.  
А возможно мы найдем какие-то ошибки в сервисах, исправим их, и вообще обойдемся без больших разтрать на изменение архитектуры. 

# Выбор подхода к мониторингу
`USE` -- будем следить и вовремя выявлять, когда наши приложения и БД нуждаются в масштабировании.  

Список метрик, которые подскажут какие сервисы нужно масштабировать в первую очередь,  
а так же найдем, где теряются заказы.

## Мониторим Базы данных
`CRM db instance` -- будет мониторится после свого внедрения.
### Utilization
Загрузка CPU
- CPU % for `shop db instance`
- CPU % for `MES db instance`
- CPU % `CRM db instance`

Использование дискового пространства
- Size of `shop db instance`
- Size of `MES db instance`
- Size of `CRM db instance`

Использование памяти
- Memory Utilisation for `shop db instance`
- Memory Utilisation for `MES db instance`
- Memory Utilisation for `CRM db instance`

### Saturation
Время выполнения запросов, 98-й перцентиль
- Query Latency for `shop db instance`
- Query Latency for `MES db instance`
- Query Latency for `CRM db instance`

Количество активных соединений
- Number of connections for `shop db instance`
- Number of connections for `MES db instance`
- Number of connections for `CRM db instance`

###  Errors
Количество ошибок API
- Number of HTTP 500 for `CRM API`
- Number of HTTP 500 for `MES API`
- Number of HTTP 500 for `shop API`

Количество ошибок в логах PostgreSQL
- Database Errors for `CRM API`
- Database Errors for `MES API`
- Database Errors for `shop API`
- 
Количество ошибок подключения к БД
- Connection Errors for `CRM API`
- Connection Errors for `MES API`
- Connection Errors for `shop API`

## Мониторить Сервисы
### Utilization
Загрузка CPU
- CPU % for `shop API`
- CPU % for `CRM API`
- CPU % for `MES API`

Использование памяти
- Memory Utilisation for `shop API`
- Memory Utilisation for `CRM API`
- Memory Utilisation for `MES API`

### Saturation
Количество одновременных сессий
- Number of simultanious sessions for shop API
- Number of simultanious sessions for CRM API
- Number of simultanious sessions for MES API

Время ответа API, 98-й перцентиль
- Response time (latency) for shop API
- Response time (latency) for CRM API
- Response time (latency) for MES API

Количество сообщений в пути
- Number of message in flight in RabbitMQ

###  Errors
Количество ошибок API
- Number of HTTP 500 for `CRM API`
- Number of HTTP 500 for `MES API`
- Number of HTTP 500 for `shop API`

Колличество не доставленных сообщений
- Number of dead-letter-exchange letters in RabbitMQ



# План действий

В первую очередь настроим мониторинг Баз данных и API, чтобы решить проблемы с потерянными заказами.  
Используя этот же мониторинг сможем определить будущее масштабирование.

А после масштабирования и решения проблем можно будет вернуться к настройкам мониторинга,
чтобы настроить RED или «Четыре золотых сигнала» (решим на следующем этапе).


