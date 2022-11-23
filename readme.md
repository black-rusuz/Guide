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
При необходимости обновляем и используем везде        _// TODO: Прикрутить OpenAPI_

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