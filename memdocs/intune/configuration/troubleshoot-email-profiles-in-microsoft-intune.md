---
title: Устранение неполадок в профилях электронной почты в Microsoft Intune — Azure | Документация Майкрософт
description: Узнайте о распространенных проблемах с профилями электронной почты в Microsoft Intune, включая дублирующиеся профили электронной почты и ошибки на устройствах Android с Samsung KNOX Standard, и способах их решения.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4d7e3b5b9a169baf336b0d4e7d8d66b06af38061
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79361423"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Распространенные проблемы с профилями электронной почты в Microsoft Intune и способы их решения

Ознакомьтесь с распространенными проблемами, возникающими с профилями электронной почты, а также способами их устранения.

## <a name="what-you-need-to-know"></a>Что необходимо знать

- Профили электронной почты развертываются для пользователя, который зарегистрировал устройство. Чтобы настроить профиль электронной почты, Intune использует свойства Azure Active Directory (AD) в профиле электронной почты пользователя во время регистрации. Дополнительные сведения см. в статье [Добавление параметров электронной почты на устройства](email-settings-configure.md).
- Для Android Enterprise разверните Gmail или Nine for Work с помощью управляемого приложения Google Play Маркет. Подробное описание действий см. в статье [Добавление управляемых приложений Google Play](../apps/apps-add-android-for-work.md).
- Microsoft Outlook для iOS/iPadOS и Android не поддерживают профили электронной почты. Вместо этого разверните политику конфигурации приложений. Дополнительные сведения см. в статье [Параметры конфигурации Outlook](../apps/app-configuration-policies-outlook.md).
- Профили электронной почты, предназначенные для групп устройств (не для групп пользователей), могут быть не доставлены на устройство. Если у устройства есть основной пользователь, выбор устройства в качестве цели должен работать. Если профиль электронной почты содержит сертификаты пользователей, обязательно настройте целевые группы пользователей.
- Пользователям могут последовательно отображаться несколько запросов на ввод пароля для профиля электронной почты. В этом сценарии проверьте все сертификаты, указанные в профиле электронной почты. Если один из сертификатов не предназначен для пользователя, Intune повторяет попытку развертывания профиля электронной почты.

## <a name="device-already-has-an-email-profile-installed"></a>На устройстве уже установлен профиль электронной почты

Если пользователи создают профиль электронной почты перед регистрацией в Intune или Office 365 MDM, профиль электронной почты, развернутый Intune, может работать не так, как ожидалось:

- **iOS/iPadOS**. Intune обнаружит существующий дубликат профиля электронной почты по имени узла и адресу электронной почты. Созданный пользователем профиль электронной почты не позволит развернуть профиль, созданный Intune. Это распространенная проблема, так как пользователи iOS/iPadOS обычно сначала создают профиль электронной почты и только потом проходят регистрацию. В приложении Корпоративного портала сообщается о том, что пользователь не соответствует требованиям, и предлагается пользователю удалить профиль электронной почты.

  Пользователь должен удалить свой профиль электронной почты, чтобы можно было развернуть профиль Intune. Чтобы предотвратить эту проблему, попросите пользователей зарегистрироваться и разрешить Intune развернуть профиль электронной почты. Пользователи могут создавать собственные профили электронной почты.

- **Windows**: Intune обнаружит существующий дубликат профиля электронной почты по имени узла и адресу электронной почты. Intune перезаписывает существующий профиль электронной почты, созданный пользователем.

- **Samsung KNOX Standard**. Intune обнаружит дубликат учетной записи электронной почты по адресу электронной почты и перезапишет его данными профиля Intune. Если пользователь настроил эту учетную запись, она будет снова заменена на профиль Intune. Это может вызвать некоторую путаницу для пользователя, конфигурация учетной записи которого перезаписывается.

Samsung KNOX не использует имя узла для идентификации профиля. Не рекомендуется создавать на разных узлах несколько профилей электронной почты с одним адресом, так как они перезаписывают друг друга.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Ошибка 0x87D1FDE8 для устройства KNOX Standard

**Проблема**. После создания и развертывания профиля электронной почты Exchange Active Sync для разных устройств с Android в Samsung KNOX Standard отображается ошибка с кодом **0x87D1FDE8** или сообщением о **сбое исправления** на вкладке политики в свойствах устройства.

Проверьте конфигурацию профиля EAS для Samsung KNOX и исходную политику. Параметр синхронизации заметок Samsung больше не поддерживается, поэтому не следует выбирать его в своем профиле. Убедитесь, что у устройств достаточно времени (до 24 часов) на обработку политики.

## <a name="unable-to-send-images-from--email-account"></a>Не удается отправить изображения из учетной записи электронной почты

Пользователи, учетные записи электронной почты которых настраиваются автоматически, не могут отправлять изображения или рисунки со своих устройств. Это может произойти, если параметр **Разрешить отправку сообщений электронной почты сторонними приложениями** отключен.

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации**.
3. Выберите профиль электронной почты > **Свойства** > **Параметры**.
4. Установите для параметра **Allow e-mail to be sent from third-party applications** (Разрешить отправку сообщений электронной почты из сторонних приложений) значение **Включить**.

## <a name="next-steps"></a>Дальнейшие шаги

Получите [поддержку от корпорации Майкрософт](../fundamentals/get-support.md) или обратитесь на [форумы сообщества](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
