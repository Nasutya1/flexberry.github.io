---
title: Доступность операций на OLV в зависимости от прав пользователя
sidebar: product--sidebar
keywords: Flexberry Winforms
toc: true
permalink: ru/fw_object-list-view-rights.html
folder: products/flexberry-winforms/
lang: ru
---

OLV автоматически устанавливает доступность операций редактирования в зависимости от прав. Применяются следующие правила:

# При отсутствии прав на INSERT объекта на списке недоступны операции "Создания" и "Создания по шаблону".
# При отсутствии прав на DELETE объекта недоступна операция "Удалить".
# При (отсутствии прав на UPDATE объекта и наличии прав на READ) операция называться "Просмотр", а объект открывается только на просмотр.

При наличии в списке нескольких типов объектов доступные операции отображаются в зависимости от выбранного объекта.
Текущую настройку можно узнать с помощью свойства `ObjectListView.RightSet`, а смену доступности отследить с помощью события `ObjectListView.RightSetChanged`.