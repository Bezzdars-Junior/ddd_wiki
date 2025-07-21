# Сценарии главной страницы
## Сценарий старта страницы
Во время открытия страницы на сервер отправляется get-запрос на адрес localhost:8080/main_page для получения JSON со списком проектов.\
Пример ответа при get запросе:
```json
 {
[
   {
   "id": 0,
   "dateTime" : "23-12-2024 22:00:00",
   "dateChange" : "23-12-2024 22:00:00",
   "description" : "Описание проекта",
   "favourite" : false,
   "projectName" : "DDD",
   "image" : "https://media1.tenor.com/m/BSYeNq2POsQAAAAC/gachimuchi.gif"
   },
   {
   "id": 1,
   "dateTime" : "23-12-2024 22:00:00",
   "dateChange" : "23-12-2024 22:00:00",
   "description" : "Ту ту ту ту ту",
   "favourite" : true,
   "projectName" : "Крутой проект",
   "image" : "https://media1.tenor.com/m/BSYeNq2POsQAAAAC/gachimuchi.gif"
   },
   {}
]
 }
```

|Имя поля|Тип данных|Описание|
|-|--------|---|
|id|int|ID проекта|
|dateTime|String|Дата создания проекта|
|dateChange|String|Дата последнего обновления проекта|
|description|String|Описание проекта|
|favourite|bool|Поле, в котором хранится информация о признаке "избранная" у проекта|
|projectName|String|Имя проекта|
|image|String|Ссылка на картинку из интернета|

## Сценарий добавления нового проекта
Пользователь кликает на иконку добавления нового проекта и заполняет поля с названием проекта и его описанием. Затем отправляется post запрос на сервер localhost:8080/main_page: \
Примре запроса:
```json
 {
"projectName": "project_1",
"description": "description_1"
"favourite": false,
"image" : "https://media1.tenor.com/m/BSYeNq2POsQAAAAC/gachimuchi.gif"
 }
```
Новый проект должен сохраниться в базу данных. В ответ должен прийти json с присвоенным id и временем создания и изменения:
```json
 {   
   "id": 0,
   "dateTime" : "23-12-2024 22:00:00",
   "dateChange" : "23-12-2024 22:00:00",
   "description" : "description_1",
   "favourite" : false,
   "projectName" : "project_1",
   "image" : "https://media1.tenor.com/m/BSYeNq2POsQAAAAC/gachimuchi.gif"
 }
```

## Сценарий изменения проекта
Пользователь кликает на иконку изменения проекта и заполняет поля с названием проекта и его описанием. Затем отправляется put запрос на сервер localhost:8080/main_page/id (id - айди проекта в БД): \
В теле запроса можно изменять любое поле: \
Примры запроса:
```json
 {
"projectName": "project_1",
 }
```

```json
 {
"projectName": "project_1",
"description": "description_1"
"favourite" : true,
"image" : "https://media1.tenor.com/m/BSYeNq2POsQAAAAC/gachimuchi.gif"
 }
```
Изменения проекта должны сохраниться в базу данных. 

## Сценарий удаления проекта
Пользователь кликает на иконку удаления проекта. После этого отправляется delete запрос на сервер localhost:8080/main_page/id (id - айди проекта в БД): \
```json
 {

 }
```

## Сценарий удаления/добавления признака "избранный" у проекта
Пользователь кликает на иконку добавить/удалить из избранного проект. После этого отправляется put запрос на сервер localhost:8080/main_page/id (id - айди проекта в БД): \
```json
 {
"favourite": true
 }
```

## Сценарий перехода на страницу проекта
Пользователь кликает на название проекта и переходит на страницу проекта. Затем отправляется get запрос для получения JSON со списком фичей проекта.\
Пример ответа при get-запросе:
```json
 {
  [
   {
   "id": 0,
   "dateTime" : "23-12-2024 22:00:00",
   "dateChange" : "23-12-2024 22:00:00",
   "content" : [
            {
         "anal": "anal_1",
         "dev": ["dev_1.1", "dev_1.2", "dev_1.3"],
         "test": ["test_1.1","test_1.2","test_1.3"],
            },
            {
         "anal": "anal_2",
         "dev": ["dev_2.1", "dev_2.2", "dev_2.3"],
         "test": ["test_2.1","test_2.2","test_2.3"],
            },
            ...
            ],
   "favourite" : false,
   "featureName" : "feature_name1",
   },
   {
   "id": 1,
   "dateTime" : "23-12-2024 22:00:00",
   "dateChange" : "23-12-2024 22:00:00",
   "content" : [
            {
         "anal": "anal_1",
         "dev": ["dev_1.1", "dev_1.2", "dev_1.3"],
         "test": ["test_1.1","test_1.2","test_1.3"],
            },
            {
         "anal": "anal_2",
         "dev": ["dev_2.1", "dev_2.2", "dev_2.3"],
         "test": ["test_2.1","test_2.2","test_2.3"],
            },
            ...
            ],
   "favourite" : false,
   "featureName" : "feature_name2",
   },
   {}
]
 }
```

|Имя поля|Тип данных|Описание|
|-|--------|---|
|id|int|ID фичи|
|dateTime|String|Дата создания фичи|
|dateChange|String|Дата последнего обновления фичи|
|content|List|Массив содержащий контент наполнения|
|anal|String|Поле содержащее информацию о коллонке "Аналитика"|
|dev|List|Массив содержащий информацию о коллонке "Разработка"|
|test|List|Массив содержащий информацию о коллонке "Тестирование"|
|favourite|bool|Поле, в котором хранится информация о признаке "избранная" у фичи|
|featureName|String|Имя фичи|
