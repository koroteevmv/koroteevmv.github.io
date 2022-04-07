---
section: wd
title: "Основы Express.js"
---

Express - быстрый минималистичный серверный веб-фреймворк, написанный на node.js.
Можно использовать для создания полноценный веб-приложений, или для создания API. 
Может отдавать JSON или формировать HTML. 
Самый популярный фреймворк для JavaScript.

Самый простой веб-сервер:

```js
const express = require('express');

const app = express();

// define endpoints
app.get('/', function(req, res){
  res.send('Hello, world');
});

app.listen(5000);
```

Что можно делать в обработчике пути?
* получать данные из базы данных
* генерировать HTML-страницы
* возвращать JSON
* обрабатывать данные из запроса

Очень простое задание точек приложения (путей, ендпойтнов). Есть методы app.get(), app.post(), app.delete() и так далее.

Можно создавать связующие функции (middleware).

Рекомендуется использовать Postman для тестирования запросов к серверу.

### Простейший сервер

Создание проекта express:

```bash
$ mkdir express_app && cd express_app
$ npm init -y
$ npm i express
$ touch index.js
```

Создание пустого сервера в файле index.js:

```js
// index.js
const express = require('express');

const app = express();

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Запуск сервера:

```bash
$ node index
```
Создание первого пути:

```js
// index.js
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('<h1>Hello, world!</h1>');
})

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

### Установка живого  сервера nodemon

```bash
$ npm i -D nodemon
```

Создание скриптов запуска приложения:

```json
// package.json
"scripts":{
  "start": "node index",
  "dev": "nodemon index"
}
```

Запуск приложения по скрипту:

```bash
$ npm run dev
```

### Отправка файла

```js
// index.js
const express = require('express');
const path = require('path');

const app = express();

app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
})

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```bash
$ mkdir ./public
$ touch ./public/index.html
```

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My Website</title>
  </head>
  <body>
    <h1>My Website</h1>
  </body>
</html>
```

### Статический сервер

```js
// index.js
const express = require('express');
const path = require('path');

const app = express();

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```bash
$ touch ./public/about.html
```

```html
<!-- about.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>About</title>
  </head>
  <body>
    <h1>About</h1>
  </body>
</html>
```

### Возврат JSON

```js
// index.js
const express = require('express');
const path = require('path');
const members = require('./Members');

const app = express();

// Get all members
app.get('/api/members', (req, res) => {
  res.json(members);
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```js
// Members.js
const members = [
  {
    id: 1,
    name: 'John Doe',
    email: 'john@gmail.com',
    status: 'active'
  },
  {
    id: 2,
    name: 'Bob Williams',
    email: 'bob@gmail.com',
    status: 'inactive'
  },
  {
    id: 3,
    name: 'Shannon Jackson',
    email: 'shannon@gmail.com',
    status: 'active'
  }
];

module.exports = members;
```

### Создание связующей функции

Создание связующей функции (middlware):

```js
// index.js
const express = require('express');
const path = require('path');
const members = require('./Members');

const app = express();

const logger = (req, res, next) => {
  console.log('Hello');
  next();
};

// Init middleware
app.use(logger);

// Get all members
app.get('/api/members', (req, res) => {
  res.json(members);
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Логирование обращения клиента

```js
// index.js
const express = require('express');
const path = require('path');
const members = require('./Members');

const app = express();

const logger = (req, res, next) => {
  console.log(`${res.protocol}://${req.get('host')}${req.originalUrl}`);
  next();
};

// Init middleware
app.use(logger);

// Get all members
app.get('/api/members', (req, res) => {
  res.json(members);
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Установка модуля работы с датами:

```bash
$ npm i moment
```

Использование дат в логировании:

```js
// index.js
const express = require('express');
const path = require('path');
const moment = require('moment');
const members = require('./Members');

const app = express();

const logger = (req, res, next) => {
  console.log(`${res.protocol}://${req.get('host')}${
    req.originalUrl}: ${moment().format()}`);
  next();
};

// Init middleware
app.use(logger);

// Get all members
app.get('/api/members', (req, res) => {
  res.json(members);
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Пример вывода:

```bash
Server started on port 5000.
http://localhost:5000/api/members: 2022-04-04T09:22:45+03:00
```

### Создание RestAPI

Использование параметров

```js
// index.js
const express = require('express');
const path = require('path');
const logger = require('./middleware/logger');
const members = require('./Members');

const app = express();

// Init middleware
app.use(logger);

// Get all members
app.get('/api/members', (req, res) => res.json(members));

// Get single member
app.get('/api/members/:id', (req, res) => {
  res.send(req.params.id);
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Отдача одного элемента

```js
// index.js
const express = require('express');
const path = require('path');
const logger = require('./middleware/logger');
const members = require('./Members');

const app = express();

// Init middleware
app.use(logger);

// Get all members
app.get('/api/members', (req, res) => res.json(members));

// Get single member
app.get('/api/members/:id', (req, res) => {
  res.json(members.filter(member => member.id === parseInt(req.params.id)));
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Обработка пустого вывода:

```js
// index.js
const express = require('express');
const path = require('path');
const members = require('./Members');

const app = express();

// Get all members
app.get('/api/members', (req, res) => res.json(members));

// Get single member
app.get('/api/members/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));
  if (found){
    res.json(members.filter(member => member.id === parseInt(req.params.id)));
  }
  else {
    res.status(400).json({msg: `No member with id of ${req.params.id}`});
  }
});

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

#### Использование роутера

```bash
$ mkdir ./routes
$ mkdir ./routes/api
$ touch ./routes/api/members.js
```

Выделение путей в отдельный файл:

```js
// ./routes/api/members.js
const express = require('express');
const router = express.Router();
const members = require('../../Members');

const app = express();

// Get all members
router.get('/api/members', (req, res) => res.json(members));

// Get single member
router.get('/api/members/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));
  if (found){
    res.json(members.filter(member => member.id === parseInt(req.params.id)));
  }
  else {
    res.status(400).json({msg: `No member with id of ${req.params.id}`});
  }
});

module.exports = router;
```

Рефакторинг основного файла:

```js
// index.js
const express = require('express');
const path = require('path');

const app = express();

app.use('/api/members', require(./routes/api/members));

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

Удаление общей части пути:

```js
// ./routes/api/members.js
const express = require('express');
const router = express.Router();
const members = require('../../Members');

const app = express();

// Get all members
router.get('/', (req, res) => res.json(members));

// Get single member
router.get('/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));
  if (found){
    res.json(members.filter(member => member.id === parseInt(req.params.id)));
  }
  else {
    res.status(400).json({msg: `No member with id of ${req.params.id}`});
  }
});

module.exports = router;
```

#### Создание объекта на сервере

Использование тела запроса:

```js
// ./routes/api/members.js
const express = require('express');
const router = express.Router();
const members = require('../../Members');

const app = express();

// Get all members
router.get('/', (req, res) => res.json(members));

// Get single member
router.get('/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));
  if (found){
    res.json(members.filter(member => member.id === parseInt(req.params.id)));
  }
  else {
    res.status(400).json({msg: `No member with id of ${req.params.id}`});
  }
});

// Create member
router.post('/', (req, res) => {
  res.send(req.body);
});

module.exports = router;
```

```js
// index.js
const express = require('express');
const path = require('path');

const app = express();

// Body parser middleware
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.use('/api/members', require(./routes/api/members));

// Создание статической папки
app.use(express.static(path.join(__dirname, 'public')));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```bash
$ npm i uuid
```

```js
// ./routes/api/members.js
const express = require('express');
const uuid = require('uuid');
const router = express.Router();
const members = require('../../Members');

const app = express();

// ...

// Create member
router.post('/', (req, res) => {
  const newMember = {
    id: uuid.v4(),
    name: req.body.name,
    email: req.body.email,
    status: 'active',
  }
  if (!newMember.name || !newMember.email) {
    return res.status(400).json({ msg: 'Please include a name and email' });
  }
  members.push(newMember);
  res.json(members);
});

module.exports = router;
```

#### Изменение объекта на сервере

```js
// ./routes/api/members.js
const express = require('express');
const uuid = require('uuid');
const router = express.Router();
const members = require('../../Members');

const app = express();

// ...

// Update Member
router.put('/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));

  if (found) {
    const updMember = req.body;
    members.forEach((member, i) => {
      if (member.id ===  parseInt(req.params.id)) {
        member.name = updMember.name;
        member.email = updMember.email;
      }
    });
  } 
  else {
    res.status(400).json({ msg: `No member with the id of ${req.params.id}` });
  }
});

module.exports = router;
```

```js
// ./routes/api/members.js
const express = require('express');
const uuid = require('uuid');
const router = express.Router();
const members = require('../../Members');

const app = express();

// ...

// Update Member
router.put('/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));

  if (found) {
    const updMember = req.body;
    members.forEach((member, i) => {
      if (member.id ===  parseInt(req.params.id)) {
        member.name = updMember.name ? updMember.name : member.name;
        member.email = updMember.email ? updMember.email : member.email;
        res.json({ msg: 'Member updated', updMember });
      }
    });
  } 
  else {
    res.status(400).json({ msg: `No member with the id of ${req.params.id}` });
  }
});

module.exports = router;
```

#### Удаление объекта

```js
// ./routes/api/members.js
const express = require('express');
const uuid = require('uuid');
const router = express.Router();
const members = require('../../Members');

const app = express();

// ...

// Update Member
router.put('/:id', (req, res) => {
  const found = members.some(member => member.id === parseInt(req.params.id));

  if (found) {
    res.json({
      msg: 'Member deleted',
      members: members.filter(member => !idFilter(req)(member))
    });
  } 
  else {
    res.status(400).json({ msg: `No member with the id of ${req.params.id}` });
  }
});

module.exports = router;
```

### Использование шаблонизатора handlebars

```bash
$ npm i express-handlebars
$ mkdir ./views/
$ mkdir ./views/layouts/
$ touch ./views/layouts/main.handlebars
$ touch ./views/index.handlebars
```

```js
// index.js
const express = require('express');
const path = require('path');
const exphbs = require('express-handlebars');

const app = express();

//Handlebars middleware
app.engine('handlebars', exphbs());
app.set('view engine', 'handlebars');

// Body parser middleware
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.get('/', (req, res) => res.render('index'));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```html
<!-- ./views/layouts/main.handlebars -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
    integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">
    <title>Members app/title>
  </head>
  <body>
    <div class="container mt-4">
      {{{body}}}
    </div>
  </body>
</html>
```

```html
<!-- ./views/index.handlebars -->
<h1 class="text-center mb-3">Member app</h1>
```

#### Использование полей в шаблоне

```js
// index.js
const express = require('express');
const path = require('path');
const exphbs = require('express-handlebars');

const app = express();

//Handlebars middleware
app.engine('handlebars', exphbs());
app.set('view engine', 'handlebars');

// Body parser middleware
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.get('/', (req, res) => res.render('index', {
  title: "Member app"
}));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```html
<!-- ./views/index.handlebars -->
<h1 class="text-center mb-3">{{Title}}</h1>
```

```js
// index.js
const express = require('express');
const path = require('path');
const exphbs = require('express-handlebars');
const members = require('./Members');

const app = express();

//Handlebars middleware
app.engine('handlebars', exphbs());
app.set('view engine', 'handlebars');

// Body parser middleware
app.use(express.json());
app.use(express.urlencoded({ extended: false }));

app.get('/', (req, res) => res.render('index', {
  title: "Member app",
  members
}));

const PORT = process.env.PORT || 5000;

app.listen(PORT, () => console.log(`Server started on port ${PORT}.`));
```

```html
<!-- ./views/index.handlebars -->
<h1 class="text-center mb-3">{{Title}}</h1>

<h4>Members</h4>
<ul class="list-group">
  {{#each members}}
  <li class="list-group-item">{{this.name}}: {{this.email}}</li>
  {{/each}}
</ul>
```

#### Добавление записи из формы

```html
<!-- ./views/index.handlebars -->
<h1 class="text-center mb-3">{{Title}}</h1>

<form action="/api/members" method="POST" class="mb-4">
  <div class="form-group">
    <label for="name">Name</label>
    <input type="text" name="name" class="form-control">
  </div>
  <div class="form-group">
    <label for="email">Email</label>
    <input type="email" name="email" class="form-control">
  </div>
  <input type="submit" value="Add Member" class="btn btn-primary btn-block">
</form>

<h4>Members</h4>
<ul class="list-group">
  {{#each members}}
  <li class="list-group-item">{{this.name}}: {{this.email}}</li>
  {{/each}}
</ul>
```

```js
// ./routes/api/members.js
const express = require('express');
const uuid = require('uuid');
const router = express.Router();
const members = require('../../Members');

const app = express();

// ...

// Create member
router.post('/', (req, res) => {
  const newMember = {
    id: uuid.v4(),
    name: req.body.name,
    email: req.body.email,
    status: 'active',
  }
  if (!newMember.name || !newMember.email) {
    return res.status(400).json({ msg: 'Please include a name and email' });
  }
  members.push(newMember);
  // res.json(members);
  res.redirect('/');
});

module.exports = router;
```