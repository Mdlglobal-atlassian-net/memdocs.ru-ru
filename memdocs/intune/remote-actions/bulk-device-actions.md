---
title: Использование массовых действий устройств на устройстве с Microsoft Intune.
titleSuffix: ''
description: Использование массовых удаленных действий устройств.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 3/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3c1b9a695830380c00900d0fe94ec075b21def0a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989353"
---
# <a name="use-bulk-device-actions"></a>Использование массовых действий устройств

Вы можете использовать массовые действия устройств для выполнения следующих удаленных действий.
- [Сброс Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset)
- [Настраиваемые уведомления](custom-notifications.md#send-a-custom-notification-to-a-single-device)
- [Удалить](devices-wipe.md#delete-devices-from-the-intune-portal)
- [Переименовать](device-rename.md)
- [Перезапуск](device-restart.md)
- [Синхронизация](device-sync.md)
- [Очистка](devices-wipe.md#wipe)

## <a name="use-a-bulk-device-action"></a>Использование массового действия устройства

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Последовательно выберите **Устройства** > **Все устройства** > **Массовые действия устройств**.
![Массовые действия устройств](./media/bulk-device-actions/bulk-device-actions.png)
3. На странице **Массовое действие устройства** выберите **ОС** и **Действие устройства**. Для некоторых действий нужно указать дополнительные параметры или заполнить дополнительные поля. Нажмите кнопку **Далее**.
4. На странице **Устройства** выберите от 1 до 100 устройств и нажмите кнопку **Далее**.
5. На странице **Проверка и создание** нажмите кнопку **Создать**.

## <a name="next-steps"></a>Дальнейшие действия
[Общие сведения об управлении устройствами](device-management.md)
