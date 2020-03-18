---
title: Настройка интеграции Better Mobile с Intune
titleSuffix: Intune on Azure
description: Интеграция соединителя Better Mobile с Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/25/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: a509c24e4b84c1f72a5efa4f6691f69b8a309f00
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79354143"
---
# <a name="integrate-better-mobile-with-intune"></a>Интеграция Better Mobile с Intune

Чтобы интегрировать решение Better Mobile Threat Defense с Intune, выполните следующие действия.

## <a name="before-you-begin"></a>Подготовка к работе

Следующие шаги необходимо выполнить в консоли администрирования Better Mobile, чтобы установить соединение со службой Better Mobile для зарегистрированных устройств Intune (с помощью соответствия устройств) [и](https://aad.bmobi.net) незарегистрированных устройств (с помощью политик защиты приложений).

Перед началом интеграции Better Mobile с Intune проверьте, что у вас есть следующее.

- Подписка на Microsoft Intune

- Учетные данные администратора Azure Active Directory для предоставления следующих разрешений:

  - Вход и чтение профилей пользователей

  - Доступ к каталогу от имени вошедшего в систему пользователя

  - Чтение данных каталога

  - Отправка сведений об устройстве в Intune

- Учетные данные администратора для доступа к консоли администрирования Better Mobile.

### <a name="better-mobile-app-authorization"></a>Авторизация приложения Better Mobile

Авторизация приложения Better Mobile выполняется следующим образом:

- Вы разрешаете службе Better Mobile передавать в Intune сведения о состоянии работоспособности устройства.

- Better Mobile синхронизируется с членством в группе регистрации Azure AD и заполняет базу данных устройства.

- Вы разрешаете консоли администрирования Better Mobile использовать единый вход Azure AD.

- Вы разрешаете приложению Better Mobile использовать единый вход в Azure AD.

## <a name="to-set-up-better-mobile-integration"></a>Настройка интеграции Better Mobile

1. Перейдите в [консоль администрирования Better Mobile](https://aad.bmobi.net) и войдите со своими учетными данными.
2. Выберите **Интеграция** > **EMM/MDM** > **Добавить учетную запись**.

     ![Изображение консоли администрирования Better Mobile](./media/better-mobile-mtd-connector-integration/better_mobile_console.png)

3. Выберите **Intune**.
4. В поле **Имя учетной записи** введите дескриптор.
5. В **окне входа Майкрософт** введите свои учетные данные Intune.
6. В окне **Запрошенные разрешения** выберите **Принять**.
7. Найдите группы безопасности Azure AD, с которыми Better Mobile необходимо синхронизировать устройства, и выберите их в списке. Затем нажмите **Продолжить**.
8. Нажмите кнопку **Готово**.
9. Вновь откроется страница **Добавление учетной записи**. Закройте эту страницу.

## <a name="next-steps"></a>Дальнейшие шаги

- [Настройка приложений Better Mobile для зарегистрированных устройств](mtd-apps-ios-app-configuration-policy-add-assign.md)
- [Настройка приложений Better Mobile для незарегистрированных устройств](mtd-add-apps-unenrolled-devices.md)