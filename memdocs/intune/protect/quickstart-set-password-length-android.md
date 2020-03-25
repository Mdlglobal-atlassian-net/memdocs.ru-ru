---
title: Краткое руководство. Создание политики соответствия требованиям к паролю для устройств Android
titleSuffix: Microsoft Intune
description: В этом кратком руководстве описано, как с помощью Microsoft Intune настроить длину пароля, требуемую для всех устройств Android.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/21/2019
ms.topic: quickstart
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 81b4fa08-5333-4c54-9f49-8db5f6984ed2
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b7330f50c61679ab91b5f364f718cefcc456435f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351270"
---
# <a name="quickstart-create-a-password-compliance-policy-for-android-devices"></a>Краткое руководство. Создание политики соответствия требованиям к паролю для устройств Android

В этом кратком руководстве описано, как с помощью Microsoft Intune настроить для сотрудников, использующих устройства Android, требование указывать пароль определенной длины для доступа к данным на устройствах Android.

Политика соответствия Intune для устройств указывает правила и параметры, которым должны соответствовать устройства. Политики соответствия можно использовать с условным доступом для разрешения или блокировки доступа к ресурсам организации. Вы также можете получать отчеты об устройствах и принимать меры в случае несоответствия.

> [!IMPORTANT]
> Помимо параметров пароля следует использовать и другие параметры системы безопасности для защиты сотрудников. См. дополнительные сведения о других [параметрах безопасности системы](compliance-policy-create-android-for-work.md).

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).

## <a name="sign-in-to-intune"></a>Вход в Intune

Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) в качестве [глобального администратора](../fundamentals/users-add.md#types-of-administrators) или [администратора службы](../fundamentals/users-add.md#types-of-administrators) Intune.

## <a name="create-a-device-compliance-policy"></a>Создание политики соответствия устройств

Создайте политику соответствия устройств, чтобы настроить для сотрудников, использующих устройства Android, требование указывать пароль определенной длины для доступа к данным на устройствах Android.

1. В Intune выберите **Устройства** > **Политики соответствия** > **Создать политику**.

2. Укажите **Соответствие требованиям для Android** в поле **Имя**. Также введите **Описание**.

3. В качестве **платформы** выберите **Android для бизнеса**.

4. В разделе **Тип профиля** выберите **Рабочий профиль**.

5. Выберите **Параметры** > **Безопасность системы**, чтобы отобразить колонку **Безопасность системы** для Android.

6. В поле **Требовать пароль для разблокировки мобильных устройств** выберите **Требовать**.

7. Для параметра **Требуемый тип пароля** выберите **По крайней мере цифры**.

8. В поле **Минимальная длина пароля** введите значение **6**.

    ![Снимок экрана создания группы в Microsoft Intune](./media/quickstart-set-password-length-android/quickstart-set-password-length-android-01.png)

9. По завершении нажмите кнопки **ОК** > **ОК** > **Создать**, чтобы создать политику.

Если все прошло успешно, созданная политика появится в списке политик соответствия устройств.

## <a name="clean-up-resources"></a>Очистка ресурсов

Если политика больше не нужна, удалите ее. Для этого выберите политику соответствия и нажмите кнопку **Удалить**.

## <a name="next-steps"></a>Дальнейшие шаги

В этом кратком руководстве описано, как с помощью Intune создать политику соответствия требованиям для устройств Android, которые используются вашими сотрудниками, в соответствии с которой пароль должен иметь длину не менее шести символов. Дополнительные сведения о создании политик соответствия см. в разделе [Начало работы с политиками соответствия устройств в Intune](device-compliance-get-started.md).

Чтобы выполнить эту серию кратких руководств по Intune, переходите к следующему руководству.

> [!div class="nextstepaction"]
> [Краткое руководство. Отправка уведомлений на несоответствующие устройства](quickstart-send-notification.md)