---
title: Создание коллекций
titleSuffix: Configuration Manager
description: Создавайте коллекции в Configuration Manager, чтобы упростить управление группами пользователей и устройств.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3f178b41fbb305ef938063bd9b9743daa6b5c69
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695342"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Создание коллекций в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Коллекции — это группы пользователей или устройств. Коллекции можно использовать для таких задач, как управление приложениями, развертывание параметров соответствия и установка обновлений программного обеспечения. Кроме того, вы можете использовать коллекции для управления группами параметров клиентов. Совместное использование с ролевым администрированием позволяет указать ресурсы, к которым может получать доступ пользователь с правами администратора. Configuration Manager содержит несколько встроенных коллекций. Дополнительные сведения см. в разделе [Общие сведения о коллекциях](introduction-to-collections.md).  

> [!NOTE]  
> Коллекция может содержать либо пользователей, либо устройства. Смешанные коллекции не поддерживаются.  


В этой статье приведены сведения о создании коллекций в Configuration Manager. Кроме того, можно импортировать коллекции, созданные на этом или другом сайте Configuration Manager. Дополнительные сведения об экспорте и импорте коллекций см. в статье [Управление коллекциями в Configuration Manager](manage-collections.md).  


## <a name="collection-rules"></a>Правила коллекции

В Configuration Manager существуют различные типы правил, которые можно использовать для настройки членства в коллекции.  


### <a name="direct-rule"></a>Прямое правило

Прямые правила позволяют выбирать пользователей или компьютеры, которые требуется добавить в коллекцию. Членство этого типа не изменяется, если только вы не удалите ресурс из Configuration Manager. Прежде чем ресурсы можно будет добавлять в коллекцию с правилами непосредственного членства, Configuration Manager должен выполнить обнаружение ресурсов или их необходимо импортировать вручную. Коллекции с прямыми правилами предполагают более высокие административные временные затраты по сравнению с коллекциями с правилами запросов, так как они требуют внесения изменений вручную.


### <a name="query-rule"></a>Правило запроса

Позволяет динамически обновлять членство в коллекции на основе запроса, выполняемого Configuration Manager по расписанию. Например, можно создать коллекцию пользователей, которые являются членами подразделения "Кадры" в доменных службах Active Directory. Такая коллекция обновляется автоматически при добавлении новых пользователей в подразделение "Кадры" или их удалении из него.

Примеры запросов для создания коллекций см. в статье [Создание запросов в System Center Configuration Manager](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Правило категории устройств

Вы может упростить управление устройствами, сопоставив категории устройств с коллекциями устройств. 

Дополнительные сведения см. в статье [Автоматическое разбиение устройств по коллекциям с помощью System Center Configuration Manager](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Правило включения коллекции

Позволяет включать членов другой коллекции в коллекцию Configuration Manager. Если включенная коллекция изменилась, Configuration Manager обновляет членство в текущей коллекции по расписанию.

Вы можете добавить в коллекцию несколько правил включения коллекции.


### <a name="exclude-collection-rule"></a>Правило исключения коллекции

Правило исключения коллекции позволяет исключать члены другой коллекции из коллекции Configuration Manager. Если исключенная коллекция изменилась, Configuration Manager обновляет членство в текущей коллекции по расписанию.

Вы можете добавить в коллекцию несколько правил исключения коллекции. Если к коллекции применяются правила включения и исключения коллекции и между ними возникает конфликт, приоритетным является правило исключения.

#### <a name="example"></a>Пример
Вы создаете коллекцию, которая имеет одно правило включения коллекции и одно правило исключения коллекции. Правило включения коллекции предназначено для коллекции настольных систем Dell. Правило исключения коллекции создается для коллекции компьютеров, имеющих менее 4 ГБ ОЗУ. В состав новой коллекции войдут настольные компьютеры Dell, имеющие не менее 4 ГБ ОЗУ.



## <a name="create-a-collection"></a><a name="bkmk_create"></a> Создание коллекции  

1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**.  

    - Чтобы создать *коллекцию устройств*, выберите узел **Коллекции устройств**. Затем на вкладке ленты **Главная** в группе **Создать** выберите **Создать коллекцию устройств**.  

    - Чтобы создать *коллекцию пользователей*, выберите узел **Коллекции пользователей**. Затем на вкладке ленты **Главная** в группе **Создать** выберите **Создание коллекции пользователей**.  

2. На странице мастера **Общие** заполните поля **Имя** и **Комментарий**. В разделе **Ограничивающая коллекция** выберите **Обзор** и укажите ограничивающую коллекцию. Создаваемая коллекция будет содержать только члены ограничивающей коллекции.  

4. На странице **Правила членства в коллекции** в списке **Добавить правило** выберите тип правила членства, которое будет использоваться для этой коллекции. Для каждой коллекции можно настроить несколько правил. Настройки правил различаются. Дополнительные сведения о настройке каждого правила см. в следующих разделах статьи:  
    - [Прямое правило](#bkmk-direct)
    - [Правило запроса](#bkmk-query)
    - [Правило категории устройств](#bkmk-category)
    - [Правило включения коллекции](#bkmk-include)
    - [Правило исключения коллекции](#bkmk-exclude)

5. На странице **Правила членства в коллекции** также проверьте приведенные ниже параметры.

    - **Использовать добавочные обновления для этой коллекции**. Выберите этот параметр, чтобы периодически выполнять поиск и обновление только новых или измененных ресурсов на основе предыдущей оценки коллекции. Этот процесс не зависит от выполнения полной оценки коллекции. По умолчанию добавочные обновления выполняются каждые 5 минут.  

        > [!IMPORTANT]  
        >  Добавочные обновления не поддерживаются коллекциями с правилами запроса, в которых используются следующие классы:  
        >   
        > -   SMS_G_System_CollectedFile,  
        > -   SMS_G_System_LastSoftwareScan,  
        > -   SMS_G_System_AppClientState,  
        > -   SMS_G_System_DCMDeploymentState,  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails,  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails,  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails,  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (только для коллекций пользователей),  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (только для коллекций пользователей),  
        > -   SMS_G_System_SoftwareUsageData,  
        > -   SMS_G_System_CI_ComplianceState,  
        > -   SMS_G_System_EndpointProtectionStatus,  
        > -   SMS_GH_System_*,  
        > -   SMS_GEH_System_*.  

    - **Запланировать полное обновление этой коллекции**. Этот параметр позволяет запланировать регулярную полную оценку членства в коллекции.  

        Начиная с версии 1810 в оценке коллекции произошли следующие изменения, повышающие производительность сайта:<!--3607726-->  

        - Ранее, когда вы настраивали расписание для коллекции на основе запроса, сайт продолжал вычислять запрос независимо от значения параметра **Запланировать полное обновление этой коллекции**. Чтобы полностью отключить расписание, приходилось отключать расписание (значение **Нет**).

            Теперь сайт автоматически очищает расписание при отключении этого параметра. Чтобы задать расписание для оценки коллекции, включите параметр **Запланировать полное обновление этой коллекции**.  

            При обновлении сайта включается параметр **Запланировать полное обновление этой коллекции** во всех существующих коллекциях, для которых вы указали расписание. Такая конфигурация не всегда соответствует потребностям, но зато она совпадает с фактическом поведением расписания перед обновлением сайта. Чтобы остановить оценку коллекций по расписанию, отключите этот параметр для сайта.  

        - Вы не можете отключить оценку для встроенных коллекций, например **Все системы**, но теперь вы можете настроить для них расписание. Это позволяет запланировать оценку на определенное время в соответствии с вашими требованиями. 

            > [!TIP]  
            > Изменяйте в пользовательских расписаниях для встроенных коллекций только параметр **Время**. Не изменяйте параметр **Шаблон повторений**. Для следующих итераций может задаваться определенный шаблон повторений.  

6. Следуйте указаниям мастера, чтобы завершить создание новой коллекции. Созданная коллекция отображается в узле **Коллекции устройств** рабочей области **Активы и соответствие** .  

> [!NOTE]  
> Необходимо обновить или повторно загрузить консоль Configuration Manager, чтобы отобразить члены коллекции. Они не отображаются в коллекции до первого запланированного обновления. Можно также вручную выполнить действие **Обновить членство** для коллекции. Для завершения обновления коллекции может потребоваться несколько минут.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> Настройка прямого правила  

1. На странице **Поиск ресурсов** **мастера создания статических правил членства в коллекции** укажите приведенные ниже сведения.  

    - **Класс ресурсов**: в списке выберите тип ресурсов, которые требуется найти и добавить в коллекцию. Пример.
        - **Системный ресурс**. Поиск данных инвентаризации, возвращенных с клиентских компьютеров.
        - **Неизвестный компьютер**. Возможность выбора значений, возвращенных неизвестными компьютерами.
        - **Пользователь (ресурс)** . Поиск сведений о пользователе, собранных Configuration Manager.
        - **Группа пользователей (ресурс)** . Поиск сведений о группе пользователей, собранных Configuration Manager.

    - **Имя атрибута**: выберите атрибут, связанный с выбранным классом ресурсов, поиск которого требуется выполнить. Пример.  

        - Чтобы выбрать компьютеры по их NetBIOS-именам, выберите в списке **Класс ресурсов** вариант **Системный ресурс**, а в списке **Имя атрибута** — **NetBIOS-имя**.  

        - Чтобы выбрать пользователей по названию их подразделения, выберите в списке **Класс ресурсов** вариант **Пользователь (ресурс)** , а в списке **Имя атрибута** — **Имя подразделения пользователя**.  

    - **Исключить ресурсы, помеченные как устаревшие**. Если клиентский компьютер помечен как устаревший, он не будет отображаться в результатах поиска.  

    - **Исключить ресурсы без установленного клиента Configuration Manager**. Такие ресурсы не будут отображаться в результатах поиска.  

    - **Значение**. Введите значение, которое требуется найти для выбранного имени атрибута. В качестве подстановочного знака используйте символ процента (%). Пример.  
        - Чтобы найти компьютеры, NetBIOS-имя которых начинается с буквы "M", введите **M%** в этом поле.  
        - Чтобы найти пользователей в подразделении Contoso, введите **Contoso** в этом поле.

2. На странице **Выбранные ресурсы** выберите в списке **Ресурсы** ресурсы, которые требуется добавить в коллекцию, а затем нажмите кнопку **Далее**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> Настройка правила запроса  

В диалоговом окне **Свойства правил запросов** укажите приведенные ниже сведения.  

- **Имя** — укажите уникальное имя для запроса.  

- **Импортировать инструкцию запроса**. Появится диалоговое окно **Обзор запроса**. Выберите [Configuration Manager query](../../../servers/manage/create-queries.md) (Запрос Configuration Manager) в качестве правила запроса для коллекции.   

- **Класс ресурсов**: в списке выберите тип ресурсов, которые требуется найти и добавить в коллекцию. Выберите значение со списка **Системный ресурс**, чтобы выполнить поиск данных инвентаризации, возвращенных с клиентских компьютеров, или **Неизвестный компьютер**, чтобы выбрать значения, возвращенные неизвестными компьютерами.  

- **Изменить инструкцию запроса**. Появится диалоговое окно **Свойства формы запроса**, в котором можно создать запрос, используемый в качестве правила для коллекции. Дополнительные сведения о запросах см. в статье [Общие сведения о запросах в System Center Configuration Manager](../../../servers/manage/introduction-to-queries.md).  

        
        > [!TIP]  
        > On the General tab, selecting the checkbox to **Omit duplicate rows (select distinct)** may result in less rows returned and potentially quicker results. 

### <a name="device-category-rule"></a><a name="bkmk-category"></a> Правило категории устройств

В окне **Выберите категории устройств** доступны приведенные ниже действия.

- **Создать**. Укажите имя, чтобы создать категорию.
- **Переименовать**. Переименуйте выбранную категорию.
- **Удалить**: Удалите одну или несколько категорий из списка, выбрав их.

Дополнительные сведения см. в статье [Автоматическое разбиение устройств по коллекциям с помощью System Center Configuration Manager](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> Настройка правила включения коллекции  

В диалоговом окне **Выбор коллекций** выберите коллекции, которые требуется включить в новую коллекцию, и нажмите кнопку **ОК**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> Настройка правила исключения коллекции  

В диалоговом окне **Выбор коллекций** выберите коллекции, которые требуется исключить из новой коллекции, и нажмите кнопку **ОК**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> Импорт коллекции  

При экспорте коллекции с сайта Configuration Manager сохраняет ее в виде MOF-файла. Эта процедура позволяет импортировать такой файл в базу данных сайта. Чтобы завершить ее, вам потребуется **создать** разрешения для класса коллекций.

> [!IMPORTANT]  
> - Убедитесь, что файл, который содержит только данные коллекции, получен из надежного источника и не был незаконно изменен.  
> 
> - Убедитесь, что файл экспортирован с сайта с такой же версией Configuration Manager.  

Дополнительные сведения об экспорте коллекций см. в статье [Управление коллекциями в Configuration Manager](manage-collections.md).


1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**. Выберите узел **Коллекции пользователей** или **Коллекции устройств**.  

2. На вкладке ленты **Главная** в группе **Создать** выберите **Импортировать коллекции**.  

3. На странице **Общие** **мастера импорта коллекций** нажмите кнопку **Далее**.  

4. На странице **Имя MOF-файла** выберите **Обзор**. Перейдите к MOF-файлу, который содержит данные импортируемой коллекции.  

5. Завершите работу мастера, чтобы импортировать коллекцию. Новая коллекция отображается в узле **Коллекции пользователей** или **Коллекции устройств** рабочей области **Активы и соответствие** . Обновите или повторно загрузите консоль Configuration Manager, чтобы увидеть члены недавно импортированной коллекции.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> Синхронизация результатов членства в коллекции с группами Azure Active Directory

<!--3607475-->
> [!Tip]  
> Эта функция появилась в версии 1906 [на стадии предварительного выпуска](../../../servers/manage/pre-release-features.md). Начиная с версии 2002, эта функция больше не считается функцией предварительной версии.  

Теперь вы можете включить синхронизацию членства в коллекциях с группой Azure Active Directory (Azure AD). Эта синхронизация позволяет использовать существующие локальные правила группирования в облаке, создавая членство в группах Azure AD на основе результатов членства в коллекции. Вы можете синхронизировать коллекции устройств. В группе Azure AD отображаются только устройства с записью Azure Active Directory. Поддерживаются устройства с гибридным присоединением к Azure AD и подключением к Azure Active Directory.

Синхронизация с Azure AD будет выполняться каждые пять минут. Это односторонний процесс — из Configuration Manager в Azure AD. Изменения, внесенные в Azure AD, не отражаются в коллекциях Configuration Manager, но и не перезаписываются со стороны Configuration Manager. Например, если в коллекции Configuration Manager есть два устройства, а в группе Azure AD есть три различных устройств, синхронизация группы Azure AD даст в результате пять устройств.


### <a name="prerequisites"></a>Предварительные условия

- [Управление облачными клиентами](../../../servers/deploy/configure/azure-services-wizard.md)
- [Обнаружение пользователя Azure Active Directory](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Создайте группу и установите владельца в Azure AD

1. Перейдите на страницу [https://portal.azure.com](https://portal.azure.com).
1. Перейдите к **Azure Active Directory** > **Группы** > **Все группы**.
1. Щелкните **Создать группу**, введите **Имя группы** и **Описание группы**.
1. Убедитесь, что **Тип членства** **назначено**.
1. Выберите **Владельцы**, а затем добавьте идентификатор, который создаст связь синхронизации в Configuration Manager.
1. Нажмите кнопку **Создать**, чтобы завершить создание группы Azure AD.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Включение синхронизации коллекций для службы Azure

1. В консоли Configuration Manager последовательно выберите **Администрирование** > **Обзор** > **Облачные службы** > **Службы Azure**.
1. Щелкните правой кнопкой мыши арендатор Azure AD, в котором была создана группа, и выберите пункт **Свойства**.
1. На вкладке **Синхронизация коллекции** установите флажок **Включить синхронизацию группы каталогов Azure**.
1. Нажмите **ОК**, чтобы сохранить параметры.

### <a name="enable-the-collection-to-synchronize"></a>Включение синхронизации коллекции

1. В консоли Configuration Manager перейдите в раздел **Активы и соответствие** > **Обзор** > **Коллекции устройства**.
1. Щелкните правой кнопкой мыши коллекцию для синхронизации, а затем выберите пункт **Свойства**. 
1. На вкладке **Синхронизация группы AAD** нажмите кнопку **Добавить**.
1. В раскрывающемся меню выберите пункт **Арендатор**, для которого была создана группа Azure AD.
1. Введите условия поиска в поле**Имя начинается с**, а затем нажмите кнопку **Поиск**.
  - При появлении запроса на вход используйте удостоверение, указанное для владельца группы Azure AD.
1. Выберите целевую группу, а затем нажмите кнопку **ОК**, чтобы добавить группу, и снова нажмите кнопку **ОК**, чтобы выйти из свойств коллекции.
1. Необходимо подождать около 5–7 минут, прежде чем можно будет проверить принадлежность к группам на портале Azure.
   - Чтобы запустить полную синхронизацию, щелкните правой кнопкой мыши коллекцию и выберите команду **Синхронизировать членство**.


### <a name="verify-the-azure-ad-group-membership"></a>Проверка членства в группе Azure AD

1. Перейдите на страницу [https://portal.azure.com](https://portal.azure.com).
1. Перейдите к **Azure Active Directory** > **Группы** > **Все группы**.
1. Найдите созданную группу и выберите **Члены**. 
1. Убедитесь, что члены группы отображаются в коллекции Configuration Manager.
   - В группе будут отображаться только устройства с удостоверением Azure AD.


![Синхронизация коллекций в Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Использование PowerShell

С помощью PowerShell вы можете создавать и импортировать коллекции. Дополнительные сведения см. на странице

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Дальнейшие шаги

[Управление коллекциями](manage-collections.md)