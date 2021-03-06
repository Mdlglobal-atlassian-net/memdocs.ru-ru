---
title: Настройка параметров ограничений устройств с Windows 8.1 в Microsoft Intune в Azure | Документы Майкрософт
titleSuffix: ''
description: Сведения о параметрах Intune, с помощью которых можно управлять параметрами и работой устройств Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80407671"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Параметры ограничений для устройств с Windows 8.1 в Microsoft Intune

В этой статье описаны все параметры ограничений устройств в Microsoft Intune, которые можно настроить для устройств под управлением Windows 8.1.

## <a name="general"></a>Общие

- **Публикация данных об использовании**. Значение **Блокировать** запрещает устройствам отправлять телеметрические данные о диагностике и использовании в корпорацию Майкрософт. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Брандмауэр**. Значение **Требовать** включает брандмауэр Windows. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Контроль учетных записей**. Настройка контроля учетных записей (UAC). Выберите, как пользователи получают уведомления об изменениях на устройствах. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Всегда уведомлять**
  - **Уведомлять об изменениях приложений**
  - **Уведомлять об изменениях в приложении, но без затемнения рабочего стола**
  - **Не уведомлять**

## <a name="password"></a>Пароль

- **Требуемый тип пароля**. Выберите, должен ли пользователь ввести пароль для доступа к устройству. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Буквенно-цифровой**. Пароль должен содержать сочетание букв и цифр.
  - **Числовой**. Пароль должен состоять только из цифр.
- **Минимальная длина пароля**. Введите минимальное число обязательных символов (6–16). Например, введите `6`, чтобы требовать по крайней мере шесть символов в пароле.
- **Число неудачных попыток входа перед очисткой устройства**. Введите число попыток ввода пароля до очистки устройств (от 1 до 14).
- **Максимальное время бездействия (в минутах), по истечении которого экран блокируется**. Введите период бездействия устройства, по истечении которого экран автоматически блокируется (от 1 до 60). Например, введите значение `5`, чтобы блокировать устройства после 5 минут бездействия. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.
- **Срок действия пароля (в днях)** . Задайте время, по истечении которого требуется сменить пароль для устройства (от 1 до 255). Например, чтобы изменить пароль через 90 дней, введите `90`. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Запретить использование предыдущих паролей**. Введите число предыдущих паролей, которые нельзя использовать повторно (1–24). Значение `5` означает, что в качестве нового пароля пользователь не может установить свой текущий или любой из четырех предыдущих паролей. Если значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Графический пароль и ПИН-код**. Значение **Блокировать** запрещает использование изображения или ПИН-кода в качестве пароля. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. Графический пароль позволяет пользователю войти в систему с помощью жестов по изображению. ПИН-код позволяет быстро войти в систему по коду из четырех цифр.
- **Шифрование**. Значение **Требовать** делает обязательным шифрование на устройствах, включая файлы. Не все устройства поддерживают шифрование. Если задано значение **Не настроено**, Intune не изменяет или не обновляет этот параметр.

  Чтобы настроить этот параметр и правильно сообщить о соответствии требованиям, также настройте следующие элементы:
  - **Требуемый тип пароля**. Установите как минимум значение **Числовой**.
  - **Минимальная длина пароля**. Установите как минимум значение `4`.

  Чтобы применить шифрование на устройствах, работающих под управлением Windows 8.1, необходимо установить [обновление клиента MDM для Windows за декабрь 2014 года](https://support.microsoft.com/kb/3013816) на каждом устройстве.

  Если включить этот параметр для устройств с Windows 8.1, все пользователи таких устройств должны иметь учетную запись Майкрософт.

  Для выполнения шифрования устройства должны соответствовать требованиям к сертификации оборудования [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97).

  При включении шифрования для устройства ключ восстановления доступен только из учетной записи Майкрософт пользователя, к которой осуществляется доступ из его учетной записи OneDrive. Этот ключ нельзя восстановить для пользователя.

## <a name="browser"></a>Браузер

- **Автозаполнение**. Значение **Блокировать** запрещает пользователям изменять параметры автозаполнения в браузере и автоматически заполнять поля формы. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может разрешить автозаполнение.
- **Предупреждение о мошенничестве**. Значение **Требовать** отображает предупреждения о мошенничестве в браузере для потенциально мошеннических веб-сайтов. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **SmartScreen для Microsoft Edge**. Значение **Блокировать** отключает SmartScreen в Microsoft Defender. SmartScreen ищет потенциально мошеннические схемы и вредоносные программы при доступе к веб-сайтам и загруженным файлам. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. По умолчанию ОС может включить SmartScreen.
- **JavaScript**. Значение **Блокировать** запрещает выполнять в браузере скрипты, такие как JavaScript. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Всплывающие окна**. Значение **Блокировать** включает блокировку всплывающих окон, чтобы запретить их отображение в веб-браузере. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Заголовки Do Not Track**. Значение **Блокировать** запрещает устройству отправлять заголовки Do Not Track на веб-сайты, запрашивающие сведения для отслеживания. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Подключаемые модули**. Значение **Блокировать** запрещает пользователям добавлять подключаемые модули в Internet Explorer. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Ввод одного слова для сайта интрасети**. Ввод одного слова позволяет пользователям перейти на сайт интрасети, введя одно слово, например `hr` или `benefits`. Если выбрать **Блокировать**, использовать эту функцию будет запрещено. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Автоматически обнаруживать сайт интрасети**. Значение **Блокировать** запрещает автоматическое обнаружение сайта интрасети. Правила сопоставления интрасети блокируются. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Уровень интернет-безопасности**. Задает уровень безопасности сайтов в Интернете. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Средняя**
  - **Умеренно высокий**
  - **Высокая**
- **Уровень безопасности интрасети**. Задает уровень безопасности сайтов интрасети. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Низкая**
  - **Умеренно низкий**
  - **Средняя**
  - **Умеренно высокий**
  - **Высокая**
- **Уровень безопасности надежных сайтов**. Задает уровень безопасности для зоны доверенных сайтов. Доступны следующие параметры:
  - **Не настроено** (по умолчанию). Intune не изменяет или не обновляет этот параметр.
  - **Низкая**
  - **Умеренно низкий**
  - **Средняя**
  - **Умеренно высокий**
  - **Высокая**
- **Высокий уровень безопасности для опасных сайтов**. Задает уровень безопасности для зоны ограниченных сайтов. Значение **Настроено** обеспечивает применение высокого уровня безопасности для опасных сайтов. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.
- **Доступ к режиму предприятия через меню**. Значение **Блокировать** запрещает пользователям доступ к параметрам меню режима предприятия из Internet Explorer. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр. Если задано значение **Блокировать**, также введите следующие значения:
  - **URL-адрес расположения отчета о ведении журнала**. Введите URL-адрес, по которому следует получить отчеты, отображающие веб-сайты с включенным доступом в режиме предприятия.
- **Расположение списка сайтов для режима предприятия (только для настольных компьютеров)** . Введите расположение списка веб-сайтов, открываемых в режиме предприятия.

## <a name="cellular"></a>Сотовая сеть

- **Передача данных в роуминге**. Значение **Блокировать** запрещает передачу данных в роуминге, когда устройства находятся в сети сотовой связи. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="cloud-and-storage"></a>Облако и хранилище

- **URL-адрес рабочих папок**. Введите URL-адрес рабочей папки, чтобы обеспечить синхронизацию документов на устройствах. Если задано значение **Не настроено** (по умолчанию) или значение не указано, Intune не изменяет или не обновляет этот параметр.
- **Доступ к приложению "Почта Windows" без учетной записи Майкрософт**. Значение **Блокировать** запрещает доступ к приложению "Почта Windows" без учетной записи Майкрософт. Если задано значение **Не настроено** (по умолчанию), Intune не изменяет или не обновляет этот параметр.

## <a name="next-steps"></a>Дальнейшие шаги

Создание профиля ограничений [устройств с Windows 10 и более поздних версий](device-restrictions-windows-10.md).
