# Создание форм

### Описание

В проекте можно создавать формы справочников и формы документов. Формы размещаются в каталоге components в подкаталогах Catalogs и Documents соответственно. Для каждой формы прикладного объекта создается отдельный каталог с именем прикладного объекта. Для каждого прикладного объекта можно создать форму списка и форму элемента.
Форма списка предназначена для вывода списков документов или списка справочника. Форма элемента предназначена для отображения элемента списка справочника или документа.

### Компоненты формы

Для верстки форм предназначены следующие компоненты:

1. `<d-form-header>` - заголовок формы
2. `<d-toolbar>` - командная панель
3. `<d-form-element-field>` - поле ввода
4. `<d-object-list-form>` - таблица списка
5. `<d-tabular-sections>` - табличная часть

### Верстка шаблона формы (`<template>`)

Все формы содержат корневой блок div:

```
<div ref="Form" class="form">
```

Для верстки формы существует два типа блока которые размещаются в корневом блоке:

1. `<div class="height-fixed">` - предназначен для размещения компонентов имеющих фиксированную высоту
2. `<div class="height-auto">` - предназначен для размещения компонентов с изменяющейся высотой

Допускается размещение в блоках, блочных html тегов для корректировки расположения компонентов. В одном блоке может быть расположено несколько компонентов.

В первом блоке допускается размещение следующих компонентов:

1. `<d-form-header>`
2. `<d-toolbar>`
3. `<d-form-element-field>`

Во втором блоке допускается размещение следующих компонентов:

1. `<d-object-list-form>`
2. `<d-tabular-sections>`

### Пример верстки формы списка

##### Шаблон формы списка (`<template>`)

```
<template>
  <div ref="Form" class="form"> // корневой блок

    <div class="height-fixed"> // блок для элементов с фиксированной высотой
      <d-form-header // компонент заголовка
        :applied-object="appliedObject"
        :object-slug="objectSlug"
      ></d-form-header>
    </div>

    <div class="height-fixed">
      <d-toolbar :options="optionsToolbar"></d-toolbar> // компонент тулбара формы
    </div>

    <div class="height-auto"> // блок для элементов с изменяемой высотой
      <d-object-list-form // компонент таблиицы списка
        ref="FormName"
        :applied-object="appliedObject"
        :options="formName"
      >
      </d-object-list-form>
    </div>

  </div>
</template>
```

##### Описание формы списка (`<script>`)

В начало секции script формы необходимо импортировать модуль миксина FormList:
`import FormList from "../../../../node_modules/da-platform_front/src/mixins/FormList";`

В секции `export default` необходимо указать:

1. имя формы `name`
2. зарегистрировать миксин `mixins: [FormList]`
3. в секции `data` размещается следующая информация:

   а. имя прикладного объекта - `objectSlug`

   б. объект с описанием полей таблицы списка:

   ```
   formName: {
       fields: [
         { field: "code", align: "end", width: [null, 96] },
         { field: "name", width: [100] },
       ],
       slug: "FormName",
       refRelatedItem: "FormName",
     },
   ```

##### Стили формы списка (`<style>`)

В секцию `<style lang="scss" scoped>` необходимо импортировать стили:

`@import "../../../scss/forms/form.scss";`

### Пример верстки формы элемента:

##### Шаблон формы элемента (`<template>`)

```
<template>
  <div ref="Form" class="form"> // корневой блок

    <div class="height-fixed"> // блок для элементов с фиксированной высотой
      <d-form-header // компонент заголовка
        :object-slug="objectSlug"
        :applied-object="appliedObject"
      ></d-form-header>
    </div>

    <div class="height-fixed">
      <d-toolbar // компонент тулбара формы
        :options="optionsToolbarList"
      ></d-toolbar>
    </div>

    <div class="height-fixed" style="padding-top: 10px">
      <div style="width: 150px">
        <d-form-element-field
          :options="code"
          :object-slug="objectSlug"
          v-model="appliedObject.code"
        ></d-form-element-field>
      </div>
      <div style="padding-top: 20px">
        <d-form-element-field
          :options="name"
          :object-slug="objectSlug"
          v-model="appliedObject.name"
        ></d-form-element-field>
      </div>
    </div>

    <div class="height-fixed">
      <d-toolbar :options="optionsToolbarTabcatCharacteristicValue"></d-toolbar> // компонент тулбара табличной части
    </div>

    <div class="height-auto"> // блок для элементов с изменяемой высотой
      <d-tabular-sections // компонент табличной части
        ref="TabcatBaseService"
        :options="tabcat_characteristic_value"
        :object-slug="objectSlug"
        v-model="appliedObject.tabcat_characteristic_value"
      />
    </div>
  </div>
</template>
```

##### Описание формы элемента (`<script>`)

В начало секции script формы необходимо импортировать модуль миксина FormElement:
`import FormList from "../../../../node_modules/da-platform_front/src/mixins/FormElement";`

В секции `export default` необходимо указать:

1. имя формы `name`
2. зарегистрировать миксин `mixins: [FormElement]`
3. в секции `data` размещается следующая информация:

   а. имя прикладного объекта - `objectSlug`

   б. объекты с описанием полей формы:

   ```
   code: { field: "code" }, // поле формы
    name: { field: "name" },
    ...
   ```

   если поле является табличной частью, то необходимо так же описать поля табличной части:

   ```
   field_tch: { // поле формы
       fields: [
         { field: "line_number", width: 120, align: "end" },
         { field: "srvscodenew" },
         { field: "charcode" },
         { field: "indexcharcode" },
         { field: "owner" },
       ],
       field: "field_tch",
       refRelatedItem: "TabcatFieldTCh", // ссылка на компонент табличной части
     },
   ```

4. для тулбара табличной части необходимо добавить вычисляемое свойство:

```
computed: {
    optionsToolbarTabcatCharacteristicValue() {
      return {
        ...this.optionsToolbarTabularSection,
        refRelatedItem: "TabcatCharacteristicValue", // ссылка на компонент табличной части
      };
    },
  },
```

##### Стили формы элемента (`<style>`)

В секцию `<style lang="scss" scoped>` необходимо импортировать стили:

`@import "../../../scss/forms/form.scss";`

### Свободная форма

В проекте есть возможность создания свободных форм. Допускается размещение таких форм в в подкаталоге каталога `components`. Для открытия такой формы необходимо сгенерировать на шину событий следующее событие:

```
this.$eventBus.$emit('open:freeForm', {
        mode: 'free',
        path: 'components/FreeForm/FreeFormOne', // путь к форме
        tabHeader: 'Свободная форма',
      });

```

Данные с формы можно вернуть в в открывшую ее форму сгенерировав на шину событий следующее событие:

```
this.$eventBus.$emit('return:selection', {
        appliedObject: this.appliedObject,
        sourseFormIndex: this.sourseFormIndex,
      });
```

Для закрытия формы необходимо сгенерировать на шину событий следующее событие:

```
this.$eventBus.$emit('close:form');
```

##### Шаблон свободной формы (`<template>`)

Верска шаблона свободной формы осуществляется по тем же принципам что и формы списков и формы элементов.

##### Описание свободной формы (`<script>`)

В начало секции script формы необходимо импортировать модуль миксина Form:
`import Form from "../../../../node_modules/da-platform_front/src/mixins/Form";`

В секции `export default` необходимо указать:

1. имя формы `name`
2. зарегистрировать миксин `mixins: [Form]`

Дальнейшее описание свободной формы зависит от ее назначения.
