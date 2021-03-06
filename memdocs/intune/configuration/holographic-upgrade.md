---
title: Обновление до Windows Holographic for Business
titleSuffix: Microsoft Intune
description: Сведения о том, как обновить устройства с Windows Holographic и перевести их на Windows Holographic for Business
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e809a888fc2696e54540ee6baa2271d7340579
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79361059"
---
# <a name="upgrade-devices-running-windows-holographic-to-windows-holographic-for-business"></a>Обновление устройств с Windows Holographic до Windows Holographic for Business

Microsoft Intune включает множество параметров для управления и защиты устройств. В этой статье перечислены и описаны параметры, которые можно использовать, чтобы обновить устройства Windows Holographic до Windows Holographic for Business. Эти параметры создаются в профиле конфигурации обновлений в Intune, отправляемых или развернутых на устройствах.

В рамках решения в системе управления мобильными устройствами используйте эти параметры для обновления ваших устройств Windows Holographic. Для получения нужной лицензии на обновление Microsoft HoloLens вы можете приобрести пакет Commercial Suite. Дополнительные сведения: [Разблокировка функций Windows Holographic for Business](https://docs.microsoft.com/hololens/hololens1-upgrade-enterprise).

Дополнительные сведения об этой функции см. в разделе [Обновление Windows 10 или выход из S-режима в Intune с помощью профиля конфигурации](edition-upgrade-configure-windows-10.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создайте профиль конфигурации устройства](edition-upgrade-configure-windows-10.md#create-the-profile).

## <a name="edition-upgrade"></a>Обновление выпусков

- В поле **Выпуск, до которого необходимо обновить** выберите **Windows 10 Holographic for Business**.
- **Файл лицензии**: укажите расположение полученного вами XML-файла лицензии.

  ![Введите имя файла XML, которое включает информацию о Holographic for Business.](./media/holographic-upgrade/Holographic-edition-upgrade.png)
 
## <a name="next-steps"></a>Дальнейшие действия

Профиль создан, но пока в нем ничего нельзя делать. Обязательно изучите статьи [Назначение профилей пользователей и устройств в Microsoft Intune](device-profile-assign.md) и [Мониторинг профилей устройств в Microsoft Intune](device-profile-monitor.md).

Вы можете также создать профили обновления выпусков для устройств [Параметры устройства Windows 10 (и более поздних) для обновления выпусков или включения S-режима в Intune](edition-upgrade-windows-settings.md).
