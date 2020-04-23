---
title: Консоль Configuration Manager
titleSuffix: Configuration Manager
description: Сведения о навигации по консоли Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f6bcd0bc06721fbd6ea3ce1226867db522bb2560
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700342"
---
# <a name="how-to-use-the-configuration-manager-console"></a>Использование консоли Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Администраторы используют консоль Configuration Manager для управления средой Configuration Manager. В этой статье рассмотрены основы навигации по консоли.  

## <a name="open-the-console"></a><a name="bkmk_open"></a> Открытие консоли

Консоль Configuration Manager всегда устанавливается на каждом сервере сайта. Кроме того, ее можно установить на других компьютерах. Дополнительные сведения см. в статье [Установка консоли Configuration Manager](../deploy/install/install-consoles.md).

Проще всего открыть консоль на компьютере Windows 10: нажмите кнопку **Пуск** и начните вводить `Configuration Manager console`. Вам может оказаться достаточно ввести лишь часть строки для Windows, чтобы найти наилучшее соответствие.

Если вы открыли меню "Пуск", найдите значок **Консоль Configuration Manager** в группе **Microsoft Endpoint Manager**.

![Значки меню "Пуск" Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

> [!NOTE]
> В версии 1910 путь к меню "Пуск" изменился. В версии 1906 и более ранних папка называется **System Center**. При обновлении Configuration Manager до версии 1910 или более поздней обновите всю внутреннюю документацию, которую вы ведете, включив в нее это новое расположение.

## <a name="connect-to-a-site-server"></a>Подключение к серверу сайта

Консоль подключается к серверу сайта центра администрирования или к серверам первичного сайта. Консоль Configuration Manager нельзя подключить к вторичному сайту. Во время установки вы указываете полное доменное имя сервера сайта, к которому будет подключена консоль.

Чтобы подключиться к другому серверу сайта, используйте следующие шаги:

1. Щелкните стрелку в верхней части [ленты](#ribbon) и выберите команду **Подключение к новому сайту**.  

    ![Подключение консоли к новому сайту](media/connect-to-a-new-site.png)  

2. Введите полное доменное имя для сервера сайта. Если вы уже подключались к серверу сайта, выберите его в раскрывающемся списке.  

    ![Окно подключения сайта; введите полное доменное имя сервера сайта](media/site-server-fqdn.png)  

3. Выберите **Подключиться**.  

С версии 1810 вы можете указать минимально необходимый уровень аутентификации для доступа администраторов к сайтам Configuration Manager. Эта функция позволяет настроить для администраторов требование входить в Windows с определенным уровнем. Дополнительные сведения см. в разделе [Планирование использования поставщика SMS](../../plan-design/hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  

## <a name="navigation"></a>Навигация

Некоторые области в консоли могут не отображаться в зависимости от назначенной вам роли безопасности. Дополнительные сведения о ролях см. в разделе [Основы ролевого администрирования](../../understand/fundamentals-of-role-based-administration.md).

### <a name="workspaces"></a>Рабочие области

Консоль Configuration Manager имеет четыре **рабочие области**:  

- **Активы и соответствие**  

- **Библиотека программного обеспечения**  

- **Мониторинг**  

- **Администрирование**  

![Рабочие области Configuration Manager с контекстным меню](media/configuration-manager-workspaces.png)  

Измените порядок кнопок для рабочих областей, щелкнув стрелку вниз и выбрав пункт **Параметры области навигации**. Выберите элемент **Вверх** или **Вниз**. Нажмите кнопку **Сброс**, чтобы восстановить порядок кнопок по умолчанию.  

![Окно "Параметры панели переходов" для изменения порядка рабочих областей](media/navigation-pane-options.png)  

Можно свернуть кнопку рабочей области, выбрав параметр **Скрыть дополнительные кнопки**. Сначала уменьшается кнопка рабочей области, стоящая последней в списке. Нажав уменьшенную кнопку и выбрав **Показать дополнительные кнопки**, можно восстановить исходный размер кнопки.

![Свернутые рабочие области в консоли Configuration Manager](media/workspace-buttons.png)  

### <a name="nodes"></a>Узлы

Рабочие области представляют собой коллекцию **узлов**. Одним из примеров узла является узел **Группы обновлений программного обеспечения** в рабочей области **Библиотека программного обеспечения**.

После перехода к этому узлу можно щелкнуть стрелку, чтобы свернуть область навигации.  

![Пример узла, выделена стрелка "Свернуть"](media/software-update-groups-node.png)  

Когда область навигации свернута, для перемещения по консоли можно использовать **панель навигации**.  

![Свернутая область навигации Configuration Manager](media/minimized-navigation-pane.png)  

В консоли узлы иногда упорядочены по папкам. При выборе папки обычно отображается **индекс навигации** или **панель мониторинга**.  

![Указатель навигации для обновлений программного обеспечения Configuration Manager](media/software-updates-navigation-index.png)  

### <a name="ribbon"></a>Лента

Лента находится в верхней части консоли Configuration Manager. Она может содержать несколько вкладок и может быть свернута с помощью стрелки справа. Кнопки на ленте изменяются в зависимости от узла. Большинство кнопок на ленте также доступны и в контекстных меню.  

![Пример ленты, выделено несколько вкладок и стрелка "Свернуть"](media/ribbon.png)

### <a name="details-pane"></a>Область сведений

Дополнительную информацию об элементах можно получить в области сведений. Она может иметь одну или несколько вкладок. Вкладки зависят от узла.  

![Пример области сведений Configuration Manager](media/details-pane.png)

### <a name="columns"></a>Столбцы

Вы можете добавить, удалить, переупорядочить столбцы и изменить их размер. Эти действия позволяют отображать нужные вам данные. Доступные столбцы зависят от узла. Щелкните правой кнопкой мыши существующий заголовок столбца, а затем щелкните элемент, который нужно добавить или удалить в представлении. Чтобы изменить порядок столбцов, перетащите заголовок столбца на нужное место.  

![Добавление столбца в Configuration Manager](media/add-columns.png)  

В нижней части контекстного меню столбца можно выполнить сортировку или группирование по столбцу. Кроме того, можно выполнить сортировку по столбцу, щелкнув его заголовок.  

![Группирование по столбцу в Configuration Manager](media/column-group-by.png)  

## <a name="reclaim-lock-for-editing-objects"></a><a name="bkmk_sedo"></a> Снятие блокировки на объектов

<!--4786915-->

Если консоль Configuration Manager перестает отвечать на запросы, внесение изменений может быть заблокировано на 30 минут. Эта блокировка является одним из механизмов системы SEDO (сериализованное изменение распределенных объектов) в Configuration Manager. Дополнительные сведения см. в статье [Система SEDO в Configuration Manager](../../../develop/core/understand/sedo.md).

Начиная с версии [Current Branch 1906](../../plan-design/changes/whats-new-in-version-1906.md#reclaim-sedo-lock-for-task-sequences), можно было снять блокировку с последовательности задач. Начиная с версии 1910 вы можете снять блокировку с любого объекта в консоли Configuration Manager.

Это действие применяется только к заблокированной учетной записи пользователя и только на устройстве, на котором сайт установил блокировку. При попытке доступа к заблокированному объекту теперь можно **отменить изменения** и продолжить изменять объект. Когда срок действия блокировки завершится, эти изменения в любом случае будут потеряны.

## <a name="view-recently-connected-consoles"></a><a name="bkmk_viewconnected"></a> Просмотр недавно подключенных консолей

<!--3699367-->
Начиная с версии 1902 можно просматривать сведения о последних подключениях консоли Configuration Manager. В представлении отображаются сведения об активных и недавних подключениях. В списке всегда есть текущее подключение консоли и содержатся только подключения из консоли Configuration Manager. В нем нет подключений PowerShell или других подключений на основе SDK к поставщику SMS. Элементы старше 30 дней из списка удаляются.

### <a name="prerequisites-to-view-connected-consoles"></a><a name="bkmk_connections-prereq"></a> Предварительные требования для просмотра сведений о подключенных консолях

- У вашей учетной записи должно быть разрешение на **чтение** для объекта **SMS_Site**.

- Настройка REST API службы администрирования. Дополнительные сведения см. в разделе [Что такое служба администрирования?](../../../develop/adminservice/overview.md)

### <a name="view-connected-consoles"></a>Просмотр подключенных консолей

1. В консоли Configuration Manager перейдите к рабочей области **Администрирование**.  

2. Разверните узел **Безопасность** и выберите узел **Подключения консолей**.  

3. Для последних подключений доступны следующие свойства:  

    - Имя пользователя
    - Имя компьютера
    - Код подключенного сайта
    - Версия консоли
    - Время последнего подключения: когда пользователь *открывал* консоль в последний раз
    - Начиная с версии 1910 столбец **Последний пульс консоли** заменил столбец **Время последнего подключения**. <!--4923997-->
       - Открытая консоль на переднем плане отправляет пакет пульса каждые 10 минут.

![Просмотр подключений консоли Configuration Manager](media/console-connections.png)

## <a name="start-microsoft-teams-chat-from-console-connections"></a><a name="bkmk_message"></a> Запуск чата Microsoft Teams через подключения консоли
<!--4923997-->
*(Представлено в версии 1910)*

Начиная с версии 1910 вы можете отправлять сообщения другим администраторам Configuration Manager из узла **Подключения консолей** с помощью Microsoft Teams. Если вы выбираете **Запуск чата Microsoft Teams** с администратором, тогда открывается Microsoft Teams и чат с этим пользователем.

### <a name="prerequisites"></a>Предварительные условия

- Для запуска чата с администраторами учетная запись, с которой вы хотите запустить чат, должна быть обнаружена с помощью [Azure AD или Обнаружения пользователей AD](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Если на устройстве, с которого запускается консоль, установлен Microsoft Teams.
Примечание.
- Все [предварительные требования для просмотра сведений о подключенных консолях](#bkmk_connections-prereq)

### <a name="start-microsoft-teams-chat"></a>Запуск чата Microsoft Teams

1. Перейдите в **Администрирование** > **Безопасность** > **Подключения консоли**.
1. Щелкните правой кнопкой мыши консольное подключение пользователя и выберите пункт **Запуск чата Microsoft Teams**.
    - Если основное имя пользователя для выбранного администратора не найдено, **Запуск чата Microsoft Teams** отображается серым цветом.
    - Сообщение об ошибке, включая ссылку для скачивания, отображается, если Microsoft Teams не установлено на устройстве, с которого запускается консоль.
    - Если на устройстве, с которого запускается консоль, установлено Microsoft Teams, откроется чат с пользователем.

### <a name="known-issues"></a>Известные проблемы

Сообщение об ошибке, уведомляющее о том, что Microsoft Teams не установлено, не отображается, если следующий раздел реестра не существует:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Чтобы устранить эту ошибку, создайте раздел реестра вручную.

## <a name="configuration-manager-console-notifications"></a><a name="bkmk_notify"></a> Уведомления консоли Configuration Manager

<!--3556016, fka 1318035-->
Начиная с версии Configuration Manager 1902, консоль уведомляет вас о следующих событиях:

- Когда доступно обновление для Configuration Manager
- При возникновении событий жизненного цикла и обслуживания в среде

Это уведомление представляет собой панель в верхней части окна консоли под лентой. Он заменяет старый интерфейс, который использовался, когда появлялись обновления Configuration Manager. ти уведомления в консоли по-прежнему отображают критически важную информацию, но не мешают работе в консоли. Невозможно отменить критически важные уведомления. В консоли все уведомления отображаются в новой области уведомлений строки заголовка.

![Панель уведомлений и флаг в консоли](./media/1318035-notify-eval-version-expired.png)

### <a name="configure-a-site-to-show-non-critical-notifications"></a>Настройка сайта так, чтобы показывать и некритические уведомления

Можно настроить каждый сайт так, чтобы показывать и некритические уведомления в свойствах сайта.

1. В рабочей области **Администрирование** разверните элемент **Конфигурация сайта**, а затем выберите узел **Сайты**.
1. Выберите сайт, для которого хотите настроить некритические уведомления.
1. На ленте щелкните **Свойства**.
1. На вкладке **Оповещения** выберите параметр **Включить уведомления консоли об изменении работоспособности некритических сайтов**.
   - Если этот параметр включен, все пользователи консоли видят критические, предупредительные и информационные оповещения. Этот параметр выбран по умолчанию.  
   - Если этот параметр отключен, пользователи консоли будут видеть только критически важные уведомления.  

Большинство уведомлений консоли относятся к конкретным сеансам. Консоль оценивает запросы, когда пользователь запускает их. Чтобы увидеть изменения в уведомлениях, перезапустите консоль. Если пользователь закрывает некритические уведомления, он уведомляется снова при перезапуске консоли, если они по-прежнему применимы.

Следующие уведомления проверяются заново каждые пять минут:

- Сайт работает в режиме обслуживания  
- Сайт работает в режиме восстановления  
- Сайт работает в режиме обновления  

Уведомления следуют разрешениям ролевого администрирования. Например, если у пользователя нет разрешений на просмотр обновлений Configuration Manager, он не увидит эти уведомления.

Некоторые уведомления связаны с действиями. Например, если версия консоли не совпадает с версией сайта, выберите пункт **Установка новой версии консоли**. При этом запускается программа установки консоли.

Следующие уведомления наиболее применимы к ветви Technical Preview:  

- Ознакомительная версия находится в пределах 30 дней до истечения срока действия (предупреждение): текущая дата — в пределах 30 дней до срока действия ознакомительной версии  
- Истек срок действия ознакомительной версии (критическое): текущая дата выходит за пределы срока действия ознакомительной версии  
- Несовпадение версий консоли (критическое): версия консоли не совпадает с версией сайта  
- Обновление сайта доступно (предупреждение): доступен новый пакет обновления  

Дополнительные сведения и справку по устранению неполадок см. в файле **SmsAdminUI.log** на компьютере с консолью. По умолчанию этот файл расположен по следующему пути: `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\AdminUILog\SmsAdminUI.log`.


## <a name="in-console-documentation-dashboard"></a><a name="bkmk_doc-dashboard"></a> Панель мониторинга документации в консоли

<!--3556019 FKA 1357546-->
Начиная с версии Configuration Manager 1902, в новой рабочей области **Сообщества** есть узел **Документация**. Этот узел содержит актуальную информацию о документации и справочных статьях по Configuration Manager. Она включает следующие разделы:  

### <a name="product-documentation-library"></a>Библиотека документации по продукту

- **Рекомендуемые**. Список важных статей, формируемый вручную.
- **Популярные**. Наиболее популярные статьи за последний месяц.
- **Недавно обновленные**. Статьи, измененные за последний месяц.

### <a name="support-articles"></a>Справочные статьи

- **Статьи об устранении неполадок**. Пошаговые руководства для устранения неполадок в компонентах и функциях Configuration Manager.
- **Новые и обновленные справочные статьи**. Справочные статьи, созданные или обновленные за два последних месяца.

### <a name="troubleshooting-connection-errors"></a>Устранение ошибок подключения
Узел **Документация** не имеет явной конфигурации прокси-сервера. Он использует любой определенный ОС прокси в приложении панели управления **Настройки интернета**. Чтобы повторить попытку после ошибки подключения, обновите узел**Документация**.


## <a name="command-line-options"></a>Параметры командной строки

Консоль Configuration Manager включает следующие параметры командной строки.

|Параметр|Описание:|  
|------------|-----------------|  
|`/sms:debugview=1`|DebugView включается во все ResultView, которые указывают представление. DebugView отображает необработанные свойства (имена и значения).|  
|`/sms:NamespaceView=1`|Показано представление пространства имен в консоли.|  
|`/sms:ResetSettings`|Консоль игнорирует сохраняемое подключение пользователя и состояния просмотра. Размер окна не сбрасывается.|  
|`/sms:IgnoreExtensions`|Отключает все расширения Configuration Manager.|  
|`/sms:NoRestore`|Консоль игнорирует предыдущую сохраненную навигацию по узлам.|  


## <a name="tips"></a>"Советы"

### <a name="general"></a>Общие

#### <a name="improvements-to-console-search"></a><a name="bkmk_search"></a> Улучшения поиска из консоли
<!--4640570-->
*(Представлено в версии 1910)*

- Вы можете использовать параметр поиска **Все вложенные папки** из узлов **Пакеты драйверов** и **Запросы**.<!--2841181,5424892--> Начиная с версии 2002, используйте этот параметр из узлов **Элементы конфигурации** и **Конфигурационные базы**.<!--5891241-->

- Если поиск возвращает более 1000 результатов, можно нажать кнопку **ОК** на панели уведомлений, чтобы просмотреть дополнительные результаты.<!--4640570-->

    ![Снимок экрана: панель уведомлений при слишком большом числе результатов поиска](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > По умолчанию предельное число результатов поиска равно 1000. Это значение по умолчанию можно изменить. В консоли Configuration Manager перейдите на вкладку **Поиск** на ленте. В группе **Параметры** выберите **Параметры поиска**. Измените значение **Результаты поиска**. Отображение большего количества результатов поиска может занять больше времени.
    >
    > По умолчанию верхний предел равен 100 000. Чтобы изменить этот предел, задайте значение DWORD **QueryResultCountMaximum** в следующем разделе реестра:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > Параметр в консоли соответствует значению **QueryResultCountLimit** в том же разделе. Администратор может настроить эти значения в кусте HKLM для всех пользователей устройства. Значение HKCU переопределяет параметр HKLM.

#### <a name="role-based-administration-for-folders"></a>Администрирование папок на основе ролей
<!--3600867-->
*(Представлено в версии 1906)*

Теперь вы можете установить области безопасности для папок. Если у вас есть доступ к объекту в папке, но нет доступа к папке, вы не будете видеть объект. Аналогичным образом, если у вас есть доступ к папке, но не объекту внутри нее, вы не увидите этот объект. Щелкните папку правой кнопкой мыши, выберите **Установить области безопасности**, а затем выберите области безопасности, которые вы хотите применить.

#### <a name="views-sort-by-integer-values"></a>Сортировка представлений за целочисленными значениями

*(Представлено в версии 1902)*

Мы улучшили способ сортировки данных в различных представлениях. Например, в узле **Развертывания** рабочего пространства **Мониторинг** следующие столбцы теперь сортируются как числа, а не строковые значения.  

- Число ошибок
- Число выполняемых
- Число прочих
- Число успешно выполненных
- Число неизвестных  

#### <a name="move-the-warning-for-a-large-number-of-results"></a>Переместить предупреждение для большого количества результатов

*(Представлено в версии 1902)*

При выборе узла в консоли, которая возвращает более 1000 результатов, Configuration Manager отображает следующее предупреждение.

> Configuration Manager возвратил большое количество результатов. Выполнив поиск, можно сузить свой результирующий набор. Или щелкните здесь, чтобы просмотреть максимум 100 000 результатов.

Теперь между этим предупреждением и полем поиска есть дополнительное пустое пространство. Этот шаг помогает предотвратить непреднамеренный выбор предупреждения для отображения большего количества результатов.

#### <a name="send-feedback"></a>Отправить отзыв

*(Представлено в версии 1806)*
<!--1357542-->

Вы можете отправить отзывы о продукте из консоли.  

- **Отправить смайлик**: отправка отзыва о том, что вам понравилось.  

- **Отправить нахмуренный смайлик**: отправка отзыва о том, что вам не понравилось.  

- **Отправить предложение**: переход на сайт UserVoice, чтобы поделиться своей идеей.  

Дополнительные сведения см. в статье [Отзыв о продукте](../../understand/find-help.md#BKMK_1806Feedback).


### <a name="assets-and-compliance-workspace"></a>Рабочая область "Активы и соответствие"

#### <a name="real-time-actions-from-device-lists"></a>Действия в режиме реального времени из списков устройств
<!--4616810-->
*(Представлено в версии 1906)*

Существует несколько способов для отображения списка устройств в узле **Устройства** рабочей области **Активы и соответствие**.

- В рабочей области **Активы и соответствие** выберите узел **Коллекции устройств**. Выберите коллекцию устройств и выберите действие **Показать состав**. Это действие открывает подузел **Устройства** со списком устройств в этой коллекции.  

  - Выбрав подузел коллекции, теперь вы можете запустить **CMPivot** из группы коллекции на ленте.  

- В рабочей области **Мониторинг** щелкните узел **Развертывание**. Выберите развертывание, а затем действие **Просмотр состояния** на ленте. В области состояния развертывания дважды щелкните общие активы для сквозной детализации к списку устройств.  

  - При выборе устройства в этом списке теперь вы можете запустить **CMPivot** и **выполнять сценарии** в группе устройств на ленте.  


#### <a name="collections-tab-in-devices-node"></a>Вкладка "Коллекции" в узле "Устройства"
<!--4616810-->
*(Представлено в версии 1906)*

Перейдите в рабочую область **Активы и соответствие** и выберите узел **Устройства**, затем выберите устройство. В области сведений перейдите на новую вкладку **Коллекции**. Это список коллекций, которые включают это устройство. 

> [!Note]  
> - Эта вкладка в настоящее время недоступна из подузла устройств в узле **Коллекции устройств**. Например, если выбран параметр **Показать состав** для коллекции.
> - Для некоторых пользователей эта вкладка может не заполняться должным образом. Просмотреть полный список коллекций, к которым принадлежит устройство, может только пользователь с ролью безопасности **Полный администратор**. Это известная проблема. <!--5107309--> <!--5107309-->


#### <a name="add-smbios-guid-column-to-device-and-device-collection-nodes"></a>Добавление столбца GUID SMBIOS на устройство и в узлы коллекции устройств

*(Представлено в версии 1906)*

<!--4526580-->
В узлах **коллекций устройств** и **устройств** теперь можно добавить новый столбец для **GUID SMBIOS**. Это значение совпадает со значением свойства **GUID BIOS** класса ресурсов системы. Это уникальный идентификатор оборудования устройства.

#### <a name="search-device-views-using-mac-address"></a>Поиск в представлениях устройств по MAC-адресу

<!--3600878-->
*(Представлено в версии 1902)*

Теперь доступна возможность поиска в представлении устройств консоли Configuration Manager по MAC-адресу. Она может пригодиться администраторам развертывания ОС при устранении неполадок развертываний на основе PXE. При просмотре списка устройств добавьте в представление столбец **MAC-адрес**. В поле поиска добавьте условие поиска **MAC-адрес**.

#### <a name="view-users-for-a-device"></a>Просмотр пользователей устройства

С версии 1806 в узле **Устройства** доступны следующие столбцы:  

- **Основные пользователи** <!--1357280-->  

- **Текущий пользователь** <!--1358202-->  

    > [!NOTE]  
    > Для просмотра вошедшего пользователя требуется [обнаружение пользователей](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) и [сопоставление устройств пользователей](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

Дополнительные сведения о том, как отобразить столбец не по умолчанию, см. в разделе [Столбцы](#columns).

#### <a name="improvement-to-device-search-performance"></a>Улучшения производительности при поиске устройств

<!-- 3614690 -->
Начиная с версии 1806 при поиске в коллекции устройств ключевое слово, связанное со всеми свойствами объекта, не ищется. Если вы не указываете конкретный объект для поиска, выполняется поиск по следующим четырем свойствам:

- Имя
- основные пользователи;
- текущий вошедший в систему пользователь;
- имя последнего пользователя.

Такое поведение значительно ускоряет поиск по имени, особенно в большой среде. Это изменение не затрагивает настраиваемый поиск по определенным критериям.


### <a name="software-library-workspace"></a>Рабочая область "Библиотека программного обеспечения"

#### <a name="order-by-program-name-in-task-sequence"></a>Упорядочение по имени программы в последовательности задач
<!--4616810-->
*(Представлено в версии 1906)*

В рабочей области **Библиотека программного обеспечения** разверните **Операционные системы** и выберите узел **Последовательности задач**. Изменяя последовательность задач, выберите или добавьте шаг [Установить пакет](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage). Если пакет содержит более одной программы, в раскрывающемся списке программы теперь будут отсортированы.

#### <a name="task-sequences-tab-in-applications-node"></a>Вкладка последовательности задач в узле "Приложения"
<!--4616810-->
*(Представлено в версии 1906)*

Перейдите в рабочую область **Библиотека программного обеспечения**, разверните узел **Управление приложениями** и выберите узел **Приложения**, затем выберите приложение. В области сведений перейдите на новую вкладку **Последовательности задач**. На этой вкладке приведен список последовательностей задач, которые ссылаются на это приложение.

#### <a name="drill-through-required-updates"></a>Детализация необходимых обновлений
<!--4224414-->
*(Представлено в версии 1906)*

1. В консоли Configuration Manager перейдите в один из следующих разделов:

   - **Библиотека программного обеспечения** > **Обновления программного обеспечения** > **Все обновления программного обеспечения**
   - **Библиотека программного обеспечения** > **Обслуживание Windows 10** > **Все обновления Windows 10**
   - **Библиотека программного обеспечения** > **Управление клиентами Office 365** > **Обновления Office 365**

1. Выберите любое обновление, которое требуется по крайней мере на одном устройстве.
1. Перейдите на вкладку **Сводка** и найдите круговую диаграмму в разделе **Статистика**.
1. Для детализации по списку устройств щелкните гиперссылку **Просмотреть обязательные** рядом с круговой диаграммой.
1. В результате откроется временный узел в разделе **Устройства**, в котором представлены устройства, требующие обновления. В узле также можно выполнить такие действия, как создание коллекции на основе списка.


#### <a name="maximize-the-browse-registry-window"></a>Развертывание окна обзора реестра

<!--3594151 includes all MMS 1902 console changes-->
*(Представлено в версии 1902)*

1. В рабочей области **Библиотека программного обеспечения** разверните **Управление приложениями** и выберите узел **Приложения**.
1. Выберите приложение, тип развертывания которого имеет метод обнаружения. Например, метод обнаружения установщика Windows.
1. В области сведений перейдите на вкладку **Типы развертывания**.
1. Откройте свойства типа развертывания и перейдите на вкладку **Метод обнаружения**. Выберите **Добавить предложение**.
1. Измените **Тип параметра** на **Реестр** и выберите **Обзор**, чтобы открыть окно **Обзор реестра**. Теперь можно развернуть это окно.  

#### <a name="edit-a-task-sequence-by-default"></a>Изменение последовательности задач по умолчанию

*(Представлено в версии 1902)*

В рабочей области **Библиотека программного обеспечения** разверните **Операционные системы** и выберите узел **Последовательности задач**. Теперь при открытии последовательности задач **Изменить** является действием по умолчанию. Ранее действием по умолчанию была панель **Свойства**.  

#### <a name="go-to-the-collection-from-an-application-deployment"></a>Переход к коллекции из развертывания приложения

*(Представлено в версии 1902)*

1. В рабочей области **Библиотека программного обеспечения** разверните **Управление приложениями** и выберите узел **Приложения**.
1. Выберите приложение. В области сведений перейдите на вкладку **Развертывания**.
1. Выберите развертывание, а затем выберите новый параметр **Коллекция** в ленте вкладки "Развертывание". Это действие меняет представление на коллекцию, которая является целью развертывания.
   - Это действие также доступно в контекстном меню правой кнопки мыши при развертывании в этом представлении.


### <a name="monitoring-workspace"></a>Рабочая область "Наблюдение"

#### <a name="correct-names-for-client-operations"></a>Правильные имена для операций клиента
<!--4616810-->
*(Представлено в версии 1906)*

В рабочей области **Мониторинг** разверните узел **Операции клиента**. Операция **Перейти к следующей точке обновления программного обеспечения** теперь называется правильно.

#### <a name="show-collection-name-for-scripts"></a>Показать имя коллекции для сценариев
<!--4616810-->
*(Представлено в версии 1906)*

В рабочей области **Мониторинг** щелкните узел **Состояние скрипта**. Теперь здесь есть **Имя коллекции**, помимо ее идентификатора.

#### <a name="remove-content-from-monitoring-status"></a>Удаление содержимого из состояния мониторинга

*(Представлено в версии 1902)*

1. В рабочей области **Мониторинг** разверните узел **Состояние распространения** и выберите **Состояние содержимого**.
1. Выберите элемент в списке и выберите в ленте параметр **Просмотр состояния**.
1. В панели сведений о ресурсах щелкните правой кнопкой мыши точку распространения и выберите новый параметр **Удалить**. Это действие удаляет содержимое из выбранной точки распространения.

#### <a name="copy-details-in-monitoring-views"></a>Копируйте сведения в представлениях мониторинга

*(Представлено в версии 1806)*
<!--1357856-->
Скопируйте сведения из области **Сведения об активе** для следующих узлов мониторинга:  

- **Состояние распространения содержимого**  

- **Состояние развертывания**  

![Представление состояния развертывания, копирование сведений об активе](media/1810-deployment-status.PNG)

### <a name="administration-workspace"></a>Рабочая область "Администрирование"

<!--4223683-->
Начиная с версии 1906, вы можете включить некоторые узлы в узле **Безопасность** для использования службы администрирования. Это изменение позволяет консоли взаимодействовать с поставщиком SMS по протоколу HTTPS, а не с помощью WMI. Дополнительные сведения см. в разделе [Настройка службы администрирования](../../../develop/adminservice/set-up.md#bkmk_console).

## <a name="next-steps"></a>Дальнейшие шаги

[Специальные возможности](../../understand/accessibility-features.md)

[Редактор последовательности задач](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)