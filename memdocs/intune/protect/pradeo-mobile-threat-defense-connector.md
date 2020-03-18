---
title: Соединитель Mobile Threat Defense Pradeo с Intune
titleSuffix: Intune on Azure
description: Узнайте, как выполнить интеграцию Intune с соединителем Pradeo Mobile Threat Defense для управления доступом к корпоративным ресурсам с мобильных устройств.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/09/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: cde4d389-1770-4226-85a3-a2f3b3fb92a3
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a23155c31586992c82781998bb664bf2ce6a0889
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79339180"
---
# <a name="pradeo-mobile-threat-defense-connector-with-intune"></a>Соединитель Mobile Threat Defense Pradeo с Intune

Вы можете управлять доступом к корпоративным ресурсам с мобильных устройств посредством условного доступа на основании оценки рисков, проведенной Pradeo, — решением защиты мобильных устройств от угроз Mobile Threat Defense (MTD), интегрированным с Microsoft Intune. Оценка рисков основана на данных телеметрии, собранных с устройств, на которых выполняется приложение Pradeo.

Вы можете настроить политики условного доступа на основе оценки рисков Pradeo, реализуемой с помощью политик соответствия устройств Intune. Эти политики также можно использовать для разрешения или запрета доступа несовместимых устройств к ресурсам организации на основании обнаруженных угроз.

> [!NOTE]
> Этот поставщик защиты от мобильных угроз не поддерживается для незарегистрированных устройств.

## <a name="supported-platforms"></a>Поддерживаемые платформы

- **Android 4.0.3 и более поздних версий**

- **iOS 7 и более поздних версий**

## <a name="prerequisites"></a>Предварительные условия

- Azure Active Directory Premium

- Подписка на Microsoft Intune

- Подписка на службу Pradeo Security для Mobile Threat Defense

  - Дополнительные сведения см. на [веб-сайте Pradeo](https://www.pradeo.com/en-US/mobile-threat-protection).

## <a name="how-do-intune-and-pradeo-help-protect-your-company-resources"></a>Как Intune и Pradeo помогают защитить ресурсы вашей организации?

Приложение Pradeo для Android или iOS/iPadOS регистрирует сведения о файловой системе и сетевом стеке, а также данные телеметрии устройств и приложений (при наличии), и отправляет их в облачную службу Pradeo для оценки риска в отношении угроз для мобильного устройства.

Политика соответствия устройств Intune включает правило для защиты мобильных устройств от угроз Pradeo, основанное на оценке рисков Pradeo. При включении этого правила Intune оценивает соответствие устройства заданной политике. Если устройство определяется как несоответствующее, его доступ к таким ресурсам, как Exchange Online и SharePoint Online, блокируется. Пользователи заблокированных устройств получают от мобильного приложения Pradeo рекомендации по устранению проблемы и восстановлению доступа к корпоративным ресурсам.

## <a name="sample-scenarios"></a>Примеры сценариев

Далее приведены некоторые распространенные сценарии.

### <a name="control-access-based-on-threats-from-malicious-apps"></a>Управление доступом на основании оценки угроз от вредоносных приложений

При обнаружении на устройствах вредоносного ПО можно заблокировать следующие действия до устранения угрозы:

- Подключение к корпоративной электронной почте

- Синхронизация корпоративных файлов с помощью приложения OneDrive для работы

- Доступ к приложениям организации

*Блокировка при обнаружении вредоносных программ:*

![Схематическое изображение обнаруженных вредоносных приложений](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-blocked.png)

*Доступ восстановлен после исправления:*

![Обнаружены вредоносные приложения, доступ предоставлен](./media/pradeo-mobile-threat-defense-connector/pradeo-maliciousapps-unblocked.png)

### <a name="control-access-based-on-threat-to-network"></a>Управление доступом на основе угроз для сети

Обнаружение угроз для вашей сети, таких как атаки **злоумышленник в середине**, и защита доступа к сети Wi-Fi на основе рисков, связанных с устройствами.

*Блокировка доступа к сети через Wi-Fi:*

![Блокировка доступа к сети через Wi-Fi](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-blocked.png)

*Доступ восстановлен после исправления:*

![Схематическое изображение предоставления доступа после устранения угрозы](./media/pradeo-mobile-threat-defense-connector/pradeo-network-wifi-unblocked.png)

### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>Управление доступом к SharePoint Online на основе оценки угроз для сети

Обнаружение угроз для вашей сети, таких как атаки **злоумышленник в середине**, и блокирование синхронизации корпоративных файлов на основании риска для устройства.

*Блокирование SharePoint Online при обнаружении сетевых угроз:*

![Блокировка SharePoint Online при обнаружении сетевых угроз](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-blocked.png)

*Доступ восстановлен после исправления:*

![Схематическое изображение примера предоставления доступа к Sharepoint после устранения угрозы](./media/pradeo-mobile-threat-defense-connector/pradeo-network-spo-unblocked.png)

<!-- 
### Control access on unenrolled devices based on threats from malicious apps

When the Pradeo Mobile Threat Defense solution considers a device to be infected:

![App protection policy blocks due to detected malware](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-block.png)

Access is granted on remediation:

![Access is granted on remediation for App protection policy](./media/pradeo-mobile-threat-defense-connector/pradeo-app-policy-remediated.png)
-->

## <a name="next-steps"></a>Дальнейшие шаги

- [Интеграция Pradeo с Intune](pradeo-mtd-connector-integration.md)

- [Настройка приложений Pradeo](mtd-apps-ios-app-configuration-policy-add-assign.md)

- [Создание политики соответствия устройств Pradeo](mtd-device-compliance-policy-create.md)

- [Включение соединителя MTD Pradeo](mtd-connector-enable.md)
