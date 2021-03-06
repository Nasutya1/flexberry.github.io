---
title: Универсальная форма редактирования 
sidebar: product--sidebar
keywords: Windows UI (формы)
toc: true
permalink: ru/fw_Универсальная-форма-редактирования.html
folder: products/flexberry-winforms/
lang: ru
---

Конечно, можно «вручную» размещать контролы и связывать их через `EditManager` с объектами данных, однако, для облегчения этого труда, существует универсальная форма редактирования, которая автоматически, по указанию типа объекта данных, представлений, размещает элементы управления и обеспечивает пользователя интерфейсом по редактированию объекта данных (панель инструментов, строка статуса). 

Для того, чтобы использовать универсальную форму редактирования, необходимо:
# Конструировать универсальную форму редактирования, передав в конструктор параметром представления, в которых должно осуществляться редактирование:
```
StormNetUI.IDpdEditForm editcont = new StormNetUI.UniWinEdit(new StormNet.View[]{viewforedit});
```
# Установить обработчики на события (как минимум, на `CloseEvent`, чтобы можно было закрыть форму и `SaveEvent`, чтобы «отловить» вызов пользователем сохранения).
# Вызвать метод Edit, передавая объект данных.

Следует понимать, что форма реализует абсолютно «голый» пользовательский интерфейс, вся реакция от пользователя транслируется «наружу» формы через события, соответственно, эта самая «наружа» управляет формой через набор методов. Так, когда пользователь просто закрывает форму редактирования, посылается сообщение `CloseEvent`, но сама форма не закрывается. Чтобы закрыть форму, необходимо вызвать метод `Close`.



Пример обработчика события CloseEvent:

```cs
private void ContainerCloseHandler (object sender, StormNetUI.CloseEventArgs args)
		{
			((StormNetUI.IDpdForm)sender).CloseForm();
		}
```
