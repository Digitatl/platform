# Описание класса ObjectMetadata

Класс ObjectMetadata предназначен для создания объектов метаданных прикладных объектов используемых в проекте и в менеджере данных.
Для создания объекта метаданных прикладного объекта, необходимо в конструктор класса передать следующие параметры:

```
/**
   * Constructor
   * @param {String} objectSlug - идентификатор объекта
   * @param {String} type - тип (указывается у полей табличной части)
   * @param {String} modelType - тип модели
   * @param {String} relatedModelView - представление
   * @param {String} idField - поле идентификатора
   * @param {String} verboseName - имя объекта (человекочитаемое)
   * @param {String} verboseNamePlural - имя объекта во множ. числе (человекочитаемое)
   * @param {String} accessPoint - поле точки доступа
   * @return {ObjectMetadata} - instance ObjectMetadata
   */
```

Класс ObjectMetadata имеет следующие методы:

1. `addField` - добавляет поля с типом ObjectField к объекту метаданных (см. "Описание связного класса ObjectField")
2. `getField` - получает поле метаданных типа ObjectField по имени поля

##### Описание связного класса ObjectField

Класс ObjectField предназначен для создания объектов полей метаданных прикладных объектов. Для создания объекта поля метаданных прикладного объекта, необходимо в конструктор класса передать объект со следующими параметрами:

```
/**
   * Constructor
   * @param {String} objectSlug - имя связанного объекта
   * @param {ObjectMetadata|EnumType} type - тип
   * @param {Boolean} readOnly - признак только чтение
   * @param {Boolean} required - признак обязательности
   * @param {String} verboseName - описание
   * @return {ObjectField}
   */
```

#### Пример создания объекта метаданных

```
// создание объекта метаданных
const CatOkfs = new ObjectMetadata(
  'CatOkfs',
  null,
  'Catalogs',
  '{name}',
  'id',
  'ОКФС',
  'ОКФС',
  'cat-okfs',
);

// добавление полей к объекту метаданных
CatOkfs.addField('id', 'ID', true, 'undefined', false, 'integer');
CatOkfs.addField('code', 'Код', false, 'undefined', false, 'string');
CatOkfs.addField('name', 'Наименование ОКФС по РУБПНУБП ', false, 'undefined', false, 'string');

// добавление объекта метаданных в глобальную переменную $metadata
Vue.prototype.$metadata.set('CatOkfs', CatOkfs);
```
