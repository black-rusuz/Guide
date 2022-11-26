# Х А К А Т О Н С Т В О

1. Продумываем модели (ВСЕ ВМЕСТЕ)
2. Разделяемся:
    - Ксюша делает дизайн **на основании моделей**
    - Я инитю проект
    - Оля инитит проект
3. Приоритет методов

   3.1 Клиентская часть:
    - Репозиторий с получением всех списков
    - Блок для главных экранов
    - Вёрстка

   3.2. Серверная часть:
    - гетОлл для каждой модели
    - Остальные круды

4. Изменения в моделях откладываем на одну большую общую миграцию
5. Не делаем логин и регистрацию (либо с токеном в ответе)

## Конвенция json:

1. **Ключи в lower_snake_case !!!**
2. Массивы в виде

```
arr: [
  {
    'key': 'value'
  },
  {
    'key': 'value'
  }
]
```

## Роутинг и запросы:

### 0. Login: POST

URL: `api.choodoo.team/login` или `api.choodoo.team/auth`

BODY:

```
{
  'login': 'admin',
  'password': 'admin'
}
```

RESPONSE:

```
{
  'token': 'md5_hash'
}
```

### 1. Получение списка:

GET: `api.choodoo.team/items`

RESPONSE:

```
{
  items: [
    {
      'id': 0,
      'name': 'Zalupa',
      'image_url': 'qwerty.com/0.jpg'
    },
    {
      'id': 1,
      'name': 'Pizda',
      'image_url': 'qwerty.com/1.jpg'
    }
  ]
}
```

### 2. Создание объекта: POST

URL: `api.choodoo.team/item`

BODY:

```
{
  'id': 1,
  'name': 'Pizda',
  'image_url': 'qwerty.com/1.jpg'
}
```

RESPONSE:

```
{
  'id': 1,
  'name': 'Pizda',
  'image_url': 'qwerty.com/1.jpg'
}
```

### 3. Удаление объекта: DELETE

URL: `api.choodoo.team/item?id=0`

RESPONSE: 'Да похуй какой респонс'

### 4. Обновление объекта:

Либо то же, шо и создание, либо через UPDATE

(Хотя нахуй оно надо?)

## Дефолтные модели данных:

При необходимости обновляем и используем везде_// TODO: Прикрутить OpenAPI_

[//]: # (TODO: Прикрутить OpenAPI)

<details> 
   <summary>User / Person </summary>

   ```
   id: int
   name: String
   image_url: String
   position: String?
   bio: String?
   ```

</details>

## Рабочий вариант деплоя:

_Перед началом деплоя пинаем Олю до того момента, пока в Postman не будет строчки `Access-Control-Allow-Origin: *`
в `response/headers`_

1. Берём хостинг на джино
2. Прикручиваем `domain.com`
3. Подключаем SSL (с поддоменами или без)
4. Создаём поддомен `api.domain.com`:
    - Создаём одноимённую папку в domains
    - Добавить домен > Существующий
5. Берём бэк и льём на сервер по FTP
6. На фронте `npm run build` и льём в `domain.com` по FTP

**Важно заливать проект целиком, ибо не получится загрузить `vendor` и `node_modules` из консоли**

### Настройка

1. Меняем файл .env в соответствии с mySQL на Jino
2. Льём `.htaccess` и `public/.htaccess`
3. Открываем консоль, пишем `cd domains/api.domain.com`

### Синхронизация данных

1. Когда изменён код:
    - **Локально**: `git push`
    - **Jino console**: `git clone`
2. Когда изменена база
    - **В локальной**: `Экспорт > SQL` (файл)
    - **Jino mySQL**: `Импорт > Выбрать файл`

TODO: Сделать автоматическую синхронизацию