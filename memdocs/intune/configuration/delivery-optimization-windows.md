---
title: Параметры оптимизации доставки для устройств Windows 10 в Microsoft Intune — Azure | Документация Майкрософт
description: Настройте способ, которым устройства Windows 10, управляемые через Intune, используют оптимизацию доставки. Узнайте, как в Intune создать профиль конфигурации устройства, чтобы устанавливать обновления из Интернета, и как заменить существующие круги обновления профилем оптимизации доставки.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: c37563dee40d776d352dec4e0b8ef11b1dc8f67b
ms.sourcegitcommit: 7b3eed763b394075766ea080968889a8538bfe56
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506545"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Параметры оптимизации доставки в Microsoft Intune

С помощью Intune можно применять параметры оптимизации доставки для устройств Windows 10, чтобы снизить использование пропускной способности при загрузке этими устройствами приложений и обновлений. Настройте оптимизацию доставки в своих профилях конфигурации устройств.  

В этой статье описывается, как настроить параметры оптимизации доставки в профиле конфигурации устройства. После создания профиля можно назначить или развернуть этот профиль на устройствах Windows 10.

Список параметров оптимизации доставки, поддерживаемых Intune, представлен в разделе [Параметры оптимизации доставки для Intune](delivery-optimization-settings.md).  

Сведения об оптимизации доставки в Windows 10 см. в разделе [Оптимизация доставки обновлений](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) в документации по Windows.  

## <a name="create-the-profile"></a>Создание профиля

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.

3. Укажите следующие свойства.
   - **Платформа**. Выберите **Windows 10 и более поздних версий**.
   - **Тип профиля**. Выберите **Оптимизация доставки**.

4. Щелкните **Создать**.

5. На странице **Основные** введите имя и описание профиля, а затем щелкните **Далее**.

6. На странице **Параметры конфигурации** укажите способ загрузки обновлений и приложений. Сведения о доступных параметрах см. в разделе [Параметры оптимизации доставки для Intune](delivery-optimization-settings.md).

   Завершив настройку параметров, нажмите **Далее**.

7. На странице **Область (теги)** щелкните **Выберите теги области**, чтобы открыть панель *Выбор тегов*, в которой можно назначить теги области для профиля.
  
   Нажмите кнопку **Далее**, чтобы продолжить.

8. На странице **Назначения** выберите группы, которые получат этот профиль. Дополнительные сведения о назначении профилей см. в статье [Назначение профилей пользователей и устройств](../configuration/device-profile-assign.md).

   Выберите **Далее**.

9. На странице **Правила применимости** используйте параметры **Правило**, **Свойство** и **Значение**, чтобы определить, как этот профиль применяется в назначенных группах.

10. На странице **Проверка и создание** после завершения нажмите **Создать**. Созданный профиль отобразится в списке. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Удаление оптимизации доставки из кругов обновления Windows 10

Оптимизация доставки ранее была настроена в рамках кругов обновления программного обеспечения. Начиная с февраля 2019 г., параметры оптимизации доставки настраиваются в профиле конфигурации устройств, включая дополнительные параметры, влияющие на доставку обновлений программного обеспечения на устройства. Если вы еще не сделали этого, удалите параметр оптимизации доставки из кругов обновления, задав для него значение *Не настроено*, а затем используйте профиль оптимизации доставки для управления широким набором доступных параметров.

1. Создайте профиль конфигурации устройств для оптимизации доставки:

    1. В Центре администрирования Microsoft Endpoint Manager выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
    2. Укажите следующие свойства.

        - **Имя** — Введите описательное имя для нового профиля.
        - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.
        - **Платформа**. Выберите **Windows 10 и более поздних версий**.
        - **Тип профиля**. Выберите **Оптимизация доставки**.
        - **Параметры**: Для **режима скачивания с оптимизацией доставки** выберите тот же режим, который используется в существующем круге обновления программного обеспечения, если вы не хотите менять параметры ваших устройств. Доступны следующие параметры:
            - **Не настроено**.
            - **Только HTTP, без пиринга**.
            - **HTTP и пиринг с общим NAT**.
            - **HTTP и пиринг в частной группе**.
            - **Сочетание HTTP с интернет-пирингом**.
            - **Режим простого скачивания без пиринга**.
            - **Режим обхода**.
    3. Настройте дополнительные параметры, которыми вы хотите управлять.

2. Назначьте этот новый профиль устройствам и пользователям, которые используют существующий круг обновления программного обеспечения. Инструкции см. в статье [Назначение профилей пользователей и устройств в Microsoft Intune](device-profile-assign.md).

3. Чтобы отменить настройки существующего круга обновления программного обеспечения, сделайте следующее:
    1. В Центре администрирования Microsoft Endpoint Manager выберите **Обновления программного обеспечения** &gt; "Круги обновления Windows 10".
    2. В списке выберите свой круг обновления.
    3. В разделе параметров в поле **Режим скачивания с оптимизацией доставки** задайте вариант **Не настроено**.
    4. Последовательно выберите **OK** > **Сохранить**, чтобы сохранить изменения.

## <a name="next-steps"></a>Дальнейшие шаги

[Назначьте профиль](device-profile-assign.md) и выполните [мониторинг его состояния](device-profile-monitor.md).  
См. [параметры оптимизации доставки](delivery-optimization-settings.md) для Intune.
