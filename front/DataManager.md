# Менеджер данных

Менеджер данных представляет из себя plugin. Для регистрации плагина в main.js необходимо перед `new Vue` добавить следующий код:

```
Vue.use(DataManager, {
  Vue,
  baseURL, // базовый URL
  accessPointPath, // путь до точек запросов
  metadata: Vue.prototype.$metadata, // метаданные прикладных объектов
  enums: Vue.prototype.$enums, // перечисления прикладных объектов
});
```

Доступ к методам менеджера данных осуществляется через `this.$root.dataManager`

#### Методы менеджера данных

| Name                           | Parameters                            | Return                          | Description                                                                      |
| ------------------------------ | ------------------------------------- | ------------------------------- | -------------------------------------------------------------------------------- |
| authorization                  | { userName, userPassword }            | token пользователя              | Запрашивает авторизацию на сервере                                               |
| authorizationHas               |                                       | true/false                      | Проверяет авторизован ли пользователь                                            |
| authorizationSet               | { token, userName }                   |                                 | Устанавливает параметры авторизации в localstore                                 |
| create                         | objectSlug, appliedObject             | Возвращает appliedObject        | Отправляет POST запрос на сервер                                                 |
| createOrUpdate                 | objectSlug, appliedObject             | Возвращает appliedObject        | Отправляет POST или PUT запрос на сервер (зависит от наличия id в appliedObject) |
| delete                         | objectSlug, appliedObject             |                                 | Отправляет DELETE запрос на сервер                                               |
| executeActionAppliedObject     | objectSlug, appliedObject, actionName | Зависит от actionName           | Выполняет POST запрос с actionName                                               |
| executeActionAppliedObjectList | objectSlug, appliedObject, actionName | Зависит от actionName           | Выполняет GET запрос с actionName                                                |
| getList                        | objectSlug, filters = {}              | Возвращает массив элементов     | Отправляет GET запрос на сервер                                                  |
| getObject                      | objectSlug, { id }                    | Возвращает объкт элемента по id | Отправляет GET запрос на сервер                                                  |
| put                            | objectSlug, id, appliedObject         | Возвращает appliedObject        | Отправляет PUT запрос на сервер                                                  |
|                                |                                       |                                 |                                                                                  |
