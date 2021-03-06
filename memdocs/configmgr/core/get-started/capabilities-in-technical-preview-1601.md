---
title: Возможности технической версии 1601
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1601.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed3f53b6e2e9557def20fc459dfcf4641b0e396d
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905821"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Возможности в Technical Preview 1601 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в Technical Preview для Configuration Manager версии 1601. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager.      Перед установкой этой версии прочтите вводную статью [Technical Preview для Configuration Manager](../../core/get-started/technical-preview.md), чтобы ознакомиться с общими требованиями и ограничениями на использование ознакомительной технической версии, а также узнать, как выполнять обновления и оставлять отзывы о возможностях этого выпуска.  

 **Известные проблемы в этой версии Technical Preview**  

-   При управлении **параметрами обновления клиента** для повышения предварительной версии клиента до рабочей в тексте для флажка отображается нулевая версия клиента (0) вместо фактического номера сборки клиента. Правильная предварительная версия клиента отображается в области над этим параметром и представляет собой версию клиента, которая повышается до рабочей при выборе этого параметра.  

-   При обновлении до версии Technical Preview 1601, если выбрать проверку клиента Configuration Manager в предварительной коллекции, пакет клиента для этой коллекции не будет обновлен. Эта проблема присутствует только в версии Technical Preview 1601.  

     Чтобы обойти эту проблему, выполните одно из следующих действия.  

    -   Выполните следующий сценарий SQL для базы данных первичного сайта:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Добавьте новую роль системы сайта точки распространения на сайт лаборатории. Новая точка распространения обновит предварительную коллекцию с помощью нового пакета клиента.  

**Ниже перечислены новые возможности, доступные в этой версии.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a> Усовершенствования интеграции Microsoft Intune  
В Technical Preview 1601 добавлена поддержка следующих возможностей.  

### <a name="improvements-to-conditional-access"></a>Усовершенствования условного доступа  

-   **Поддержка условного доступа для компьютеров, управляемых с помощью Configuration Manager**  

     Теперь вы можете задать политики условного доступа для компьютеров, управляемых Configuration Manager, которые будут требовать соответствия ПК политике для доступа к службам Exchange Online и SharePoint Online.  Эта особенность, кроме того, позволяет регистрировать ПК в Azure AD с помощью политики соответствия, а также выполнять мониторинг и создавать отчеты о регистрации Azure AD.  

    > [!NOTE]  
    >  Условный доступ пока не поддерживается в Windows 10.  

    Ниже перечислены необходимые условия для использования этой функции.  

    -   Подписка Azure Active Directory Premium и ADFS Sync.  

    -   Подписка Microsoft Intune. Подписка Microsoft Intune должна быть настроена в консоли Configuration Manager.  

    -   [Необходимые условия для автоматической регистрации Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Для использования этой возможности необходимо создать политику соответствия в Configuration Manager с определенными описанными ниже правилами и задать политику условного доступа в консоли Intune.  Кроме того, чтобы предоставлять доступ только соответствующим компьютерам, для требования к ПК Windows необходимо задать параметр **Устройства должны соответствовать требованиям**. Ниже приведены правила политики соответствия, применимые к ПК под управлением Configuration Manager.  

    -   **Требовать регистрацию в Azure Active Directory:** это правило проверяет, присоединено ли устройство пользователя к Azure AD. Если нет, устройство автоматически регистрируется в Azure AD. Автоматическая регистрация поддерживается только в Windows 8.1. Для ПК Windows 7 разверните MSI-файл, выполняющий автоматическую регистрацию. Дополнительные сведения см. [здесь](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Установлены все необходимые обновления со сроком, превышающим определенное количество дней:** это правило проверяет, установлены ли на устройстве пользователя все необходимые обновления (указанные в правиле **Обязательные автоматические обновления**) в срок и в течение указанного льготного периода, и автоматически устанавливает все отложенные обязательные обновления.  

    -   **Требовать шифрование диска BitLocker:** это правило проверяет, зашифрован ли основной диск (например, C:\\) на устройстве с помощью BitLocker. Если шифрование Bitlocker не включено на основном устройстве, доступ к электронной почте и службам SharePoint блокируется.  

    -   **Требовать защиту от вредоносных программ:** это правило проверяет, включено и выполняется ли программное обеспечение по защите от вредоносных программ (System Center Endpoint Protection или только Защитник Windows).  
         Если ПО не включено, доступ к электронной почте и службам SharePoint блокируется.  

    Конечные пользователи, заблокированные из-за несоответствия требованиям, смогут просматривать сведения о соответствии в центре программного обеспечения и запускать новые оценки политики после устранения проблем соответствия.  

-   **Условный доступ с помощью службы аттестации работоспособности**. Теперь вы можете ограничить доступ к электронной почте и службам Office 365 на основе состояния работоспособности устройств, указываемого службой аттестации работоспособности.  Кроме того, устройства под управлением Intune включаются в отчеты о работоспособности устройств.  

    В консоль Configuration Manager добавлено новое правило соответствия, которое позволяет указывать, следует ли предоставить или заблокировать доступ устройству на основе его состояния работоспособности.  Чтобы создать это правило, откройте **мастер создания политики соответствия** и добавьте новое правило.  В качестве условия выберите **Указано службой аттестации работоспособности как рабочее** и задайте значение **True**.  В этом случае доступ к ресурсам организации получат только устройства, указанные как работоспособные. Дополнительные сведения о службе аттестации работоспособности и отражении данных о работоспособности устройств в Intune см. в статье [Аттестация работоспособности устройств](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Новые параметры политики соответствия**. С помощью новых параметров политики соответствия можно повысить уровень безопасности и защиты на устройствах, которые используются для доступа к корпоративной электронной почте и службам SharePoint.  

    -   **Требовать получение автоматических обновлений**. Можно требовать, чтобы устройства Windows 8.1 или более поздних версий разрешали автоматическую установку обновлений, а также указывать класс устанавливаемых обновлений.  Вы можете выбрать установку только обновлений, помеченных как важные, или установку всех рекомендуемых обновлений.  

         Чтобы создать правило для автоматических обновлений, откройте **мастер создания политики соответствия** и добавьте новое правило.  В качестве условия выберите **Минимальная классификация обязательных обновлений** и задайте одно из доступных значений: **None**, **Recommended** и **Important**.  

        -   **None** — обновления не устанавливаются автоматически.  

        -   **Recommended** — устанавливаются все рекомендованные обновления.  

        -   **Important** — устанавливаются только обновления, которые классифицируются как важные.  

    -   **Требовать пароль для разблокировки мобильных устройств**. Если задан параметр **Да**, пользователи должны вводить пароль для доступа к устройствам.  

         Чтобы создать правило пароля для разблокировки мобильных устройств, откройте **мастер создания политики соответствия** и добавьте новое правило. В качестве условия выберите **Требовать пароль для разблокировки бездействующего устройства** и задайте значение **True**.  

    -   **Минуты бездействия до требования пароля**.  Задает время бездействия, по истечении которого пользователю потребуется ввести пароль повторно.  

         Чтобы создать это правило, откройте **мастер создания политики соответствия** и добавьте новое правило. В качестве условия выберите **Требовать ввод пароля после следующего периода бездействия (в минутах)** и задайте одно из доступных значений: 1 минута, 5 минут, 15 минут, 30 минут, 1 час.  

-   **Переопределение правила по умолчанию — всегда разрешать зарегистрированным и соответствующим устройствам Intune доступ к локальной организации Exchange.**  

     Если выбран этот параметр, устройства, зарегистрированные в Intune и соответствующие политикам, получают доступ к локальной организации Exchange. Это правило переопределяет правило по умолчанию, то есть даже если вы настроите правило по умолчанию для помещения в карантин или блокировку доступа, зарегистрированные и соответствующие требованиям устройства по-прежнему будут иметь доступ к локальной организации Exchange.  
     Используйте этот параметр, если требуется, чтобы зарегистрированные и соответствующие требованиям устройства всегда получали доступ к электронной почте через локальную организацию Exchange.  

     Эта возможность поддерживается на следующих платформах:  Windows Phone 8, iOS 6 и более поздние их версии. Android 4.0 и более поздние версии, Samsung KNOX Standard 4.0 и более поздние версии  

     Чтобы использовать этот параметр, перейдите на страницу **Общие** **мастера настройки политики условного доступа** для локальной организации Exchange.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a> Состояние клиента в сети  
Начиная с версии Technical Preview 1601, вы можете быстро определить, в сети или вне сети клиент в консоли Configuration Manager. Обновленные значки и столбцы в списке устройств консоли позволяют оценивать состояние клиентов в вашей среде для определения проблемных областей и других вопросов, которые могут потребовать вашего внимания.  

Клиент находится в сети, если он в настоящее время подключен к роли системы сайта точки управления Configuration Manager. Пока точка управления получает от клиента сообщения, подобные сообщениям проверки связи, он находится в сети. Если точка управления не получает сообщение в течение примерно 5 минут, состояние клиента изменяется на "вне сети".  

### <a name="icons-for-client-status"></a>Значки состояния клиента  

|||  
|-|-|  
|![значок состояния "в сети" для клиентов](media/online-status-icon.png)|Клиент находится в сети.|  
|![значок состояния "не в сети" для клиентов](media/offline-status-icon.png)|Клиент находится вне сети.|  
|![значок неизвестного состояния для клиентов](media/unknown-status-icon.png)|Состояние клиента неизвестно.|  

### <a name="prerequisites"></a>Предварительные условия  
 Предварительные требования к состоянию клиента отсутствуют. Вы можете начать использование сразу после установки Configuration Manager Technical Preview 1601.  

### <a name="limitations"></a>Ограничения  
 Состояние клиента в сети доступно только для компьютеров Windows с установленным клиентом Configuration Manager. Состояние клиента не поддерживается для компьютеров Mac, компьютеров Linux или UNIX, а также для устройств, управляемых с помощью локального управления устройствами.\-  

### <a name="to-view-client-online-status"></a>Просмотр состояния клиента в сети  

1. В консоли Configuration Manager последовательно выберите **Активы и соответствие > Обзор > Коллекции устройств**.  

2. Щелкните правой кнопкой мыши заголовок столбца, а затем выберите одно из полей состояния клиента в сети, чтобы добавить его в представление устройства. Доступны следующие поля:  

   -   **Состояние устройства в сети** указывает текущее состояние клиента — в сети или вне сети.  

   -   **Последнее время в сети** указывает время изменения состояния клиента с "вне сети" на "в сети".  

   -   **Последнее время не в сети** указывает время изменения состояния клиента с "в сети" на "вне сети".  

   Чтобы отобразить последние изменения в состоянии клиента, обновите консоль.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a> Улучшения в управлении приложениями  
 В Technical Preview 1601 добавлена поддержка следующих возможностей.  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Управление приложениями для устройств iOS, приобретенными по корпоративной программе  
 Некоторые магазины приложений позволяют приобретать сразу несколько лицензий, если приложение планируется использовать в организации. Это позволяет сократить административные расходы на отслеживание нескольких приобретенных копий приложения.  

 Configuration Manager помогает управлять приложениями, приобретенными по такой программе, импортируя сведения о лицензиях из магазина приложений и отслеживая число используемых лицензий.  


### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS — конфигурация для гибридных<br />приложений  
 Некоторые приложения iOS поддерживают предварительную настройку таких параметров, как сервер или база данных, к которым должно подключаться приложение. Теперь Configuration Manager поддерживает развертывание политик конфигурации приложений на устройстве, что позволяет пользователю начать работу с приложением немедленно, без знания этих параметров. Разработчикам необходимо включить эту функциональность в своих приложениях.  

 В настоящее время предварительную настройку параметров поддерживает ограниченное количество общедоступных приложений. Кроме того, у вас могут быть бизнес-приложения собственной разработки, поддерживающие такую настройку.  

#### <a name="prerequisites-for-this-scenario"></a>Предварительные требования для данного сценария  

-   Подписка Microsoft Intune должна быть добавлена в Configuration Manager.  

-   В подписку Intune необходимо добавить действительный сертификат Apple APNs.  

-   Должно быть развернуто приложение iOS, поддерживающее конфигурацию приложений.  

#### <a name="try-it-out"></a>Попробуйте!  
 После выполнения указанных выше условий необходимо создать приложение Configuration Manager, которое использует тип развертывания iOS. Это приложение должно поддерживать конфигурацию приложений. Чтобы узнать, какие конкретные элементы (пары имен и значений) вы можете настроить, см. документацию поставщика приложения.  

 Затем во время развертывания приложения свяжите политику конфигурации приложения с типом развертывания iOS. Кроме того, вы можете развернуть политику из узла **Политики конфигурации приложений** для существующего приложения и коллекции.  

 Попробуйте выполнить следующие задачи, а затем используйте информацию для обратной связи, расположенную ближе к началу этой статьи, чтобы сообщить нам о полученном результате.  

-   Если у вас есть приложение iOS, которое поддерживает конфигурацию приложений, обратитесь к документации поставщика приложения, чтобы узнать имена пар имен и значений, которые необходимо указать для настройки приложения.  

-   Запустите мастер **создания политики конфигурации приложения**. В мастере на странице **Политика iOS** попытайтесь добавить пары имен и значений, найденные в документации поставщика приложения. Кроме того, вы можете импортировать XML-файл, содержащий необходимые значения.  

-   В мастере **развертывания программного обеспечения** на странице **Политика конфигурации приложения** свяжите созданную политику конфигурации приложения с совместимым типом развертывания из приложения.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a> Усовершенствования параметров соответствия  
 В Technical Preview 1601 добавлена поддержка следующих возможностей.  

### <a name="microsoft-edge-browser-settings"></a>Параметры браузера Microsoft Edge  
 В элемент конфигурации **Windows 8.1 и Windows 10** (параметры применяются только к устройствам Windows 10) были добавлены новые параметры браузера Microsoft Edge.  

 Чтобы просмотреть новые параметры, выберите **Microsoft Edge** в элементе конфигурации **Параметры устройства** на странице мастера **создания элементов конфигурации**.  

 Дополнительные сведения см. в статье [Создание элементов конфигурации для устройств Windows 8.1 и Windows 10, управляемых без использования клиента Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Параметры соответствия устройств Windows 10 для совместной работы  
 Используйте эти новые параметры соответствия для настройки устройств под управлением Windows 10 для совместной работы, например устройств Surface Hub.  

 Чтобы просмотреть новые параметры, выберите **Windows 10 для совместной работы** в элементе конфигурации **Параметры устройства** на странице мастера **создания элементов конфигурации**.  

 Дополнительные сведения см. в статье [Создание элементов конфигурации для устройств Windows 8.1 и Windows 10, управляемых без использования клиента Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android — режим киоска для гибридных устройств Samsung KNOX Standard<br />приложений  
 Режим киоска позволяет блокировать устройство, разрешая работу только определенных функций. Например, можно разрешить устройству выполнять только одно управляемое приложение или отключить кнопки громкости на устройстве. Эти параметры могут использоваться для демонстрационной модели устройства или устройства, предназначенного для выполнения только одной функции, например кассовый терминал. Эти параметры недоступны для устройств Samsung KNOX Standard в элементе конфигурации **Windows 8.1 и Windows 10** (параметры применяются только к устройствам Windows 10).  

 Чтобы просмотреть новые параметры, выберите **Режим киоска — Samsung KNOX** в элементе конфигурации **Параметры устройства** на странице мастера **создания элементов конфигурации**.  

 Дополнительные сведения см. в статье [Создание элементов конфигурации для устройств Windows 8.1 и Windows 10, управляемых без использования клиента Configuration Manager](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
