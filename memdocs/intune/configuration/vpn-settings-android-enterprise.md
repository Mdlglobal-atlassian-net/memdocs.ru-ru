---
title: Настройка параметров VPN для устройств Android в Microsoft Intune в Azure | Документация Майкрософт
description: 'Просмотрите все параметры для создания VPN-подключений на устройствах Android Enterprise в Microsoft Intune. Введите имя подключения, IP-адрес или полное доменное имя VPN-сервера, выберите способ проверки подлинности пользователей и выберите один из типов подключения: Citrix, SonicWall, Check Point Capsule или Pulse Secure.'
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58069b074db2d885ad63f03c4ba5877458bc7bc1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364075"
---
# <a name="android-enterprise-device-settings-to-configure-vpn-in-intune"></a>Параметры устройства Android Enterprise для настройки VPN в Intune

В этой статье перечислены и описаны различные параметры VPN-подключения, которыми можно управлять на устройствах Android Enterprise. В рамках решения по управлению мобильными устройствами (MDM) используйте эти параметры для создания VPN-подключения, выбора способа проверки подлинности VPN, выбора типа VPN-сервера и т. д.

Как администратор службы Intune вы можете создавать и назначать параметры VPN для устройств Android Enterprise. 

Дополнительные сведения о профилях VPN в Intune см. в [этой статье](vpn-settings-configure.md).

> [!NOTE]
> Чтобы настроить режим всегда включенного VPN, необходимо создать профиль VPN и профиль [ограничений устройств](device-restrictions-android-for-work.md#connectivity) с настроенным параметром всегда включенного VPN.

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства](vpn-settings-configure.md#create-a-device-profile) и выберите **Android Enterprise**.

## <a name="device-owner-only"></a>Только владелец устройства

- **Имя подключения**. Введите имя подключения. Конечные пользователи увидят это имя при поиске устройства в списке доступных VPN-подключений. Например, введите `Contoso VPN`.
- **IP-адрес или полное доменное имя**. Укажите IP-адрес или полное доменное имя VPN-сервера, к которому подключаются устройства. Например, введите **192.168.1.1** или **vpn.contoso.com**.

  - **Метод проверки подлинности.** Укажите, как устройства будут проходить проверку подлинности на VPN-сервере. Доступны следующие параметры:
  
    - **Сертификаты**. Выберите существующий профиль сертификата SCEP или PKCS для проверки подлинности подключения. В разделе [Настройка сертификатов](../protect/certificates-configure.md) перечислены шаги для создания профиля сертификата.
    - **Имя пользователя и пароль**. При входе на VPN-сервер пользователям будет предложено ввести имя пользователя и пароль.

- **Тип подключения**. Выберите тип VPN-подключения. Доступны следующие параметры:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**

## <a name="work-profile-only"></a>Только рабочий профиль

- **Имя подключения**. Введите имя подключения. Конечные пользователи увидят это имя при поиске устройства в списке доступных VPN-подключений. Например, введите `Contoso VPN`.
- **IP-адрес или полное доменное имя**. Укажите IP-адрес или полное доменное имя VPN-сервера, к которому подключаются устройства. Например, введите **192.168.1.1** или **vpn.contoso.com**.

  - **Метод проверки подлинности.** Укажите, как устройства будут проходить проверку подлинности на VPN-сервере. Доступны следующие параметры:
  
    - **Сертификаты**. Выберите существующий профиль сертификата SCEP или PKCS для проверки подлинности подключения. В разделе [Настройка сертификатов](../protect/certificates-configure.md) перечислены шаги для создания профиля сертификата.
    - **Имя пользователя и пароль**. При входе на VPN-сервер пользователям будет предложено ввести имя пользователя и пароль.

- **Тип подключения**. Выберите тип VPN-подключения. Доступны следующие параметры:

  - **Cisco AnyConnect**
  - **F5 Access**
  - **Pulse Secure**
  - **SonicWall Mobile Connect**;
  - **Check Point Capsule VPN**;

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

Вы также можете создавать профили VPN для устройств [Android](vpn-settings-android.md), [iOS и iPadOS](vpn-settings-ios.md), [macOS](vpn-settings-macos.md), [Windows 10 и более поздних версий](vpn-settings-windows-10.md), [Windows 8.1](vpn-settings-windows-8-1.md) и [Windows Phone 8.1](vpn-settings-windows-phone-8-1.md).
