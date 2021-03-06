---
title: Настройка меню приложения для разных ролей пользователей
sidebar: guide-practical-guides_sidebar
keywords: guide
toc: true
permalink: ru/gpg_customize-application-menu.html
lang: ru
---

Чтобы настроить меню сгенерированного веб-приложения в соответствии с функциями, которые были ранее определены для каждой роли на основании диаграммы вариантов использования, необходимо:

1.Создать файлы `Web.config` во всех папках внутри папки `forms` проекта веб-приложения, куда были сгенерированы веб-формы (то есть это папки `Employees`, `Orders` и `Products`). Для этого для каждой из этих папок по очереди необходимо выполнить следующее:

* Правой кнопкой мыши щелкнуть по папке в `Solution Explorer`
* В открывшемся меню выбрать `Add` -> `New Item…` (добавить новый элемент)
 
![](/images/pages/guides/flexberry-aspnet/add-new-item.png)

* В открывшемся окне в дереве слева выбрать `Geleral` (Общие), а в средней части окна выбрать `Web Configuration File`.
 
![](/images/pages/guides/flexberry-aspnet/configuration-file.png)

2.Файлы `Web.config` в папках `Employees`, `Orders` и `Products` исправить следующим образом:

* В папке `Employees`:

![](/images/pages/guides/flexberry-aspnet/employees-config.jpg)
 
* В папке `Orders`:

![](/images/pages/guides/flexberry-aspnet/orders-config.jpg)
 
* В папке `Products`:

![](/images/pages/guides/flexberry-aspnet/products-config.jpg)
 
3.Исправить файл `Web.sitemap`, который находится в корне проекта веб-приложения, следующим образом:
 
![](/images/pages/guides/flexberry-aspnet/web-sitemap.png)
 
__Примечание:__ Помимо изменения названий ролей также необходимо изменить комментарий в самом начале файла: `FlexberryAutogenerated="False"`. Это требуется для того, чтобы при последующей перегенерации приложения из [Flexberry Designer](fd_landing_page.html) содержимого данного файла не генерировалось заново (то есть чтобы все изменения в файле сохранились).

Подобные комментарии специального вида есть также в `.cs-` и `.aspx-файлах` данного проекта для возможности сохранять измененный код при перегенерации приложения.  
В проекте `АСУ_Склад(Objects)` в `.cs-файлах` с определением классов данных имеются также специальные секции для возможности сохранять написанный разработчиком код при перегенерации приложения – такие секции называются `скобками программиста`:

![](/images/pages/guides/flexberry-aspnet/objects-project.png)

После выполнения всех перечисленных выше действий необходимо перестроить и запустить приложение, далее – аутентифицироваться по очереди под каждым из ранее созданных пользователей и проверить соответствие отображаемых после авторизации пунктов веб-приложения меню тем функциям, которые были определены в самом нечале лабораторной работы для соответствующей роли пользователя.

## Перейти

* <i class="fa fa-arrow-left" aria-hidden="true"></i> [Настройка путей генерации форм веб-приложения](gpg_configuring-paths-generating.html)
* [Практическое руководство  «Делай как я»](gpg_landing-page.html) <i class="fa fa-arrow-up" aria-hidden="true"></i> 
