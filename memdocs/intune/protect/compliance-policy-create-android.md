---
title: Параметры соответствия устройств с Android в Microsoft Intune — Azure | Документация Майкрософт
description: Список всех параметров, которые можно использовать при настройке соответствия требованиям для устройств с Android в Microsoft Intune. Задайте набор правил для паролей, выберите минимальную или максимальную версию операционной системы, ограничьте использование конкретных приложений, предотвратите повторное использование паролей и многое другое.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729230"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Параметры Android, позволяющие пометить устройства как соответствующие или не соответствующие политике с помощью Intune

В этой статье перечислены и описаны параметры соответствия, которыми можно управлять на устройствах с Android. Используйте эти параметры в рамках своего решения для управления мобильными устройствами, чтобы помечать устройства с административным доступом (со снятой защитой) как не соответствующие требованиям, настроить допустимый уровень угроз, включить защиту Google Play и многое другое.

Данная функция применяется к:

- Администратор устройства с Android

Как администратор Intune используйте эти параметры соответствия для защиты ресурсов организации. Дополнительные сведения о политиках соответствия требованиям и их действии см. в статье [Начало работы с политиками соответствия устройств](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создание политики соответствия](create-compliance-policy.md#create-the-policy) В поле **Платформа** выберите значение **Администратор устройства Android**.

## <a name="microsoft-defender-atp"></a>ATP в Microsoft Defender

- **Требовать тот же или более низкий уровень риска устройства**  

  Выберите максимально допустимый уровень риска для устройств, оцениваемых ATP в Microsoft Defender. Устройства, превышающие этот показатель, помечаются как несоответствующие.
  - **Не настроено** (*по умолчанию*)
  - **Очистить**
  - **Низкая**
  - **Средняя**
  - **Высокая**

## <a name="device-health"></a>Работоспособность устройств

- **Устройства под управлением администратора**  
  Возможности для *администратора устройств* заменены на возможности Android для бизнеса.

  - **Не настроено** (*по умолчанию*)
  - **Блокировать** — при блокировке администратора устройства пользователям будет предложено перейти к управлению рабочим профилем Android Enterprise для восстановления доступа.

- **Устройство с root-доступом**  
  Предотвращение корпоративного доступа к устройствам с административным доступом. (Эта проверка соответствия поддерживается для Android 4.0 и более поздних версий.)

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — пометить устройства с административным доступом (со снятой защитой) как не соответствующие требованиям.

- **Требовать тот же или более низкий уровень угрозы для устройства**  
  Этот параметр позволяет использовать оценку рисков в подключенной службе Mobile Threat Defense как условие для проверки соответствия требованиям.

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Безопасное** — это самый безопасный уровень, при котором устройство не может содержать угроз. В случае обнаружения на устройстве угрозы любого уровня оно признается не соответствующим требованиям.
  - **Низкий** — если обнаруженные на устройстве угрозы имеют низкий уровень, считается, что оно соответствует требованиям. Любая угроза с уровнем выше низкого переводит устройство в состояние несоответствия.
  - **Средний** — если обнаруженные на устройстве угрозы имеют низкий или средний уровень, считается, что оно соответствует требованиям. Если на устройстве найдены угрозы с высоким уровнем, оно признается не соответствующим требованиям.
  - **Высокий** — этот уровень является наименее безопасным и включает все уровни угроз. Он может быть полезным при использовании решения только для формирования отчетов.

### <a name="google-play-protect"></a>Google Play Protect

- **Сервисы Google Play настроены**  
  Сервисы Google Play предоставляют обновления системы безопасности и зависимость базового уровня для реализации многих функций безопасности на устройствах, сертифицированных Google.

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.  
  - **Требовать** — приложение служб Google Play должно быть установлено и включено.  

- **Обновление поставщика безопасности**

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — обновляемый поставщик безопасности должен защищать устройство от известных уязвимостей.

- **Проверка угроз в приложениях**

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — требовать включения функции **Проверка приложений** в Android.

  > [!NOTE]
  > В прежних версиях платформы Android эта функция представлена параметром обеспечения соответствия. Intune может только проверить, включен ли этот параметр на уровне устройства.

- **Аттестация устройства SafetyNet**  
  Введите уровень [аттестации SafetyNet](https://developer.android.com/training/safetynet/attestation.html), которого требуется достичь. Доступны следующие параметры:

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Проверка базовой целостности**.
  - **Проверка базовой целостности и сертифицированных устройств**.

> [!NOTE]
> Чтобы настроить параметры защиты Google Play с помощью политик защиты приложений, см. в статье [Параметры политики защиты приложений Intune](../apps/app-protection-policy-settings-android.md#conditional-launch) раздел для Android.

## <a name="device-properties"></a>Свойства устройства

### <a name="operating-system-version"></a>Версия операционной системы

- **Минимальная версия ОС**  
  Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Отобразится ссылка со сведениями о том, как выполнить обновление. Пользователь может обновить устройство, после чего он получит доступ к ресурсам организации.

  *По умолчанию версия не настроена*.

- **Максимальная версия ОС**  
  Если устройство использует версию ОС, более позднюю по сравнению с указанной в правиле, доступ к ресурсам организации блокируется. Пользователю будет предложено обратиться к ИТ-администратору. До изменения правила для разрешения конкретной версии ОС это устройство невозможно будет использовать для доступа к ресурсам организации.

  *По умолчанию версия не настроена*.

## <a name="system-security"></a>Безопасность системы

### <a name="password"></a>Пароль

- **Требовать пароль для разблокировки мобильных устройств**  
  *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

  Этот параметр указывает, потребуется ли пользователю вводить пароль, прежде чем он сможет получить доступ к данным на своем мобильном устройстве. Рекомендованное значение: Require  

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — пользователи должны ввести пароль, прежде чем они смогут получить доступ к своему устройству.

- **Требуемый тип пароля**  
  *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

  Укажите, каким должен быть пароль: содержать только цифровые символы или сочетание цифр и других символов.

  - **По умолчанию для устройства**. Чтобы оценить соответствие паролей требованиям, обязательно выберите стойкость пароля, отличную от **По умолчанию для устройства**.
  - **Биометрический с низким уровнем безопасности**
  - **По крайней мере числа**
  - **Числовой комплекс** — повторяющиеся или последовательные числа, такие как `1111` или `1234`, не допускаются.
  - **По крайней мере буквы**
  - **По крайней мере буквы и цифры**
  - **По крайней мере цифры, буквы и символы**

  В зависимости от конфигурации этого параметра доступны один или несколько из следующих вариантов.

  - **Минимальная длина пароля**  
    *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

    Введите минимальное число цифр или символов в пароле пользователя.

  - **Максимальное время бездействия (в минутах), по истечении которого запрашивается пароль**  
    *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

    Введите время бездействия, по истечении которого пользователю потребуется ввести пароль повторно. Если вы укажете **Не настроено** (по умолчанию), этот параметр не учитывается при оценке соответствия требованиям.

  - **Число дней до обязательной смены пароля**  
  *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

  Укажите число дней, по истечении которого пользователю необходимо создать новый пароль.

  - **Число предыдущих паролей для запрета повторного использования**  
    Введите число недавних паролей, которые не могут использоваться повторно. С помощью этого параметра можно запретить пользователю применять использованные ранее пароли. (Поддерживается для Android 4.0 и более поздних версий или KNOX 4.0 и более поздних версий.)

### <a name="encryption"></a>Encryption

- **Шифрование хранилища данных на устройстве**  
  *Поддерживается в Android 4.0 и более поздних версиях или KNOX 4.0 и более поздних версиях.*

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — шифрование хранилища данных на устройствах. Шифрование для устройств будет включено, если выбран параметр **Require a password to unlock mobile devices** (Запрашивать пароль для разблокировки мобильных устройств).

### <a name="device-security"></a>Безопасность устройств

- **Блокировать приложения из неизвестных источников**.  
  *Поддерживается в версиях с Android 4.0 по Android 7.x. Не поддерживается для Android 8.0 и более поздних версий*

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — блокировка устройств со включенными источниками **Безопасность > Неизвестные источники** (*поддерживается в версиях с Android 4.0 по Android 7.x. Не поддерживается в Android 8.0 и более поздних версиях*).

  Для загрузки неопубликованных приложений необходимо разрешить неизвестные источники. Установите **Заблокировать**, чтобы включить эту политику соответствия требованиям, если вы не загружаете неопубликованные приложения Android.

  > [!IMPORTANT]
  > Для загрузки неопубликованных приложений требуется, чтобы параметр **Block apps from unknown sources** (Блокировать приложения из неизвестных источников) был включен. Примените эту политику соответствия требованиям, только если вы не загружаете на устройства неопубликованные приложения Android.

- **Целостность среды выполнения приложения корпоративного портала**
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — выберите *Требовать*, чтобы подтвердить, что приложение корпоративного портала соответствует всем следующим требованиям:

    - Среда выполнения по умолчанию установлена.
    - Имеется надлежащая подпись.
    - Не находится в режиме отладки.
    - Установлено из известного источника.

- **Блокировать отладку по USB на устройстве**;  
  *(Поддерживается в Android 4.2 и более поздних версий)*

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — запретить устройствам использовать функцию отладки USB.

- **Минимальный уровень обновления для системы безопасности**  
  *(Поддерживается в Android 6.0 и более поздних версий)*

  Выберите самый старый уровень обновления системы безопасности для устройства. Устройства, не имеющие этот уровень обновления безопасности или выше, считаются не соответствующими политике. Дату необходимо ввести в формате `YYYY-MM-DD`.

  *По умолчанию дата не настроена*.

- **Ограниченные приложения**  
  Введите **Имя приложения** и **Идентификатор пакета приложения** для приложений, которые должны быть ограничены, а затем выберите **Добавить**. Устройство, на котором установлено хотя бы одно ограниченное приложение, помечается как не соответствующее требованиям.

## <a name="next-steps"></a>Дальнейшие шаги

- [Добавление действий для несоответствующих устройств](actions-for-noncompliance.md) и [Использовать теги области для фильтрации политик](../fundamentals/scope-tags.md).
- [Мониторинг политик соответствия](compliance-policy-monitor.md).
- См. раздел [Параметры политики соответствия для Android для бизнеса](compliance-policy-create-android-for-work.md).
