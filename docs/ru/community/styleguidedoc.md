---
title: Документация руководства по стилю
lastChanged: 13.06.2019
editLink: https://github.com/ioBroker/ioBroker.docs/edit/master/docs/ru/community/styleguidedoc.md
translatedFrom: de
translatedWarning: Если вы хотите отредактировать этот документ, удалите поле «translationFrom», в противном случае этот документ будет снова автоматически переведен
hash: mfCPW6sFRTOA8DZNqHydfib2TK+qdfZMNwiFfig9vtw=
---
# Руководство по стилю документации
* Документация создается с использованием языка [Markdown] [].
* Имена файлов и папок пишутся строчными буквами.

Допускаются символы `a-z`, `0-9`, подчеркивание `_` и десятичная точка `.`.

* В документах должен быть разрыв строки из 80 символов.
* Желательно, чтобы форматирование текста выполнялось как в файле `.editorconfig`

  описано.

      * [Плагин] [] для автоматического применения этих правил предназначен для

        доступны разные редакторы.

* Для немецких текстов требуется соответствие новой немецкой орфографии.

  предпочтительнее.

* В справочной документации использование личных местоимений (например,

  «Я», «ты», «мы») следует избегать.

* Используйте нейтральные в гендерном отношении местоимения и множественные существительные.
    * ОК: «они (несколько)», «их (собственность)», «лица»,

      «Люди», «разработчики»

    * Не нормально: «его», «она», «он», «она (женщина)», «мальчики», «девочки».

* Если используются скобочные элементы (все скобочные формы и

  Кавычки), знаки препинания выставляются следующим образом:

    * Внутри кронштейна, если элемент кронштейна является полным

    Предложение содержит (подлежащее, сказуемое, объект).

    * За пределами скобки, если элемент скобки является только подмножеством

    содержит.

* Документы всегда начинаются заголовком на уровне H1.
* Ссылки не помещаются в строку (например, с помощью `[ссылка] (http://example.com)`),

но с помощью встроенных `[a link][]` и `[a link]: https://a.link/to/know` в конце документа.

* При использовании тире используется краткое обозначение

  со знаком минус, а не «-» или `Option+Shift+"-"` в OSX.

* Дополнительный контент:
      * Документы, такие как двоичные файлы, изображения, видео или аудиозаписи, будут

      хранится в папке `media`.

      * Медиа включены в текст для общих файлов

с помощью `§§LLLLL_0§§` и для изображений с помощью `![Медиа-термин](../../de/community/media/{dateiname})`.

      * Изображения желательно хранить в формате SVG. Когда SVG

невозможно, тогда как файл jpg или png. Следите за размером файла.

* Следующее относится к разделам исходного кода:
      * В зависимости от языка исходного кода должна быть выбрана соответствующая разметка. К

        Пример ` ```js` для JavaScript.

      * Исходный текст может, но не обязательно, быть полным. Блоки исходного кода

представлены примеры, поясняющие только что изложенную точку зрения, поэтому нет необходимости доставлять полностью исполняемые программы. Однако, если должна быть предоставлена полностью исполняемая программа, это делается в виде медиафайла в папке `media/{code_beispieldatei}` с соответствующей ссылкой в документации.

* Если используются подчеркивания, кавычки, звездочки или обратная косая черта

должны быть использованы правильные символы побег: `\_`, `\*`, `\\` и ``\`` ` anstelle von `_`, ` * §§ SSSSS_6§ § \ ` und `` ` ''.

* Чтобы заметка выделялась, следуйте инструкциям ниже.

  соблюдать:

     - Идентификатор «Примечание:» должен быть выделен курсивом, т.е. как `* Note *:`.
     - После идентификатора «Примечание:» продолжайте с заглавной буквы.
     - Заметку следует разместить в начале нового абзаца, чтобы она была более заметной.

* Для документации по адаптеру существует отдельное [Руководство по стилю] [].

[Plugin]: http://editorconfig.org/#download

[Style Guide]: https://www.iobroker.net/#de/documentation/dev/adapterdocstyleguide.md

[Markdown]: https://www.iobroker.net/#de/documentation/community/docmarkdown.md