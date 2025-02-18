---
translatedFrom: en
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/adapterref/iobroker.eventlist/README.md
title: ioBroker.eventlist
hash: pMEjj/E/4LClSw8GSTCvaYfgt5JuNQxvWKqQv9loPTQ=
---
![Логотип](../../../en/adapterref/iobroker.eventlist/admin/eventlist.png)

![версия NPM](http://img.shields.io/npm/v/iobroker.eventlist.svg)
![Загрузки](https://img.shields.io/npm/dm/iobroker.eventlist.svg)
![Количество установок (последние)](http://iobroker.live/badges/eventlist-installed.svg)
![Количество установок (стабильно)](http://iobroker.live/badges/eventlist-stable.svg)
![Статус зависимости](https://img.shields.io/david/bluefox/iobroker.eventlist.svg)
![Известные уязвимости](https://snyk.io/test/github/bluefox/ioBroker.eventlist/badge.svg)
![НПМ](https://nodei.co/npm/iobroker.eventlist.png?downloads=true)

# IoBroker.список событий
## Адаптер Event-List для ioBroker
Позволяет определить состояния, которые должны регистрироваться в списке событий.

Список можно показать в админке, сети, визе, сохранить в формате PDF, материале (пока не реализовано).

Кроме того, вы можете отправлять события через Telegram или WhatsApp.

![Список](../../../en/adapterref/iobroker.eventlist/img/list.png)

![PDF](../../../en/adapterref/iobroker.eventlist/img/pdf.png)

## Режим тревоги
События могли генерироваться только в режиме тревоги.
Режим тревоги может управляться переменной `eventlist.X.alarm`.

Кроме того, сообщения в мессенджеры можно было отправлять только при включенном режиме тревоги.

Вариант использования:

- напр. датчик двери может отправлять сообщения, только если никого нет дома. В противном случае события об открытии двери будут собираться только в списке событий.

## Возможные презентации
### В админке как вкладка
Вы можете включить список событий как вкладку в админке.

### Интернет
Список событий может отображаться в разделе `http://<IP>:8082/eventlist/index.html`. (для экземпляров > 0: `http://<IP>:8082/eventlist/index.html?X`, где X — номер экземпляра)

### Виджет для просмотра
Список событий может отображаться в виде виджета.

### Генерация PDF
Есть возможность создать PDF документ со всеми событиями.

Название документа может состоять из даты создания, если в него поместить шаблон: `Event list on {{YYYY MM DD}}`.
Точное описание формата времени можно найти здесь: https://momentjs.com/docs/#/displaying/format/

Генерацию PDF можно запустить, записав `true` в `eventlist.0.triggerPDF`.

Доступ к PDF-файлу можно получить через:

- Интернет: `http://<IP>:8082/eventlist/eventlist/report.pdf` (для экземпляров > 0: `http://<IP>:8082/eventlist/eventlist/report-X.pdf`, где X — номер экземпляра)
- администратор: `http://<IP>:8081/files/eventlist/report.pdf` (для экземпляров > 0: `http://<IP>:8081/files/eventlist/report-X.pdf`, где X — номер экземпляра)

**Значки не отображались в формате PDF.**

## Окно сообщения
Пользователь может добавлять пользовательские события в список через javascript:

```
// add custom event to event list
sendTo('eventlist.0', 'insert', {
    event: 'My custom text',
    id: 'ID.that.linked.with.this.event',  // optional
    ts: new Date('2020-09-25T16:11:00',    // optional. Default is Date.now()
    val: 5,                                // optional
    duration: 5                            // in ms
});

// Or simple
sendTo('eventlist.0', 'insert', 'My custom text');
// or
setState('eventlist.0.insert', 'My custom text');
// or
setState('eventlist.0.insert', {event: 'My custom text %s', val: 5});
```

Пользователь может запросить отформатированный список JSON для определенного идентификатора. Конечно, идентификатор должен быть включен в `eventlist` до этого.

```
// add custom event to event list
sendTo('eventlist.0', 'list', {
    ids: ['my.0.state.id1', 'my.0.state.id2'],
    count: 10, // optional limit of maximal lines in table,
    allowRelative: false, // optional if relative times, e.g. "one minute ago", may be used (Default: true)
}, result => {
    console.log(JSON.stringify(result)); // array with events
    // result = [{id: 'my.0.state.id1',
    //
});

// or
sendTo('eventlist.0', 'list', 'my.0.state.id1', result => {
    console.log(JSON.stringify(result)); // array with events
});
```

Пользователь может удалить некоторые или все события из списка событий.

```
// delete all events
sendTo('eventlist.0', 'delete', '*', result => {
    console.log(`Deleted ${result.deleted} events`);
});

// delete all events for specific state ID
sendTo('eventlist.0', 'delete', 'hm-rpc.0.AEOI99389408.1.STATE', result => {
    console.log(`Deleted ${result.deleted} events`);
});

// delete one event by timestamp
sendTo('eventlist.0', 'delete', '2020-10-20T21:00:12.000Z', result => {
    console.log(`Deleted ${result.deleted} events`);
});
```

## Шаблоны
В текстах событий и в текстах состояний могут использоваться следующие шаблоны:

- %s - значение (`Состояние изменено на %s` => `Состояние изменено на 5`),
- %u - единица (`Состояние изменено на %s%u` => `Состояние изменено на 5%`),
- %n - имя (`%n изменил состояние на %s` => `Устройство A изменило состояние на 5`),
- %t - время (`Состояние изменено на %t` => `Состояние изменено сен пт, 16:32:00`),
- %r - относительное время (`Состояние изменено %r` => `Состояние изменено 5 секунд назад`),
- %d - продолжительность (`Состояние было в предыдущем состоянии в течение %d` => `Состояние было в предыдущем состоянии в течение 5 с`),
- %g - разница значений (`Состояние было изменено на %g%` => `Состояние было изменено на 1%`),
- %o - разница значений (`Состояние изменилось с %o на %` => `Состояние изменилось на 1%`)

## Использование нескольких экземпляров в сети
Например. вы можете показать конкретный список для экземпляра 2, например `http://IP:8082/eventlist/index.htmlindex.html?2`.

Сгенерированный отчет будет сохранен, например, под номером 0 в `eventlist/report.pdf` и, например, под номером 1 в `eventlist/report-1.pdf`.

## Сделать
- Изменить начальные тексты в PDF на соответствующем языке
- Множество предустановленных иконок (минимум 100)
- Материальный виджет
- Отправка сообщений в системный журнал (возможно, splunk) https://www.npmjs.com/package/splunk-logging

<!-- Заполнитель для следующей версии (в начале строки):

### __РАБОТА ВЫПОЛНЯЕТСЯ__ -->

## Changelog
### 0.5.4 (2022-02-14)
* (bluefox) Corrected the image paths

### 0.5.3 (2022-02-13)
* (bluefox) Corrected the error with "changes only" option
* (bluefox) Added possibility to use icons with custom events

### 0.4.4 (2021-06-24)
* (bluefox) Corrected the warning for js-controller 3.x

### 0.4.3 (2021-04-19)
* (bluefox) Added the support of Admin5

### 0.4.2 (2020-12-05)
* (bluefox) Added possibility to add multiple states
* (bluefox) Moved the duration to previous state
* (bluefox) Support of multiple instances

### 0.4.0 (2020-11-10)
* (bluefox) Added setting of even/odd background for widget
* (bluefox) Added filter

### 0.2.9 (2020-10-20)
* (bluefox) Corrected error in GUI by disabling of state
* (bluefox) Implemented the deletion of events from the event list

### 0.2.8 (2020-10-14)
* (bluefox) Corrected error in pdf settings  
* (bluefox) Implemented the recalculation of the relative time every 10 seconds

### 0.2.6 (2020-09-25)
* (bluefox) Corrected error in pdf creation

### 0.2.5 (2020-09-24)
* (bluefox) Extended icon selector

### 0.2.1 (2020-09-21)
* (bluefox) Vis-widget was corrected

### 0.1.3 (2020-09-15)
* (bluefox) Implemented the alarm mode and messengers

### 0.0.3 (2020-09-08)
* (bluefox) Objects with states are supported now

### 0.0.2 (2020-09-07)
* (bluefox) initial commit

### 0.0.1
* (bluefox) initial release

## License
MIT License

Copyright (c) 2020-2022 ioBroker <dogafox@gmail.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.