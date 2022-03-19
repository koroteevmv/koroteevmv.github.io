---
title: "Черновик учебника"
---

# Основы серверного программирования на node.js

## Знакомство с node.js и npm

### Что такое node.js и зачем он нужен?

1. Node.js - это среда исполнения JavaSript.
1. Первая версия платформы выпущена в 2009 году. 
1. Сейчас пользуется высокой популярностью. 
1. Сейчас платформа использует JavaScript движок V8 от Google, который используется в браузере Google Chrome. 
1. Позволяет создавать серверные приложения.
1. Использует циклю событий с асинхронными функциями.


### Что нужно знать перед изучением node.js

Основы JavaScript
HTTP
JSON
Стрелочные функции
Промисы
Шаблон проектирования MVC

### Как установить node.js на компьютер?

```bash
sudo apt update
sudo apt install -y build-essential
curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt install -y nodejs
sudo apt update
```

Установка из официального сайта на Windows.
На Linux - установка из официального и кастомного репозитория.
Команда node без параметров запускает интерактивный интерпретатор (RELP)
Команда node filename  позволяет запускать программы на JavaScript.
В node нет окружения браузера, а значит - объекта document.
Но зато мы можем работать с файловой системой

### Что такое NPM и зачем нужен он?

```bash
npm -v
npm help

node

node app.js
```

```bash
npm install lodash

npm install -g lodash

npm install -D lodash

npm install -save lodash

npm remove gulp --save-dev

npm update lodash --save
```

```json
"scripts": {
    "start": "node index.js",
    "dev": "live-server"
  }
```

```bash
$ npm start
$ npm run dev
```

1. Программа управления пакетами node.js - Node package manager
1. Примерно аналогично программе pip в python, только для пакетов JavaScript
1. Устанавливается вместе с node.js (изучать необязательно)
1. Позволяет легко устанавливать пакеты/модули в систему
1. Модули на практике это библиотеки JavaScript
1. Облегчает совместную разработку и повторное использование кода
1. позволяет создавать пользовательские скрипты

### Как выглядит Hello world на node.js?

```js
console.log("Hello, world!")
```

```bash
node index.js
```

```bash
node index
```

```js
function hello(msg){
	concole.log(msg);
}

hello("Hello from function!")
```

Функции, классы.

### Зачем нужен файл package.json?

```json
{
  "name": "docker_web_app",
  "version": "1.0.0",
  "description": "node.js on docker",
  "author": "first last <first.last@example.com>",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```

Манифест приложения, показывает основную информацию о приложении
Перечисление зависимостей (имя и версия)
Указания, если версия должна обновляться
Может использоваться для создания скриптов
Легко создать с помощью npm init


```bash
npm init
```

### Как импортировать модули и файлы в программу?

```js
//person.js
const person = {
	name: 'John Doe',
	age: 30
};

module.exports = person;
```

```js
//index.js
const person = require('./person');
console.log(person.age);
```

Импорт переменной из другого файла
Импорт функции, класса
Импорт стандартного модуля
Импорт стороннего модуля

### Как создать простое серверное приложение?

```js
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
})

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
})
```

```js
const http = require('http');
const fs = require('fs');

const hostname = '127.0.0.1';
const port = 3000;

fs.readFile('index.html', (err, html) => {
	if (err){
		throw err;
	}
	const server = http.createServer((req, res) => {
		res.statusCode = 200;
		res.setHeader('Content-Type', 'text/html');
		res.write(html);
		res.end();
	})

	server.listen(port, hostname, () => {
		console.log(`Server running at http://${hostname}:${port}/`);
	})
});


```

Простой сервер
Работа с файлом index.html

### Где получить помощь?

Официальная документация
