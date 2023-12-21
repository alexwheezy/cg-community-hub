---
title: О конвертации hipnc в hip
---

## Введение

В общем и целом, `hipnc` и `hiplc` (а так же `hdanc` и `hdalc`) - особые "ограниченные" подформаты `hip` (и `hda`) файлов, в которые
сохраняются сцены гудини, работающего с некоммерческой и инди лицензией соответственно.

Данные форматы применяют ряд мер по усложнению прямой конвертации их в полноценные (`hip` и `hda`) форматы, однако
в самом гудини имеется достаточно инструментов, чтобы эти самые ограничения частично или даже полностью обходить, по этому изначальная задумка
авторов не совсем понятна.

## Конвертация

Известно несколько методов

### Полноценные методы:

#### Orbolt (hda)

Загрузка `hdanc`/`hdalc` на орболт автоматически конвертит ассеты в коммерческие

#### 3rd party

Был найден тор-сайт, конвертящий любые некоммерческие хипфайлы или ассеты целиком и полноценно, без каких-либо ограничений:
[onion сайт](http://2hip2nc744lqw3u63oynxnnex6x75oiqfe7ls5om3s6mcmyiuadj4qad.onion/)

(доступ только через [тор-броузер](https://www.torproject.org/ru/download/))

### Частичные методы:

Гудини имеет функционал по генерации питон или хскрипт кода, воссоздающего заданный граф нод.

Сгенерированный код не имеет ограничений и может быть выполнен в гудини с коммерческой лицензией.

Самый простой способ использовать этот функционал - перетягивание нод на шелф:
* выделяете нужные ноды, перетягиваете их на пустое место на любом шелфе
  * гудини сделает тулзу, создающую выбранные ноды
* в коммерческой версии тыкаете тулзу, она создает сохраненные ноды

этот способ ограниченный, например ассеты он никак не перегоняет, и в принципе гарантированно работать не будет.

Тот же самый трюк, но через hscript файл вместо шелфа:
* В не коммерческой сцене откройте Window/HScript Textport
* `opscript -G -r / > $TEMP/temp.cmd`
* Закройте гудини
* В новой коммерческой сессии откройте текстпорт
* `cmdread $TEMP/temp.cmd`

В `temp.cmd` сохраняются хскрипт команды для создания нод сцены, затем эти команды выполняются в другой сессии гудини,
воссоздавая в итоге исходную сцену

Ограничения:
* Определения ассетов не передаются
* Содержимое залоченных нод не передаётся
