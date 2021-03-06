---
title: Настройки фильтров. FilterSettings.
sidebar: product--sidebar
keywords: Windows UI (формы), Ограничения
toc: true
permalink: ru/fw_filter-settings.html
folder: products/flexberry-winforms/
lang: ru
---

## Настройки фильтров

Эти настройки можно задавать при помощи специального приложения, которое называется AdmConsole.

Данные настройки фильтров должны указывать какие представления используются для отображения детейлов в дереве на [форме задания ограничений](limit-editor-simple-view.html) и какие списковые формы должны открываться для выбора значения мастера.



В общем виде настройка выглядит следующим образом:
# Задать настройки в AdmConsole
#* "Вручную"
#* При помощи генератора настроек
# Проставить название FilterSetting списковой форме
#* При помощи дизайнера
#* В коде

## Запуск AdmConsole
# В файле "AdmConsole.exe.config" необходимо прописать ConnectionString к базе приложения;
# Запустить AdmConsole и в главном меню выбрать пункт "Кэш сборок" -> "Папка кэша сборок". Необходимо выбрать папку со сборкой объектов приложения

## Создание настройки "автоматически" в AdmConsole
Настройки детейлов еще можно проставлять [(X(1)S(btehd455wqxd0i45e2rlp345))/Edit.aspx?Page=FilterSettings#Создание_настройки_вручную_в_AdmConsole_2|вручную], но настройки лукапов доставляют много неудобства. Для того, чтобы упростить задание настроек для лукапов можно воспользоваться генератором настроек фильтров ([Генератор настроек фильтров](прикладные-системы_Генератор-настроек-фильтров.html))


Форму генератора настроек открыть можно следующим образом
# В папке с кэшем сборок должна находиться сборка "IIS.WinUI.AdvancedFSCtrl.dll" (DLL находится в папке с AdmConsole);
# В папке с кэшем сборок должна находиться сборка форм, для удобного проставления настроек лукапов (Сборка форм берется из проекта, и имеет вид <ИмяПроекта>(Forms).dll);
# В AdmConsole открыть списковую форму "Специальные формы настройки" -> "Настройки фильтров". Форма выглядит следующим образом:
![](/images/pages/img/Ограничения/FilterSettings/filtersettings_generated1.JPG)
![](/images/pages/img/Ограничения/FilterSettings/filtersettings_generated2.JPG)

## Создание настройки "вручную" в AdmConsole
# Открыть списковую форму "Общие" -> "Настройки фильтров".
# Нажать на кнопку добавления объекта
# Появится форма
![](/images/pages/img/Ограничения/FilterSettings/filtersettings_before.JPG)
# Поля: 
#* `Name` - название настройки, 
#* `DataObjectView` - представление объекта, на которое накладывается ограничение
#* `Lookups` - список мастеров, иcпользуемых в представлении, для возможности построения ограничения по первичному ключу мастера. Отличие мастеровых атрибутов заключается в том, что для выбора значения поднимается списковая форма объекта, что дает более широкий круг возможностей (поиск, сортировка, наложение ограничений).
#** `DataObjectType` – тип объекта мастера
#** `Container` – путь к списковой форме объекта (например: IIS.MOB.UgStat.Справочники.КтоУстановилL, IIS.MOB.UgStat.Справочники(Forms))
#** `FieldsToView` – список свойств (через запятую, без пробела), которые будут отображаться при выборе значения мастера  для ограничения. Для простых справочников, которые не имеют мастеров, обычно используется свойство “Наименование”. Для других объектов перечень этих атрибутов должен составлять аналитик, либо же они должны быть указаны в постановке.
#* `Details` - список детейлов для фильтра.

При этом могут быть неявные детейлы. Неявным детейлом является любой несправочный объект, ссылающийся на объект, фильтр которого мы настраиваем.

Неявные детейлы должны указываться после явных. Порядок внутри этих групп должнен определять аналитик.
#** `Caption` – заголовок детейла
#** `DataObjectView` – [D-представление](d-view.html) детейла
#** `[ConnectMasterProp](Фильтрация-по-детейлам-мастера--connect-master-prop--owner-connect-prop.html)` – имя свойства, ссылающегося на класс мастера.
#** `[OwnerConnectProp](Фильтрация-по-детейлам-мастера--connect-master-prop--owner-connect-prop.html)` – имя свойства, ссылающегося на класс детейла.
Мастера детейлов должна быть также добавлены в список Lookups 
# После заполнения всех полей форма может выглядеть следующим образом:
![](/images/pages/img/Ограничения/FilterSettings/filtersettings_after.JPG)


## Задание настройки форме в дизайнере VS
Имя настройки, сохранённой в базе прикладной системы необходимо указать на списковой форме в компоненте `AdvLimit`. 
На списковой форме нужно выделить AdvLimitComponent и установить ему свойство "FilterSettingName".
![](/images/pages/img/Ограничения/FilterSettings/filtersettings_vs.JPG)

## Задание настройки форме в коде
Если списковая форма является универсальной формой (сгенерированного кода нет), то имя настройки фильтра можно указать в независимой форме в методе ('''применимо если на форме только один список'''): 
```cs
protected override ICSSoft.STORMNET.UI.IEditInitiator GetDpdForm()
{
// *** Start programmer edit section *** (ПроектL.GetDpdForm() start)

// *** End programmer edit section *** (ПроектL.GetDpdForm() start)
ICSSoft.STORMNET.Windows.Forms.Operations objOperations1 =
	ICSSoft.STORMNET.Windows.Forms.Operations.GetAllTrue();
ICSSoft.STORMNET.UI.UniWinListStandard form =
	new ICSSoft.STORMNET.UI.UniWinListStandard(new ICSSoft.STORMNET.UI.ObjectListViewInformation[]{
new ICSSoft.STORMNET.UI.ObjectListViewInformation(ICSSoft.STORMNET.Information.GetView("ПроектL",
typeof (IIS.Звонки.Проект)),objOperations1, new System.Type[]{typeof (IIS.Звонки.Проект)}, null)}, "Проекты");
// *** Start programmer edit section *** (ПроектL.GetDpdForm() end)
form.FilterSettingName = "Проект";
// *** End programmer edit section *** (ПроектL.GetDpdForm() end))
return form;
}
```

строка `form.FilterSettingName = "Проект";` должна быть написана в [скобках программиста](programmer-brackets.html) (чтобы не потерять изменения при перегенерации).

## Пример

Пример использования AdvLimit и настройки FilterSettings можно посмотреть в [этой статье](filter-example.html)

