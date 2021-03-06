---
title: Генерация форм для external-классов
sidebar: flexberry-designer_sidebar
keywords: Flexberry Designer, Web UI Контролы
toc: true
permalink: ru/fd_generate-forms-external-classes.html
folder: products/flexberry-designer/generate/
lang: ru
---

## Задание external-класса на форме

Задание представления [external-класса](fd_external-classes.html) на [форме редактирования](fd_editform.html) и на [списковой форме](fd_listform.html) происходит стандартным образом: у [external-класса](fd_external-classes.html) отображаются представления из соответствующего ему класса из другой стадии.

## Генерация форм

На настоящий момент доступна только [генерация web-форм](fa_flexberry-asp-net-form-generation.html).

Необходимо выполнить следующую последовательность действий:

* Сгенерировать объекты.
* Проставить ссылки на внешние классы.
* Скомпилировать объекты.
* Сборку с объектами, на которые ссылается external-класс, положить в папку, где лежат собственные скомпилированные сборки с объектами.
* [Сгенерировать web-приложение](fa_asp-net-generator.html).
* В сгенерированном приложении проставить ссылку на сборку с внешними классами. Добавить ссылки на соответствующих формах. 
