---
title: Обновления в консоли
titleSuffix: Configuration Manager
description: Установка обновлений для Configuration Manager из облака Майкрософт
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fee0cdf72ae8975d26bebd4da765941116421c25
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694592"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Установка обновлений в консоли для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager синхронизируется с облачной службой Майкрософт для получения обновлений. После этого обновления устанавливаются из консоли Configuration Manager.

## <a name="get-available-updates"></a>Получение доступных обновлений

Сайт загружает только те обновления, которые относятся к вашей инфраструктуре и версии. Процесс синхронизации может быть автоматическим или выполняться вручную в зависимости от того, как настроить точку подключения службы для иерархии.

- В **режиме "в сети"** точка подключения службы автоматически подключается к облачной службе Майкрософт и загружает необходимые обновления.  

    По умолчанию Configuration Manager проверяет наличие новых обновлений каждые 24 часа. В консоли Configuration Manager можно проверить наличие обновлений вручную. Перейдите к рабочей области **Администрирование**, выберите узел **Обновления и обслуживание** и щелкните **Проверить наличие обновлений** на ленте.  

- В **автономном режиме** точка подключения службы не подключается к облачной службе Майкрософт. Чтобы скачать и импортировать доступные обновления, необходимо [применить средство подключения службы](use-the-service-connection-tool.md).  

> [!NOTE]  
> При необходимости в консоль можно импортировать внешние исправления. Для этого используйте [средство регистрации обновлений](use-the-update-registration-tool-to-import-hotfixes.md). Эти внешние исправления дополняют обновления, которые вы получаете при синхронизации с облачной службой Майкрософт.  

После синхронизации обновлений их можно просмотреть в консоли Configuration Manager. Перейдите к рабочей области **Администрирование** и выберите узел **Обновления и обслуживание**.  

- Неустановленные обновления отображаются как **доступные**.  

- Установленные обновления отображаются как **установленные**. Отображается только последнее установленное обновление. Чтобы просмотреть ранее установленные обновления, выберите **Журнал** на ленте.  

Перед настройкой точки подключения службы определите и спланируйте область ее применения. Следующие варианты использования могут повлиять на выбор настроек для этой роли системы сайта.  

- Сайт использует точку подключения службы для отправки сведений об использовании веб-сайта. Эти сведения помогают облачной службе Майкрософт определить обновления, доступные для текущей версии вашей инфраструктуры. Дополнительные сведения см. в статье [Данные о диагностике и использовании](../../plan-design/diagnostics/diagnostics-and-usage-data.md).  

Чтобы лучше понять, что происходит при загрузке обновлений, см. следующие блок-схемы:  

- [Блок-схема: скачивание обновлений](download-updates-flowchart.md)  

- [Блок-схема: репликация обновлений](update-replication-flowchart.md)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Назначение разрешений для просмотра и управления обновлениями и компонентами

Чтобы пользователь мог просматривать обновления в консоли, ему должна быть назначена роль безопасности ролевого администрирования, которая включает класс безопасности **Обновление пакетов**. Этот класс предоставляет доступ для просмотра обновлений и управления ими в консоли Configuration Manager.

### <a name="about-the-update-packages-class"></a>Сведения о классе "Пакеты обновления"

По умолчанию класс **Пакеты обновления** (SMS_CM_Updatepackages) является частью следующих встроенных ролей безопасности с указанными далее разрешениями.  

- **Полный администратор** с разрешениями **Изменение** и **Чтение**  

  - Пользователь с этой ролью безопасности и доступом к области безопасности **Все** может просматривать обновления и устанавливать их. Пользователь может также включать компоненты во время установки и отдельные компоненты после обновления сайта.  

  - Пользователь с этой ролью безопасности и доступом к области безопасности **По умолчанию** может просматривать обновления и устанавливать их. Пользователь может также включать компоненты во время установки и просматривать отдельные компоненты после обновления сайта. При этом включать функции после обновления сайта пользователь не может.  

- **Аналитик с правами только для чтения** с разрешением **Чтение**  

  - Пользователь с этой ролью безопасности и доступом к области **По умолчанию** может просматривать обновления, но не может их устанавливать. Кроме того, он может просматривать функции после обновления сайта, но не может их включать.  

### <a name="permissions-required-for-updates-and-servicing"></a>Разрешения, необходимые для установки обновлений и обслуживания

- Используйте учетную запись, которой назначена роль безопасности, включающая класс **Пакеты обновления**, с разрешениями **Изменение** и **Чтение**.  

- Назначьте учетной записи область **по умолчанию**.  

### <a name="permissions-to-only-view-updates"></a>Разрешения, позволяющие только просматривать обновления

- Используйте учетную запись, которой назначена роль безопасности, включающая класс **Пакеты обновления**, только с разрешением **Чтение**.  

- Назначьте учетной записи область **по умолчанию**.  

### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Разрешения, необходимые для включения функций после обновления сайта

- Используйте учетную запись, которой назначена роль безопасности, включающая класс **Пакеты обновления**, с разрешениями **Изменение** и **Чтение**.  

- Назначьте учетной записи **все** области.  

## <a name="before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Перед установкой обновлений в консоли  

Прежде чем устанавливать обновления из консоли Configuration Manager, выполните указанные ниже действия.  

### <a name="step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Шаг 1. Просмотр контрольного списка обновления  

Просмотрите контрольный список действий, которые необходимо выполнять перед запуском обновления.

- [Контрольный список для установки обновления до версии 2002](checklist-for-installing-update-2002.md)

- [Контрольный список для установки обновления до версии 1910](checklist-for-installing-update-1910.md)  

- [Контрольный список для установки обновления до версии 1906](checklist-for-installing-update-1906.md)  

- [Контрольный список для установки обновления до версии 1902](checklist-for-installing-update-1902.md)

### <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step2"></a> Шаг 2. Запуск средства проверки готовности перед установкой обновления  

Перед установкой обновления рекомендуется выполнить проверку готовности к установке этого обновления. Если перед установкой обновления запустить средство проверки готовности, то будут выполнены следующие действия.  

- Сайт реплицирует файлы обновления на другие сайты до установки обновления.  

- Если выбрать установку обновления, средство проверки готовности автоматически запускается еще раз.  

> [!NOTE]  
> Когда вы запустите средство проверки готовности, состояние этапа **установки** будет активным. Тем не менее фактически сайт не устанавливает обновления. Чтобы выполнить проверку готовности, процесс обновления извлекает пакет из библиотеки содержимого. Затем он помещает пакет в промежуточную папку, где к нему сможет получить доступ средство проверки готовности. При установке обновления выполняется этот же процесс. Именно поэтому этап установки отображается как **Выполняется**. А в категории установки отображается только этап *Распаковать пакет обновления*.  

Затем, при установке обновления, можно настроить процесс так, чтобы предупреждения средства проверки готовности игнорировались.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Выполните следующие действия, чтобы запустить средство проверки готовности перед установкой обновления.  

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование** и выберите узел **Обновления и обслуживание**.  

2. Выберите пакет обновления, для которого требуется выполнить проверку готовности к установке.  

3. Щелкните **Запустить проверку готовности** на ленте.  

    При выполнении проверки готовности к установке содержимое обновления реплицируется на подчиненные сайты. Просмотрите файл **distmgr.log** на сайте сервера, чтобы убедиться, что содержимое реплицируется успешно.  

4. Для просмотра результатов проверки готовности выполните следующее:  

    1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**.  

    2. Выберите узел **Состояние обновлений и обслуживания** и найдите состояние готовности к установке.  

    3. Дополнительные сведения см. в журнале **ConfigMgrPrereq.log** на сервере сайта.  

## <a name="install-in-console-updates"></a><a name="bkmk_install"></a> Установка обновлений в консоли  

Когда все будет готово для установки обновлений с помощью консоли Configuration Manager, начните с сайта верхнего уровня иерархии. Это сайт центра администрирования или автономный первичный сайт.  

Устанавливайте обновления для каждого сайта в нерабочее время, чтобы не прерывать бизнес-процессы. Во время установки обновлений могут выполняться такие действия, как переустановка компонентов сайта и ролей системы сайта.  

- Подчиненные первичные сайты автоматически запускают процесс обновления после того, как сайт центра администрирования завершит установку обновления. Это рекомендуемый процесс, выполняемый по умолчанию. Для управления временем установки обновлений можно использовать [периоды обслуживания для серверов сайта](service-windows.md).  

- Когда обновление родительского первичного сайта будет завершено, необходимо вручную обновить вторичные сайты из консоли Configuration Manager. Автоматическое обновление серверов вторичных сайтов не поддерживается.  

- При использовании консоли Configuration Manager после обновления сайта предлагается обновить консоль.  

- После того как на сервере сайта успешно завершается установка обновления, на нем автоматически обновляются все применимые роли системы сайта. Однако ни одна из точек распространения не устанавливается заново; они одновременно переходят в автономный режим для обновления. Вместо этого сервер сайта использует параметры распространения содержимого сайта для одновременного распространения обновления в подмножество точек распространения за раз. В результате для установки обновления переходить в автономный режим будут только некоторые точки распространения. Точки распространения, для которых обновление еще не началось или уже завершилось, остаются в сети и предоставляют содержимое клиентам.

### <a name="overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Общие сведения об установке обновления в консоли  

#### <a name="1-when-the-update-installation-starts"></a>1. При запуске установки обновления

Откроется мастер установки обновлений, в котором будет показан список областей продукта, к которым применяется обновление.  

- На странице мастера **Общие** при необходимости можно настроить **Предупреждения по необходимым компонентам**.  

  - Ошибки при проверке на наличие необходимых компонентов всегда прерывают установку обновления. Чтобы повторно запустить установку обновления, устраните ошибки. Дополнительные сведения см. в разделе [Повторная попытка установки обновления в случае сбоя](#bkmk_retry).  

  - Предупреждения о необходимых компонентах также могут остановить процесс установки обновления. Чтобы повторно запустить установку обновления, устраните проблемы, описанные в этих предупреждениях. Дополнительные сведения см. в разделе [Повторная попытка установки обновления в случае сбоя](#bkmk_retry).  

  - **Игнорировать предупреждения проверки на наличие необходимых компонентов и продолжить установку**. Задайте условие для установки обновления игнорировать предупреждения проверки. Это позволит продолжить установку обновления. Если этот параметр не выбран, установка обновления будет останавливаться при появлении предупреждений. Если ранее не выполнялась проверка готовности к установке и не были разрешены предупреждения о необходимых компонентах для сайта, то не используйте этот параметр.  

    В рабочих областях **Администрирование** и **Мониторинг** в узле "Обновления и обслуживание" на ленте появилась новая кнопка **Пропускать предупреждения о необходимых компонентах**. Эта кнопка становится доступной, когда не удается завершить установку пакета обновления из-за предупреждения проверки готовности к установке. Например, если вы устанавливаете обновление, не настроив игнорирование предупреждений о необходимых компонентах (в мастере обновления). Установка обновления останавливается, если нет ошибок, но есть предупреждения о необходимых компонентах. Затем щелкните **Пропускать предупреждения о необходимых компонентах** на ленте. Это действие активирует автоматическое продолжение установки обновлений, при котором эти предупреждения будут игнорироваться. Если этот параметр используется, установка обновления продолжается автоматически через несколько минут.  

- Когда обновление применяется к клиенту Configuration Manager, протестируйте обновление клиента с ограниченным набором клиентов. Дополнительные сведения см. в статье [Проверка обновления клиента в предварительной коллекции](../../clients/manage/upgrade/test-client-upgrades.md).  

#### <a name="2-during-the-update-installation"></a>2. Во время установки обновления

В ходе установки обновления Configuration Manager выполняет указанные ниже действия.  

- Переустанавливает все затронутые обновлением компоненты, например роли системы сайта или консоль Configuration Manager.  

- Управляет обновлениями для клиентов на основе настроек, заданных для пилотной подготовки клиента и для [автоматического обновления клиента](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md#bkmk_autoupdate).  

- Серверы системы сайта обычно не перезагружаются во время обновления. Если роль использует .NET, а пакет обновляет этот обязательный компонент, система сайта может перезагружаться.  

> [!TIP]  
> При установке обновлений Configuration Manager сайт также обновляет папку CD.Latest. Дополнительные сведения см. в разделе [Папка CD.Latest](the-cd.latest-folder.md).  

#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Отслеживание хода выполнения обновлений по мере их установки

Используйте следующие действия для отслеживания хода выполнения.  

- В консоли Configuration Manager перейдите в рабочую область **Администрирование** и выберите узел **Обновления и обслуживание**. В этом узле показано состояние установки для всех пакетов обновления.  

- В консоли Configuration Manager перейдите в рабочую область **Мониторинг** и выберите узел **Состояние обновлений и обслуживания**. В этом узле показано состояние установки только текущего пакета обновления, который сейчас устанавливает сайт.  

    Установка обновления состоит из нескольких этапов для упрощения мониторинга. Для каждого из следующих этапов в состоянии установки содержится имя файла журнала, в котором содержится дополнительная информация:  

  - **Скачивание**. Этот этап применяется только к сайту верхнего уровня с точкой подключения службы.

  - **Репликация**

  - **Проверка готовности к установке**

  - **Установка**

  - **После установки**. Дополнительные сведения см. в описании [задач, выполняемых после установки](#post-installation-tasks).  

- Просмотрите файл **CMUpdate.log** в папке `<ConfigMgr_Installation_Directory>\Logs` на сервере сайта.  

>[!NOTE]
> Начиная с версии 1906, состояние задачи **Обновить базу данных ConfigMgr** можно увидеть на этапе **установки**.
>
> - Если обновление базы данных заблокировано, то вы получите предупреждение **В состоянии выполнения, требует внимания**.
>   - В файле cmupdate.log будет указано имя программы и sessionid из SQL, которые блокируют обновление базы данных.
> - Если обновление базы данных больше не блокируется, состояние вернется к пунктам **Выполняется** или **Завершено**.
>   - Пока обновление базы данных заблокировано, каждые 5 минут выполняется проверка, чтобы увидеть, сохраняется ли блокировка.

#### <a name="4-when-the-update-installation-completes"></a>4. По завершении установки обновления

После завершения установки обновления на первом сайте:  

- Дочерние первичные сайты устанавливают обновление автоматически. В дальнейших действиях нет необходимости.  

- Обновите вторичные сайты вручную с помощью консоли Configuration Manager. Дополнительные сведения см. в разделе [Запуск установки обновления на вторичном сайте](#bkmk_secondary).  

- Пока все сайты в иерархии не будут обновлены до новой версии, иерархия будет работать в режиме смешанных версий. Дополнительные сведения см. в статье [Взаимодействие различных версий](../../plan-design/hierarchy/interoperability-between-different-versions.md).  

#### <a name="5-update-configuration-manager-consoles"></a>5. Обновление консолей Configuration Manager

После обновления сайта центра администрирования или первичного сайта необходимо также обновить каждую консоль Configuration Manager, которая подключается к этому сайту. Обновить консоль предлагается в следующих случаях:  

- При открытии консоли.  

- При переходе на новый узел в открытой консоли.  

Обновите консоль сразу после обновления сайта.  

После завершения обновления консоли проверьте, что версии консоли и сайта верные. Выберите пункт **О Configuration Manager** в левом верхнем углу консоли.  

> [!Note]  
> Версия консоли несколько отличается от версии сайта. Дополнительный номер версии консоли теперь соответствует версии выпуска Configuration Manager. Например, в версии Configuration Manager 1802 начальная версия сайта имеет номер 5.0.8634.1000, а начальная версия консоли — номер 5.**1802**.1082.1700. Номера сборки (1082) и редакции (1700) в будущем могут изменяться после выхода новых исправлений.

### <a name="to-start-the-update-installation-at-the-top-level-site"></a><a name="bkmk_toptier"></a> Запуск установки обновления на сайте верхнего уровня  

В сайте верхнего уровня вашей иерархии в консоли Configuration Manager перейдите в рабочую область **Администрирование** и выберите узел **Обновления и обслуживание**. Выберите обновление с состоянием **Доступно** и щелкните **Установить пакет обновления** на ленте.  

### <a name="to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Запуск установки обновления на вторичном сайте  

После обновления родительского первичного сайта вторичного сайта обновите вторичный сайт из консоли Configuration Manager. Чтобы это сделать, используйте **мастер обновления вторичных сайтов**.  

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта** и выберите узел **Сайты**. Выберите дополнительный сайт, который необходимо обновить, и щелкните **Обновить** на ленте.  

2. Чтобы начать обновление дополнительного сайта, щелкните **Да**.  

Для отслеживания состояния установки на дополнительном сайте выберите этот сайт и щелкните **Показать состояние установки** на ленте. Также добавьте в узел сайтов столбец **Версия**, чтобы иметь возможность просматривать версию каждого вторичного сайта.  

В некоторых случаях состояние в консоли не обновляется или указывает, что обновление завершилось с ошибкой. После успешного обновления вторичного сайта используйте параметр **Повторить попытку установки**. Этот параметр не переустанавливает обновление для вторичного сайта, на котором оно было успешно установлено, но обновляет его состояние в консоли.

### <a name="post-installation-tasks"></a>Задачи, выполняемые после установки

Когда сайт устанавливает обновление, некоторые задачи нельзя выполнять, пока не завершится установка обновления на сервере сайта. В их число входят задачи, которые выполняются после установки и являются критическими для операций сайта и иерархии. Из-за своей важности они активно отслеживаются. Дополнительные задачи, которые непосредственно не отслеживаются, включают повторную установку ролей системы сайта. Чтобы просмотреть состояние важных задач, выполняемых после установки, выберите задачу **После установки** во время наблюдения за установкой обновления для сайта.

Не все задачи выполняются немедленно. Некоторые задачи не будут запущены до завершения установки обновления для каждого сайта. Новые функциональные возможности могут появиться уже после завершения этих задач. Включение новых компонентов не начинается, пока все сайты не завершат установку обновления, поэтому новые возможности могут не отображаться некоторое время.

Задачи, выполняемые после установки

- **Установка службы SMS_EXECUTIVE**

  - Важная служба, которая работает на сервере сайта.
  - Переустановка этой службы должна завершиться быстро.

- **Установка компонента SMS_DATABASE_NOTIFICATION_MONITOR**

  - Важные поток компонента сайта для службы SMS_EXECUTIVE.
  - Переустановка этой службы должна завершиться быстро.

- **Установка компонента SMS_HIERARCHY_MANAGER**

  - Важный компонент сайта, который работает на сервере сайта.
  - Он отвечает за переустановку ролей на серверах системы сайта. Состояние переустановки отдельных ролей системы сайта не отображается.
  - Переустановка этой службы должна завершиться быстро.

    > [!Note]
    > Некоторые роли сайта Configuration Manager совместно используют структуру клиента, например точку управления и точку распространения по запросу. Когда эти роли обновляются, обновление версии клиента на этих серверах происходит одновременно. См. сведения об [обновлении клиентов](../../clients/manage/upgrade/upgrade-clients-for-windows-computers.md).

- **Установка компонента SMS_REPLICATION_CONFIGURATION_MONITOR**

  - Важный компонент сайта, который работает на сервере сайта.
  - Переустановка этой службы должна завершиться быстро.

- **Установка компонента SMS_POLICY_PROVIDER**

  - Важный компонент сайта, который работает только на первичных сайтах.
  - Переустановка этой службы должна завершиться быстро.

- **Мониторинг инициализации репликации**

  - Эта задача отображается только на сайте центра администрирования и первичных дочерних сайтах.
  - Зависит от компонента SMS_REPLICATION_CONFIGURATION_MONITOR.
  - Должен установиться быстро.

- **Обновление подготовительного пакета клиента Configuration Manager**

  - Эта задача отображается, даже если предварительный клиент (пилотное развертывание клиента) не включен для использования.
  - Не запускается, пока все сайты в иерархии не завершат установку обновления.

- **Обновление папки Client на сервере сайта**

  - Эта задача не отображается, если вы используете клиент в предварительной среде.  
  - Должен установиться быстро.

- **Обновление пакета клиента Configuration Manager**

  - Эта задача не отображается, если вы используете клиент в предварительной среде.  
  - Устанавливается только после установки обновлений на все сайты.  

- **Включение компонентов**

  - Эта задача отображается только на сайте верхнего уровня иерархии.
  - Не запускается, пока все сайты в иерархии не завершат установку обновления.
  - Отдельные компоненты не отображаются.

## <a name="retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Повторная попытка установки обновления в случае сбоя  

При сбое установки обновления просмотрите отчет об ошибках в консоли, чтобы определить, какие действия необходимы для устранения предупреждений и ошибок. Дополнительные сведения можно просмотреть в журнале **ConfigMgrPrereq.log** на сервере сайта. Перед повторной попыткой установки обновления необходимо устранить ошибки, а также устранить предупреждения.  

> [!TIP]  
> Если не удается скачать или реплицировать обновление, используйте [средство сброса обновления](update-reset-tool.md).  

Когда вы будете готовы повторить установку обновления, выберите обновление, установка которого завершилась сбоем, а затем выберите соответствующий вариант. Режим повторной попытки установки обновления зависит от узла, с которого начинается повтор, и выбранного метода повторной попытки.  

### <a name="retry-installation-for-the-hierarchy"></a>Повторная установка для иерархии

Повторите установку обновления для всей иерархии, если это обновление находится в одном из следующих состояний:  

- Проверка готовности пройдена с одним предупреждением или несколькими, а параметр, позволяющий пропустить все ошибки проверки готовности в мастере обновлений, не установлен. (Для параметра **Пропустить предупреждение о необходимых компонентах** в узле **Обновления и обслуживание** обновлению присвоено значение **Нет**.)

- Сбой проверки готовности к установке

- Сбой установки  

- Сбой репликации содержимого на сайт

Перейдите к рабочей области **Администрирование** и выберите узел **Обновления и обслуживание**. Выберите обновление и затем один из следующих вариантов.  

- **Повторить**. При выборе параметра **Повторить** в разделе **Обновления и обслуживание** установка обновления начинается снова, а предупреждения о необходимых компонентах пропускаются автоматически. Если ранее не удалось выполнить репликацию, содержимое для обновления реплицируется еще раз.  

- **Пропускать предупреждения о необходимых компонентах**. Если установка обновления останавливается из-за предупреждения, можно выбрать **Пропускать предупреждения о необходимых компонентах**. Это действие позволяет продолжить установку обновления через несколько минут и использует функцию пропуска предупреждений проверки.

### <a name="retry-installation-for-the-site"></a>Повторная установка для сайта

Повторите установку обновления для определенного сайта, если это обновление находится в одном из следующих состояний:  

- Проверка готовности пройдена с одним предупреждением или несколькими, а параметр, позволяющий пропустить все ошибки проверки готовности в мастере обновлений, не установлен. (Для параметра **Пропускать предупреждения о необходимых компонентах** в узле "Обновления и обслуживание" обновлению присвоено значение **Нет**.)  

- Сбой проверки готовности к установке

- Сбой установки

Перейдите в рабочую область **Мониторинг** и выберите узел **Состояние обслуживания сайта**. Выберите обновление и затем один из следующих вариантов.  

- **Повторить**. При выборе параметра **Повторить** в разделе **Состояние обслуживания сайта** установка обновления перезапускается только для этого сайта. В отличие от применения параметра **Повторить** из узла **Обновления и обслуживание** в этом режиме предупреждения о необходимых компонентах не пропускаются.  

- **Пропускать предупреждения о необходимых компонентах**. Если установка обновления останавливается из-за предупреждения, щелкните **Пропускать предупреждения о необходимых компонентах**. Это действие позволяет продолжить установку обновления через несколько минут и использует функцию пропуска предупреждений проверки.  

## <a name="after-a-site-installs-an-update"></a><a name="bkmk_after"></a> После установки обновления на сайте  

Когда сайт обновится, просмотрите контрольный список действий, выполняемых после обновления, для соответствующей версии:  

- [Контрольный список действий, выполняемых после обновления, для версии 2002](checklist-for-installing-update-2002.md#post-update-checklist)

- [Контрольный список действий, выполняемых после обновления, для версии 1910](checklist-for-installing-update-1910.md#post-update-checklist)  

- [Контрольный список действий, выполняемых после обновления, для версии 1906](checklist-for-installing-update-1906.md#post-update-checklist)  

- [Контрольный список действий, выполняемых после обновления, для версии 1902](checklist-for-installing-update-1902.md#post-update-checklist)  

## <a name="enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Включение дополнительных функций из обновлений  

Если обновление содержит один или несколько дополнительных компонентов, можно включить эти компоненты в иерархии. Это можно сделать во время установки обновления или вернуться в консоль позже, чтобы включить дополнительные компоненты.

Чтобы просмотреть доступные функции и их состояние, в консоли перейдите к рабочей области **Администрирование**, разверните **Обновления и обслуживание** и выберите узел **Функции**.

Если компонент не является дополнительным, он устанавливается автоматически. Он не отображается в узле **Компоненты**.  

> [!Important]  
> В иерархии с несколькими сайтами можно включайте дополнительные компоненты и компоненты предварительной версии только с сайта центра администрирования. Это поведение позволяет гарантировать отсутствие конфликтов в иерархии. <!--507197-->  

При включении новой функции или функции предварительного выпуска диспетчер иерархии Configuration Manager (HMAN) должен обработать данное изменение, прежде чем эта функция станет доступной. Обработка изменения часто выполняется сразу же. В зависимости от цикла обработки HMAN это может занять до 30 минут. После обработки изменения и перед использованием функции следует перезапустить консоль.

Начиная с версии 2002,<!--5834830--> при появлении новых облачных компонентов, доступных для использования в центре администрирования Microsoft Endpoint Manager или в других подключенных облачных службах для локальной установки Configuration Manager, теперь вы можете включать их в консоли Configuration Manager.

### <a name="list-of-optional-features"></a>Список дополнительных компонентов

Следующие компоненты являются необязательными в последней версии Configuration Manager:<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](install-in-console-updates.md#bkmk_options).  

-->

- [Управление BitLocker](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Синхронизация результатов членства в коллекции с Azure Active Directory](../../clients/manage/collections/create-collections.md#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->
- [Обнаружение групп пользователей Azure Active Directory](../deploy/configure/configure-discovery-methods.md#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->
- [Группы приложений](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Отладчик последовательности задач](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Диспетчер преобразования пакетов](../../../apps/pcm/package-conversion-manager.md) <!--1357861,4E0C09AF-7FC1-4412-A8BB-166D9BCD0093-->
- [Клиентские приложения для совместно управляемых устройств](../../../comanage/workloads.md#client-apps) (ранее — *Мобильные приложения для совместно управляемых устройств*) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C-->
- [Обновление стороннего программного обеспечения](../../../sum/deploy-use/third-party-software-updates.md)<!--1357605,1352101,1358714;B5E192AE-C81F-4348-9EF9-07A3C0FBE597-->
- [Утверждение запросов приложений для пользователей на каждом устройстве](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->  
- [Создание и выполнение скриптов](../../../apps/deploy-use/create-deploy-scripts.md) <!--1236459,566F8720-F415-4E10-9A51-CDE682BA2B2E-->
- [Обновления драйверов Surface](../../../sum/get-started/configure-classifications-and-products.md) <!--1098490,82AD973A-7CDF-4B67-A665-72875D6E099A-->
- [Шлюз управления облаком](../../clients/manage/cmg/plan-cloud-management-gateway.md) <!--1101764,DD043119-789C-4158-AC79-725E999F385A-->
- [Создание PFX](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Соединитель Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Политика Exploit Guard в Защитнике Windows](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN для Windows 10](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Обслуживание кластерной коллекции (группы серверов)](../../../sum/deploy-use/service-a-server-group.md) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697-->
- [Windows Hello для бизнеса](../../../protect/deploy-use/windows-hello-for-business-settings.md) (ранее — *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!Tip]  
> Дополнительные сведения о компонентах, на включение которых требуется согласие, см. в разделе [Компоненты предварительной версии](pre-release-features.md).  
>
> Дополнительные сведения о компонентах, которые доступны только в ветви технической версии, см. в разделе [Technical Preview](../../get-started/technical-preview.md).

## <a name="use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Использование функций предварительной версии из обновлений

В Current Branch включены компоненты предварительной версии для раннего тестирования в рабочей среде. Дополнительные сведения см. в статье [Функции предварительной версии](pre-release-features.md).

## <a name="frequently-asked-questions"></a><a name="bkmk_faq"></a> Часто задаваемые вопросы

### <a name="why-dont-i-see-certain-updates-in-my-console"></a>Почему в консоли нет определенных обновлений?

Если после успешной синхронизации с облачной службой Майкрософт в консоли не удается найти определенное обновление, это может быть вызвано одной из следующих причин.  

- Для обновления требуется конфигурация, которую не использует ваша инфраструктура, или текущая версия продукта не удовлетворяет требованиям получения обновления.  

    Если вы считаете, что у вас есть необходимые конфигурации и компоненты отсутствующего обновления, убедитесь, что точка подключения службы подключена к сети. Затем выполните принудительную проверку, выбрав параметр **Проверить наличие обновлений** в узле **Обновления и обслуживание**. Если точка подключения службы переходит в автономный режим, для ручной синхронизации с облачной службой используется средство подключения к службе.  

- Ваша учетная запись не обладает разрешениями ролевого администрирования, необходимыми для просмотра обновлений в консоли Configuration Manager. Дополнительные сведения см. в разделе [Разрешения для управления обновлениями](#assign-permissions-to-view-and-manage-updates-and-features).  