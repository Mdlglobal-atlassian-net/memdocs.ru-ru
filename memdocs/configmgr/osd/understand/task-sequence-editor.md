---
title: Использование редактора последовательности задач
titleSuffix: Configuration Manager
description: Сведения об использовании редактора последовательности задач в консоли Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a4e8bb56-ee85-49fd-8b1c-c8f513cec671
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2047ae9e276ac94b633d1dc30814ed641cd34d03
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691152"
---
# <a name="use-the-task-sequence-editor"></a>Использование редактора последовательности задач

*Область применения: Configuration Manager (Current Branch)*

Измените последовательность задач в консоли Configuration Manager, используя **редактор последовательности задач**. Используйте редактор, чтобы:  

- открывать представление последовательности задач в режиме только для чтения;

- добавлять шаги в последовательность задач и удалять их;  

- изменять порядок шагов в последовательности задач;  

- добавлять или удалять группы шагов;  

- копировать и вставлять шаги между последовательностями задач;

- задавать параметры шагов, например будет ли продолжаться выполнение последовательности задач в случае возникновения ошибки;  

- добавлять условия в шаги и группы последовательности задач.  

- Копирование и вставка условий между шагами в последовательности задач

- выполнять поиск по последовательности задач, чтобы быстро находить шаги.

Прежде чем изменить последовательность задач, ее необходимо создать. Дополнительные сведения см. в статье [Создание последовательностей задач и управление ими](../deploy-use/manage-task-sequences-to-automate-tasks.md).

## <a name="about-the-task-sequence-editor"></a>Сведения о редакторе последовательности задач

Редактор последовательности задач включает следующие компоненты.

![Снимок экрана с заметками: пример окна редактора последовательности задач](media/task-sequence-editor.png)

<!-- The following numbered steps correspond to annotations in the above screenshot. Don't change the step numbers without also revising the image! -->

1. Имя последовательности задач
2. Поиск. Дополнительные сведения см. в разделе [Поиск](#bkmk_search).
3. **Свойства** для выбранной группы или шага в последовательности

    Дополнительные сведения о свойствах и параметрах конкретного шага см. в разделе [О шагах последовательности задач](task-sequence-steps.md).

4. **Параметры** для выбранной группы или шага в последовательности

    Дополнительные сведения об общих параметрах всех шагов или параметрах конкретного шага см. в разделе [О шагах последовательности задач](task-sequence-steps.md).

    Дополнительные сведения о настройке условий см. в разделе [Условия](#bkmk_conditions).

5. **Добавление** группы или шагов
6. **Удаление** группы или шагов
7. Свертывание или развертывание всех групп
8. Изменение положения группы или шага в последовательности (переместить вверх, переместить вниз)
9. Последовательность задач:
    - Просмотр порядка шагов и групп.
    - Развертывание или свертывание группы.
    - При отключении шага или группы в **параметрах** они выделяются серым цветом в последовательности.
    - Значок шага изменится на красную ошибку, если с шагом возникла проблема. Например, отсутствует обязательное значение.
10. **OK**: сохранить и закрыть
11. **Отмена**: закрыть без сохранения изменений
12. **Применить**: сохранить изменения и не закрывать

Изменить размер редактора последовательности задач можно с помощью стандартных элементов управления Windows. Чтобы изменить ширину двух основных панелей, с помощью мыши выберите полосу между последовательностью задач и свойствами шага, а затем перетащите ее влево или вправо.

## <a name="view-a-task-sequence"></a><a name="bkmk_view"></a> Просмотр последовательности задач

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**, разверните узел **Операционные системы** и выберите **Последовательности задач**.  

2. В списке **Последовательность задач** выберите последовательность задач, которую требуется просмотреть.  

3. На вкладке **Главная** в ленте выберите в группе **Последовательность задач** действие **Просмотреть**.

    > [!TIP]
    > Это действие по умолчанию. Если дважды щелкнуть последовательность задач, вы сможете **просмотреть** ее.

Это действие открывает редактор последовательности задач в режиме только для чтения. В этом режиме возможно осуществление приведенных ниже действий.

- Просмотр всех групп, шагов, свойств и параметров
- Развертывание и свертывание групп
- Поиск последовательности задач
- Изменение размера окна редактора

В этом режиме только для чтения нельзя вносить изменения, включая копирование шага или условия. Это действие не блокирует последовательность задач для изменения. Дополнительные сведения об этих блокировках см. в разделе [Снятие блокировки на изменение последовательностей задач](#bkmk_sedo).

Чтобы внести изменения в последовательность задач, закройте редактор последовательности задач, открытый в режиме только для чтения. Затем выберите [Редактировать](#bkmk_edit) последовательность задач.

> [!NOTE]  
> Во время просмотра или редактирования последовательности задач, созданной мастером создания последовательности задач, отображается имя шага, которое может быть действием шага или типом шага. Например, можно увидеть шаг с именем "Создать разделы на диске 0", являющийся действием для шага с типом [Отформатировать диск и создать разделы](task-sequence-steps.md#BKMK_FormatandPartitionDisk). Все шаги последовательности задач документируются по своему *типу*, что не всегда совпадает с отображаемыми в редакторе именами шагов.  

## <a name="edit-a-task-sequence"></a><a name="bkmk_edit"></a> Изменение последовательности задач

Используйте следующую процедуру для изменения существующей последовательности задач.  

1. В консоли Configuration Manager перейдите к рабочей области **Библиотека программного обеспечения**, разверните узел **Операционные системы** и выберите **Последовательности задач**.  

2. В списке **Последовательность задач** выберите последовательность задач, которую требуется отредактировать.  

3. На вкладке **Главная** в ленте выберите в группе **Последовательность задач** действие **Редактировать**. Затем выполните одно из следующих действий.  

    - **Добавление шага**. Выберите **Добавить**, выберите категорию, а затем выберите шаг для добавления. Например, чтобы добавить шаг [выполнения из командной строки](task-sequence-steps.md#BKMK_RunCommandLine), щелкните **Добавить**, выберите категорию **Общие**, а затем — **Выполнить из командной строки**. Это действие добавляет шаг после текущего выбранного шага.

    - **Добавление группы**. Выберите **Добавить**, а затем **Создать группу**. После добавления группы добавьте в нее шаги.  

    - **Изменение порядка**. Выберите шаг или группу, порядок которых хотите изменить. Затем используйте значки **Вверх** или **Вниз**. Одним действием можно переместить только один шаг или группу. Эти действия также доступны, если щелкнуть правой кнопкой мыши группу или шаг.

        Можно вырезать, копировать и вставлять группу или шаг. Щелкните элемент правой кнопкой мыши и выберите действие. Для каждого действия можно также использовать стандартные сочетания клавиш.

        - Вырезать: **CTRL** + **X**
        - Копировать: **CTRL** + **C**
        - Вставить: **CTRL** + **V**

    - **Удалить шаг или группу**. Выберите шаг или группу и щелкните **Удалить**.  

4. Щелкните **ОК**, чтобы сохранить изменения и закрыть это окно. Щелкните **Отмена**, чтобы отменить изменения и закрыть окно. Щелкните **Применить**, чтобы сохранить изменения и оставить редактор последовательности задач открытым.  

Список доступных шагов последовательности задач см. в статье [Шаги последовательности задач](task-sequence-steps.md).  

> [!IMPORTANT]  
> Если после редактирования в последовательности задач появятся несвязанные ссылки на объекты, редактор потребует исправить такие ссылки перед закрытием. Вы можете выбрать следующие варианты действий:  
>
> - исправить проблемную ссылку;
> - удалить из последовательности задач объект, на который нет ссылок;  
> - временно отключить проблемный шаг последовательности задач, пока не появится возможность исправить или удалить нерабочую ссылку.  

Одновременно можно открыть несколько экземпляров редактора последовательности задач. Такое поведение позволяет сравнивать несколько последовательностей задач, а также копировать и вставлять шаги между ними. Можно **изменить** одну последовательность задач и **просмотреть** другую, но нельзя выполнять оба действия с одной и той же последовательностью задач.

## <a name="conditions"></a><a name="bkmk_conditions"></a> Условия

Используйте условия для управления поведением последовательности задач. Условия можно добавить в один шаг или группу шагов. Последовательность задач оценивает условия перед выполнением шага на устройстве. Она выполняет шаг только в том случае, если условия оцениваются как true. Если условие оценивается как false, последовательность задач пропускает группу или шаг.

Используйте вкладку **Параметры** для управления условиями:

![Управление условиями на вкладке "Параметры" в редакторе последовательности задач](media/4621098-copy-paste-ts-condition.png)

Доступны следующие типы условий.

- **Оператор if**. Используйте оператор *if* для группирования условий. Можно оценить **Все условия**, **Любое условие** или **Никакие**.

- **Переменная последовательности задач**. Оцените текущее значение любой встроенной, пользовательской, доступной только для чтения или связанной с действием [переменной последовательности задач](task-sequence-variables.md) в среде последовательности задач. Дополнительные сведения см. в разделе [Условия шагов](using-task-sequence-variables.md#bkmk_access-condition).

    > [!NOTE]
    > В этом условии можно использовать переменную массива, но необходимо указать конкретный элемент массива. Например, `OSDAdapter0EnableDHCP` указывает, активирует ли *первый* сетевой адаптер DHCP. Дополнительные сведения см. в статье [Переменные массива](using-task-sequence-variables.md#bkmk_array).

- **Версия ОС**. Оцените версию ОС устройства, на котором выполняется последовательность задач. Этот список представляет собой общие версии ОС, используемые в Configuration Manager. Чтобы оценить более подробную версию ОС, например определенную версию Windows 10, используйте условие **Запрос WMI**.

- **Язык ОС**. Оцените язык ОС устройства, на котором выполняется последовательность задач. Этот список включает 257 языков, поддерживаемых Windows.

- **Свойства файла**. Оцените версию или метку времени любого файла на устройстве, где выполняется последовательность задач.

- **Свойства папки**. Оцените метку времени любой папки на устройстве, где выполняется последовательность задач.

- **Параметр реестра**. Оцените значение раздела реестра на устройстве, где выполняется последовательность задач.

- **Запрос WMI**. Укажите пространство имен и запрос для вычисления на устройстве, где выполняется последовательность задач.

- **Установленное ПО**. Укажите файл установщика Windows, чтобы загрузить сведения о продукте для сопоставления на устройстве, где выполняется последовательность задач. Можно выполнить сопоставление с конкретным продуктом или с любой версией продукта.

### <a name="cmdlets-for-conditions"></a>Командлеты для условий

Для управления этими условиями используйте следующие командлеты PowerShell.<!-- SCCMDocs #1118 -->

- [Get-CMTSStepConditionFile](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFile?view=sccm-ps)
- [Get-CMTSStepConditionFolder](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionFolder?view=sccm-ps)
- [Get-CMTSStepConditionIfStatement](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionIfStatement?view=sccm-ps)
- [Get-CMTSStepConditionOperatingSystem](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionOperatingSystem?view=sccm-ps)
- [Get-CMTSStepConditionQueryWmi](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionQueryWmi?view=sccm-ps)
- [Get-CMTSStepConditionRegistry](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionRegistry?view=sccm-ps)
- [Get-CMTSStepConditionSoftware](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionSoftware?view=sccm-ps)
- [Get-CMTSStepConditionVariable](https://docs.microsoft.com/powershell/module/configurationmanager/Get-CMTSStepConditionVariable?view=sccm-ps)

### <a name="copy-and-paste-conditions"></a>Условия копирования и вставки

<!-- 4621098 -->

Чтобы повторно использовать условия одного шага в другом, начиная с версии 1910, можно скопировать и вставить условия в редакторе последовательности задач. Выберите условие, которое нужно вырезать или скопировать. Если условие имеет дочерние элементы, будет скопирован весь блок. Если в буфере обмена есть условие, его можно вставить, используя следующие параметры:

- "Вставить до";
- Paste after (Вставить после);
- Paste under (Вставить в) (применяется только к вложенным условиям).

Используйте стандартные сочетания клавиш, чтобы скопировать (**CTRL** + **C**) и вырезать (**CTRL** + **X**). Стандартное сочетание клавиш **CTRL** + **V** выполняет действие **Paste after** (Вставить после).

Существуют также новые параметры для перемещения условий вверх или вниз по списку.

> [!Note]  
> Вы можете копировать и вставлять условия между шагами в последовательности задач. Это действие не поддерживается между разными последовательностями задач.

## <a name="reclaim-lock-for-editing"></a><a name="bkmk_sedo"></a> Снятие блокировки на редактирование

<!--3699337-->
Если консоль Configuration Manager перестает отвечать на запросы, внесение изменений может быть заблокировано на 30 минут. Эта блокировка является одним из механизмов системы SEDO (сериализованное изменение распределенных объектов) в Configuration Manager. Дополнительные сведения см. в статье [Система SEDO в Configuration Manager](../../develop/core/understand/sedo.md).

Начиная с версии 1906, можно снять блокировку с последовательности задач. Это действие применяется только к заблокированной учетной записи пользователя и только на устройстве, на котором сайт установил блокировку. При попытке доступа к заблокированной последовательности задач теперь можно **отменить изменения** и продолжить изменять объект. Когда срок действия блокировки завершится, эти изменения в любом случае будут потеряны.

> [!TIP]
> Начиная с версии 1910 вы можете снять блокировку с любого объекта в консоли Configuration Manager. Дополнительные сведения см. в статье [Использование консоли Configuration Manager](../../core/servers/manage/admin-console.md#bkmk_sedo).<!--4786915-->

## <a name="search"></a><a name="bkmk_search"></a> Поиск

<!-- 4621085 -->

В последовательности задач с большим количеством групп и шагов найти конкретные шаги бывает непросто. Начиная с версии 1910, вы можете осуществлять поиск в редакторе последовательности задач. Она позволяет быстрее находить в последовательности требуемые шаги.

![Поиск в редакторе последовательности задач](media/4621085-task-sequence-search.png)

Введите слово для поиска. Вы можете ограничить область поиска, используя следующие типы.

- Имя шага
- Описание шага
- Тип шага
- Имя группы
- Описание группы
- Имя переменной
- Условия
- Другое содержимое, например строки со значениями переменных или строки команд

По умолчанию включаются все области.

Вы также можете отфильтровать все шаги со следующими атрибутами:

- Продолжать при ошибке
- Содержит условия

По умолчанию не включается ни один фильтр.

Шаги, соответствующие условиям поиска, выделяются в окне редактора желтым цветом.

Вы можете быстро переходить к этим полям поиска и перемещаться по результатам, используя следующие сочетания клавиш:

- **CTRL** + **F**: ввод строки поиска
- **CTRL** + **O**: выбор параметров поиска для ограничения области результатов
- **F3** или **ВВОД**: переход вперед по результатам
- **SHIFT** + **F3**: переход назад по результатам

## <a name="see-also"></a>См. также

- [Создание последовательностей задач и управление ими](../deploy-use/manage-task-sequences-to-automate-tasks.md)

- [Сведения о шагах последовательности задач](task-sequence-steps.md)

- [Создание переменных последовательности задач](using-task-sequence-variables.md)

- [Использование консоли Configuration Manager](../../core/servers/manage/admin-console.md)