---
title: Краткое руководство. Создание группы для управления пользователями
titleSuffix: Microsoft Intune
description: В этом кратком руководстве вы будете использовать Microsoft Intune для создания группы на основе существующих пользователей.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/17/2020
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 723f4b4e-3090-4811-84ff-6af652abea5a
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7adb23f4709bf3ead07a01cb00d1b38fcb23c40
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79356912"
---
# <a name="quickstart-create-a-group-to-manage-users"></a>Краткое руководство. Создание группы для управления пользователями

В этом кратком руководстве вы будете использовать Intune для создания группы на основе существующих пользователей. Группы используются для управления пользователями и контроля доступа сотрудников к ресурсам компании. Эти ресурсы могут быть частью интрасети вашей компании либо могут быть внешними ресурсами, такими как сайты SharePoint, приложения SaaS или веб-приложения.

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](free-trial-sign-up.md).

>[!NOTE]
>В консоли Intune для вашего удобства доступны предварительно созданные группы **Все пользователи** и **Все устройства** со встроенной оптимизацией.

## <a name="prerequisites"></a>Предварительные условия

- Подписка Microsoft Intune: [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).
- Для работы с этим кратким руководством необходимо [создать пользователя](quickstart-create-user.md).

## <a name="sign-in-to-intune-in-the-microsoft-endpoint-manager"></a>Вход в Intune с помощью Microsoft Endpoint Manager

Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) в качестве [глобального администратора или администратора службы Intune](users-add.md#types-of-administrators). Если вы создали подписку на пробную версию Intune, учетная запись, с помощью которой вы создали подписку, является глобальным администратором.

## <a name="create-a-group"></a>Создание группы

Вы создадите группу, которая будет использоваться далее в этой серии кратких руководств. Создание группы

1. Открыв **Microsoft Endpoint Manager**, выберите **Группы** > **Новая группа**.
2. В раскрывающемся списке **Тип группы** выберите **Безопасность**.
3. В поле **Имя группы** введите имя новой группы (например, **Тестеры Contoso**).
4. Введите **описание группы** для группы.
5. Задайте значение **Назначено** для параметра **Тип членства**. 
6. В разделе **Члены**выберите ссылку и добавьте одного или несколько членов группы из списка.

    ![Снимок экрана создания группы в Microsoft Intune](./media/quickstart-create-group/quickstart-use-groups-01.png)

7. Нажмите **Выбрать** > **Создать**.

Успешно созданная группа появится в списке **Все группы**. 

## <a name="next-steps"></a>Дальнейшие действия

В этом кратком руководстве вы с помощью Intune создали группу на основе существующих пользователей. Дополнительные сведения о добавлении групп в Intune см. в разделе [Добавление групп для организации пользователей и устройств](groups-add.md).

Чтобы выполнить эту серию кратких руководств по Intune, переходите к следующему руководству.

> [!div class="nextstepaction"]
> [Краткое руководство. Настройка автоматической регистрации устройств Windows 10](../enrollment/quickstart-setup-auto-enrollment.md)
