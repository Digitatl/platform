# da-platform_front

### Публикация библиотеки \*

Для публикации библиотеки необходимо выполнить команду:

```
npm publish
```

### Установка среды разработки

1. Установить NodeJs (также должен установится npm)
2. Установить Git
3. Установить Vue CLI глобально - npm install -g @vue/cli
4. Клонировать репозиторий
5. Перейти в папку проекта, выполнить - npm install

### Развертывание проекта

Если проект разворачивается не в корне сервера, необходимо в файле node_modules/@vue/cli-service/lib/options.js, указать publicPath:

```
publicPath: (process.env.NODE_ENV === 'production') ? '/<имя-проекта>/' : '/',
```

### Перед установкой библиотеки в проект

Необходимо установить в проект следующие зависимости:

```

"dependencies": {
    "axios": "^0.27.2",
    "v-mask": "^2.3.0",
    "vue-router": "^3.2.0",
    "vue2-teleport": "^1.0.1",
    "vuetify": "^2.6.0"
},

```

### Установка

```
npm install da-platform_front
```

### После установки

1. Необходимо скопировать файлы:

   а. node_modules/da-platform_front/src/scss-import/variables.scss в /src/scss/;

   б. node_modules/da-platform_front/src/scss-import/variablesLib.scss в src/scss/variablesLib.scss;

   в. node_modules/da-platform_front/src/scss-import/forms/form.scss в src/scss/forms/form.scss;

2. В файл main.js после импортов добавить следующий код:

```

import dmanager from '../node_modules/da-platform_front/src/plugins/data-manager';
import ObjectMetadata from '../node_modules/da-platform_front/src/models/ObjectMetadata';
import EnumType from '../node_modules/da-platform_front/src/models/types/EnumType';

const baseURL = ''; // указать адрес сервера
const accessPointPath = ''; // указать путь до точек доступа
const projectUid = ''; // указать идентификатор проекта

Vue.use(dmanager, {
  Vue,
  baseURL,
  accessPointPath,
  metadata: Vue.prototype.$metadata,
  enums: Vue.prototype.$enums,
  projectUid,
});

Vue.prototype.$eventBus = new Vue();

```

3. Скопировать файл node_modules/da-platform_front/src/CreateFolders.vbs в ./src/
4. Скопировать файл node_modules/da-platform_front/src/App.vue в ./src/
5. Скопировать файл node_modules/da-platform_front/src/views/Home.vue в ./src/views/
6. Скопировать файл node_modules/da-platform_front/src/views/Login.vue в ./src/views/
7. Скопировать файл node_modules/da-platform_front/src/views/Control.vue в ./src/views/
8. Скопировать файл node_modules/da-platform_front/src/views/Menu.vue в ./src/views/
9. Скопировать файл node_modules/da-platform_front/src/router/index.js в ./src/router/
10. Скопировать файл node_modules/da-platform_front/public/index.html в ./public/
11. Скопировать файл node_modules/da-platform_front/public/font-awesome-4.7.0 в ./public/

### Запустить сервер разработки

1. Перейти на страницу \Login - залогинется
2. Перейти на страницу \Control - запросить данные, разложить данные по файлам
3. Запустить /src/CreateFolders.vbs для создания структуры каталогов и файлов форм
4. Скоректировать формы

#### Links

[Form components](FormComponents.md)

[Create forms](CreateForms.md)

[Data manager](DataManager.md)

[Object metadata](ObjectMetadata.md)

[Table](DTableGrid.md)
