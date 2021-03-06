---
title: Устранение проблем с установкой приложений
titleSuffix: Microsoft Intune
description: Используйте панель Microsoft Intune для устранения неполадок, которые возникают при установке приложений.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/21/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: b613f364-0150-401f-b9b8-2b09470b34f4
ms.reviewer: mghadial
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1c98de99eb8f72840080ca720465559c462bc77f
ms.sourcegitcommit: fb84a87e46f9fa126c1c24ddea26974984bc9ccc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2020
ms.locfileid: "82023373"
---
# <a name="troubleshoot-app-installation-issues"></a>Устранение проблем с установкой приложений

Иногда установка приложения на устройствах, управляемых с помощью Microsoft Intune MDM, может завершиться сбоем. В таких случаях определение причины или устранение неполадок может оказаться сложной задачей. Microsoft Intune предоставляет сведения о сбоях, которые происходят во время установки приложений. Это позволяет операторам службы технической поддержки и администраторам Intune просматривать сведения о приложении и обрабатывать запросы на поддержку от пользователей. Область устранения неполадок в Intune предоставляет сведения о сбоях, в том числе сведения об управляемых приложениях на устройстве пользователя. Сведения о жизненном цикле приложения предоставляются в области **управляемых приложений** отдельно для каждого устройства. Вы можете просмотреть проблемы с установкой, например сведения о времени создания, изменения и назначения приложения и его передачи на устройство.

> [!NOTE]
> Сведения о коде ошибки установки конкретного приложения см. в [справочнике по ошибкам установки приложений Intune](app-install-error-codes.md).

## <a name="app-troubleshooting-details"></a>Сведения для устранения неполадок в приложениях

Intune предоставляет сведения для устранения неполадок в приложениях, установленных на определенном устройстве пользователя.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устранение неполадок и поддержка**.
3. Щелкните **Выбрать пользователя**, чтобы выбрать пользователя, для которого необходимо устранить неполадки. Отобразится панель **Выбор пользователей**.
4. Выберите пользователя, введя его имя или адрес электронной почты. Щелкните **Выбрать** в нижней части панели. Сведения по устранению неполадок для пользователя отображаются в области **Устранение неполадок**. 
5. В списке **Устройства** выберите устройство, на котором необходимо устранить проблему.
    ![Область устранения неполадок Intune.](./media/troubleshoot-app-install/troubleshoot-app-install-01.png)
6. В области выбранного устройства выберите **Управляемые приложения**. Отобразится список управляемых приложений.
    ![Сведения о конкретном устройстве под управлением Intune.](./media/troubleshoot-app-install/troubleshoot-app-install-02.png)
7. В списке выберите приложение, **состояние установки** которого указывает на сбой.
    ![Выбранное приложение, для которого указаны сведения о сбое при установке.](./media/troubleshoot-app-install/troubleshoot-app-install-03.png)

    > [!Note]  
    > Это же приложение могло быть назначено нескольким группам, но с другими необходимыми действиями (намерениями) для приложения. К примеру, разрешенное намерение для приложения будет отображаться как **исключенное**, если приложение было исключено для пользователя на момент назначения. Дополнительные сведения см. в разделе [Способы устранения конфликтов между намерениями приложений](apps-deploy.md#how-conflicts-between-app-intents-are-resolved).<br><br>
    > В случае сбоя при установке необходимого приложения вы или ваша служба поддержки можете синхронизировать устройство и повторить попытку установки приложения.

Сведения об ошибке установки укажут на проблему. С помощью этих сведений можно определить наиболее подходящее действие, которое необходимо предпринять для устранения проблемы. Дополнительные сведения об устранении неполадок при установке приложений см. в разделах [Ошибки установки приложений Android](app-install-error-codes.md#android-app-installation-errors) и [Ошибки установки приложений iOS](app-install-error-codes.md#ios-and-ipados-app-installation-errors).

> [!Note]  
> Чтобы получить доступ к панели **Устранение неполадок**, перейдите в браузере по адресу: [https://aka.ms/intunetroubleshooting](https://aka.ms/intunetroubleshooting).

## <a name="user-group-targeted-app-installation-does-not-reach-device"></a>Установка приложения для группы пользователей не достигает устройства
Следуйте инструкциям при возникновении проблем с установкой приложений:
- Если приложение не отображается на Корпоративном портале, убедитесь, что приложение развернуто с намерением **Доступно** и что пользователь обращается на Корпоративный портал с типа устройства, поддерживаемого приложением.
- Для устройств Windows BYOD пользователю необходимо добавить рабочую учетную запись на устройство.
- Проверьте, превышает ли пользователь ограничение на число устройств AAD:
  1. Перейдите в раздел [Параметры устройств Azure Active Directory](https://portal.azure.com/#pane/Microsoft_AAD_IAM/DevicesMenupane/DeviceSettings/menuId).
  2. Запишите значение, заданное для параметра **Максимальное число устройств на пользователя**.
  3. Перейдите к разделу [Пользователи Azure Active Directory](https://portal.azure.com/#pane/Microsoft_AAD_IAM/UsersManagementMenupane/AllUsers).
  4. Выберите соответствующего пользователя и щелкните **Устройства**.
  5. Если пользователь превышает установленный лимит, удалите устаревшие записи, которые больше не нужны.
- Для устройств с iOS и iPadOS DEP убедитесь, что для пользователя отображается элемент **Зарегистрированные пользователем** на панели "Обзор устройств" в Intune. Если отображается значение Н/Д, разверните политику конфигурации для Корпоративного портала Intune. Дополнительные сведения см. в разделе [Настройка приложений на Корпоративном портале](app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-dep-devices).

## <a name="win32-app-installation-troubleshooting"></a>Устранение неполадок установки приложения Win32

Выберите приложение Win32, которое было развернуто с помощью расширения управления Intune. Можно выбрать параметр **Собирать журналы** при сбое установки приложения Win32. 

> [!IMPORTANT]
> Параметр **Собирать журналы** не будет включен, если приложение Win32 успешно установлено на устройстве.<p>Прежде чем можно будет собирать сведения журналов приложений Win32, на клиенте Windows должно быть установлено расширение управления Intune. Расширение управления Intune устанавливается при развертывании скрипта PowerShell или приложения Win32 для пользователя или группы безопасности устройств. Дополнительные сведения см. в разделе [Предварительные требования для совместного управления](intune-management-extension.md#prerequisites).

### <a name="collect-log-file"></a>Собирать файлы журналов

Чтобы собрать журналы установки приложения Win32, сначала выполните действия, описанные в разделе [Сведения для устранения неполадок в приложениях](troubleshoot-app-install.md#app-troubleshooting-details). Затем выполните следующие действия.

1. Щелкните **Сбор журналов** в панели **Сведения об установке**.

    <image alt="Win32 app installation details - Collect log option" src="./media/troubleshoot-app-install/troubleshoot-app-install-04.png" width="500" />

2. Укажите пути к файлам журнала, чтобы начать процесс сбора файлов журнала, и нажмите кнопку **ОК**.

    > [!NOTE]
    > Сбор журналов займет не более двух часов. Поддерживаемые типы файлов: *LOG, TXT, DMP, CAB, ZIP, XML, EVTX и EVTL*. Разрешено не более 25 путей к файлам.

3. После сбора файлов журнала можно выбрать ссылку **Журналы**, чтобы скачать файлы.

    <image alt="Win32 app log details - Download logs" src="./media/troubleshoot-app-install/troubleshoot-app-install-05.png" width="500" />

    > [!NOTE]
    > Отображается уведомление, обозначающее успешный сбор журналов приложений.

#### <a name="win32-log-collection-requirements"></a>Требования к сбору журналов Win32

Существуют определенные требования, которые должны выполняться для сбора файлов журнала:

- Необходимо указать полный путь к файлу журнала. 
- Можно указать переменные среды для сбора журналов, например следующие:<br>
  *%PROGRAMFILES%, %PROGRAMDATA% %PUBLIC%, %WINDIR%, %TEMP%, %TMP%*
- Разрешены только точные расширения файлов, такие как:<br>
  *LOG, TXT, DMP, CAB, ZIP, XML*
- Максимальный размер и количество отправляемых файлов журнала — 60 МБ или 25 файлов (в зависимости от того, какое ограничение будет превышено раньше). 
- Сбор журналов установки приложения Win32 включен для приложений, соответствующих обязательным, доступным целям и целям удаления приложения.
- Сохраненные журналы шифруются для защиты любых персональных данных, содержащихся в журналах.
- При открытии обращений по поводу сбоев приложений Win32 прикладывайте соответствующие журналы, выполнив действия, описанные выше.

## <a name="troubleshooting-apps-from-the-microsoft-store"></a>Устранение неполадок приложений из Магазина Майкрософт

Сведения из раздела [Устранение неполадок упаковки, развертывания и запросов приложений Магазина Майкрософт](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx) помогают устранить распространенные проблемы, которые могут возникнуть при установке приложений из Магазина Майкрософт с помощью Intune или других средств.

## <a name="app-troubleshooting-resources"></a>Ресурсы по устранению неполадок в приложении
- [Развертывание Visio и Project в составе развертывания Приложений Microsoft 365](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Deploying-Visio-and-Project-as-part-of-your-Office/ba-p/701795)
- [Убедитесь, что приложения MSfB, развернутые с помощью Intune, устанавливаются в Windows 10 1903](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Take-Action-to-Ensure-MSfB-Apps-deployed-through/ba-p/658864)
- [Устранение неполадок развертывания приложений MSI в Microsoft Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Troubleshooting-MSI-App-deployments-in-Microsoft/ba-p/359125)
- [Рекомендации по распространению программного обеспечения на классический агент ПК Windows с Intune](https://support.microsoft.com/en-us/help/2583929/best-practices-for-intune-software-distribution-to-windows-pc)

## <a name="next-steps"></a>Дальнейшие шаги

- Дополнительные сведения об устранении неполадок в службе Intune см. в руководстве по [использованию портала диагностики для оказания помощи пользователям в вашей компании](../fundamentals/help-desk-operators.md). 
- Вы можете узнать об известных проблемах в Microsoft Intune. Дополнительные сведения см. в [блоге Intune об успехах клиентов](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/bg-p/IntuneCustomerSuccess).
- Нужна дополнительная помощь? См. [ Получение поддержки для Microsoft Intune](../fundamentals/get-support.md).
