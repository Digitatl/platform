### Описание компонентов

#### DNavigationPanel

Компонент предназначен для навигации по формам.

##### Props

| Name     | Type   | Default                                                                                   | Description                                                                        |
| -------- | ------ | ----------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| tabMenu  | Object | { tabHeader: 'Главная', path: 'views/Menu', component: () => import('@/views/Menu.vue') } | Компонент/страница которые будут смонтированы на первой табке компонента навигации |
| tabStyle | Object | { padding: '0px', height: 'calc(100vh - 32px)' }                                          | Кастомный стиль для отображения всех табок                                         |

##### Description

Компонент слушает и обрабатывает следующие события из шины событий:

| Name               | Parameters                                                  | Description                                                          |
| ------------------ | ----------------------------------------------------------- | -------------------------------------------------------------------- |
| action:formElement | { objectSlug, appliedObject, actionName }                   | Выполняет action для формы элемента                                  |
| action:formList    | { objectSlug, appliedObject, actionName }                   | Выполняет action для формы списка                                    |
| close:form         |                                                             | Закрывает активную форму(табку)                                      |
| delete:formList    |                                                             | deprecated                                                           |
| open:formElement   | { appliedObjectForResponse, mode, path, state, objectSlug } | Открывает форму элемента                                             |
| open:formList      | { appliedObjectForResponse, mode, path, state, objectSlug } | Открывает форму списка                                               |
| open:freeForm      |                                                             | Открывает свободную форму                                            |
| refresh:formList   |                                                             | deprecated                                                           |
| save:formElement   |                                                             | deprecated                                                           |
| return:selection   | { appliedObject, sourseFormIndex }                          | Возвращает значение appliedObject в форму с индексом sourseFormIndex |

#### DFormHeader

Компонент предназначен для размещения на форме заголовка формы

##### Props

| Name          | Type            | Default | Description                 |
| ------------- | --------------- | ------- | --------------------------- |
| appliedObject | [Array, Object] | []      | Массив или Объект с данными |
| objectSlug    | String          |         | Имя прикладного объекта     |

##### Emits

Компонент генерирует на шину событий следующие события:

| Name       | Parameters | Description     |
| ---------- | ---------- | --------------- |
| close:form |            | Закрывает форму |

#### DToolbar

Компонент предназначен для размещения командной панели

##### Props

| Name       | Type    | Default                           | Description                             |
| ---------- | ------- | --------------------------------- | --------------------------------------- |
| dense      | Boolean | true                              | Задает высоту тулбара (dense ? 28 : 48) |
| options    |         | { items: [ { action: 'spacer' } ] | Опции тулбара (см. Description)         |
| mode       |         |                                   | deprecated                              |
| isActive   |         |                                   | deprecated                              |
| isDisabled |         |                                   | deprecated                              |

##### Description

Существует 4 набора стандартных опций командной панели:

1. `optionsToolbarList` - набор для формы списка
2. `optionsToolbarElementCatalog` - набор для формы элемента каталога
3. `optionsToolbarElementDocument` - набор для формы элемента документа
4. `optionsToolbarTabularSection` - набор для табличной части

При необходимости можно переопределить любой из наборов или создать на форме свой. Для этого необходимо на форме, в секции data, определить новый объект вида (при совпадении имени объекта со стандартными из набора, стандартный будет переопределен, но только для этой формы):

```
optionsToolbarListNew: {
        items: [
          TOOLBAR_ITEMS.CREATE, // стандартные действия
          TOOLBAR_ITEMS.COPY,
          TOOLBAR_ITEMS.EDIT,
          TOOLBAR_ITEMS.DELETE,
          TOOLBAR_ITEMS.REFRESH,
          {
            action: 'openFreeForm', // пользовательское действие
            icon: ICON.DIAGRAM,
            tooltip: 'Открыть свободную форму',
          },
        ],
        refRelatedItem: 'CatBaseService',
      },
```

При добавлении пользовательского действия, необходимо так-же добавить его к стандартным действиям командной панели указав имя action и выполняемое действие:

```
toolbarActions: {
        openFreeForm: this.openFreeForm,
      },
```

Для опций командной панели ТЧ необходимо прописать refRelatedItem в опциях тулбара, например, на форме есть ТЧ TabdocBaseService, необходимо добавить следующее computed свойство:

```
optionsToolbarTabdocBaseService() {
      return {
        ...this.optionsToolbarTabularSection,
        refRelatedItem: 'TabdocBaseService',
      };
    },
```

и в props - options командной панели для ТЧ передать значение optionsToolbarTabdocBaseService.

Компонент не генерирует никаких событий.
При клике на элемент тулбара, компонент вызывает метод родителя executeAction, со следующими параметрами:

| Name           | Description                                |
| -------------- | ------------------------------------------ |
| refRelatedItem | Имя (ref) связанного с тулбаром компонента |
| actionName     | Имя action                                 |

#### DFormElementField

Компонент предназначен для размещения на форме полей ввода

##### Props

| Name       | Type                                    | Default | Description                           |
| ---------- | --------------------------------------- | ------- | ------------------------------------- |
| value      | [String, Number, Date, Boolean, Object] | null    | Значение переданное через v-modal     |
| options    | Object                                  | {}      | Объект содержащий имя связанного поля |
| objectSlug | String                                  |         | Имя прикладного объекта               |

#### DObjectListForm

Компонент предназначен для размещения на форме списка элементов

##### Props

| Name          | Type   | Default | Description                      |
| ------------- | ------ | ------- | -------------------------------- |
| appliedObject | Array  | []      | Массив с данными                 |
| options       | Object | {}      | Объект содержаший описание полей |

У компонента есть внешние методы:

1. setHeight - устанавливает высоту компонента таблицы, в качестве параметра методу передается высота
2. getCurrentRow - возвращает текущую выбранную строку

Компонент не генерирует никаких событий.
При клике на элемент тулбара, компонент вызывает метод родителя selectRow, со следующими параметрами:
| Name | Description |
| -------------- | ------------------------------------------ |
| refRelatedItem | Имя (ref) компонента |

#### DTabularSections

Компонент предназначен для размещения на форме табличной части

##### Props

| Name           | Type   | Default | Description                               |
| -------------- | ------ | ------- | ----------------------------------------- |
| appliedObjects | Array  | []      | Массив с данными переданнsq через v-modal |
| options        | Object | {}      | Объект содержаший описание полей          |
| objectSlug     | String |         | Имя прикладного объекта                   |

У компонента есть внешние методы:

1. setHeight - устанавливает высоту компонента таблицы, в качестве параметра методу передается высота
2. getCurrentRow - возвращает текущую выбранную строку

Компонент не генерирует никаких событий.
При клике на элемент тулбара, компонент вызывает метод родителя selectRow, со следующими параметрами:
| Name | Description |
| -------------- | ------------------------------------------ |
| refRelatedItem | Имя (ref) компонента |

#### DTabs

Компонент предназначен для размещения на форме вкладок с элементами формы. Является родителем для
компонента DTab. Позволяет размещать на себе несколько вкладок. 

У компонента есть внешний метод:

1. setHeight - устанавливает высоту компонента таблицы, в качестве параметра методу передается высота.

Компонент не генерирует никаких событий.
Для компонента обязательно наличие компонента DTab.

* __DTab__

  Компонент является дочерним компонентом для DTabs, то есть вкладкой. Предназначен для размещения элементов формы. 
  Рекомендуется обворачивать размещаемые элементы в блоки с классом `.height-fixed` и `.height-auto`.
  ##### Props

| Name       | Type   | Default | Description                                            |
|------------|--------|---------|--------------------------------------------------------|
| label      | String | 'Tab'   | Наименование вкладки. Название должно быть уникальное. |

Пример кода:
```vue
<d-tabs>
  <d-tab label="Tab 1">
    <div class="height-fixed">
      <div>
        <d-form-element-field
                :options="options"
                :object-slug="objectSlug"
                v-model="value"
        ></d-form-element-field>
      </div>
    </div>
  </d-tab>

  <d-tab label="Tab 2">
    <div class="height-fixed">
      <d-toolbar
              :options="optionsToolbarTabdocBudgetGzCoefficient"
      ></d-toolbar>
    </div>
    <div class="height-auto">
      <d-tabular-sections
            ref="tab_2_1"
            :options="options1"
            :object-slug="objectSlug"
            v-model="appliedObject.value1"
      />
    </div>
    <div class="height-auto">
      <d-tabular-sections
            ref="tab_2_2"
            :options="options2"
            :object-slug="objectSlug"
            v-model="appliedObject.value2"
      />
    </div>
  </d-tab>
</d-tabs>
```