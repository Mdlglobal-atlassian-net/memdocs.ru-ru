---
title: Включение соединителя Mobile Threat Defense в Microsoft Intune
titleSuffix: Microsoft Intune
description: Включение соединителя между партнером по Mobile Threat Defense (MTD) и Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/19/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: dbb6a37e-ba47-4b69-922c-d25e66c279f6
ms.reviewer: davidra
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee2d88e444941f2b75e6dcc716748c442de459a6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351517"
---
# <a name="enable-the-mobile-threat-defense-connector-in-intune"></a>Включение соединителя Mobile Threat Defense в Intune

Во время установки Mobile Threat Defense (MTD) вы настроили политику классификации угроз в консоли партнера MTD и создали политику соответствия устройств в Intune. Если вы уже настроили соединитель Intune на консоли партнера по MTD, можете включить соединение с MTD для партнерских приложений MTD.

> [!NOTE]
> Этот раздел относится ко всем партнерам по Mobile Threat Defense.

## <a name="classic-conditional-access-policies-for-mtd-apps"></a>Классические политики условного доступа для приложений MTD

При интеграции нового приложения с Intune Mobile Threat Defense и активации подключения к Intune служба Intune создает классическую политику условного доступа в Azure Active Directory. Каждое интегрируемое приложение MTD, включая [Защитник ATP](advanced-threat-protection.md) или любое из наших дополнительных [партнерских приложений MTD](mobile-threat-defense.md#mobile-threat-defense-partners), создает новую классическую политику условного доступа. Эти политики можно игнорировать, но нельзя изменять, удалять или отключать.

Если классическая политика удалена, нужно удалить подключение к Intune, которое обеспечивало ее создание, а затем снова настроить его. Этот процесс повторно создает классическую политику. Он не поддерживается для переноса классических политик для приложений MTD на новый тип политики для условного доступа.

Классические политики условного доступа для приложений MTD:

- Используются Intune MTD для обязательной регистрации устройств в Azure AD, чтобы они имели идентификатор устройства перед установлением связи с партнерами MTD. Этот идентификатор необходим для того, чтобы устройства могли успешно сообщить свое состояние в Intune;

- Не влияют на другие облачные приложения или ресурсы.

- отличаются от политик условного доступа, которые могут быть созданы для помощи в управлении MTD;

- по умолчанию не взаимодействуют с другими политиками условного доступа, используемыми для оценки.

Чтобы просмотреть классические политики условного доступа в [Azure](https://portal.azure.com/#home), перейдите в раздел **Azure Active Directory** > **Условный доступ** > **Классические политики**.

## <a name="to-enable-the-mobile-threat-defense-connector"></a>Включение соединителя Mobile Threat Defense

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Выберите **Администрирование клиента** > **Соединители и токены** > **Mobile Threat Defense**.

3. На панели **Mobile Threat Defense** выберите **Добавить**.

4. Выберите решение MTD в раскрывающемся списке **Настраиваемый соединитель Mobile Threat Defense**.

5. Установите переключатели параметров в соответствии с требованиями вашей организации. Отображаемые переключатели зависят от партнера MTD.  Например, на следующем рисунке показаны параметры, доступные для Symantec Endpoint Protection.

   ![Настройка MTD на портале Intune Azure](./media/mtd-connector-enable/enable-mtd-connector-1.png)

## <a name="mobile-threat-defense-toggle-options"></a>Переключатели параметров Mobile Threat Defense

Установите переключатели параметров MTD в соответствии с требованиями вашей организации. Все партнеры Mobile Thread Defense поддерживают не все перечисленные ниже параметры.

**Параметры политики соответствия MDM**

- **Подключите устройства Android версии _\<поддерживаемые версии>_ к _\<имя партнера MTD>_** : При выборе этого параметра устройства с Android версии 4.1 и более поздней могут отправлять отчеты о рисках безопасности в Intune.

- **Подключите устройства iOS версии _\<поддерживаемые версии>_ к _\<имя партнера MTD>_** : При выборе этого параметра устройства с iOS версии 8.0 и более поздней могут отправлять отчеты о рисках безопасности в Intune.

- **Включение синхронизации приложений для устройств с iOS**. Позволяет партнеру Mobile Threat Defense запрашивать в Intune метаданные приложений iOS. Эти метаданные будут использоваться для анализа угроз.

- **Блокировать неподдерживаемые версии ОС**. Блокировка устройств с операционной системой, версия которой ниже минимальной поддерживаемой.

**Параметры политик для защиты приложений**

- **Подключите устройства Android версии *\<поддерживаемые версии>* к *\<имя партнера MTD>* , чтобы включить оценку политики защиты**: При включении этого параметра политики защиты приложений, использующие правило уровня угроз для устройства, будут оценивать устройства, включая данные из этого соединителя.

- **Подключите устройства iOS версии *\<поддерживаемые версии>* к *\<имя партнера MTD>* , чтобы включить оценку политики защиты**: При включении этого параметра политики защиты приложений, использующие правило уровня угроз для устройства, будут оценивать устройства, включая данные из этого соединителя.

Дополнительные сведения об использовании соединителей Mobile Threat Defense для оценки политики "Защита приложений Intune" см. в статье [Включение соединителя Mobile Threat Defense в Intune для незарегистрированных устройств](mtd-enable-unenrolled-devices.md).

**Основные общие параметры**

- **Число дней, через которое партнер считается неотвечающим**. Период отсутствия активности в днях, по истечении которого Intune считает партнера неотвечающим из-за потери соединения. Intune не учитывает состояние соответствия неотвечающих партнеров MTD.

> [!IMPORTANT]
> При возможности рекомендуем перед созданием правил для политик соответствия устройств и условного доступа добавить и назначить приложения MTD. Это помогает гарантировать, что приложение MTD будет готово к работе и доступно для установки конечными пользователями, прежде чем они смогут получать доступ к электронной почте или другим корпоративным ресурсам.

> [!TIP]
> На панели Mobile Threat Defense вы увидите соответствующие значения в полях **Состояние подключения** и **Последняя синхронизация** для Intune и партнера по MTD.

## <a name="next-steps"></a>Дальнейшие шаги

- [Создание политики защиты приложений Mobile Threat Defense (MTD) в Intune](mtd-app-protection-policy.md).