---
title: Базовая системно-технологическая архитектура Flexberry Winforms
sidebar: product--sidebar
keywords: Flexberry Winforms, Ключевые понятия
toc: true
permalink: ru/fw_flexberry-winforms-architecture.html
folder: products/flexberry-winforms/
lang: ru
---

# Архитектурные концепции и их реализация
## Архитектурные логические уровни системы на базе Flexberry Platform
![](/images/pages/img/«Аксиомы» Flexberry/пример4.jpg)
Любая прикладная система, создаваемая на базе `Flexberry Platform`, содержит три логических уровня:
# Пользовательский интерфейс.
# Бизнес-логика.
# Данные, метаданные и доступ к данным.

Уровень III представлен объектами данных, с приписанными им декларативно метаданными и сервисами данных, обеспечивающими базовые функции по работе с хранилищами.


Уровень II представлен [бизнес-сервером](fo_business-servers-wrapper-business-facade.html), где содержится код общесистемных операций над объектами данных, а также операций, выполняющихся при работе сервисов данных (обработчиков). [Бизнес-сервер](fo_business-servers-wrapper-business-facade.html) может быть исполнен как самостоятельно, так и через некоторые обёртки (например, обёртка `COM+` позволяет выполнять бизнес-сервис под `COM+`). Доступ к [бизнес-серверу](fo_business-servers-wrapper-business-facade.html) происходит через т.н. [бизнес-фасад](fo_business-servers-wrapper-business-facade.html), для того, чтобы специфика реализации самого [бизнес-сервера и обёрток](fo_business-servers-wrapper-business-facade.html) не была важна для клиента. Фактически, [бизнес-фасад](fo_business-servers-wrapper-business-facade.html) обеспечивает маршрутизацию вызовов к той или иной обёртке в зависимости от конфигурации системы. [Бизнес-фасад](fo_business-servers-wrapper-business-facade.html) имеет, как минимум, тот же набор методов, что и бизнес-сервер.


Уровень I представлен собственно пользовательским интерфейсом, зависящим от среды реализации (это может быть настольный клиент, браузер (UI-зависимая форма), пользовательским интерфейсом, не зависящим от среды реализации (UI-независимая форма) и сценаристом. Принципиально, пользовательская логика отделена от зависимого от реализации клиента. Так, например, логика наложения ограничения должна быть реализована в UI-независимой форме, что позволит использовать одну и ту же логику вне зависимости от UI-зависимой реализации пользовательского интерфейса. Таким образом, внутренняя реализация системы максимально независима от пользовательского интерфейса, обладая при этом повторной применимостью даже пользовательской логики.



## Архитектурные физические уровни системы на базе Flexberry Platform (Многоуровневая распределённая клиент-серверная архитектура с обособленными серверами приложений и её реализация)

Логическая архитектура системы физически может быть реализована как:


# Монолитная.
# Двухуровневая клиент-серверная.
# Распределённая многоуровневая.
# Распределённая многоуровневая в `WEB`.

Сервисы данных могут обслуживать как локальные источники (файлы), так и СУБД, поэтому физические архитектуры могут быть реализованы так:
# Самостоятельный бизнес-сервер, сервис данных локального источника (напр. XMLDataService).
# Самостоятельный бизнес-сервер, сервис данных СУБД-источника (напр. ODBCDataService).
# Бизнес-сервер под COM+, сервис данных СУБД-источника.
# Бизнес-сервер под Web Service, сервис данных СУБД-источника.

Это основные типы, могут быть и «экзотические», типа, локального файла, но `Web`-сервиса.


Очевидно, применение различных средств даёт различные возможности. Здесь всё остаётся на усмотрение разработчика.



## Интеграция систем

Физическое расположение кода (как исходного, так и двоичного в сборках) не имеет значения. Подключение частей какой-либо системы и чужой системы как подсистемы осуществляются подключением соответствующих сборок.


Деление на сборки внутри системы относится к компетенции разработчика.


## Метаданные объектной структуры

Отдельно существующих метаданных не существует, вместо этого определение дополнительных свойств классов ([представлений](fd_view-definition.html), например), [атрибутов](fo_attributes-class-data.html) (например `[NotNull](fo_attributes-class-data.html)`), методов и т.п. осуществляется указанием атрибутов `.Net`. В сущности, все дополнительные метаданные определяются декларативно `.Net`-атрибутами непосредственно классам данных, их свойствам и т.п.


Существует универсальный [Information-obtainingmetadata|информационный класс (`ICSSoft.STORMNET.DataObject.Information`) со статическими методами для получения метаданных]. Доступ прикладного разработчика к декларативно определённым метаданным (`.Net`-атрибутам) не должен вестись напрямую (через `.NET Reflection`), а только через соответствующие методы этого [Information-obtainingmetadata|информационного класса]. Исключение составляют только те атрибуты, которые вводятся непосредственно самим прикладным разработчиком.



## Хранение данных и независимость от хранилища

'''Сервисом данных''' называется любая реализация абстрактного класса `ICSSoft.STORMNET.Business.DataService`, обеспечивающая сохранение/чтение любых объектов данных в какое-либо хранилище.
 Подробности в статье "[Сервис данных](fo_data-service.html)".


## Формы
Формы предназначены для обеспечения взаимодействия с пользователем.

'''Формой''' называется способ предоставления пользовательского интерфейса для доступа к одному или нескольким объектам  данных. Формы бывают '''UI-зависимые''' (зависят от физической природы интерфейса – `WinForms, WebForms`) и '''UI-независимые'''. Пользовательская логика должна реализовываться в UI-независимых формах, что позволит вносить меньше изменений, а также избежать дублирования кода при реализации в системе других типов пользовательского интерфейса.


UI-зависимые формы могут быть '''универсальными''', т.е. реализовывать некоторую стандартную функциональность без возможности какой-либо модификации. Как правило, это необходимо для очень простых объектов, для которых имеет смысл сэкономить на создании отдельных форм. '''Неуниверсальные''' UI-зависимые формы могут быть сгенерированы (получены в исходном коде) и, затем, допрограммированы.


'''Формы редактирования'''  позволяют пользователю редактировать собственные атрибуты объектов данных, связи с мастеровыми объектами данных, агрегированные объекты данных, в соответствии с одним или несколькими представлениями. Форма редактирования обеспечивает ''полиморфное'' редактирование: как объектов данных собственного класса, так и всех наследуемых классов, в представлении(ях) собственного класса.


'''Форма списка''' позволяет пользователю ''полиморфно'' работать со списком объектов данных как собственного класса, так и любых наследуемых классов. При этом, форме списка указываются классы данных потомков и имя совместимого представления.


'''Форма печати''' позволяет получить печатную копию объекта данных в соответствии с представлением(ями).


## Бизнес-сервер
[Бизнес-сервер](fo_business-servers-wrapper-business-facade.html) предназначен для логического выделения операций, которые относятся к системе. В сущности: бизнес-сервер есть набор методов. Соответственно, бизнес-сервер не имеет состояния (общепринято — stateless). В [CASE бизнес-сервер отрисовывается UML-классом с установленным атрибутом «businessserver»](business-servers.html). Система может содержать произвольное число бизнес-серверов. В общем, число бизнес-серверов и состав их методов определяется прикладным разработчиком.


Бизнес-сервис также применяется в случаях, когда при работе сервиса данных с хранилищем (добавление, удаление и т.п. объекта), требуется выполнить какие-либо действия.


При генерации кода для каждого бизнес-сервера создаётся:

# Код бизнес-сервера с определениями методов;
# Код нужных заглушек («нужные» — определяются разработчиком в CASE в свойствах класса);
# Бизнес-фасад.

## Сценарист
Существует следующая проблема при создании многоуровневых систем: хорошо, мы имеем по отдельности доступ к данным, бизнес-логику, пользовательский интерфейс. Однако как (чем) мы будем объединять эти части в непосредственно работающую систему? Иначе говоря, как (где) должно быть записано, что при определённых манипуляциях пользовательским интерфейсом формы открываются в определённой последовательности и когда происходит вызов операций бизнес-сервера?


Конечно, можно, как это обыкновенно и делается, «жёстко» прописать вызовы прямо в код, например, в пользовательский интерфейс, однако, это является плохой идеей по следующим причинам:

# Части системы перестают быть «частями», поскольку начинают «знать» о существовании друг друга, что может сделать затруднительным повторное использование.
# Модификация этой самой объединяющей логики трудоёмка, поскольку та располагается во многих местах («разбросана» по частям, сборкам, классам).
# Модификация объединяющей логики требует вмешательства в исходный код системы (требует программиста). Если система сможет модифицироваться снаружи, можно дать возможность гибко настраивать логику из готовых частей непосредственно пользователю.
# Вообще затруднено создание логики, которая включает в себя процесс выполнения операций, который сильно ветвится в зависимости от каких-либо условий. Либо, различное выполнение логики в зависимости от полномочий пользователя.

В то же время, эта самая объединяющая логика есть ничто иное, как некоторый сценарий работы для пользователя и может быть описана как самостоятельная сущность.


Для решения этой проблемы, в `Flexberry Platform` предусмотрено создание событийно-ориентированных сценариев (`EBS — Event-Based Script`) и их интерпретации.


Существует специальный графический язык, позволяющий описывать сценарии (`EBSD — Event-Based Script Diagram`, соответствующий диаграммный метод, реализованный в `Flexberry`).


Существует специальный компонент — '''Сценарист '''(`EBSI — Event-Based Script Interpreter`), обеспечивающий выполнение (интерпретацию) сценария в `RunTime`.



