---
title: Статические свойства для доступа к представлениям класса
sidebar: flexberry-orm_sidebar
keywords: DataObject (объекты данных), Flexberry ORM, Public, View (представление)
toc: true
permalink: en/fo_static-view-accessors.html
folder: products/flexberry-orm/
lang: en
---

## Статические свойства для доступа к представлениям класса

При загрузке объектов практически всегда требуется указать [представление](fd_view-definition.html). Для этого может использоваться строковое наименование желаемого представления. Это сопряжено со следующими проблемами:

* Существование представления не может быть проверено на этапе компиляции.
* При написании кода нет удобного способа выбрать представление из списка всех представлений класса.

Для удобства в классы объектов данных добавлены статические свойства для доступа ко всем статическим [представлениям класса](fd_view-definition.html). Для каждого класса генерируется служебный вложенный класс `Views`, и для каждого [представления](fd_view-definition.html) генерируется свойство для доступа к этому [представлению](fd_view-definition.html). 

Рекомендуется использовать эти свойства при любой работе с представлениями класса. Это позволяет своевременно обнаружить ошибки, связанные с удалением или переименованием использующихся представлений (ошибка возникнет на этапе компиляции, а не во время работы приложения).

### Примеры

Без использования статических свойств:

``` csharp
View view = Information.GetView("КошкаL", typeof(Кошка));
```

С использованием статических свойств:

``` csharp
View view = Кошка.Views.КошкаL;
```

Пример определения статических свойств доступен по адресу [https://github.com/Flexberry/FlexberryORM-DemoApp/blob/master/FlexberryORM/CDLIB/Objects/CDDA.cs]().
