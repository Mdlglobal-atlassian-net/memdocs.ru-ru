---
title: Назначение приложений группам в Microsoft Intune
titleSuffix: ''
description: Сведения о назначении приложений Intune группам пользователей или группам устройств с помощью Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dc349e22-9e1c-42ba-9e70-fb2ef980ef7a
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b80527921172201dc86c5f3241e9978525afa083
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83984822"
---
# <a name="assign-apps-to-groups-with-microsoft-intune"></a>Назначение приложений группам с помощью Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

[Добавив приложение](apps-add.md) в Microsoft Intune, вы сможете назначить его пользователям и устройствам. Важно отметить, что вы можете назначить приложение любому устройству, даже если оно не находится под управлением Intune.

> [!NOTE]
> Намерение развертывания на основе доступности не поддерживается для групп устройств — только для групп пользователей.

В приведенной ниже таблице представлены доступные варианты для назначения приложений пользователям и устройствам.

|   | Устройства, зарегистрированные в Intune | Устройства, не зарегистрированные в Intune |
|-------------------------------------------------------------------------------------------|------------------------------|----------------------------------|
| Назначение для пользователей | Да | Да |
| Назначение для устройств | Да | Нет |
| Назначение упакованных приложений или приложений, содержащих пакет SDK для Intune (для политик защиты приложений) | Да | Да |
| Назначение приложений в качестве доступных | Да | Да |
| Назначение приложений в качестве необходимых | Да | Нет |
| Удаление приложений | Да | Нет |
| Получение обновления приложений в Intune | Да | Нет |
| Установка доступных приложений пользователями через приложение корпоративного портала | Да | Нет |
| Установка доступных приложений пользователями через корпоративный веб-портал | Да | Да |

> [!NOTE]
> Сейчас вы можете назначать приложения iOS/iPadOS и Android (бизнес-приложения и приложения, приобретенные в магазине) устройствам, не зарегистрированным в Intune.
>
> Чтобы получить обновление приложений на устройствах, которые не зарегистрированы в Intune, пользователи этих устройств должны открыть корпоративный портал и установить обновления вручную.

## <a name="assign-an-app"></a>Назначение приложения

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Приложения** > **Все приложения**.
3. На панели **Приложения**, выберите приложение, которое вы намерены назначить.
4. В разделе меню **Управление** выберите **Назначения**.
5. Выберите **Добавить группу**, чтобы открыть область **Добавить группу** для этого приложения.
6. Выберите **Тип назначения** для конкретного приложения.
   - **Available for enrolled devices** (Доступно для зарегистрированных устройств). Вы можете назначить приложение группам пользователей, которые могут устанавливать приложение через приложение или веб-сайт Корпоративного портала.
   - **Available with or without enrollment** (Доступно с регистрацией или без нее). Назначает это приложение группам пользователей, чьи устройства не зарегистрированы в Intune. Пользователям должна быть назначена лицензия Intune. Дополнительные сведения см. в разделе [Лицензии, включающие в себя Intune](../fundamentals/licenses.md).
   - **Обязательное**. Приложение устанавливается на устройствах в выбранных группах. На некоторых платформах могут возникать дополнительные запросы, которые пользователь должен подтвердить, прежде чем начнется установка приложения.
   - **Удалить**. Приложение удаляется с устройств в выбранных группах, если в Intune приложение ранее установлено на устройство через назначение Available for enrolled devices (Доступно для зарегистрированных устройств) или "Обязательно" с использованием одного развертывания. Веб-ссылки не могут быть удалены после развертывания.

     > [!NOTE]
     > **Только для приложений iOS/iPadOS**.
     > - Для настройки того, что происходит с управляемыми приложениями, когда устройства больше не управляются, можно выбрать предполагаемый параметр в разделе **Удалить при удалении устройства**. Дополнительные сведения см. в разделе [Параметр удаления приложения для приложений, управляемых iOS/iPadOS](apps-deploy.md#app-uninstall-setting-for-ios-managed-apps).
     > - Если вы создали профиль VPN iOS/iPadOS, который содержит настройки VPN на уровне приложения, такой профиль можно выбрать в списке **VPN**. VPN-подключение открывается при запуске приложения. Дополнительные сведения см. в разделе [Параметры VPN для устройств iOS/iPadOS](../configuration/vpn-settings-ios.md).
     >
     > **Только для приложений Android**. Если вы развернете приложение Android как **доступное с регистрацией или без нее**, состояние отчетности будет доступно только на зарегистрированных устройствах.
     >
     > Для параметра **Доступно для зарегистрированных устройств**. Приложение отображается как доступное, только если пользователь, вошедший в корпоративный портал, является основным пользователем, зарегистрировавшим устройство, а приложение применимо к устройству.

7. Чтобы выбрать группы пользователей, которых затронет это назначение приложения, щелкните **Включенные группы**.
8. Выберите одну или несколько групп для включения и щелкните **Выбрать**.
9. На панели **Назначить** выберите **ОК**, чтобы завершить выбор включенных групп.
10. Щелкните **Исключить группы**, если вы хотите исключить из назначения приложения какие-либо группы пользователей.
11. Если вы решили исключить группы, в колонке **Выбор групп** щелкните **Выбрать**.
12. На панели **Добавить группу** нажмите кнопку **OK**.
13. На панели **Назначения** выберите **Сохранить**.

Теперь приложение назначено группам, которые вы только что выбрали. Дополнительные сведения о включении и исключении назначений приложений см. в статье [Включение и исключение назначений приложений в Microsoft Intune](apps-inc-exl-assignments.md).

## <a name="how-conflicts-between-app-intents-are-resolved"></a>Способы устранения конфликтов между намерениями приложений

Не допускается, чтобы одна группа была предназначена для нескольких целей назначения приложения. Однако, если пользователь или устройство принадлежит к нескольким группам, каждая из которых назначена с различными намерениями, это приведет к конфликту. Создавать конфликты назначения для приложений не рекомендуется.
Сведения в следующей таблице помогут разобраться в намерениях для таких случаев:

| Намерение группы 1 | Намерение группы 2 | Итоговое намерение |
|-----------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|Требуется пользователь|Доступен пользователь|Обязательно и доступно|
|Требуется пользователь|Удаление пользователя|Обязательное|
|Доступен пользователь|Удаление пользователя|Удаление|
|Требуется пользователь|Требуется устройство|Существуют оба, Intune обрабатывает намерение "Требуется"
|Требуется пользователь|Удаление устройства|Существуют оба, Intune разрешает намерение "Требуется"
|Доступен пользователь|Требуется устройство|Существуют, Intune разрешает намерение "Требуется" ("Обязательно" и "Доступно")
|Доступен пользователь|Удаление устройства|Существуют оба, Intune разрешает намерение "Доступно"<br><br>Приложение отображается на корпоративном портале.<br><br>Если приложение уже установлено (как обязательное приложение с предыдущим намерением), оно удаляется.<br><br>Если пользователь выбрал **установку с корпоративного портала**, приложение устанавливается, а намерение удаления не учитывается.|
|Удаление пользователя|Требуется устройство|Существуют оба, Intune разрешает намерение "Требуется"|
|Удаление пользователя|Удаление устройства|Существуют оба, Intune разрешает намерение "Удалено"|
|Требуется устройство|Удаление устройства|Обязательное|
|Обязательный и доступный пользователь|Доступен пользователь|Обязательно и доступно|
|Обязательный и доступный пользователь|Удаление пользователя|Обязательно и доступно|
|Обязательный и доступный пользователь|Требуется устройство|Существуют оба, обязательно и доступно
|Обязательный и доступный пользователь|Удаление устройства|Существуют, Intune разрешает намерение "Требуется" ("Обязательно" и "Доступно")
|Доступен пользователь без регистрации|Обязательный и доступный пользователь|Обязательно и доступно
|Доступен пользователь без регистрации|Требуется пользователь|Обязательное
|Доступен пользователь без регистрации|Доступен пользователь|Доступно|
|Доступен пользователь без регистрации|Требуется устройство|Обязательно и доступно без регистрации|
|Доступен пользователь без регистрации|Удаление устройства|Удаление и доступно без регистрации.<br><br>Если пользователь не устанавливал приложение с корпоративного портала, соблюдается намерение удаления.<br><br>Если пользователь устанавливает приложение с корпоративного портала, установка имеет приоритет над удалением.|

> [!NOTE]
> При добавлении управляемых приложений магазина iOS в Microsoft Intune и назначении их в качестве **обязательных** такие приложения автоматически создаются с намерениями **Обязательно** и **Доступно**.<br><br>
> Приложения из магазина iOS/iPadOS (не приобретенные в рамках программы VPP) с намерением "Обязательно" устанавливаются на устройстве при его регистрации в системе, а также отображаются в приложении "Корпоративный портал".<br><br>
> При возникновении конфликтов в параметре **Удалить при удалении устройства** приложение не удаляется с устройства, если оно больше не управляется.

## <a name="managed-google-play-app-deployment-to-unmanaged-devices"></a>Развертывание приложений типа "Управляемый Google Play" на неуправляемых устройствах
Для устройств Android, задействованных в сценарии развертывания в рамках политики защиты приложений без регистрации (APP-WE), вы можете с помощью управляемого Google Play для пользователей развертывать приложения из магазина и бизнес-приложения. Приложения типа "Управляемый Google Play", **доступные с регистрацией или без регистрации**, появятся в приложении Магазина Google Play на устройствах пользователей, а не в приложении Корпоративного портала. Пользователи будут просматривать и устанавливать приложения, развернутые таким образом из Магазина Google Play. Так как приложения устанавливаются из управляемого Google Play, пользователям не понадобится изменять параметры своего устройства и разрешать установку приложений из неизвестных источников. Это означает, что устройства будут более защищенными. Если разработчик приложения опубликует новую версию приложения для Магазина Google Play, которая установлена на устройствах пользователей, Магазин Google Play автоматически обновит приложение. 

Инструкции по назначению приложения типа "Управляемый Google Play" неуправляемым устройствам:

1. Подключите клиент Intune к управляемому Google Play. Если вы уже сделали это, чтобы управлять рабочим профилем Android для бизнеса для выделенных или полностью управляемых устройств, повторно этого делать не нужно.
2. Добавьте приложения из управляемого Google Play в консоль Intune.
3. Для желаемой группы пользователей назначьте приложения управляемого Google Play как **доступные с регистрацией или без регистрации**. Ориентирование приложений как **обязательных** и **предназначенных для удаления** не поддерживается для незарегистрированных устройств.
4. Назначьте группе пользователей политику защиты приложений.
5. В следующий раз, когда пользователь откроет приложение Корпоративного портала, он увидит сообщение о том, что в приложении Магазина Google Play доступны приложения.  Пользователи могут щелкнуть уведомление. При этом они будут перенаправлены в приложение Магазин Google Play и увидят корпоративные приложения или же смогут самостоятельно отрыть приложение Магазина Google Play.
6. Пользователи могут развернуть контекстное меню в приложении Магазина Google Play и переключаться между личной учетной записью Google (где отображаются личные приложения) и рабочей учетной записью (где отображаются приложения из магазина и бизнес-приложения, предназначенные для них). Пользователи устанавливают приложения, нажав кнопку "Установить" в приложении Магазина Google Play.

Если в консоли Intune выполняется выборочная очистка приложений, рабочая учетная запись будет автоматически удалена из приложения Магазина Google Play и с этого момента рабочие приложения больше не будут отображаться в каталоге приложений Магазина Google Play. При удалении с устройства рабочей учетной записи приложения, установленные из Магазина Google Play, не удаляются. 

## <a name="app-uninstall-setting-for-ios-managed-apps"></a>Параметр удаления приложения для приложений, управляемых iOS
Для устройств iOS/iPadOS можно выбрать, что произойдет с управляемыми приложениями при отмене регистрации устройства в Intune или удалении профиля управления с помощью параметра **Удалить при удалении устройства**. Этот параметр применяется только к приложениям после регистрации устройства и установки приложений как управляемых. Параметр не может быть настроен для веб-приложений или веб-ссылок. После выхода из системы с помощью выборочной очистки приложений удаляются только данные, защищенные системой управления мобильными приложениями (MAM).

Значения по умолчанию для этого параметра предварительно заполнены для новых назначений следующим образом:

|Тип приложения iOS | Значение по умолчанию для параметра "Удалить при удалении устройства" |
|--------------------|----------------|
| Бизнес-приложение | Да |
| Приложение магазина | Нет |
| Приложение VPP | Нет |
| Встроенное приложение | Нет |

>[!NOTE]
>**"Доступные" типы назначений:** Если этот параметр обновляется для групп "доступные для зарегистрированных устройств" или "доступные с регистрацией или без нее", пользователи, у которых уже есть управляемое приложение, не получат обновленный параметр, пока они не синхронизируют устройство с Intune и не переустановят приложение. 
>
>**Существовавшие ранее назначения:** Назначения, существовавшие до появления этого параметра, не изменяются, а все управляемые приложения будут удалены из управления при удалении устройства.

## <a name="next-steps"></a>Дальнейшие шаги

Дополнительные сведения о мониторинге назначения приложений см. в статье [о мониторинге приложений](apps-monitor.md).
