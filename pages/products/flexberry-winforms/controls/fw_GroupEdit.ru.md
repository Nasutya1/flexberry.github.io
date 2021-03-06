---
title: GroupEdit
sidebar: product--sidebar
keywords: Windows UI (Контролы)
toc: true
permalink: ru/fw_group-edit.html
folder: products/flexberry-winforms/
lang: ru
---

(((Данная статья ещё редактируется)))


# GroupEdit
`GroupEdit` - Windows-контрол для создания и редактирования [Детеиловые-ассоциации-и-их-своиства|детейлов].

## [Свойства](http://storm:20013/class_i_c_s_soft_1_1_s_t_o_r_m_n_e_t_1_1_windows_1_1_forms_1_1_group_edit_base.html) GroupEdit'a
{|
! Свойство !! Описание
|-
| `AdvansedMarks` || Добавление дополнительных кнопок управления выделением строк и меток на панель управления GroupEdit'a.
|-
| `AllowRowLocking` || Поддержка режима редактирования с блокировками.
|-
| `AlternativeColor` || Альтернативный цвет для раскраски строк.
|-
| `BackOnShiftEnter` || Переход на следующую ячейку по нажатию &lt;Shift&gt; + &lt;Enter&gt; при выключенном режиме `EditOnEnter`.
|-
| `DoNotAutoLoadItems` || Не загружать данные из базы автоматически.
|-
| `EnableValueDisplayResponsibility` || Поддержка режима `[ValueDisplayResponsibility](displaying-master-in--group-edit.html)`.
|-
| `EditOnEnter` || Редактирование содержимого ячейки по нажатию на клавишу &lt;Enter&gt;
|-
| `GenerateValueChangedEventOnRowOperations` || Генерировать события изменения при добавлении или удалении строки.
|-
| `KeepFocus` || По умолчанию "false". Если установлено "true", то при сохранении будет установлен фокус на той же строке, где он был до сохранения. Запоминается не номер строки, а идентификатор выделенного объекта.
|-
| `LeaveOnLastEnter` || Переходить к следующему контролу при нажатии на клавишу &lt;Enter&gt; в последней строке.
|-
| `MoveNextOnEnter` || Переходить к следующей ячейке по клавише &lt;Enter&gt; при включенном режиме `EditOnEnter`.
|-
| `NewRowOnInsert` || Переходить на первую ячейку новой строки при нажатии &lt;Enter&gt;.
|-
| `NextOnEnter` || Перемещать активную ячейку по клавише &lt;Enter&gt; при выключенном режиме `EditOnEnter`.
|-
| `ReadOnly` || Режим "только чтение".
|-
| `SortOrder` || Настройка сортировки столбца: Asc (по возрастанию), Desc (по убыванию), None (без сортировки). SortPriority
|-
| `SortPriority` || Настройка приоритета сортировки столбца.
|-
| `ShowStatusBar` || Отображение полосы состояния, на которой показывается количество элементов.
|-
| `UseAlernativeColoring` || Использовать чередующуюся окраску строк (базовый/альтернативный цвет).
|-
|}


## Изменение значения в контроле, который вставлен в GroupEdit
Для того, чтобы выполнить настройку контрола, который встраивается в ячейку GroupEdit, нужно использовать событие `gr_SetupEditorEventHandler`, обработчик которого автоматически генерируется на формах редактирования. В аргументы данного события передаются и объект данных, контрол и имя редактируемого в данный момент свойства.
Пример:
```cs
protected override void gr_SetupEditorEventHandler(object sender, ICSSoft.STORMNET.Windows.Forms.SetupEditorEventArgs e)
{
    // *** Start programmer edit section *** (gr_SetupEditorEventHandler( object sender, ICSSoft.STORMNET.Windows.Forms.SetupEditorEventArgs e ))
            
    // *** End programmer edit section *** (gr_SetupEditorEventHandler( object sender, ICSSoft.STORMNET.Windows.Forms.SetupEditorEventArgs e ))
    base.gr_SetupEditorEventHandler(sender, e);
    // *** Start programmer edit section *** (gr_SetupEditorEventHandler( object sender, ICSSoft.STORMNET.Windows.Forms.SetupEditorEventArgs e ) End)
    DateTimePicker dateTimePicker = e.control as DateTimePicker;
    ICSSoft.STORMNET.DataObject dataObject = e.dataObject;
    string propertyName = e.propertyName;

    if (dateTimePicker != null && dataObject.GetStatus() == ObjectStatus.Created)
    {
        dateTimePicker.Value = DateTime.Now.AddMonths(1);
    }

    // *** End programmer edit section *** (gr_SetupEditorEventHandler( object sender, ICSSoft.STORMNET.Windows.Forms.SetupEditorEventArgs e ) End)
}
```
## Сортировка
Как и [ObjectListView](object-list-view.html) `GroupEdit` позволяет отсортировать содержимое по различным столбцам. Чтобы быстро настроить многоуровневую сортировку, можно щелкать по столбцам левой кнопокой мыши, зажав клавишу &lt;Ctrl&gt;

Чтобы многоуровневая сортировка не сбросилась при случайном нажатии на столбец, в версиях Flexberry после 2013.11.14 добавлен уточняющий вопрос о смене сортировки.


## Именованые настройки отображения столбцов
В версиях Flexberry после 2013.11.14 добавлена возможность сохранения именованых настроек отображения столбцов по аналогии с [ObjectListView](object-list-view.html). Настройки сохраняются в базе данных отдельно для каждого пользователя.

(((<msg type=note>Данная опция работает только при включенной настройке `UseSettings = true` в файле конфигурации.</msg>)))

## Прорисовка границ ячеек
Сделать рамки в `GroupEdit` можно, используя следующий код:

```

C1FlexGrid ge = GetGridFromGE(Лапа);
ge.Styles.Normal.Border.Direction = BorderDirEnum.Both;
ge.Styles.Normal.Border.Style = BorderStyleEnum.Flat;
```
`GroupEdit` с прорисованными границами будет выглядеть следующим образом:

![](/images/pages/img/page/GroupEdit/РазъясненияПоGE.png)

## EditManager
Обычно `GroupEdit` располагается на [форме редактирования](fd_classes-with-stereotype-editform.html), имеющей свой `[EditManager](edit-manager.html)`. Однако, у `GroupEdit'а` есть __свой `EditManager`__, отвечающий за связывание и события.

К примеру, если необходимо отловить событие возврата значения при выборе мастера, то необходимо подписаться на событие `AfterChangeProperty` EditManager'a, относящегося к GroupEdit'у, а не к странице редактирования:

```

GroupEdit1.EditManager.AfterChangeProperty += (o, s) => 
{
    // Обработчики
};
```

(((<msg type=Important>Стоит учесть, что событие `AfterChangeProperty` при выборе мастера сработает __дважды__: 1ый раз при нажатии на кнопку [лукапа](look-up--overview.html), а 2ой раз при возврате значения.</msg>)))



# Версии
В версии Flexberry после 27.09.2013 в `GroupEdit` добавлена полоса состояния, отображающая количество элементов.

Чтобы включить отображение полосы состояния, необходимо установить свойство `ShowStatusBar = true;`


# Полезные ссылки по GroupEdit
* Некоторые часто задаваемые вопросы освящены в статье [FAQ по вводному обучению](initial-trainig-f-a-q.html), а также в статье [WinForms UI FAQ](win-forms-u-i--f-a-q.html).
* [Обработка-нажатии-клавиш-контролами-в-GE|Обработка нажатий клавиш контролами в GE] и [Переход по Enter в `GroupEdit`](прикладные-системы_Переход-по--enter-в--group-edit.html).
* [Отображение мастера в `GroupEdit`](displaying-master-in--group-edit.html).
* [Блокировка редактирования отдельных записей в `GroupEdit`](lock-rows-in-group-edit.html).
* [Настроика-ToolBar-в-GroupEdit-настроика-вертикального-размера|Настройка `ToolBar` в `GroupEdit` (настройка вертикального размера)].
* [Установка формата даты](Установка-формата-даты.html).
* [Получение FlexGrid из GroupEdit](flex-grid.html).
* Обработка событий:
** [Обработка-события-отметки-строк-в-GroupEdit|Обработка события отметки строк в `GroupEdit`].
** [События-добавления-и-удаления-в-GroupEditBase|События добавления и удаления в `GroupEdit`].
* [Ограничение-тип-лукапа-combo-в-GroupEdit|Ограничение на тип лукапа «combo» в `GroupEdit`].
* [Функциональность-при-работе-с-массивами-детеиловых-объектов-DetailArray|Функциональность при работе с массивами детейловых объектов (DetailArray)].
* [Наложение ограничений на GroupEdit](add-limit-to-group-edit.html).


# Расширения GroupEdit
Для `GroupEdit` существует ряд расширений, например:
* [GEEditorExt](g-e-editor-ext.html) (редактирование детейлов в отдельном окне).
* [GEEmptyDetailRemover](g-e-empty-detail-remover.html) (удаление пустых строк).
----* [Переход по Enter в GroupEdit](прикладные-системы_Переход-по--enter-в--group-edit.html)