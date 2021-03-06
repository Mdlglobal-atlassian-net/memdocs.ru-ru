---
title: Использование политик для упрощения управления компьютерами Windows
titleSuffix: Microsoft Intune
description: Описание политик управления компьютерами Windows и параметров для Центра Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/01/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f0afda7e-f4c3-4bcd-b4bf-4304103cf73e
ms.reviewer: owenyen
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic-keep
ms.collection: M365-identity-device-management
ms.openlocfilehash: 275939c4c97b25f7e9b2ab179a7491d47801e48e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79355066"
---
# <a name="use-policies-to-simplify-windows-pc-management"></a>Использование политик для упрощения управления компьютерами Windows

[!INCLUDE [classic-portal](../includes/classic-portal.md)]

Для управления настольными системами Windows как компьютерами путем запуска на них программного клиента Intune можно использовать только политики из группы **Управление компьютером** в консоли администрирования Intune. Все другие политики, указанные в консоли администрирования, предназначены только для мобильных устройств. С помощью политик **Управление компьютером** можно настроить параметры в Microsoft Intune Center, управлять обновлениями ПК и настроить брандмауэр Windows для ПК.

![Шаблон политик для компьютеров под управлением Windows](./media/use-policies-to-simplify-windows-pc-management/pc_policy_template.png)

## <a name="manage-the-microsoft-intune-center"></a>Управление Microsoft Intune Center
Пользователи видят программный клиент Intune как **Microsoft Intune Center**. Microsoft Intune Center позволяет пользователям:

- получать приложения с корпоративного портала;

- проверять наличие обновлений;

- управлять программой Microsoft Intune Endpoint Protection;

- запрашивать удаленную помощь.

Microsoft Intune Center устанавливается на всех управляемых компьютерах. В политике Intune Center можно настроить следующие параметры, которые будут отображаться для пользователей в Microsoft Intune Center:

|Параметр политики|Сведения|
|------------------|--------------------|
|**Имя**|Имя администратора, который управляет компьютером.<br />Максимальная длина: 40 символов|
|**Номер телефона**|Номер телефона администратора, который управляет компьютером.<br />Максимальная длина: 20 символов.|
|**Адрес электронной почты**|Адрес электронной почты администратора, который управляет компьютером.<br />Максимальная длина: 40 символов|
|**Название веб-сайта**|Название веб-сайта технической поддержки для пользователей.<br />>Максимальная длина: 40 символов|
|**URL-адрес веб-сайта**|URL-адрес веб-сайта технической поддержки.<br />Максимальная длина: 150 символов.|
|**Примечания**|Примечание, отображаемое для пользователей.<br />Максимальная длина: 120 символов.|

Сведения о политиках и параметрах, которые можно настроить для ПК с ОС Windows, см. в следующих ресурсах:

- [Обновление программного обеспечения на компьютерах с Windows при помощи Microsoft Intune](keep-windows-pcs-up-to-date-with-software-updates-in-microsoft-intune.md) — эти политики принуждают управляемые компьютеры искать и скачивать обновления программного обеспечения Майкрософт и других поставщиков. Эти обновления не включают обновления ОС (например, обновление с Windows 7 до Windows 10 или обновления с одной из версий Windows 10 до более поздней).

- [Обеспечение защиты компьютеров с ОС Windows с помощью Endpoint Protection для Microsoft Intune](help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune.md) — эти параметры включают расписания проверки и действия, которые необходимо предпринять при обнаружении вредоносного ПО.

- [Для защиты компьютеров под управлением Windows используйте политики брандмауэра Windows в Microsoft Intune](help-protect-windows-pcs-using-windows-firewall-policies-in-microsoft-intune.md) — эти политики упрощают администрирование параметров брандмауэра Windows на управляемых компьютерах.

## <a name="see-also"></a>См. также

[Общие задачи управления ПК с Windows с программным клиентом Intune](common-windows-pc-management-tasks-with-the-microsoft-intune-computer-client.md)
