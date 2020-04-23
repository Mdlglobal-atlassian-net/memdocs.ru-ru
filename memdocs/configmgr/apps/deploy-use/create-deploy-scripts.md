---
title: Создание и выполнение сценариев
titleSuffix: Configuration Manager
description: Вы можете создавать и выполнять сценарии PowerShell на клиентских устройствах.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1c15106eeecdac0377900d913160bc23614327db
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689662"
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Создание и запуск скриптов PowerShell из консоли Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

<!--1236459-->
В Configuration Manager имеется интегрированная возможность выполнения сценариев PowerShell. PowerShell позволяет создавать сложные автоматизированные сценарии, которые могут применяться в рамках большого сообщества. Скрипты упрощают создание специальных инструментов для администрирования программного обеспечения, а также ускоряют выполнение повседневных задач, позволяя вам быстрее справляться с большим объемом работы и обеспечивать более согласованный результат.  

> [!Note]  
> По умолчанию в Configuration Manager эта дополнительная функция отключена. Перед использованием ее необходимо включить. Дополнительные сведения см. в разделе [Включение дополнительных функций из обновлений](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  


Благодаря такой интеграции в Configuration Manager вы можете использовать функцию *Выполнение сценариев* для выполнения приведенных ниже действий.

- Создание и редактирование сценариев для использования с Configuration Manager.
- Управление использованием скриптов с помощью ролей и областей безопасности. 
- Выполнение сценариев для коллекций или отдельных локальных управляемых компьютеров Windows.
- Быстрое получение объединенных результатов сценария с клиентских устройств.
- Мониторинг выполнения сценария и просмотр результатов выходных данных сценария.

> [!WARNING]
> - Учитывая все возможности, которыми обладают сценарии, мы напоминаем, что применять их нужно с определенной долей осторожности и только в тех случаях, когда это оправдано. Чтобы помочь вам, мы предусмотрели дополнительные меры предосторожности — разделили роли и области. Обязательно проверяйте точность сценариев перед запуском, а также убедитесь, что они поступили из надежного источника, чтобы предотвратить выполнение непредусмотренного сценария. Учитывайте наличие символов национального алфавита или других обфускаций, а также изучайте аспекты обеспечения безопасности для сценариев. [Дополнительные сведения о безопасности сценариев PowerShell](learn-script-security.md)
> - Некоторое программное обеспечение для защиты от вредоносных программ может случайно активировать события для сценариев запуска Configuration Manager или функций CMPivot. Рекомендуется исключить %windir%\CCM\ScriptStore, чтобы программное обеспечение для защиты от вредоносных программ не мешало выполнению этих функций.

## <a name="prerequisites"></a>Предварительные условия

- Для запуска скриптов PowerShell на клиенте должна быть запущена оболочка PowerShell версии 3.0 или более поздней. Если сам сценарий содержит функциональные возможности, добавленные в более поздних версиях PowerShell, на клиенте, где этот сценарий выполняется, должна быть установлена соответствующая версия PowerShell.
- На клиентах Configuration Manager должен работать клиент версии 1706 или более поздней, чтобы выполнять сценарии.
- Чтобы использовать скрипты, необходимо быть членом соответствующей роли безопасности Configuration Manager.
- Чтобы импортировать или создавать сценарии, нужна учетная запись с разрешениями на **создание** **сценариев SMS**.
- Чтобы утверждать или отклонять сценарии, нужна учетная запись с разрешениями на **утверждение** **сценариев SMS**.
- Чтобы выполнять сценарии, нужна учетная запись с разрешениями на **выполнение сценариев** для **коллекций**.

Дополнительные сведения о ролях безопасности Configuration Manager см. в следующих статьях.</br>
[Области безопасности для выполнения сценариев](#security-scopes)</br>
[Роли безопасности для выполнения сценариев](#bkmk_ScriptRoles)</br>
[Основы ролевого администрирования](../../core/understand/fundamentals-of-role-based-administration.md)

## <a name="limitations"></a>Ограничения

Сейчас функция выполнения сценариев поддерживает следующее:

- Языки скриптов: PowerShell
- Типы параметров: integer, string и list.


>[!WARNING]
>Имейте в виду, что при использовании параметров открывается контактная зона для возможных атак путем внедрения кода PowerShell. Существуют различные способы устранения атак и решения проблем. Например, можно использовать регулярные выражения для проверки входных параметров или использовать предопределенные параметры. Рекомендуется не включать секреты в сценарии PowerShell (не применять пароли и т. д.). [Дополнительные сведения о безопасности сценариев PowerShell](learn-script-security.md) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Авторы и утверждающие функции выполнения сценариев

Функция выполнения сценариев использует концепцию *авторов сценариев* и *утверждающих сценариев* в качестве отдельных ролей для реализации и выполнения сценария. Разделение этих ролей позволяет осуществлять важные функциональные проверки. Дополнительная роль *средств выполнения скриптов*, которая разрешает выполнение скриптов, но запрещает их создание или утверждение. См. раздел [Создание ролей безопасности для сценариев](#bkmk_ScriptRoles).

### <a name="scripts-roles-control"></a>Управление ролями сценариев

По умолчанию пользователь не может утверждать созданные им скрипты. Благодаря мощи и гибкости скриптов, а также возможности их развертывания на множестве устройств вы можете делегировать создание и утверждение скриптов разным людям. Эти роли предоставляют дополнительный уровень защиты от бесконтрольного выполнения скриптов. Для упрощения тестирования вы можете отключить дополнительный уровень утверждения.

### <a name="approve-or-deny-a-script"></a>Утверждение или отклонение сценария

Прежде чем сценарий можно будет запустить, его должен утвердить пользователь с ролью *утверждающего сценария*. Чтобы утвердить скрипт, выполните следующее.

1. В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.
2. В рабочей области **Библиотека программного обеспечения** щелкните **Скрипты**.
3. В списке **Скрипт** выберите нужный скрипт для утверждения или отклонения, затем щелкните **Утвердить или отклонить** на вкладке **Главная** в группе **Скрипт**.
4. В диалоговом окне **Утверждение или запрет сценария** выберите действие **Утвердить** или **Отклонить**. При необходимости введите комментарий о решении.  Отклоненный скрипт не может выполняться на клиентских устройствах. <br>
![Утверждение скрипта](./media/run-scripts/RS-approval.png)
1. Завершите работу мастера. Вы видите, что в списке **Скрипт** изменилось значение в столбце **Состояние утверждения** в зависимости выбранного вами действия.

### <a name="allow-users-to-approve-their-own-scripts"></a>Предоставление пользователям разрешения самостоятельно утверждать свои скрипты

Это утверждение в основном используется на этапе тестирования при разработке сценариев.

1. В консоли Configuration Manager щелкните **Администрирование**.
2. В рабочей области **Администрирование** разверните узел **Конфигурация сайта**и выберите **Сайты**.
3. В списке сайтов выберите нужный сайт и на вкладке **Главная** в группе **Сайты** щелкните **Параметры иерархии**.
4. На вкладке **Общие** в диалоговом окне **Свойства параметров иерархии** снимите флажок **Авторам скриптов требуется утверждающий**.

>[!IMPORTANT]
>Рекомендуется не разрешать автору скрипта утверждать свои собственные скрипты. Это действие должно быть разрешено только в лабораторных условиях. Примите во внимание возможные последствия изменения этого параметра в рабочей среде.

## <a name="security-scopes"></a>Области безопасности
*(Появились в версии 1710)*  
Компонент выполнения сценариев использует существующую функцию Configuration Manager — области безопасности, чтобы управлять созданием и выполнением сценариев посредством присвоения тегов, представляющих группы пользователей. Дополнительные сведения об использовании областей безопасности см. в статье [Настройка ролевого администрирования для Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="create-security-roles-for-scripts"></a><a name="bkmk_ScriptRoles"></a> Создание ролей безопасности для сценариев
Три роли безопасности, используемые для выполнения скриптов, не созданы по умолчанию в Configuration Manager. Для создания средств выполнения сценариев, авторов сценариев и ролей утверждающих сценарии выполните приведенные далее действия.

1. В консоли Configuration Manager последовательно выберите **Администрирование** >**Безопасность** >**Роли безопасности**.
2. Щелкните роль правой кнопкой мыши и выберите команду **Копировать**. Копируемой роли уже назначены разрешения. Убедитесь, что выбраны только нужные разрешения. 
3. Для пользовательской роли заполните поля **Имя** и **Описание**. 
4. Назначьте роли безопасности разрешения, описанные ниже.  

### <a name="security-role-permissions"></a>Разрешения роли безопасности  

**Имя роли**. Средства выполнения скриптов.  
- **Описание**. Эти разрешения позволяют этой роли выполнять только те скрипты, которые были ранее созданы и утверждены другими ролями.  
- **Разрешения**. Задайте значение **Да** для следующих разрешений.  

|Категория|Разрешение|Состояние|
|---|---|---|
|Коллекция|Запуск скрипта|Да|
|Сайт|Чтение|Да|
|Сценарии SMS|Чтение|Да|


**Имя роли**. Авторы скриптов.  
- **Описание**. Эти разрешения позволяют этой роли создавать скрипты, но не утверждать или выполнять их.  
- **Разрешения.** Задайте следующие разрешения.
 
|Категория|Разрешение|Состояние|
|---|---|---|
|Коллекция|Запуск скрипта|Нет|
|Сайт|Чтение|Да|
|Сценарии SMS|Создание|Да|
|Сценарии SMS|Чтение|Да|
|Сценарии SMS|Удалить|Да|
|Сценарии SMS|Изменить|Да|


**Имя роли**. Утверждающие скрипты.  
- **Описание**. Эти разрешения позволяют этой роли утверждать скрипты, но не создавать или выполнять их.  
- **Разрешения**. Задайте следующие разрешения.  

|Категория|Разрешение|Состояние|
|---|---|---|
|Коллекция|Запуск скрипта|Нет|
|Сайт|Чтение|Да|
|Сценарии SMS|Чтение|Да|
|Сценарии SMS|Утверждение|Да|
|Сценарии SMS|Изменить|Да|

     
**Пример разрешений сценариев SMS для роли авторов сценариев**  

 ![Пример разрешений сценариев SMS для роли авторов сценариев](./media/run-scripts/script_authors_permissions.png)


## <a name="create-a-script"></a>Создание сценария

1. В консоли Configuration Manager щелкните **Библиотека программного обеспечения**.
2. В рабочей области **Библиотека программного обеспечения** щелкните **Скрипты**.
3. На вкладке **Главная** в группе **Создать** щелкните **Создать скрипт**.
4. На странице **Скрипт** в **мастере создания скрипта** настройте следующие параметры.
    - **Имя скрипта**. Введите здесь имя для скрипта. Вы можете создать несколько скриптов с одинаковыми именами, но повторы имен затруднят поиск нужного скрипта в консоли Configuration Manager.
    - **Язык скрипта**. Сейчас поддерживаются только скрипты PowerShell.
    - **Импорт**. Импорт скрипта PowerShell в консоли. Скрипт отображается в поле **Скрипт**.
    - **Очистить**. Удаление текущего скрипта из поля "Скрипт".
    - **Скрипт**. Отображение текущего импортируемого скрипта. В этом поле при необходимости вы можете изменять скрипт.
5. Завершите работу мастера. Новый скрипт отображается в списке **Скрипт** с состоянием **Ожидается утверждение**. Прежде чем выполнять такой скрипт на клиентских устройствах, его необходимо утвердить. 

> [!IMPORTANT]
> Избегайте сценариев перезагрузки устройства или агента Configuration Manager, если используете функцию выполнения сценариев. Это может вызвать состояние непрерывной перезагрузки. При необходимости воспользуйтесь улучшениями для функции уведомления клиента. Они позволяют перезагружать устройства начиная с версии Configuration Manager 1710. Используя [столбец ожидания перезагрузки](../../core/clients/manage/manage-clients.md#restart-clients), можно определить устройства, которым требуется перезагрузка. 
> <!--SMS503978  -->

## <a name="script-parameters"></a>Параметры сценария
*(Появились в версии 1710)*  
Добавление параметров в сценарий позволяет повысить гибкость работы. Можно включить до 10 параметров. Ниже описаны возможности указанного компонента по использованию параметров сценария для типов данных *String* и *Integer*. Кроме того, доступны списки предварительно заданных значений. Если сценарий имеет не поддерживаемые типы данных, выдается предупреждение.

В области **Сценарий** диалогового окна **Создать сценарий** щелкните элемент **Параметры сценария**.

Каждый из параметров сценария имеет отдельное диалоговое окно для добавления дополнительных сведений и проверки. Если в скрипте есть параметр по умолчанию, он будет перечислен в пользовательском интерфейсе параметра, чтобы вы могли настроить его. Configuration Manager не перезаписывает значение по умолчанию, так как скрипт напрямую не изменяется. Это похоже на предварительно заполненные предложенные значения, которые доступны в пользовательском интерфейсе, но Configuration Manager не предоставляет доступ к значениям по умолчанию во время выполнения. Такое поведение можно изменить, отредактировав скрипт так, чтобы он включал правильные значения по умолчанию. <!--17694323-->

>[!IMPORTANT]
> Значения параметров не могут содержать символ апострофа. </br></br>
> Есть известная проблема в Configuration Manager версии 1802, когда параметры с пробелами не передаются в скрипт должным образом. При использовании пробела только первый элемент в параметре передается в скрипт, а все компоненты после пробела не передаются. Администраторы могут решить эту проблему, заменяя пробелы другими символами с последующим преобразованием или используя другие методы.


### <a name="parameter-validation"></a>Проверка параметров

Для каждого параметра в сценарии доступно диалоговое окно **Script Parameter Properties** (Свойства параметра сценариев), где можно добавить проверку соответствующего параметра. После добавления проверки вы будете получать ошибки при вводе для параметра значения, не соответствующего условиям проверки.

#### <a name="example-firstname"></a>Пример: *FirstName*

В этом примере показана возможность задать свойства параметра строки *FirstName*.

![Параметры сценария — строка](./media/run-scripts/RS-parameters-string.png)


В разделе "Проверка" диалогового окна **Свойства параметра сценария** содержатся следующие поля:

- **Минимальная длина** — минимальное число символов поля *FirstName*.
- **Максимальная длина** — максимальное число символов поля *FirstName*.
- **Регулярное выражение** — *регулярное выражение*, которое используется. Дополнительные сведения об использовании регулярных выражений см. в следующем разделе *Использование проверки регулярных выражений*.
- **Настраиваемая ошибка** — позволяет добавить собственное настраиваемое сообщение об ошибке, которое заменяет любое системное сообщение об ошибке, обнаруженное при проверке.

#### <a name="using-regular-expression-validation"></a>Использование проверки регулярных выражений

Регулярное выражение — это краткая форма программного кода для проверки строки символов на валидность кодировки. Например, можно проверить отсутствие прописной буквы в поле *FirstName*, указав `[^A-Z]` в поле *Регулярное выражение*.

Обработка регулярных выражений для этого диалогового окна поддерживается .NET Framework. Рекомендации по использованию регулярных выражений см. в статье [Регулярные выражения .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions) и [Язык регулярных выражений](https://docs.microsoft.com/dotnet/standard/base-types/regular-expression-language-quick-reference).


## <a name="script-examples"></a>Примеры скриптов

Ниже приведены некоторые примеры сценариев, которые могут вас заинтересовать.

### <a name="create-a-new-folder-and-file"></a>Создание папки и файла

Этот сценарий создает папку и файл в ней с учетом указанных вами имен.

``` PowerShell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Получение данных о версии ОС

Этот скрипт использует инструментарий WMI, чтобы запросить у компьютера данные о версии ОС.

``` PowerShell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="edit-or-copy-powershell-scripts"></a><a name="bkmk_psedit"></a> Изменение или копирование сценариев PowerShell
<!--3705507-->
*(Появились в версии 1902)*  
Функции **Изменить** и **Копировать** доступны для скриптов PowerShell в рамках функции **Выполнение сценариев**. Больше не нужно повторно создавать сценарий, если его необходимо изменить. Можно просто отредактировать его. Для обоих действий используется тот же интерфейс мастера, что и при создании сценария. Когда вы изменяете или копируете сценарий, в Configuration Manager не сохраняется состояние утверждения.

> [!Tip]  
> Не изменяйте сценарий, который выполняется в клиентах. Иначе выполнение исходного сценария не будет завершено и вы можете не получить от этих клиентов ожидаемых результатов.  

### <a name="edit-a-script"></a>Изменение сценария

1. Перейдите к узлу **Сценарии** в рабочей области **Библиотека программного обеспечения**.
1. Выберите сценарий для изменения и нажмите кнопку **Изменить** на ленте. 
1. Измените или повторно импортируйте сценарий на странице **Сведения о сценарии**.
1. Нажмите **Далее**, чтобы просмотреть **Сводку**, затем **Закрыть** по завершении редактирования.

### <a name="copy-a-script"></a>Копирование сценария

1. Перейдите к узлу **Сценарии** в рабочей области **Библиотека программного обеспечения**.
1. Выберите сценарий для копирования, а затем щелкните **Копировать** на ленте.
1. Переименуйте сценарий в поле **Имя сценария** и внесите необходимые изменения.
1. Нажмите **Далее**, чтобы просмотреть **Сводку**, затем **Закрыть** по завершении редактирования.


## <a name="run-a-script"></a>Выполнить сценарий

Утвержденный скрипт можно выполнить в одной коллекции или на одном устройстве. После начала выполнения скрипт быстро запускается через высокоприоритетную систему, время ожидания которой истечет через час. Затем результаты сценария возвращаются с помощью системы сообщений о состоянии.

Чтобы выбрать коллекцию целевых сред для своего скрипта, сделайте следующее:

1. В консоли Configuration Manager щелкните элемент **Активы и соответствие**.
2. В рабочей области "Активы и соответствие" щелкните **Коллекции устройств**.
3. В списке **Коллекции устройств** выберите нужную коллекцию, в которой будет выполняться скрипт.
4. Выберите коллекцию по своему усмотрению и щелкните **Запуск сценария**.
5. На странице **Скрипт** мастера **запуска скрипта** выберите в списке нужный скрипт. Здесь отображаются только утвержденные скрипты.
6. Нажмите кнопку **Далее** и завершите работу мастера.

> [!IMPORTANT]
> Если скрипт не выполняется (например, если целевое устройство выключено) в течение часа, его нужно запустить снова.

### <a name="target-machine-execution"></a>Выполнение на целевом компьютере

Сценарий выполняется как учетная запись *системы* или *компьютера* на целевых клиентах. Такая учетная запись имеет ограниченный доступ к сети. Это следует учитывать при предоставлении сценарию доступа к удаленным системам и расположениям.

## <a name="script-monitoring"></a>Мониторинг сценариев

Запустив сценарий для коллекции устройств, используйте описанную ниже процедуру для наблюдения за этой операцией. Начиная с версии 1710, вы можете отслеживать выполнение скрипта в режиме реального времени, а также вернуться к отчету о конкретном выполнении. Данные о состоянии скрипта очищаются как часть [задачи удаления устаревших операций клиента](../../core/servers/manage/reference-for-maintenance-tasks.md) или удаления скрипта.<br>

![Монитор скрипта — состояние выполнения скрипта](./media/run-scripts/RS-monitoring-three-bar.png)

1. В консоли Configuration Manager щелкните элемент **Мониторинг**.
2. В рабочей области **Мониторинг** щелкните **Состояние скрипта**.
3. В списке **Состояние скрипта** можно просмотреть результаты для каждого скрипта, запущенного на клиентских устройствах. Обычно код выхода **0** означает, что скрипт выполнен успешно.
    - Начиная с Configuration Manager 1802 выходные данные сценария усекаются до 4 КБ для более удобного отображения.  <!--510013-->
   
   ![Монитор скрипта — усеченный скрипт](./media/run-scripts/Script-monitoring-truncated.png)

## <a name="script-output-in-1810"></a>Выходные данные скрипта в версии 1810

Теперь подробные выходные данные скрипта можно просматривать в необработанном виде или в структурированном формате JSON. Такое форматирование упрощает чтение и анализ выходных данных. Если сценарий возвращает допустимый текст в формате JSON, просматривать подробные сведения о выходных данных можно в **формате JSON** или в виде **необработанных выходных данных**. В противном случае единственный вариант — **выходные данные сценария**.

### <a name="example-script-output-is-valid-json"></a>Пример: выходные данные скрипта доступны в формате JSON
Команда: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

### <a name="example-script-output-isnt-valid-json"></a>Пример: выходные данные сценария недоступны в формате JSON
Команда: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```

- Клиенты с версией 1810 возвращают выходные данные объемом менее 80 КБ на сайт по быстрому коммуникационному каналу. Это изменение повышает производительность просмотра выходных данных сценариев или запросов.  

  - Если выходные данные сценария или запроса превышают 80 КБ, клиент отправляет данные через сообщение о состоянии.  
  - Клиенты до версии 1802 смогут и дальше использовать сообщения о состоянии.

## <a name="script-output-pre-1810"></a>Выходные данные скрипта в версиях, предшествующих 1810

- Начиная с Configuration Manager версии 1802 выходные данные сценария выводятся в формате JSON. Этот формат согласованно возвращает доступные для чтения выходные данные скрипта. 
- Скрипты с неизвестным результатом или скрипты, при выполнении которых клиент находился в автономном режиме, не отображаются в диаграммах или наборе данных. <!--507179-->
- Следует избегать больших выходных данных скрипта, так как они усекаются до 4 КБ. <!--508488-->
- При использовании Configuration Manager 1802 или более поздней версии с более ранней версией клиента некоторые функции форматирования выходных данных скрипта недоступны. <!--508487-->
    - Если вы используете клиент Configuration Manager версии ниже 1802, данные будут выводиться в строковом формате.
    -  В клиенте Configuration Manager версии 1802 и более поздних используется формат JSON.
        - Например, в одной версии клиента может быть возвращен результат TEXT, а в другой — "TEXT" (в двойных кавычках). Эти результаты будут выведены на диаграмме в разных категориях.
        - Чтобы обойти такое поведение, можно выполнить скрипт для двух разных коллекций. В одной из них будут представлены клиенты с версией, предшествующей 1802, а в другой — клиенты с версией 1802 и последующими. Также для правильного отображения скриптов в формате JSON можно преобразовать объект enum в строковое значение. 
- Для правильного отображения сценариев в формате JSON необходимо преобразовать объект enum в строковое значение. <!--508377-->

   ![Преобразование объекта enum в строковое значение](./media/run-scripts/enum-tostring-JSON.png)

## <a name="log-files"></a>Файлы журнала

Начиная с версии 1810, добавлены дополнительные функции ведения журнала для устранения неполадок.

- На клиенте по умолчанию в папке C:\Windows\CCM\logs:  
  - **Scripts.log**,  
  - **CcmMessaging.log**.  

- На точке управления по умолчанию в папке C:\SMS_CCM\Logs:
  - **MP_RelayMsgMgr.log**  

- На сервере сайта по умолчанию в папке C:\Program Files\Configuration Manager\Logs:
  - **SMS_Message_Processing_Engine.log**

## <a name="see-also"></a>См. также

- [Настройка ролевого администрирования для Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Основы ролевого администрирования](../../core/understand/fundamentals-of-role-based-administration.md)