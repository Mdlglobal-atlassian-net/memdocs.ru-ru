---
title: Регистрация в Microsoft Intune с использованием функции администратора устройства Android
titleSuffix: ''
description: Регистрация устройств Android в Intune с помощью функции администратора устройства.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/23/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c22da8e3c4fdbcf40c3292476e734dd50f9543a
ms.sourcegitcommit: 017b93345d8d8de962debfe3db5fc1bda7719079
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/21/2020
ms.locfileid: "80086219"
---
# <a name="android-device-administrator-enrollment"></a>Регистрация с использованием функции администратора устройства Android

Функция администратора устройства Android (иногда называют устаревшим режимом управления Android — выпуск Android 2.2) — это способ управлять устройствами Android. Сейчас улучшенная функция управления доступна в [Android для бизнеса](https://www.android.com/enterprise/management/) (выпуск Android 5.0). Чтобы способствовать переходу на современные, расширенные и более безопасные средства управления устройствами, компания Google ограничивает поддержку функции администратора устройства в новых выпусках Android.

Поэтому, чтобы избежать проблем, связанных с этим ограничением, мы рекомендуем зарегистрировать новые устройства с помощью соответствующего процесса, описанного ниже.

По тем же причинам рекомендуется выполнить переход для устройств с функции управления устройством администратором, если они будут обновлены до Android 10. 

Дополнительные сведения о поддержке функции администратора устройства Android в Intune см. в разделе [Уведомления](../fundamentals/whats-new.md#decreasing-support-for-android-device-administrator).

Если вы хотите, чтобы пользователи зарегистрировали свои устройства Android с помощью функции управления администратором устройства, перейдите к следующему разделу.  

Подробнее о функциях Android для бизнеса от Google:
- [Руководство Google по переходу от функции администратора устройства на функцию Android для бизнеса](http://static.googleusercontent.com/media/android.com/en/enterprise/static/2016/pdfs/enterprise/Android-Enterprise-Migration-Bluebook_2019.pdf)
- [Документация Google по прекращению поддержки API администратора устройства](https://developers.google.com/android/work/device-admin-deprecation)

## <a name="set-up-device-administrator-enrollment"></a>Настройка регистрации с использованием функции администратора устройства

1. Чтобы подготовиться к управлению мобильными устройствами, нужно установить **Microsoft Intune** в качестве службы управления мобильными устройствами (MDM). Инструкции см. в статье [Установка центра управления мобильными устройствами](../fundamentals/mdm-authority-set.md). Этот параметр указывается только один раз при первой настройке Intune для управления мобильными устройствами.
2. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) и выберите **Устройства** > **Android** > **Регистрация устройств Android** > **Персональные и корпоративные устройства с правами администрирования устройств** > **Использовать администратор устройств для управления устройствами**.
3. [Расскажите пользователям, как регистрировать устройства](../user-help/enroll-device-android-company-portal.md).  

Когда пользователь зарегистрируется, вы начнете управлять его устройством в Intune, включая [назначение политик соответствия требованиям](../protect/compliance-policy-create-android.md), [управление приложениями](../apps/app-management.md) и многое другое.

Дополнительные сведения о других задачах для пользователей см. в статьях:
- [Ресурсы по пользовательскому интерфейсу Microsoft Intune](../fundamentals/end-user-educate.md)
- [Использование устройства Android с Intune](https://docs.microsoft.com/mem/intune/user-help/why-enroll-android-device)


## <a name="block-device-administrator-enrollment"></a>Блокировка регистрации с использованием функции администратора устройства
Дополнительные сведения о блокировании регистрации устройств Android с функцией администратора устройства или только личных устройств Android см. в разделе [Установка ограничений по типу устройства](enrollment-restrictions-set.md).


## <a name="next-steps"></a>Дальнейшие шаги
- [Назначение политик соответствия](../protect/compliance-policy-create-android.md)
- [Управление приложениями](../apps/app-management.md)
