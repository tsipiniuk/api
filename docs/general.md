# Общая информация

* Всё API работает по протоколу HTTPS.
* Авторизация осуществляется по протоколу OAuth2.  
* Все данные доступны только в формате JSON.
* Базовый URL — `https://api.hh.ru/`
* Даты форматируются в соответствии с [ISO 8601](http://en.wikipedia.org/wiki/ISO_8601): `YYYY-MM-HHThh:mm:ss±hh:mm`.

### Требования к запросами
В запросе необходимо передавать заголовок `User-Agent`, в противном случе ответом будет `400 Bad Request`. 
Указание в заголовке названия приложения и контактной почты разработчика позволит нам оперативно с вами 
связаться в случае необходимости.
```
User-Agent: MyApp/1.0 (my-app-feedback@example.com)
```

### Ошибки и коды ответов
API широко использует информирование при помощи кодов ответов:
`200, 201, 204, 301, 302, 400, 403, 404, 405, 410, 429, 500, 503`
Приложение должно корректно их обрабатывать.

В случае неполадок и сбоев, возможны ответы с кодом `503` и `500`.
При каждой ошибке, помимо кода ответа, в теле ответа может быть выдана дополнительная информация, 
позволяющая разработчику понять причину соответствующего ответа:
```json
{ "error_description": "..." }
```

### Кеширование
При необходимости, вы можете кешировать ответы от нашего API, хранить значение заголовка `Etag` 
и обращаться методом `HEAD`, сравнивая значение приходящего `Etag`.

### Пагинация
К любому запросу, подразумевающему выдачу списка объектов, можно в параметрах указать `page=N&per_page=M`. Нумерация идёт 
с нуля, по умолчанию выдаётся первая (нулевая) страница с 20 объектами на странице.

### CORS (Cross-Origin Resource Sharing) и JSONP
API поддерживает технологию [CORS](http://en.wikipedia.org/wiki/Cross-origin_resource_sharing) для запроса данных из 
браузера с проивзольного домена. Этот метод более предпочтителен, чем использование JSONP. Кроме GET запросов он 
также позволяет делать POST, PUT и DELETE.

Для оборачивания запроса в JSONP-вызов передайте параметр `?callback=callback_name`.

* [HTML5Rocks CORS Tutorial](http://www.html5rocks.com/en/tutorials/cors/)
* [JSONP on en.wikipedia.org](http://en.wikipedia.org/wiki/JSONP)