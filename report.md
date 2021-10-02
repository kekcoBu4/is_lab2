---
title: "Лабораторная работа №2. Дискреционное разграничение прав в Linux. Основные атрибуты"
author: [Радикорский Павел Михайлович, НФИбд-03-18]
institute: "RUDN University, Moscow, Russian Federation"
date: "02.10.2021"
keywords: [Безопасность, Лабораторная]
lang: "ru"
toc-title: "Содержание"
toc: true # Table of contents
toc_depth: 2
lof: true # List of figures
fontsize: 12pt
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: Consolas
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
titlepage: true
titlepage-text-color: "000000"
titlepage-rule-color: "000000"
titlepage-rule-height: 0
listings-no-page-break: true
indent: true
header-includes:
  - \usepackage{sectsty}
  - \sectionfont{\clearpage}
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
...

# Цели и задачи

**Цель:** Получение практических навыков работы в консоли с атрибутами файлов, закрепление теоретических основ дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linux

**Задачи:**

Лабораторная работа подразумевает создание гостевого пользователя, изменение и анализ прав на папки и файлы.

# Теоретическая справка

В Unix каждому файлу соответствует набор прав доступа, представленный в виде 9-ти битов режима. Он определяет, какие пользователи имеют право читать файл, записывать в него данные или выполнять его. Вместе с другими тремя битами, влияющими на запуск исполняемых файлов, этот набор образует код режима доступа к файлу. Двенадцать битов режима хранятся в 16-битовом поле индексного дескриптора вместе с 4-мя дополнительными битами, определяющими тип файла. Последние 4 бита устанавливаются при создании файлов и не подлежат изменению. Биты режима (далее права) могут изменяться либо владельцем файла, либо суперпользователем с помощью команды chmod.

# Выполнение

В установленной при выполнении предыдущей лабораторной работы операционной системе создаём учётную запись пользователя guest, задаём пароль
    
![Создание пользователя](image/1.png){ #fig:001 width=70% }

Входим в систему через пользователя guest, проверяем директорию и уточняем имя пользователя. При сравнении группы получаем совпадение
    
![Проверка пользователя](image/2.png){ #fig:001 width=70% }

Просматриваем файл /etc/passwd, находим свою учётную запись, при сравнении uid и gid получаем совпадение

![/etc/passwd](image/3.png){ #fig:001 width=70% }

Определили существующие в системе директории. Удалось получить список, в котором полные права на доступ есть только у владельцев поддиректорий

![Поддиректории /home](image/4.png){ #fig:001 width=70% }

Проверяем расширенные атрибуты. Получаем, что мы видим расширенные атрибуты только своей директории, но не остальных пользователей

![Расширенные атрибуты](image/5.png){ #fig:001 width=70% }

Создали директорию dir1, сняли с директории все атрибуты. Проверили правильность выполнения команды

![dir1](image/6.png){ #fig:001 width=70% }

Попытались создать в dir1 файл, получили отказ, связанный с отсутствием прав. То же самое произошло при попытке проверки наличия файлов в dir1.

![Создание и проверка файлов](image/7.jpg){ #fig:001 width=70% }

Заполнили таблицу «Установленные права и разрешённые действия», выполняя действия от имени владельца директории (файлов), определив опытным путём, какие операции разрешены, а какие нет

![Установленные права и разрешённые действия](image/8.jpg){ #fig:001 width=70% }

На основании заполненной таблицы определили те или иные минимально необходимые права для выполнения операций внутри директории dir1

![Права для выоплнения операций](image/9.jpg){ #fig:001 width=70% }

#  Выводы

На основании выполненной лабораторной работы были получены практические навыки работы в консоли по изменению атрибутов файлов и папок