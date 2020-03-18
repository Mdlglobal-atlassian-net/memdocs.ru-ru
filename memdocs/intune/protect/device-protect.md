---
title: Защита устройств с помощью Microsoft Intune
titleSuffix: Microsoft Intune
description: Некоторые способы защиты устройств от несанкционированного доступа и других угроз с помощью Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2018
ms.topic: conceptual
ms.subservice: protect
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: angerobe
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: c9ee00d13b32e1f52937489b86d29f075e5f580a
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352310"
---
# <a name="protect-devices-with-microsoft-intune"></a>Защита устройств с помощью Microsoft Intune

Microsoft Intune позволяет защитить управляемые устройства, а также хранящиеся на них данные.

## <a name="device-configuration"></a>Конфигурация устройства
[Политики конфигурации](../configuration/device-profiles.md) Intune помогают защитить и настроить устройства путем управления множеством параметров и функций. Пример.

- Можно ограничить на устройстве использование аппаратных возможностей, таких как камера или Bluetooth.
- Можно настроить соответствующие и несоответствующие приложения. При установке несоответствующего приложения вы получите оповещение (а некоторые платформы могут даже блокировать установку).

## <a name="reset-passcodes-when-users-are-locked-out-of-their-devices"></a>Сброс секретных кодов, если пользователи заблокированы на устройствах
Так как первый шаг при защите данных компании на мобильных устройствах — запрос секретного кода перед началом работы, иногда необходимо [сбросить секретный код](../remote-actions/device-passcode-reset.md) или помочь сотруднику сделать это, удалив секретный код или удаленно задав временный секретный код. Вы также можете [выполнить удаленную блокировку устройства](../remote-actions/device-remote-lock.md) при его утере или краже.

## <a name="retire-devices-and-remove-data"></a>Снятие устройств с учета и удаление данных
Если требуется [удалить устройство из системы управления Intune](../remote-actions/devices-wipe.md) (например, когда увольняется пользователь, а также когда устройство потеряно или украдено), вполне вероятно, что вы захотите удалить с него данные. Intune предоставляет несколько методов для защиты данных организации.

## <a name="require-devices-to-be-compliant"></a>Обязательное соответствие для устройств
Intune предоставляет [политики соответствия устройств](device-compliance-get-started.md), позволяющие оценить устройства, не соответствующие заданным правилам (а в некоторых случаях — и исправить ситуацию). Например, вы можете получить отчеты со следующими сведениями:
- об устройствах iOS/iPadOS со снятой защитой;
- о зашифрованных или нешифрованных устройств;
- о работоспособности устройств Windows 10 (в соответствии с определением службы подтверждения работоспособности).

## <a name="protect-apps-and-the-data-they-use"></a>Защита приложений и используемых ими данных
Intune предоставляет целый спектр возможностей для защиты приложений и их данных. Например, политики управления мобильными приложениями (MAM) могут:
- защитить данные от резервного копирования из защищенного приложения;
- ограничить возможность копирования и вставки данных в другие приложения;
- См. дополнительные сведения о [защите приложений и данных с помощью Microsoft Intune](../apps/app-protection-policy.md).

## <a name="add-an-additional-layer-of-protection-to-devices"></a>Добавление дополнительного уровня защиты устройств
[Многофакторная проверка подлинности (MFA)](../enrollment/multi-factor-authentication.md) представляет собой более надежный способ проверки подлинности пользователей устройств в сети.  С MFA пользователи должны подтверждать свою личность по более сложной процедуре (не только с помощью имени пользователя и пароля) — по телефону или через SMS.

## <a name="control-windows-hello-for-business-settings-on-windows-devices"></a>Управление параметрами Windows Hello для бизнеса на устройствах Windows
Intune позволяет интегрировать [Windows Hello для бизнеса](windows-hello.md) — альтернативный метод входа для Windows 10 и более поздней версии, который использует Active Directory или учетную запись Azure Active Directory в качестве замены пароля, смарт-карты или виртуальной смарт-карты.

## <a name="disable-activation-lock-on-ios-devices"></a>Отключение блокировки активации на устройствах с iOS
Блокировка активации — это функция, которая помогает защитить устройства пользователей. Эта функция требует от пользователей вводить их идентификатор Apple ID и пароль, прежде чем кто-либо сможет очистить или повторно активировать устройство. Тем не менее эта функция может привести к проблемам, например, если сотрудник уволился из организации, не сняв блокировку. [Отключение блокировки активации на устройствах с iOS/iPadOS](../remote-actions/device-activation-lock-disable.md) может помочь в решении этой проблемы, удалив блокировку с защищенных устройств с iOS/iPadOS и позволяя вам выполнить перераспределение или очистку данных для этих устройств.

## <a name="next-steps"></a>Дальнейшие шаги

См. дополнительные сведения о [Mobile Threat Defense](mobile-threat-defense.md).