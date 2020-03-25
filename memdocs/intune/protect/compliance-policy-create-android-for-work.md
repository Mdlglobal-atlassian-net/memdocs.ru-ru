---
title: Параметры соответствия Android для бизнеса в Microsoft Intune (Azure) | Документация Майкрософт
description: Список всех параметров, которые можно использовать при настройке соответствия требованиям для устройств с Android для бизнеса в Microsoft Intune. Задайте набор правил для паролей, выберите минимальную или максимальную версию операционной системы, ограничьте использование конкретных приложений, предотвратите повторное использование паролей и многое другое.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/07/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 9da89713-6306-4468-b211-57cfb4b51cc6
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26bd9a92343c1ddcc31c1ff65b43643f3d9e22c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353363"
---
# <a name="android-enterprise-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Параметры Android для бизнеса, позволяющие пометить устройства как соответствующие или не соответствующие политике с помощью Intune

В этой статье перечислены и описаны параметры соответствия, которыми можно управлять на устройствах с Android для бизнеса. Используйте эти параметры в рамках своего решения для управления мобильными устройствами, чтобы помечать устройства с административным доступом (со снятой защитой) как не соответствующие требованиям, настроить допустимый уровень угроз, включить защиту Google Play и многое другое.

Данная функция применяется к:

- Android для бизнеса

Как администратор Intune используйте эти параметры соответствия для защиты ресурсов организации. Дополнительные сведения о политиках соответствия требованиям и их действии см. в статье [Начало работы с политиками соответствия устройств](device-compliance-get-started.md).

> [!IMPORTANT]
> Политики соответствия требованиям также применяются к выделенными устройствам Android для бизнеса. Если политика соответствия назначена выделенному устройству, устройство может отображаться как **Не соответствующие требованиям**. Условный доступ и принудительное соответствие недоступны на выделенных устройствах. Не забудьте завершить все задачи или действия, чтобы обеспечить соответствие выделенных устройств назначенным политикам.

## <a name="before-you-begin"></a>Подготовка к работе

[Создание политики соответствия](create-compliance-policy.md#create-the-policy) В качестве **платформы** выберите **Android для бизнеса**.

## <a name="device-owner"></a>Владелец устройства.

### <a name="device-health"></a>Работоспособность устройств

- **Require the device to be at or under the Device Threat Level** (Требовать тот же или более низкий уровень риска устройства). Выберите максимальный уровень угроз для устройства, оцениваемый [службой защиты мобильных устройств от угроз](mobile-threat-defense.md). Устройства, превышающие этот уровень угрозы, будут отмечены как несоответствующие. Чтобы использовать этот параметр, выберите допустимый уровень угрозы:

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Защищено** — это самый безопасный уровень, при котором устройство не может содержать угроз. В случае обнаружения на устройстве угрозы любого уровня оно признается не соответствующим требованиям.
  - **Низкий** — если обнаруженные на устройстве угрозы имеют низкий уровень, считается, что устройство соответствует требованиям. Любая угроза с уровнем выше низкого переводит устройство в состояние несоответствия.
  - **Средний** — если обнаруженные на устройстве угрозы имеют низкий или средний уровень, считается, что устройство все еще соответствует требованиям. Если на устройстве найдены угрозы с высоким уровнем, оно признается не соответствующим требованиям.
  - **Высокий** — этот уровень является наименее безопасным и включает все уровни угроз. Он может быть полезным при использовании решения только для формирования отчетов.
  
> [!NOTE] 
> Все поставщики защиты мобильных устройств от угроз (MTD) поддерживаются в развертываниях владельцев устройств Android для бизнеса с помощью конфигурации приложения. Обратитесь к поставщику MTD, чтобы получить точную конфигурацию, необходимую для поддержки платформ владельцев устройств Android для бизнеса в Intune.

#### <a name="google-play-protect"></a>Google Play Protect

- **SafetyNet device attestation** (Аттестация устройств SafetyNet). Введите уровень [аттестации SafetyNet](https://developer.android.com/training/safetynet/attestation.html), которого требуется достичь. Доступны следующие параметры:
  - **Не настроено** (*по умолчанию*) — этот параметр не проверяется на соответствие или несоответствие.
  - **Проверка базовой целостности**.
  - **Проверка базовой целостности и сертифицированных устройств**.

### <a name="device-properties"></a>Свойства устройства

#### <a name="operating-system-version"></a>Версия операционной системы

- **Минимальная версия ОС**. Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Приводится ссылка на сведения о том, как выполнить обновление. Пользователь может обновить устройство и получить доступ к ресурсам организации.

  *По умолчанию версия не настроена*.

- **Максимальная версия ОС**. Если устройство использует версию ОС, более позднюю по сравнению с указанной в правиле, доступ к ресурсам организации блокируется. Пользователю будет предложено обратиться к ИТ-администратору. Пока вы не измените правило для разрешения конкретной версии ОС, это устройство не сможет получать доступ к ресурсам организации.

  *По умолчанию версия не настроена*.

- **Минимальный уровень обновления для системы безопасности**.  Выберите самый старый уровень обновления системы безопасности для устройства. Устройства, не имеющие этот уровень обновления безопасности или выше, считаются не соответствующими политике. Дату необходимо ввести в формате ГГГГ-ММ-ДД.

  *По умолчанию дата не настроена*.


### <a name="system-security"></a>Безопасность системы

- **Требовать пароль для разблокировки мобильных устройств** 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — пользователи должны ввести пароль, прежде чем они смогут получить доступ к своему устройству.
  - **Требуемый тип пароля**. Укажите, каким должен быть пароль: содержать только цифровые символы или сочетание цифр и других символов. Доступны следующие параметры:
    - **По умолчанию для устройства**. Чтобы оценить соответствие паролей требованиям, обязательно выберите стойкость пароля, отличную от **По умолчанию для устройства**.  
    - **Password required, no restrictions** (Требуется пароль, без ограничений)
    - **Ненадежные биометрические данные** - [Надежные и ненадежные биометрические данные](https://android-developers.googleblog.com/2018/06/better-biometrics-in-android-p.html) (откроется веб-сайт Android)
    - **Числовой** (*по умолчанию*). Пароль должен состоять только из цифр, например `123456789`. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
    - **Числовой комплекс**. Не допускаются комбинации из повторяющихся или идущих подряд цифр, такие как "1111" или "1234". Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
    - **Буквенный**. Обязательно использовать буквы алфавита. Цифры и символы не требуются. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
    - **Буквенно-цифровой**. Включает заглавные буквы, строчные буквы и цифровые символы. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
    - **Буквенно-цифровой с символами**. Включает заглавные и строчные буквы, цифры, знаки пунктуации и символы. Кроме того, укажите:
    
    В зависимости от выбранного *типа пароля* доступны следующие параметры:  
    - **Минимальная длина пароля**. Укажите минимальное число символов, которое должно быть в пароле (от 4 до 16 символов).  

    - **Требуемое число символов**. Укажите число символов, которое должно быть в пароле (от 0 до 16).

    - **Требуемое число строчных букв**. Укажите число строчных букв, которое должно быть в пароле (от 0 до 16).

    - **Требуемое число прописных букв**. Укажите число прописных букв, которое должно быть в пароле (от 0 до 16).

    - **Требуемое число небуквенных символов**. Укажите количество символов, не являющихся буквами (кроме букв алфавита), которое должно быть в пароле (от 0 до 16 символов).

    - **Требуемое число цифр**. Укажите количество числовых символов (`1`, `2`, `3` и т. д.), которое должно быть в пароле (от 0 до 16 символов).
    
    - **Требуемое число символов**. Укажите количество символов (`&`, `#`, `%` и т. д.), которое должно быть в пароле (от 0 до 16 символов).
 
- **Максимальное время бездействия (в минутах), по истечении которого запрашивается пароль**. Введите время бездействия, по истечении которого пользователю потребуется ввести пароль повторно. Доступны следующие варианты: *Не настроено* и от *1 минуты* до *8 часов*.

- **Число дней до обязательной смены пароля**. Укажите число дней, от 1 до 365, до обязательной смены пароля на устройстве. Например, чтобы изменить пароль через 60 дней, введите `60`. Когда срок действия пароля истекает, пользователям предлагается создать пароль.

   *По умолчанию значение не настроено*.

- **Число паролей, которые необходимо использовать перед повторным использованием пароля**. Введите число недавних паролей, от 1 до 24, которые не могут использоваться повторно. С помощью этого параметра можно запретить пользователю применять использованные ранее пароли.  

    *По умолчанию версия не настроена*.

#### <a name="encryption"></a>Encryption

- **Шифрование хранилища данных на устройстве**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — шифрование хранилища данных на устройствах.  

  Настраивать этот параметр не нужно, так как устройства с Android для бизнеса используют принудительное шифрование.

## <a name="work-profile"></a>Рабочий профиль

### <a name="device-health"></a>Работоспособность устройств

- **Устройства с административным доступом**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — пометить устройства с административным доступом (со снятой защитой) как не соответствующие требованиям.  

- **Require the device to be at or under the Device Threat Level** (Требовать тот же или более низкий уровень риска устройства). Выберите максимальный уровень угроз для устройства, оцениваемый [службой защиты мобильных устройств от угроз](mobile-threat-defense.md). Устройства, превышающие этот уровень угрозы, будут отмечены как несоответствующие. Чтобы использовать этот параметр, выберите допустимый уровень угрозы:

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Защищено** — это самый безопасный уровень, при котором устройство не может содержать угроз. В случае обнаружения на устройстве угрозы любого уровня оно признается не соответствующим требованиям.
  - **Низкий** — если обнаруженные на устройстве угрозы имеют низкий уровень, считается, что оно соответствует требованиям. Любая угроза с уровнем выше низкого переводит устройство в состояние несоответствия.
  - **Средний** — если обнаруженные на устройстве угрозы имеют низкий или средний уровень, считается, что устройство все еще соответствует требованиям. Если на устройстве найдены угрозы с высоким уровнем, оно признается не соответствующим требованиям.
  - **Высокий** — этот уровень является наименее безопасным и включает все уровни угроз. Он может быть полезным при использовании решения только для формирования отчетов.

#### <a name="google-play-protect"></a>Google Play Protect

- **Google Play Services is configured** (Сервисы Google Play настроены). 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — приложение служб Google Play должно быть установлено и включено. Сервисы Google Play предоставляют обновления системы безопасности и зависимость базового уровня для реализации многих функций безопасности на устройствах, сертифицированных Google. 
  
- **Up-to-date security provider** (Обновленный поставщик безопасности). 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — обновляемый поставщик безопасности должен защищать устройство от известных уязвимостей. 
  
- **SafetyNet device attestation** (Аттестация устройств SafetyNet). Введите уровень [аттестации SafetyNet](https://developer.android.com/training/safetynet/attestation.html), которого требуется достичь. Доступны следующие параметры:
  - **Не настроено** (*по умолчанию*) — этот параметр не проверяется на соответствие или несоответствие.
  - **Проверка базовой целостности**.
  - **Проверка базовой целостности и сертифицированных устройств**.

> [!NOTE]
> На устройствах Android для бизнеса **Проверка угроз в приложениях** — это политика конфигурации устройства. Используя политики конфигурации, администраторы могут включить параметр на устройстве. См. раздел [Параметры ограничений для устройств Android для бизнеса](../configuration/device-restrictions-android-for-work.md).

### <a name="device-properties"></a>Свойства устройства

#### <a name="operating-system-version"></a>Версия операционной системы

- **Минимальная версия ОС**. Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Приводится ссылка на сведения о том, как выполнить обновление. Пользователь может обновить устройство и получить доступ к ресурсам организации.

  *По умолчанию версия не настроена*.

- **Максимальная версия ОС**. Если устройство использует версию ОС, более позднюю по сравнению с указанной в правиле, доступ к ресурсам организации блокируется. Пользователю будет предложено обратиться к ИТ-администратору. Пока вы не измените правило для разрешения конкретной версии ОС, это устройство не сможет получать доступ к ресурсам организации.

  *По умолчанию версия не настроена*.

### <a name="system-security"></a>Безопасность системы

- **Требовать пароль для разблокировки мобильных устройств** 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям. 
  - **Требовать** — пользователи должны ввести пароль, прежде чем они смогут получить доступ к своему устройству.  

  Этот параметр применяется на уровне устройства. Если нужно требовать пароль только на уровне рабочего профиля, используйте политику конфигурации. Дополнительные сведения см. в статье [Параметры устройства Android Enterprise, которые позволяют разрешить или ограничить некоторые функции через Intune](../configuration/device-restrictions-android-for-work.md).

- **Требуемый тип пароля**. Укажите, каким должен быть пароль: содержать только цифровые символы или сочетание цифр и других символов. Доступны следующие параметры:
  - **Устройство по умолчанию**
  - **Биометрический с низким уровнем безопасности**
  - **Минимальный цифровой** (*по умолчанию*). Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
  - **Числовой комплекс**. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
  - **Минимальный буквенный**. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
  - **Минимальный буквенно-цифровой**. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).
  - **Минимальный буквенно-цифровой и символьный**. Укажите **минимальную длину пароля**, который следует ввести пользователю (от 4 до 16 символов).

  В зависимости от выбранного *типа пароля* доступны следующие параметры:  
  - **Максимальное время бездействия (в минутах), по истечении которого запрашивается пароль**. Введите время бездействия, по истечении которого пользователю потребуется ввести пароль повторно. Доступны следующие варианты: *Не настроено* и от *1 минуты* до *8 часов*.

  - **Число дней до обязательной смены пароля**. Укажите число дней, от 1 до 365, до обязательной смены пароля на устройстве. Например, чтобы изменить пароль через 60 дней, введите `60`. Когда срок действия пароля истекает, пользователям предлагается создать пароль.

  - **Минимальная длина пароля**. Укажите минимальное число символов, которое должно быть в пароле (от 4 до 16 символов). 
  
  - **Число предыдущих паролей для запрета повторного использования**. Введите число недавних паролей, которые не могут использоваться повторно. С помощью этого параметра можно запретить пользователю применять использованные ранее пароли.

#### <a name="encryption"></a>Encryption

- **Шифрование хранилища данных на устройстве**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — шифрование хранилища данных на устройствах.  

  Настраивать этот параметр не нужно, так как устройства с Android для бизнеса используют принудительное шифрование.

#### <a name="device-security"></a>Безопасность устройств

- **Блокировать приложения из неизвестных источников**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — блокировка устройств со включенными источниками **Безопасность** > **Неизвестные источники** (*поддерживается в версиях с Android 4.0 по Android 7.x. Не поддерживается для Android 8.0 и более поздних версий*).  

  Для загрузки неопубликованных приложений необходимо разрешить неизвестные источники. Установите **Заблокировать**, чтобы включить эту политику соответствия требованиям, если вы не загружаете неопубликованные приложения Android.

  > [!IMPORTANT]
  > Для загрузки неопубликованных приложений требуется, чтобы параметр **Block apps from unknown sources** (Блокировать приложения из неизвестных источников) был включен. Примените эту политику соответствия требованиям, только если вы не загружаете на устройства неопубликованные приложения Android.

  Этот параметр настраивать необязательно, так как устройства с Android для бизнеса всегда ограничивают установку из неизвестных источников.

- **Целостность среды выполнения приложения корпоративного портала**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — выберите *Требовать*, чтобы подтвердить, что приложение корпоративного портала соответствует всем следующим требованиям:
    - Среда выполнения по умолчанию установлена.
    - Имеется надлежащая подпись.
    - Не находится в режиме отладки.
    - Установлено из известного источника.

- **Блокировать отладку по USB на устройстве**. 
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — запретить устройствам использовать функцию отладки USB.  

  Этот параметр настраивать необязательно, так как отладка по USB уже отключена на устройствах с Android для бизнеса.

- **Минимальный уровень обновления для системы безопасности**.  Выберите самый старый уровень обновления системы безопасности для устройства. Устройства, не имеющие этот уровень обновления безопасности или выше, считаются не соответствующими политике. Дату необходимо ввести в формате ГГГГ-ММ-ДД.

  *По умолчанию дата не настроена*.

## <a name="next-steps"></a>Дальнейшие шаги

- [Добавление действий для несоответствующих устройств](actions-for-noncompliance.md) и [Использовать теги области для фильтрации политик](../fundamentals/scope-tags.md).
- [Мониторинг политик соответствия](compliance-policy-monitor.md).
- См. раздел [Параметры политики соответствия для устройств с Android](compliance-policy-create-android.md).