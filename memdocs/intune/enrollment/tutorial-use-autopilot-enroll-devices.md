---
title: Руководство по использованию Autopilot для регистрации устройств в Intune
titleSuffix: Microsoft Intune
description: В этом руководстве вы настроите Windows Autopilot для регистрации устройств в Intune
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 10/19/2018
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
Customer intent: As an Intune admin, I want to set up Windows Autopilot so that users can enroll in Intune.
ms.reviewer: spshumwa
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: e031acf6964c2e43bb355db85dd5e365db1a08ad
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80326899"
---
# <a name="tutorial-use-autopilot-to-enroll-windows-devices-in-intune"></a>Руководство. Использование Autopilot для регистрации устройств Windows в Intune

Windows Autopilot упрощает регистрацию устройств. Благодаря Microsoft Intune и программе Autopilot вы можете предоставлять пользователям новые устройства без необходимости создавать, обслуживать и распространять образы операционной системы.

Из этого руководства вы узнаете, как выполнять следующие задачи:
> [!div class="checklist"]
> * Добавление устройств в Intune.
> * Создание группы устройств Autopilot.
> * Создание профиля развертывания Autopilot.
> * Назначение профиля развертывания Autopilot группе устройств.
> * Распределение устройств между пользователями.

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](../fundamentals/free-trial-sign-up.md).

Общие сведения о преимуществах, сценариях и предварительных требованиях Autopilot см. в документации по [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot).


## <a name="prerequisites"></a>Предварительные условия
- [Настроенная автоматическая регистрация Windows](quickstart-setup-auto-enrollment.md).
- [Подписка Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) <!--&#40;[trial subscription](https://go.microsoft.com/fwlink/?LinkID=816845)&#41;-->


## <a name="add-devices"></a>Добавление устройств

Первым шагом при настройке Windows Autopilot является добавление устройств Windows в Intune. Для этого достаточно создать CSV-файл и импортировать его в Intune.

1. В любом текстовом редакторе создайте список значений с разделителями-запятыми (CSV-файл), которые идентифицируют устройств Windows. Используйте следующий формат:
    
    *серийный номер*, *идентификатор продукта windows*, *хэш-код оборудования*, *необязательный тег группы*
    
    Первые три элемента являются обязательными, а тег группы (прежнее название "идентификатор заказа") можно не указывать.

2. Сохраните CSV-файл.

3. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **Windows** > **Устройства** (в разделе **Программа развертывания Windows Autopilot** > **Импорт**).

    ![Снимок экрана: устройства Windows Autopilot](./media/enrollment-autopilot/autopilot-import-device.png)

4. В разделе **Добавить устройства Windows Autopilot** найдите сохраненный CSV-файл был сохранен.

    ![Снимок экрана: добавление устройств Windows Autopilot](./media/tutorial-use-autopilot-enroll-devices/autopilot-import-device2.png)

5. Выберите **Импорт**, чтобы начать импорт сведений об устройстве. Импорт может занять несколько минут.

4. После завершения импорта выберите **Устройства** > **Windows** > **Регистрация Windows** > **Устройства** (в разделе **Программа развертывания Windows AutoPilot** > **Синхронизация**). Появится сообщение о том, что выполняется синхронизация. На завершение процесса может потребоваться несколько минут в зависимости от количества синхронизируемых устройств.

5. Чтобы увидеть новые устройства, обновите представление.

## <a name="create-an-autopilot-device-group"></a>Создание группы устройств Autopilot.

Теперь вы создадите группу устройств и разместите в ней только что загруженные устройства Autopilot.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) щелкните **Группы** > **Создать группу**.
2. В колонке **Группа**
    1. В качестве **Типа группы** выберите **Безопасность**.
    2. В поле **Имя группы** введите *Группа Autopilot*. В поле **Описание группы** введите текст *Тестовая группа для устройств Autopilot*.
    3. В поле **Тип членства** выберите **Назначено**.
3. В колонке **Группа** выберите **Члены** и добавьте в группу устройства Autopilot. Для еще не зарегистрированных устройств Autopilot в качестве имени используется серийный номер устройства.
4. Выберите команду **Создать**.  

## <a name="create-an-autopilot-deployment-profile"></a>Создание профиля развертывания Autopilot.

Создав группу устройств, необходимо создать профиль развертывания, который позволяет настроить устройства Autopilot.

1. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **Windows** > **Регистрация Windows** > **Профили развертывания** > **Создать профиль**.
2. На странице **Основные сведения** введите для параметра **Имя** значение *Профиль Autopilot*. В поле **Описание** введите текст *Тестовый профиль для устройств Autopilot*.
3. Для параметра **Convert all targeted devices to Autopilot** (Преобразовать все целевые устройства в Autopilot) выберите вариант **Да**. Этот параметр гарантирует, что все устройства из списка будут зарегистрированы в службе развертывания Autopilot. Регистрация завершится в течение 48 часов.
4. Выберите **Далее**.
5. На странице **Готовый интерфейс (OOBE)** для параметра **Режим развертывания** выберите **Под управлением пользователя**. Устройства с таким профилем связываются с пользователем, регистрирующим устройство. Для регистрации устройства нужны учетные данные пользователя.
6. В поле **Тип присоединения к Azure AD** выберите **Присоединено к Azure AD**.
7. Настройте указанные ниже параметры, а для остальных задайте значения по умолчанию:
    - **Лицензионное соглашение (EULA)** : **Скрыть**
    - **Параметры конфиденциальности**: **Показать**
    - **Тип учетной записи пользователя**: **Стандартный**
8. Выберите **Далее**.
9. На странице **Назначения** выберите значение **Выбранные группы** для параметра **Кому назначить**.
10. Выберите **Выбрать группы для включения** и **Группа Autopilot**.
11. Выберите **Далее**.
12. На странице **Отзыв и создание** выберите **Создать**, чтобы создать профиль.

## <a name="distribute-devices-to-users"></a>Распределение устройств пользователям

Теперь можно распределить устройства Windows между пользователями. При первом входе пользователей система Autopilot автоматически выполнит регистрацию и настройку устройств. 

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не планируете далее использовать устройства Autopilot, их можно удалить.

1. Если устройства зарегистрированы в Intune, сначала [удалите их на портале Azure Active Directory](../remote-actions/devices-wipe.md#delete-devices-from-the-azure-active-directory-portal).

2. В [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите **Устройства** > **Windows** > **Регистрация Windows** > **Устройства** (в разделе **Программа развертывания Windows Autopilot**).

3. Выберите удаляемые устройства и нажмите кнопку **Удалить**.

4. Подтвердите удаление, щелкнув **Да**. Этот процесс может занять несколько минут.

## <a name="next-steps"></a>Дальнейшие шаги

См. дополнительные сведения о других параметрах, доступных для Windows Autopilot.

> [!div class="nextstepaction"]
> [Подробная статья о регистрации Autopilot](enrollment-autopilot.md)


