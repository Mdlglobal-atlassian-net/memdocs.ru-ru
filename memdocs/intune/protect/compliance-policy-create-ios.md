---
title: Параметры соответствия устройств iOS и iPadOS в Microsoft Intune (Azure) | Документация Майкрософт
description: Список всех параметров, которые можно использовать при настройке соответствия требованиям для устройств с iOS и iPadOS в Microsoft Intune. Требование сообщения электронной почты, проверка снятой защиты или административного доступа устройств, возможность задать допустимую минимальную и максимальную версию операционной системы, любые ограничения паролей, включая длину пароля и время бездействия устройства, ограничения приложений и многое другое.
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
ms.assetid: 3cfb8222-d05b-49e3-ae6f-36ce1a16c61d
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 536ad36120a8fb5dc4ad0d16b8f265e56260d461
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729259"
---
# <a name="iosipados-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Параметры iOS и iPadOS, позволяющие пометить устройства как соответствующие или не соответствующие политике с помощью Intune

В этой статье перечислены и описаны параметры соответствия, которые можно настроить на устройствах с iOS или iPadOS в Intune. Используйте эти параметры в рамках своего решения для управления мобильными устройствами, чтобы требовать сообщение электронной почты, помечать устройства с административным доступом (со снятой защитой) как не соответствующие требованиям, настроить допустимый уровень угроз, задать срок действия паролей и многое другое.

Данная функция применяется к:

- iOS
- iPadOS

Как администратор Intune используйте эти параметры соответствия для защиты ресурсов организации. Дополнительные сведения о политиках соответствия требованиям и их действии см. в статье [Начало работы с политиками соответствия устройств](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Подготовка к работе

[Создание политики соответствия](create-compliance-policy.md#create-the-policy) Для параметра **Платформа** выберите **iOS/iPadOS**.

## <a name="email"></a>Электронная почта

- **Невозможно настроить на устройстве электронную почту**  
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Требовать** — управляемая учетная запись электронной почты является обязательной. Если у пользователя уже есть учетная запись электронной почты на устройстве, ее необходимо удалить, чтобы Intune мог правильно настроить ее. Если на устройстве нет учетной записи электронной почты, пользователь должен обратиться к ИТ-администратору для настройки управляемой учетной записи электронной почты.

  Устройство считается несоответствующим в указанных далее ситуациях.  
  - Профиль электронной почты назначен группе пользователей, отличной от группы пользователей, на которую ориентирована политика соответствия.
  - Пользователь уже настроил учетную запись электронной почты на устройстве, соответствующем профилю электронной почты Intune, развернутому на устройстве. Intune не может перезаписать профиль, заданный пользователем, или управлять им. Чтобы обеспечить соответствие требованиям, пользователь должен удалить существующие параметры электронной почты. После этого Intune сможет установить управляемый профиль электронной почты.  

Дополнительные сведения о профилях электронной почты см. в статье [Настройка доступа к электронной почте организации с помощью профилей в Intune](../configuration/email-settings-configure.md).

## <a name="device-health"></a>Работоспособность устройств

- **Устройства со снятой защитой**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Блокировать** — пометить устройства с административным доступом (со снятой защитой) как не соответствующие требованиям.  

- **Требовать тот же или более низкий уровень угрозы для устройства**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Этот параметр позволяет использовать оценку рисков как условие для проверки соответствия требованиям. Выберите допустимый уровень угроз.
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.
  - **Защищено** — это самый безопасный уровень, при котором устройство не может содержать угроз. В случае обнаружения на устройстве угрозы любого уровня оно признается не соответствующим требованиям.
  - **Низкий** — если обнаруженные на устройстве угрозы имеют низкий уровень, считается, что оно соответствует требованиям. Любая угроза с более высоким уровнем приводит к тому, что устройство признается несоответствующим требованиям.
  - **Средний** — если обнаруженные на устройстве угрозы имеют низкий или средний уровень, считается, что устройство все еще соответствует требованиям. Если на устройстве найдены угрозы с высоким уровнем, оно признается не соответствующим требованиям.
  - **Высокий** — этот уровень является наименее безопасным и включает все уровни угроз. Он может быть полезным при использовании решения только для формирования отчетов.

## <a name="device-properties"></a>Свойства устройства

### <a name="operating-system-version"></a>Версия операционной системы  

- **Минимальная версия ОС**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Если на устройстве не установлена минимальная требуемая версия ОС, оно будет отмечено как не соответствующее требованиям. Приводится ссылка на сведения о том, как выполнить обновление. При желании пользователь может обновить свои устройства. После этого он сможет получить доступ к ресурсам компании.

- **Максимальная версия ОС**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Если устройство использует версию ОС более позднюю по сравнению с версией правиле, доступ к ресурсам организации блокируется. Пользователю будет предложено обратиться к ИТ-администратору. Пока вы не измените правило, разрешив использовать эту версию ОС, устройство не будет иметь доступ к ресурсам организации.

- **Минимальная версия сборки ОС**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Когда Apple публикует обновления для системы безопасности, обычно обновляется номер сборки, а не версия операционной системы. Используйте этот параметр, чтобы указать минимальный допустимый номер сборки на устройстве.

- **Максимальная версия сборки ОС*  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Когда Apple публикует обновления для системы безопасности, обычно обновляется номер сборки, а не версия операционной системы. Используйте этот параметр, чтобы указать максимальный допустимый номер сборки на устройстве.

## <a name="system-security"></a>Безопасность системы

### <a name="password"></a>Пароль

> [!NOTE]
> После применения политики соответствия требованиям или политики конфигурации к устройству iOS или iPadOS пользователю будет выводиться запрос на задание секретного кода каждые 15 минут. Он будет появляться до тех пор, пока пользователь не задаст секретный код. При установке секретного кода для устройства iOS или iPadOS автоматически запускается процесс шифрования. Устройство остается зашифрованным до тех пор, пока не будет отключен секретный код.

- **Требовать пароль для разблокировки мобильных устройств**  
  - **Не настроено** (*по умолчанию*) — этот параметр не учитывается при оценке соответствия требованиям.  
  - **Требовать** — пользователи должны ввести пароль, прежде чем они смогут получить доступ к своему устройству. Устройства iOS и iPadOS, использующие пароли, шифруются.

- **Простые пароли**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  - **Не настроено** (*по умолчанию*) — пользователи могут создавать простые пароли, например **1234** или **1111**.
  - **Блокировать** — пользователи не могут создавать простые пароли, такие как **1234** или **1111**.

- **Минимальная длина пароля**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Введите минимальное число цифр или символов в пароле пользователя.

- **Требуемый тип пароля**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Укажите, каким должен быть пароль: содержать только **цифры** или сочетание цифр и других символов (**буквы и цифры**).

- **Число символов, отличных от буквенно-цифровых, в пароле**  
  Введите минимальное количество специальных символов, таких как `&`, `#`, `%`, `!`, которые должны быть в пароле.

  Чем больше значение, тем более сложный пароль нужно придумать пользователю.

- **Максимальный срок после блокировки экрана (в минутах), по истечении которого запрашивается пароль**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Укажите, через какое время после блокировки экрана пользователь должен вводить пароль для доступа к устройству. Доступны следующие варианты: *Не настроено*, *Немедленно* и от *1 минуты* до *4 часов*.

- **Максимальное время бездействия (в минутах), по истечении которого экран блокируется**  
  Введите время бездействия до блокировки экрана устройством. Доступны следующие варианты: *Не настроено*, *Немедленно* и от *1 минуты* до *15 минут*.

- **Срок действия пароля (в днях)**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Выберите число дней, по истечении которого пользователю нужно будет создать новый пароль.

- **Число предыдущих паролей для запрета повторного использования**  
  *Поддерживается для iOS 8.0 и более поздних версий*

  Введите число предыдущих паролей, которые нельзя использовать повторно.

### <a name="device-security"></a>Безопасность устройств

- **Ограниченные приложения**  
  Вы можете ограничить приложения, добавив идентификаторы их пакетов в политику. Если на устройстве будет установлено такое приложение, устройство будет помечено как не соответствующее требованиям.

  - **Имя приложения** — введите понятное имя, помогающее определить идентификатор пакета.
  - **Идентификатор пакета приложений** — введите уникальный идентификатор пакета, назначенный поставщиком приложения. Сведения о том, как узнать идентификатор пакета для приложения iOS или iPadOS, см. в [этой статье](https://support.microsoft.com/help/4294074/how-to-find-the-bundle-id-for-an-ios-app) (открывается другой сайт Майкрософт).  

## <a name="next-steps"></a>Дальнейшие шаги

- [Добавление действий для несоответствующих устройств](actions-for-noncompliance.md) и [Использовать теги области для фильтрации политик](../fundamentals/scope-tags.md).
- [Мониторинг политик соответствия](compliance-policy-monitor.md).
- См. раздел [Параметры политики соответствия для устройств macOS](compliance-policy-create-mac-os.md).
