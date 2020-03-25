---
title: Параметры соответствия для Windows 8.1 в Microsoft Intune в Azure | Документация Майкрософт
description: Список всех параметров, которые можно использовать при настройке соответствия требованиям для устройств с Windows 8.1 и Windows Phone 8.1 в Microsoft Intune. Проверка соответствия на минимальное и максимальное значение версии операционной системы, ограничения и длину пароля, включение шифрования для хранения данных и многое другое.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/22/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0189fea7f73b70286a6daf844a10806d4c1e8a5d
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353207"
---
# <a name="windows-81-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Параметры Windows 8.1, позволяющие пометить устройства как соответствующие или не соответствующие политике с помощью Intune

В этой статье перечислены и описаны параметры соответствия, которыми можно управлять на устройствах с Windows 8.1. Используйте эти параметры в рамках решения для управления мобильными устройствами, чтобы блокировать использование простых паролей, задать минимальную и максимальную версии ОС и многое другое.

Данная функция применяется к:

- Windows Phone 8.1
- Windows 8.1 и более поздние версии

Как администратор Intune используйте эти параметры соответствия для защиты ресурсов организации. Дополнительные сведения о политиках соответствия требованиям и их действии см. в статье [Начало работы с политиками соответствия устройств](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создание политики соответствия](create-compliance-policy.md#create-the-policy) В качестве **платформы** выберите **Windows Phone 8.1** или **Windows 8.1 и более поздние версии**.

## <a name="device-properties"></a>Свойства устройства

### <a name="operating-system-version"></a>Версия операционной системы

**Windows Phone 8.1 и более поздней версии**
- **Минимальная версия ОС для мобильных устройств**.  
  Введите минимально допустимую версию. Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Приводится ссылка на сведения о том, как выполнить обновление. Пользователь может обновить устройство, после чего он получит доступ к ресурсам организации.

- **Максимальная версия ОС для мобильных устройств**.  
  Введите максимально допустимую версию. Если устройство использует версию ОС, более позднюю по сравнению с указанной в правиле, доступ к ресурсам организации блокируется. Пользователю устройства будет предложено связаться с ИТ-администратором. Пока вы не измените правило, разрешив использовать эту версию ОС, устройство не будет иметь доступ к ресурсам организации.

**Windows 8.1 и более поздние версии**
- **Минимальная версия ОС**.  
  Введите минимально допустимую версию. Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Приводится ссылка на сведения о том, как выполнить обновление. Пользователь может обновить устройство, после чего он получит доступ к ресурсам организации.

- **Максимальная версия ОС**.  
  Введите максимально допустимую версию. Если устройство использует версию ОС, более позднюю по сравнению с указанной в правиле, доступ к ресурсам организации блокируется. Пользователю устройства будет предложено связаться с ИТ-администратором. Пока вы не измените правило, разрешив использовать эту версию ОС, устройство не будет иметь доступ к ресурсам организации.

Компьютеры под управлением Windows 8.1 возвращают версию **3**. Если для Windows в правиле ОС задано значение Windows 8.1, устройство считается несоответствующим, даже если на нем установлена версия ОС Windows 8.1.

## <a name="system-security"></a>Безопасность системы

### <a name="password"></a>Пароль

- **Требовать пароль для разблокировки мобильных устройств**  
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — пользователи должны ввести пароль, прежде чем они смогут получить доступ к своему устройству.

- **Простые пароли**.  
  - **Не настроено** (*по умолчанию*) — пользователи могут создавать простые пароли, например **1234** или **1111**.
  - **Блокировать** — пользователи не могут создавать простые пароли, такие как **1234** или **1111**.  

- **Минимальная длина пароля**.  
  Введите минимальное число цифр или символов в пароле пользователя.

  Для устройств, работающих под управлением Windows и доступ к которым осуществляется с помощью учетной записи Майкрософт, политика соответствия требованиям не сможет правильно выполнить оценку, если выполняется любое из следующих условий.  
  - Минимальная длина пароля — больше восьми символов
  - Минимальное число наборов символов — больше двух

- **Тип пароля**.  
  Укажите, каким должен быть пароль: содержать только **цифры** или сочетание цифр и других символов (**буквы и цифры**).

  Если задано значение *Буквенно-цифровой*, доступен следующий параметр.  

  - **Число символов в пароле, кроме букв и цифр**.  
    Если для параметра *Тип пароля* задано значение **Буквенно-цифровой**, укажите минимальное число наборов символов, которое должен содержать пароль. Доступные значения: от **0** до **4** наборов и значение по умолчанию — **1**.
    
    Используются следующие четыре набора символов:
    - Строчные буквы
    - Прописные буквы
    - Символы
    - Numbers

    Чем больше значение, тем более сложный пароль нужно придумать пользователю. Для устройств, доступ к которым осуществляется с помощью учетной записи Майкрософт, политика соответствия требованиям не сможет правильно выполнить оценку, если выполняется любое из следующих условий.

    - Минимальная длина пароля — больше восьми символов
    - Минимальное число наборов символов — больше двух

- **Максимальное время бездействия (в минутах), по истечении которого запрашивается пароль**.  
  Введите время бездействия, по истечении которого пользователю потребуется ввести пароль повторно.

- **Срок действия пароля (в днях)** .  
  Укажите число дней, по истечении которых пользователю понадобится создать новый пароль.

- **Число предыдущих паролей для запрета повторного использования**.  
  Введите число предыдущих паролей, которые нельзя использовать повторно.

### <a name="encryption"></a>Encryption

- **Шифрование хранилища данных на устройстве**.  
  - **Не настроено** (*по умолчанию*)
  - **Требовать** — используйте параметр *Требовать* для шифрования хранилища данных на ваших устройствах.


<!-- not on phone   
- **Require encryption on mobile device**: **Require** the device to be encrypted to connect to data storage resources.
--> 

## <a name="next-steps"></a>Дальнейшие шаги

- [Добавление действий для несоответствующих устройств](actions-for-noncompliance.md) и [Использовать теги области для фильтрации политик](../fundamentals/scope-tags.md).
- [Мониторинг политик соответствия](compliance-policy-monitor.md).
- См. раздел [Параметры политики соответствия для устройств с Windows 10 и более поздними версиями](compliance-policy-create-windows.md).