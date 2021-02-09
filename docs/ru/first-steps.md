### Первые шаги

Из этого набора статей вы познакомитесь с **основными основами** Nest. Чтобы познакомиться с основными строительными блоками приложений Nest, мы создадим базовое приложение CRUD с функциями, которые охватывают множество вопросов на начальном уровне.

#### Язык

Мы любим [TypeScript](https://www.typescriptlang.org/) , но, прежде всего, мы любим [Node.js.](https://nodejs.org/en/) Вот почему Nest совместим как с TypeScript, так и с **чистым JavaScript** . Nest использует преимущества новейших языковых функций, поэтому для использования его с ванильным JavaScript нам понадобится компилятор [Babel](https://babeljs.io/) .

Мы в основном будем использовать TypeScript в примерах, которые мы предоставляем, но вы всегда можете **переключить фрагменты кода** на ванильный синтаксис JavaScript (просто нажмите, чтобы переключить кнопку языка в верхнем правом углу каждого фрагмента).

#### Предпосылки

Убедитесь, что в вашей операционной системе установлен [Node.js](https://nodejs.org/) (&gt; = 10.13.0).

#### Настроить

Создать новый проект с помощью [Nest CLI](/cli/overview) довольно просто. Установив [npm](https://www.npmjs.com/) , вы можете создать новый проект Nest с помощью следующих команд в терминале вашей ОС:

```bash
$ npm i -g @nestjs/cli
$ nest new project-name
```

Будет создан каталог `project` , установлены модули узлов и несколько других шаблонных файлов, а также будет создан каталог `src/` заполненный несколькими файлами ядра.

<div class="file-tree">
  <div class="item">src</div>
  <div class="children">
    <div class="item">app.controller.ts</div>
    <div class="item">app.controller.spec.ts</div>
    <div class="item">app.module.ts</div>
    <div class="item">app.service.ts</div>
    <div class="item">main.ts</div>
  </div>
</div>

Вот краткий обзор этих файлов ядра:

 |
--- | ---
`app.controller.ts` | Базовый контроллер с одним маршрутом.
`app.controller.spec.ts` | Модульные тесты для контроллера.
`app.module.ts` | Корневой модуль приложения.
`app.service.ts` | Базовая услуга с одним методом.
`main.ts` | Входной файл приложения, использующего базовую функцию `NestFactory` для создания экземпляра приложения Nest.

`main.ts` включает асинхронную функцию, которая **загрузит** наше приложение:

```typescript
@@filename(main)

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
@@switch
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

To create a Nest application instance, we use the core `NestFactory` class. `NestFactory` exposes a few static methods that allow creating an application instance. The `create()` method returns an application object, which fulfills the `INestApplication` interface. This object provides a set of methods which are described in the coming chapters. In the `main.ts` example above, we simply start up our HTTP listener, which lets the application await inbound HTTP requests.

Обратите внимание, что проект, созданный с помощью Nest CLI, создает исходную структуру проекта, которая побуждает разработчиков следовать соглашению о хранении каждого модуля в его собственном выделенном каталоге.

<app-banner-courses></app-banner-courses>

#### Платформа

Nest стремится быть платформенно-независимой структурой. Независимость от платформы позволяет создавать многократно используемые логические части, которые разработчики могут использовать в приложениях нескольких различных типов. Технически Nest может работать с любой инфраструктурой Node HTTP после создания адаптера. Из коробки поддерживаются две HTTP-платформы: [express](https://expressjs.com/) и [fastify](https://www.fastify.io) . Вы можете выбрать тот, который лучше всего соответствует вашим потребностям.

 |
--- | ---
`platform-express` | [Express](https://expressjs.com/) - это хорошо известный минималистичный веб-фреймворк для node. Это проверенная в боях, готовая к работе библиотека с множеством ресурсов, реализованных сообществом. По умолчанию используется пакет `@nestjs/platform-express` . Многие пользователи хорошо обслуживаются с помощью Express, и им не нужно предпринимать никаких действий для его включения.
`platform-fastify` | [Fastify](https://www.fastify.io/) - это высокопроизводительный фреймворк с низкими накладными расходами, ориентированный на обеспечение максимальной эффективности и скорости. Узнайте , как использовать его [здесь](/techniques/performance) .

Какая бы платформа ни использовалась, она предоставляет собственный интерфейс приложения. Они отображаются соответственно как `NestExpressApplication` и `NestFastifyApplication` .

Когда вы передаете тип `NestFactory.create()` , как в примере ниже, у объекта `app` будут методы, доступные исключительно для этой конкретной платформы. Обратите внимание, однако, что вам не **нужно** указывать тип, **если** вы действительно не хотите получить доступ к базовому API платформы.

```typescript
const app = await NestFactory.create<NestExpressApplication>(AppModule);
```

#### Запуск приложения

После завершения процесса установки вы можете запустить следующую команду в командной строке вашей ОС, чтобы запустить приложение, ожидающее входящих HTTP-запросов:

```bash
$ npm run start
```

Эта команда запускает приложение с HTTP-сервером, который прослушивает порт, определенный в файле `src/main.ts` После запуска приложения откройте браузер и перейдите по `http://localhost:3000/` . Вы должны увидеть `Hello World!` сообщение.
