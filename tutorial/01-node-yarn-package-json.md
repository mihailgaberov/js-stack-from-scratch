# 01 - Node, Yarn, and `package.json`

Кода за тази глава можете да намерите [тук](https://github.com/verekia/js-stack-walkthrough/tree/master/01-node-yarn-package-json).

В тази глава ще започнем с настройка на Node, Yarn, основен `package.json` файл и ще екпериментираме с един пакет (package).

## Node

> 💡 **[Node.js](https://nodejs.org/)** е среда за изпълнение на JavaScript. Главно се използва за бекенд разработки, но също така може да бъде използван за всякакви други. В контекста на фронтенд разбработването, може да бъде използван за изпълнението на цял набор от задачи - линтинг (linting), тестване (testing), сглобяване на файлове и т.н.

В това ръководство ще използваме Node за почти всичко, така че ще ви трябва. За да го свалите отидете [тук](https://nodejs.org/en/download/current/) за **макОС** или **Уиндоус**, или използвайте [package manager installations page](https://nodejs.org/en/download/package-manager/) за дистрибуции на Линукс.

Например, на **Ubuntu / Debian**, можете да използвате следната команда, за да инсталирате Node:

```sh
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Ще имате нужда от версии на Node > 6.5.0.

## Инструменти за управление на версиите на Node

Ако имате нужда да бъдете гъвкави и да можете да използвате различни версии на Node, прочетете [тук](https://github.com/creationix/nvm) или [тук](https://github.com/tj/n).

## NPM

NPM е основния мениджър за управление на пакети за Node. Инсталира се автоматично с инсталацията на Node. Мениджърите за управление на пакети се използват за инсталиране и управление на пакети (модули от код, написани от вас или някой друг). Ще използваме много пакети в това ръководство, но ще използваме друг пакетен мениджър, който се нарича Yarn.

## Yarn

> 💡 **[Yarn](https://yarnpkg.com/)** е друг Node пакетен мениджър, който е много по-бърз от NPM, има офлайн подръжка и си извлича зависимостите (dependencies) [по-предсказуемо](https://yarnpkg.com/en/docs/yarn-lock).

След като [излезе](https://code.facebook.com/posts/1840075619545360) през октомври 2016, получи доста добро приемане и скоро може да се превърне в избора за пакетен мениджър на JavaScript обществото. Ако искате да продължите да използвате NPM можете просто да замествате всички `yarn add` и `yarn add --dev` команди в това ръководство с `npm install --save` И `npm install --save-dev`.

Инсталирайте Yarn, следвайки следните [инструкчии](https://yarnpkg.com/en/docs/install) за вашата операционна система. Аз препоръчвам използването на  **инсталационния скрипт** от *Alternatives* таба ако сте с macOS или Unix, за да [не трябва](https://github.com/yarnpkg/yarn/issues/1505) да разчитате на други пакетни мениджъри:

```sh
curl -o- -L https://yarnpkg.com/install.sh | bash
```

## `package.json`

> 💡 **[package.json](https://yarnpkg.com/en/docs/package-json)** е файлът, който се използва за описване и конфигуриране на вашият JavaScript проект. Съдържа обща информация (името на проекта ви, версия, участници в проекта, лиценз и т.н.), конфигурационни настройки за инструментите, които използвате и дори секция за стартиране на задачи (*tasks*).

- Създайте нова папка, в която ще работите и влезте в нея с командата `cd`. 
- Стартирайте `yarn init` и отговорете на въпросите (`yarn init -y` ако искате да прескочите частта с въпросите), за да генерирате `package.json` файл автоматично.

По-долу можете да видите простичък `package.json` файл, който ще използвам в това ръководство:

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "license": "MIT"
}
```

## Hello World

- Създайте `index.js` файл, който да съдържа `console.log('Hello world')`

🏁 Изпълнете `node .` в папката (`index.js` е файла по подразбиране, за който Node търси в една папка/директория). Това трябва да отпечата "Hello world".

**Забележка**: Виждате ли онази 🏁 флаг иконка? Ще я използвам всеки път когато достигнете до ключов момент в текущото ръковоство. Понякога ще пишем много код (и ще правим много промени на веднъж), който код ще можете да изпълните едва когато достигнете до следващ такъв ключов момент, обозначен с такава иконка.

## `start` script

Стартирането на `node .`, за да изпълним нашата програма е малко на прекалено ниско ниво. Ще използваме NPM/Yarn скрипт за стартиране на изпълнението на този код вместо нас. Това ще ни даде едно ниво на абстракция, което ще ни позволи да използваме винаги `yarn start`, дори когато нашата програма стане по-сложна.

- В `package.json`, добавете `scripts` обект, както следва:

```json
{
  "name": "your-project",
  "version": "1.0.0",
  "license": "MIT",
  "scripts": {
    "start": "node ."
  }
}
```

`start` е името, което даваме на *задачата*, която ще стартира нашата програма. В това ръководство ще създадем множество различни задачи в `scripts` обекта. `start` е името, което обикновено се дава на задачата по подразбиране в едно приложение. Някои други стандартни имена на задачи са`stop` и `test`.

`package.json` трябва да бъде валиден JSON файл, което означава, че не може и не трябва да съдържа "trailing commas" - всеки ред се отделя от следващия със запетая с изключение на последния такъв, на него запетея не се поставя. Така че бъдете внимателни когато редактиране ръчно вашия `package.json` файл.

🏁 Изпълнее `yarn start`. Трябва да отпечата `Hello world`.

## Git and `.gitignore`

- Инициализирайте ново Git репозитори с `git init`

- Създайте `.gitignore` файл и добаведе следното в него:

```gitignore
.DS_Store
/*.log
```

`.DS_Store` файловете са автоматично генерирани файлове от макОС, които не трябва никога да поставяте във вашето репозитори.

`npm-debug.log` и `yarn-error.log` са файлове, които се създават когато възникне грешка при работата с вашия пакетен мениджър, тях също не бива да ги поставяме в репозиторито си, тъй като нямаме нужда от следене и контрол на версиите им.

## Инсталиране и използване на пакет

В тази глава ще инсталираме и използваме един пакет. "Пакет" (а "package") е просто парче код, който някой е написал и вие можете да използвате в вашия код. Пакетите могат да бъдат всякакви. Тук ще използваме пакет, който ви помага да манипулирате цветовете например.

- Инсталирайте пакета `color` чрез изпълнение на следната команда: `yarn add color`

Open `package.json` to see how Yarn automatically added `color` in  `dependencies`.

A `node_modules` folder has been created to store the package.

- Add `node_modules/` to your `.gitignore`

You will also notice that a `yarn.lock` file got generated by Yarn. You should commit this file to your repository, as it will ensure that everyone in your team uses the same version of your packages. If you're sticking to NPM instead of Yarn, the equivalent of this file is the *shrinkwrap*.

- Write the following to your `index.js` file:

```js
const color = require('color')

const redHexa = color({ r: 255, g: 0, b: 0 }).hex()

console.log(redHexa)
```

🏁 Run `yarn start`. It should print `#FF0000`.

Congratulations, you installed and used a package!

`color` is just used in this section to teach you how to use a simple package. We won't need it anymore, so you can uninstall it:

- Run `yarn remove color`

## Two kinds of dependencies

There are two kinds of package dependencies, `"dependencies"` and `"devDependencies"`:

**Dependencies** are libraries you need for your application to function (React, Redux, Lodash, jQuery, etc). You install them with `yarn add [package]`.

**Dev Dependencies** are libraries used during development or to build your application (Webpack, SASS, linters, testing frameworks, etc). You install those with `yarn add --dev [package]`.

Next section: [02 - Babel, ES6, ESLint, Flow, Jest, Husky](02-babel-es6-eslint-flow-jest-husky.md#readme)

Back to the [table of contents](https://github.com/verekia/js-stack-from-scratch#table-of-contents).
