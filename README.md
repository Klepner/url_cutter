#Сокращатель урлов

## Задание

Пользователи сокращают 1млн. url в сутки. 
Можно зарегистрироваться через OAuth, например через Google. 
И потом добавлять url-ы для сокращения. 
После отправки формы в ответ пользователь получает новый короткий url, 
который сразу же может работать. 
При переходе по сокращенному url редиректит на полный url. 
Статистика переходов должна сохраняться и быть доступной в виде таблиц и графиков в интерфейсе. 
После старта проекта планируется двухкратный прирост пользователей в год в течение 3 лет. 
Расчетный uptime - 99,8 в тридцатидневном скользящем окне.

Надо нарисовать схему и доказать, что она работает.

---
(rpd - requests per day)
На старте   = 1M rpd ~ 12 rps
1-й год     = 2М rpd ~ 24 rps
2-й год     = 4М rpd ~ 47 rps
3-й год     = 8М rpd ~ 93 rps


Что нужно:
1. API - web сервер (aiohttp, sanic, FastAPI) для открытия endpoint-ов для входящих запросов. 
    Endpoint-ы: (`(POST) /urls/{http"//blabla.bla/fjnf34f8ybcj29uehcbu....}`), (`(GET) /{short link for redirect}`)
2. Механизм авторизации OAuth (Google Identity, FastAPI)
3. Интерфейс для ввода оригинальной ссылки и вывода короткой ссылки для нее 
   И/ИЛИ получения оригинальной ссылки в параметре/теле запроса и возврата короткой ссылки в ответе на запрос
4. База для хранения соответствия оригинальных и коротких ссылок (key:value ~ Redis?)
5. База для хранения статистики переходов (Kafka, Elasticsearch, ClickHouse)
6. Очереди для обеих баз данных (RabbitMQ, Kafka)
7. Генератор короткой ссылки (uuid4)
