# Rubitime OpenAPI
## Описание   
API Rubitime позволяет получать, создавать, обновлять и удалять записи, получать расписание дат и времени для записи, а также принимать webhook-уведомления о создании, обновлении и удалении записей. Подробнее [на официальном сайтe](https://rubitime.ru/faq/api).

# Swagger 
[https://morevpro.github.io/rubitime-api/](https://morevpro.github.io/rubitime-api/)

## Общий формат ответа API

    Методы Rubitime возвращают JSON-объект с полями `status`, `message` и `data`.
    Бизнес-ошибка обычно передается как `status: error` внутри JSON-ответа.

## Ограничение частоты

    Отправляйте запросы к Rubitime API не чаще одного раза в 5 секунд.

# Как посмотреть

## Через Swagger Editor:

1. Откройте https://editor.swagger.io/.
2. Импортируйте файл `openapi/openapi.yaml`.

## Через статический Swagger UI:

```bash
python -m http.server 8080 --directory openapi
```

После запуска откройте `http://localhost:8080/`


# Как получить API-ключ

    1. Авторизуйтесь в Rubitime ( https://rubitime.ru/profile/ )
    2. Откройте настройки .
    3. Перейдите на 5 шаг настроек.
    4. Найдите блок "Получение и сохранение данных при помощи API".
    5. Нажмите "Сгенерировать ключ".

    API-ключ передается в JSON-теле каждого запроса в поле `rk`.

# Как включить webhook

    В том же блоке настроек укажите публичный HTTPS-адрес вашего обработчика в поле "Вебхук URL".
    Rubitime будет отправлять на этот адрес события:

    - `event-create-record` - создана новая запись;
    - `event-update-record` - обновлена запись;
    - `event-remove-record` - удалена запись.

    Чтобы webhook считался доставленным, ваш сервер должен вернуть HTTP-код `200`.
