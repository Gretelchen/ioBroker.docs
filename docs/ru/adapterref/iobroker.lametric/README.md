---
BADGE-NPM version: http://img.shields.io/npm/v/iobroker.lametric.svg
BADGE-Downloads: https://img.shields.io/npm/dm/iobroker.lametric.svg
BADGE-Stable: http://iobroker.live/badges/lametric-stable.svg
BADGE-installed: http://iobroker.live/badges/lametric-installed.svg
BADGE-Dependency Status: https://img.shields.io/david/klein0r/iobroker.lametric.svg
BADGE-Known Vulnerabilities: https://snyk.io/test/github/klein0r/ioBroker.lametric/badge.svg
BADGE-NPM: https://nodei.co/npm/iobroker.lametric.png?downloads=true
translatedFrom: en
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/adapterref/iobroker.lametric/README.md
title: ioBroker.lametric
hash: PPdeemLAczafVqXoyDFeTy8m9xySufV2zack2EfZW8E=
---
![Логотип](../../../en/adapterref/iobroker.lametric/../../admin/lametric.png)

# IoBroker.lametric
## Требования
- *LaMetric Time* с прошивкой *2.2.2* (или новее)

## Конфигурация
Вы можете получить API-ключ вашего устройства [здесь](https://developer.lametric.com/user/devices).

![API-ключ](../../../en/adapterref/iobroker.lametric/docs/apiKey.png)

## Функции
- Установите яркость дисплея (в процентах, автоматический режим / ручной режим)
- Установить громкость звука (в процентах)
- Настроить заставку (включить / выключить, по времени, в темноте)
- Активировать / деактивировать bluetooth и изменить имя bluetooth
- Переключение между приложениями (следующее, предыдущее, перейти к определенному приложению)
- Отправлять уведомления блочно (с настраиваемым приоритетом, звуком, значками, текстом и т. Д.)
- Управляйте специальными приложениями, такими как `` часы '', `` радио '', `` секундомер '' или `` погода ''
- Используйте приложение *Мои данные (DIY)* LaMetric для отображения постоянной информации

Возможности ограничены [официальные функции API](https://lametric-documentation.readthedocs.io/en/latest/reference-docs/lametric-time-reference.html).

## Примеры блоков
Вы можете использовать простую строку в качестве сообщения, которое будет отображаться в виде одного кадра.

![одиночный кадр](../../../en/adapterref/iobroker.lametric/docs/blockly1.png)

Чтобы показать несколько кадров, вы также можете предоставить массив как сообщение

![несколько кадров](../../../en/adapterref/iobroker.lametric/docs/blockly2.png)

Если вы хотите использовать рамки диаграммы, вы должны указать массив чисел как рамку

![фреймы данных диаграммы](../../../en/adapterref/iobroker.lametric/docs/blockly3.png)

## Мои данные (DIY) *(версия> 1.1.0)*
* LaMetric * предлагает приложение (на встроенном рынке приложений) для опроса пользовательских данных. Это приложение называется [Мои данные DIY](https://apps.lametric.com/apps/my_data__diy_/8942). Этот адаптер создает новое состояние в нужном формате.
Вы можете использовать Simple API Adapter для передачи данных в LaMetric Time.

```ioBroker LaMetric Adapter -> State with Frame information <- Simple API Adapter <- My Data DIY App <- LaMetric```

### Конфигурация (с аутентификацией)
1. Установите [Простой адаптер API ioBroker] (https://github.com/ioBroker/ioBroker.simple-api)
2. Создайте нового пользователя ioBroker с именем «lametric» с индивидуальным паролем (например, «HhX7dZl3Fe»).
3. Добавьте пользователя lametric в группу пользователей по умолчанию.
4. Установите это приложение *My Data DIY* на *LaMetric Time* (используйте Market).
5. Откройте настройки приложения *Мои данные (DIY)* и настройте простой URL-адрес API (см. Ниже).
6. Перейдите в конфигурацию адаптера и настройте фреймы с вашей пользовательской информацией (см. Следующую главу).

```
http://172.16.0.219:8087/getPlainValue/lametric.0.mydatadiy.obj/?json&user=lametric&pass=HhX7dZl3Fe
```

** Важно: используйте json-флаг адаптера SimpleAPI (доступен с версии 2.6.2) **

** При необходимости обновите IP-адрес, порт, пользователя и пароль в URL-адресе! **

### Конфигурация (без аутентификации)
1. Установите [Простой адаптер API ioBroker] (https://github.com/ioBroker/ioBroker.simple-api)
2. Установите это приложение *My Data DIY* на LaMetric Time (используйте Market).
3. Откройте настройки приложения *Мои данные (DIY)* и настройте простой URL-адрес API (см. Ниже).
4. Перейдите в конфигурацию адаптера и настройте фреймы с вашей пользовательской информацией (см. Следующую главу).

```
http://172.16.0.219:8087/getPlainValue/lametric.0.mydatadiy.obj/?json
```

** При необходимости обновите IP-адрес и порт в URL-адресе! **

### Конфигурация фрейма *(версия> 1.1.0)*
- Используйте значок плюса, чтобы добавить столько кадров, сколько хотите
- Значок: выберите значок на [официальном веб-сайте] (https://developer.lametric.com/icons) и введите идентификатор в поле конфигурации. **Важно: добавьте i (для статических значков) или a (для анимированных значков) в качестве префикса для этого идентификатора. (Пример: `i3389`)**
- Текст: просто введите текстовую информацию для рамки. Вы можете использовать состояния в фигурных скобках. Эта информация будет заменена соответствующим значением состояния. (Пример: `{youtube.0.channels.HausAutomatisierungCom.statistics.subscriberCount} Подписчики`)

Пример конфигурации из 3-х фреймов:

![пример конфигурации кадра](../../../en/adapterref/iobroker.lametric/docs/myDataDIYConfig.png)

## Специальные приложения / виджеты *(версия> 1.1.2)*
Вы можете управлять некоторыми приложениями с помощью настраиваемой информации.

### Clock.clockface
Допустимые значения:

- один из вариантов: weather, page_a_day, custom или none
- данные пользовательского значка в формате `data: image / png; base64, <двоичный png в кодировке base64>` или `data: image / gif; base64, <двоичный gif в кодировке base64>`

Пример: `data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAYAAADED76LAAAAOklEQVQYlWNUVFBgwAeYcEncv//gP04FMEmsCmCSiooKjHAFMEF0SRQTsEnCFcAE0SUZGBgYGAl5EwA+6RhuHb9bggAAAABJRU5ErkJggg==`

### Countdown.configure
Допустимое значение: время в секундах.

## Скрипты
Чтобы отображать сообщения / уведомления на вашем *LaMetric Time* отправьте сообщение этому экземпляру с помощью адаптера JavaScript (или любого другого):

```JavaScript
sendTo(
    "lametric.0",
    "notification",
    {
        priority: "[info|warning|critical]",
        iconType: "[none|info|alert]",
        sound: "<string from sound list>",
        lifeTime: <milliseconds>,
        icon: "<icon>",
        text: "<string|array>",
        cycles: <integer>
    }
);
```

Пример одиночного кадра:

```JavaScript
sendTo(
    "lametric.0",
    "notification",
    {
        priority: "info",
        iconType: "none",
        sound: "cat",
        lifeTime: 5000,
        icon: "i31820",
        text: "test",
        cycles: 1
    }
);
```

Пример нескольких кадров:

```JavaScript
sendTo(
    "lametric.0",
    "notification",
    {
        priority: "info",
        iconType: "none",
        sound: "cat",
        lifeTime: 5000,
        icon: "i31820",
        text: ["frame 1", "frame 2", "frame 3"],
        cycles: 1
    }
);
```

Пример отображения некоторой информации циклически:

```JavaScript
let i = 0;
function show() {
    console.log('Show ' + i);
    sendTo(
        "lametric.0",
        "notification",
        {
            priority: "info",
            iconType: "info",
            lifeTime: 5000,
            icon: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAgAAAAICAIAAABLbSncAAAAAXNSR0IArs4c6QAAAARnQU1BAACxjwv8YQUAAAAJcEhZcwAADsMAAA7DAcdvqGQAAAAYdEVYdFNvZnR3YXJlAHBhaW50Lm5ldCA0LjEuNWRHWFIAAAAySURBVBhXY4AAYdcKk1lngCSUDwHIfAQbzgLqgDCgIqRLwFkQCYQoBAD5EATl4wQMDADhuxQzaDgX0gAAAABJRU5ErkJggg==",
            text: "Hi " + i,
            cycles: 1
        }
    );
    i++;
}
setInterval(show, 10000);
show();
```

## Changelog

<!--
  Placeholder for the next version (at the beginning of the line):
  ### **WORK IN PROGRESS**
-->

### **WORK IN PROGRESS**

* (klein0r) Updated documentation

### 1.5.1

* (klein0r) Translated all objects
* (klein0r) Fixed HTTPS option

### 1.5.0

* (klein0r) Fixed myData DIY data type **(BREAKING CHANGE - requires SimpleAPI 2.6.2 or later to use json parameter)**
* (klein0r) Added version check

### 1.4.1

* (klein0r) Fixed missing translations

### 1.4.0

* (klein0r) Admin 5 Support

### 1.3.2

* (klein0r) Updated dependencies

### 1.3.1

* (klein0r) Added local start and end time for screensaver

### 1.3.0

* (klein0r) Encrypt sensitive information **(BREAKING CHANGE - RE-ENTER YOUR API KEY)**

### 1.2.1

* (klein0r) Extended regex for My Data (DIY)

### 1.2.0

* (klein0r) Added hide if value for My Data (DIY)
* (klein0r) Remove frames without text from My Data (DIY)
* (klein0r) Allow dynamic states for My Data (DIY) icons

### 1.1.3

* (klein0r) Fixed async object creation

### 1.1.2

* (klein0r) Delete app channels if app was deleted on LaMetric
* (klein0r) Custom app configuration (clockface, countdown duration)

### 1.1.1

* (klein0r) Fixed replacement issue for My Data (DIY)
* (klein0r) Updated README with more configuration details

### 1.1.0

* (klein0r) Added support for My Data (DIY)

### 1.0.1

* (klein0r) Added chart data support to notification

### 1.0.0

* (klein0r) First stable release
* (klein0r) Added iobroker sentry
* (klein0r) Added brightness and volume limit information (min, max)

### 0.0.10

* (klein0r) Switched to axios lib

### 0.0.9

* (klein0r) Added missing translations
* (GermanBluefox) Improved Blockly and main.js

### 0.0.8

* (klein0r) Updated dependencies

### 0.0.7

* (klein0r) fixed blockly

### 0.0.6

* (klein0r) switched to setTimeout instead of setInterval, improved logging and fixes eslint complaints

### 0.0.5

* (klein0r) Fixed notification, html, updated github template, enable and disable screensaver

### 0.0.4

* (klein0r) Refactored blockly sendTo / notifications

### 0.0.3

* (klein0r) Added app switching support, refactored everything
* (bluefox) The deletion of the actual shown information was added

### 0.0.2

* (Sigi74) Change message_value for variables message
* (Sigi74) Leave sound none

### 0.0.1

* (klein0r) initial release

## License

The MIT License (MIT)

Copyright (c) 2021 Matthias Kleine <info@haus-automatisierung.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.