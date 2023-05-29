### Компонент DTableGrid

Компонент предназначен для отображения данных в виде таблицы

#### Props

| Name                | Type                       | Default        | Description                                                     |
| ------------------- | -------------------------- | -------------- | --------------------------------------------------------------- |
| alternationColorRow | Boolean                    | true           | Тирговая раскраска строк                                        |
| borderAround        | Boolean                    | true           | Внешняя граница                                                 |
| borderX             | Boolean                    | true           | Горизонтальные границы                                          |
| borderY             | Boolean                    | true           | Вертикальные границы                                            |
| borderYFooter       | Boolean                    | true           | Вертикальные границы подвала                                    |
| borderYHeader       | Boolean                    | true           | Вертикальные границы шапки                                      |
| canExpandRow        | Boolean                    |                | deprecate                                                       |
| columnResize        | Boolean                    | true           | Изменяемая ширина столбцов                                      |
| columns             | Array                      | []             | Столбцы таблицы [{ field, width, align, fixed, viewComponent }] |
| editComponent       | [String, Object, Function] | null           | Компонент редактирования                                        |
| editMode            | String                     | EDIT_MODE.ITEM | Режим редактирования                                            |
| editable            | Boolean                    | true           | Возможность редактирования                                      |
| footer              | Boolean                    | false          | Отображение футера                                              |
| hierarchyMode       | Boolean                    | false          | Иерархический режим отображения                                 |
| itemStyleFunction   | Function                   | {}             | Функция, возвращающая объект стилей ячейки                      |
| loading             | Boolean                    | false          | Отображение индикатора загрузки                                 |
| multiline           | Boolean                    | false          | Многострочный режим                                             |
| multiselect         | Boolean                    | false          | Множественный выбор                                             |
| rowHeightType       | String                     | fixed          | Тип высоты строки                                               |
| rowIdField          | String                     | id             | Поле идентификатора строки                                      |
| rowStyleFunction    | Function                   | {}             | Функция, возвращающая объект стилей строки                      |
| tableData           | Array                      | []             | Данные таблицы                                                  |
| viewFunction        | Function                   | null           | Функция отображения                                             |

#### Emits

| Name          | Parameters                          | Description                                                  |
| ------------- | ----------------------------------- | ------------------------------------------------------------ |
| edit:complete | { rowNumber, columnOptions, value } | Генерируется при завершении редактирования ячейки            |
| focus:item    | { rowNumber, colNumber }            | Генерируется при выборе ячейки                               |
| focus:row     | { rowNumber }                       | Генерируется при выборе ячейки/строки                        |
| keydown       | event                               | Генерируется при keydown на таблице                          |
| select:row    | { rowNumber, colNumber, object }    | Генерируется при двойном клике по строке                     |
| get:data      | { index, currentFocusedRow }        | Генерируется когда в срезе данных присутствуют пустые строки |

#### Outer methods

| Name                | Parameters               | Return | Description                      |
| ------------------- | ------------------------ | ------ | -------------------------------- |
| editStarted         | rowNumber, colNumber     |        | Начать редактирование ячейки     |
| getCurrentColNumber |                          | Number | Возвращает текущий номер колонки |
| getCurrentRow       |                          | Object | Возвращает текущую строку        |
| getCurrentRowNumber |                          | Number | Возвращает текущий номер строки  |
| getCurrentColName   |                          | Object | Возвращает текущую ячейку        |
| setHeight           | height                   |        | Устанавливает высоту таблицы     |
| setFocusRow         | rowNumber, colNumber = 1 |        | Устанавливает фокус на ячейку    |

---

#### Компонент DTableGridBody

#### Props

| Name                 | Type    | Default | Description                  |
| -------------------- | ------- | ------- | ---------------------------- |
| alternationColorRow  | Boolean | true    | Тирговая раскраска строк     |
| countRowInViewport   | Number  | 0       | Количество строк во вьюпорте |
| focusedIdItem        | String  | null    | id выделенной ячейки         |
| focusedIdRow         | String  | null    | null                         |
| rowStyleGridTemplate | Object  | {}      | Объект стилей ячейки         |
| startIndex           | Number  | 0       | Индекс выборки строки        |
