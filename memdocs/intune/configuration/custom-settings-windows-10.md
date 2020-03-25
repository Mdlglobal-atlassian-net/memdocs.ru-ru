---
title: Добавление настраиваемых параметров для устройств Windows 10 в Microsoft Intune в Azure | Документация Майкрософт
description: Добавьте или создайте настраиваемый профиль для использования параметров OMA-URI для устройств под управлением Windows 10 в Microsoft Intune. Используйте настраиваемый профиль для добавления настраиваемых параметров.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5b6646c67f9425d395bbec1e33c03f6f29b6af7e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361930"
---
# <a name="use-custom-settings-for-windows-10-devices-in-intune"></a>Использование настраиваемых параметров для устройств Windows 10 в Intune

Microsoft Intune позволяет добавить или создать настраиваемые параметры для ваших устройств Windows 10 с помощью настраиваемых профилей. Настраиваемые профили являются компонентом Intune. Они предназначены для добавления параметров и функций устройств, которые не встроены в Intune.

В настраиваемых профилях Windows 10 используются параметры OMA-URI для настройки различных функций. Эти параметры обычно используются производителями мобильного устройства для управления функциями на устройстве. 

В ОС Windows 10 становятся доступными многие параметры поставщика службы конфигурации CSP, например [поставщика службы конфигурации политики](https://technet.microsoft.com/itpro/windows/manage/how-it-pros-can-use-configuration-service-providers).

Если вам нужен какой-то конкретный параметр, не забывайте, что [профиль ограничения устройств Windows 10](device-restrictions-windows-10.md) содержит множество встроенных параметров. Поэтому вам может не потребоваться указывать настраиваемые значения.

Эта статья:

- описывает создание настраиваемого профиля для устройств Windows 10;
- содержит список рекомендуемых параметров OMA-URI;
- содержит пример настраиваемого профиля, который устанавливает VPN-подключение.

## <a name="create-the-profile"></a>Создание профиля

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Профили конфигурации** > **Создать профиль**.
3. Введите следующие параметры:

    - **Имя** — Введите описательное имя для нового профиля. Назначьте имена профилям, чтобы позже их можно было легко найти. Например, хорошее имя профиля — **Настраиваемый профиль Windows 10**.
    - **Описание**. Введите описание профиля. Этот параметр является необязательным, но мы рекомендуем его использовать.
    - **Платформа**. Выберите **Windows 10 и более поздних версий**.
    - **Тип профиля**. Выберите **Пользовательский**.

4. В разделе **Настраиваемые параметры OMA-URI** выберите **Добавить**. Введите следующие параметры:

    - **Имя** — Введите уникальное имя для параметра OMA-URI, чтобы его было проще найти в списке параметров.
    - **Описание**. введите описание с общими сведениями о параметре и другой важной информацией.
    - **OMA-URI** (с учетом регистра): введите код OMA-URI, для которого нужно указать параметр.
    - **Тип данных**. Выберите тип данных для этого параметра OMA-URI. Доступны следующие параметры:

        - Строка
        - Строка (XML-файл)
        - Дата и время
        - Целое число
        - Число с плавающей запятой
        - Логическое значение
        - Base64 (файл)

    - **Значение**: введите значение данных, которое нужно сопоставить с указанным OMA-URI. Значение зависит от выбранного типа данных. Например, если вы выбрали **Дата и время**, выберите значение из управляющего элемента выбора даты.

    После добавления нескольких параметров можно выбрать **Экспорт**. Элемент **Экспорт** создает список всех добавленных значений в файле с разделителями-запятыми (CSV).

5. Нажмите кнопку **OK**, чтобы сохранить изменения. Продолжайте добавлять дополнительные параметры по необходимости.
6. Закончив, нажмите кнопку **ОК** > **Создать** для создания профиля Intune. По завершении профиль отображается в списке **Устройства — профили конфигурации**.

## <a name="example"></a>Пример

В примере ниже параметр **Connectivity/AllowVPNOverCellular** включен. Он позволяет устройству с Windows 10 открыть VPN-подключение по сети мобильной связи.

![Пример настраиваемой политики, содержащий параметры VPN](./media/custom-settings-windows-10/custom-policy-example.png)

## <a name="find-the-policies-you-can-configure"></a>Поиск настраиваемых политик

Полный список всех поставщиков служб конфигурации (CSP), поддерживаемых ОС Windows 10, можно найти в [справочнике поставщиков служб конфигурации](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference).

Не все параметры совместимы со всеми версиями ОС Windows 10. [Справочник поставщиков служб конфигурации](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference) содержит сведения о том, какие версии поддерживаются для каждого поставщика служб конфигурации (CSP).

Кроме того, Intune поддерживает не все параметры, указанные в [этом справочнике](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/configuration-service-provider-reference). Чтобы узнать, поддерживает ли Intune необходимый параметр, откройте соответствующую статью для этого параметра. На странице каждого параметра отображаются сведения о поддерживаемой операции. Для работы с Intune параметр должен поддерживать операции **добавления**, **замены** и **получения**. Если значение, возвращаемое операцией **получения**, не соответствует значению, возвращаемому операцией **добавления** или **замены**, Intune сообщает об ошибке соответствия.

## <a name="next-steps"></a>Дальнейшие шаги

Профиль создан, но он пока ничего не делает. Далее [назначьте профиль](device-profile-assign.md) и [отслеживайте его состояние](device-profile-monitor.md).