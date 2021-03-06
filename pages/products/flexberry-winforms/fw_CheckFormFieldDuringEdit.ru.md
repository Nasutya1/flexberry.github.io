---
title: Проверка данных на форме во время редактирования
sidebar: product--sidebar
keywords: Windows UI (формы)
toc: true
permalink: ru/fw_check-form-field-during-edit.html
folder: products/flexberry-winforms/
lang: ru
---
Проверка данных на форме во время редактирования может осуществляться за счёт:
* [генерации исключения при неправильном вводе в методе `set` соответствующего поля объекта](check-user-field-at-set-method.html);
* определения обязательных для заполнения полей на диаграмме классов через атрибут `[Атрибуты-классов-данных|NotNull]`;
* проверки через `[DataObjectErrorProvider](data-object-error-provider.html)`;
* проверки через [ЛУСы](прикладные-системы_features-of-work-with-log-conditions.html) (при этом используется событие [EditManager](edit-manager.html).[Как-редактировать-объекты-данных-на-формах-связывание-полеи-ввода-со-своиствами-объекта-данных|AfterChangeProperty]).

{| cellspacing="0" cellpadding="2" border="1"
! Приём !! Преимущества !! Недостатки
|-
| [Генерация исключения при неправильном вводе в методе `set` соответствующего поля объекта](check-user-field-at-set-method.html) || + позволяет организовать работу таким образом, что пользователь не выйдет из поля до тех пор, пока значение поля не будет введено корректно || - для начала проверки требуется, чтобы фокус попал на соответствующее поле
|-
| Определение обязательных для заполнения полей на диаграмме классов через атрибут `[Атрибуты-классов-данных|NotNull]` || + позволяет в модели задать обязательные для заполнения поля, 
 + ненавязчивое сигнализирование о незаполненности поля || - не позволяет определять поля, обязательные только в некоторых ситуациях
|-
| Проверка через `[DataObjectErrorProvider](data-object-error-provider.html)` || + позволяет быстро прописать в коде перечень обязательных полей и пользователи приложения не смогут его менять, 
 + ненавязчивое сигнализирование о незаполненности поля  || - не позволяет пользователям менять условия проверки данных на форме
|-
| Проверка через [ЛУСы](прикладные-системы_features-of-work-with-log-conditions.html) || + даёт возможность пользователям самим настраивать условия проверки данных на форме 
 + см. [здесь](прикладные-системы_Реализация-пользовательского-интерфеиса-экранных-форм-редактирования.html) || - в приложение вообще и на конкретную форму в частности должны быть встроены [ЛУСы](прикладные-системы_features-of-work-with-log-conditions.html)
|}

Другие методы проверки данных на форме описаны [здесь](edit-form-validation.html).
----* [ЛУСы](прикладные-системы_Лусы.html)
* [Реализация пользовательского интерфейса экранных форм редактирования](прикладные-системы_Реализация-пользовательского-интерфеиса-экранных-форм-редактирования.html)
* [Особенности работы с ЛУСами](прикладные-системы_features-of-work-with-log-conditions.html)