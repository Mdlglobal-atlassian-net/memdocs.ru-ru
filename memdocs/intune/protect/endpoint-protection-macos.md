---
title: Добавление защиты конечных точек в macOS в Microsoft Intune в Azure | Документы Майкрософт
description: Используйте привратник на устройствах macOS для определения источника установки приложений, включая Mac App Store. Кроме того, включите или настройте брандмауэр для разрешения конкретных приложений, блокировки определенных приложений, использования скрытого режима и даже блокировки определенных типов входящих подключений с помощью Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8ef60333b53e03b3a6a8d736817ef27df9a182f1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79352076"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Параметры защиты конечных точек macOS в Intune  

В этой статье описаны параметры защиты конечных точек, которые можно настроить для устройств под управлением macOS. Эти параметры настраиваются с помощью профиля конфигурации устройства macOS для [защиты конечных точек](endpoint-protection-configure.md) в Intune.  

## <a name="gatekeeper"></a>Привратник  

- **Разрешить приложения, скачанные из этих расположений**  
  Ограничьте приложения, которые можно запускать на устройстве в зависимости от того, откуда они были скачаны. Цель — защитить устройства от вредоносных программ и разрешить использовать приложения только из надежных источников.  

  - **Не настроено**.  
  - **Mac App Store**  
  - **Mac App Store и известные разработчики**  
  - **Везде**  

  **По умолчанию**: Не настроено  

- **Пользователь может переопределить привратника**  
  Запрещает пользователям переопределять параметры привратника и устанавливать приложения с помощью клавиши Control. Если параметр включен, пользователь может нажать клавишу CTRL, чтобы установить приложение.  
 
  - **Не настроено**. Пользователи могут устанавливать приложения, щелкнув при нажатой клавише CTRL.  
  - **Блокировать**. Пользователям запрещено устанавливать приложения, щелкнув при нажатой клавише CTRL.  

  **По умолчанию**: Не настроено  

## <a name="firewall"></a>Брандмауэр  

Используйте брандмауэр для управления соединениями на уровне приложения, а не порта. Параметры на уровне приложения позволяют более эффективно применять преимущества защиты с помощью брандмауэра. Брандмауэр также помогает помешать нежелательным приложениям захватить сетевые порты, открытые для разрешенных приложений.  

**Общие**
- **Брандмауэр**.  
  Включите брандмауэр для настройки способа обработки входящих подключений в вашей среде.  
  - **Не настроено**.  
  - **Разрешить**  

  **По умолчанию**: Не настроено  

- **Входящие подключения**.  
  Запретите все входящие подключения, за исключением тех, которые необходимы для основных служб Интернета, таких как DHCP, Bonjour и IPSec. Эта функция также блокирует все службы общего доступа, например общий доступ к файлам или к экрану. При использовании указанных служб общего доступа этому параметру следует задать значение *Не настроен*.  
  - **Не настроено**.  
  - **Заблокировать**  

  **По умолчанию**: Не настроено  

**Разрешить или блокировать входящие подключения для конкретных приложений**  

  - **Разрешенные приложения**  
    Выберите приложения, которым явным образом разрешено принимать входящие подключения.  

  - **Заблокированные приложения**  
    Выберите приложения, которые должны блокировать входящие подключения.  

  - **Скрытый режим**.  
    Включите этот режим, чтобы компьютер не отвечал на запросы проверки. Устройство продолжает реагировать на входящие запросы авторизованных приложений. Неожиданные запросы, например ICMP (проверка связи), будут игнорироваться.  
    - **Не настроено**.  
    - **Разрешить**  

    **По умолчанию**: Не настроено  

## <a name="filevault"></a>FileVault  
Дополнительные сведения о параметрах Apple FileVault см. на странице о [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) в документации для разработчиков Apple. 

> [!IMPORTANT]  
> Начиная с macOS 10.15 для конфигурации FileVault требуется утвержденная пользователем регистрация MDM. 

- **FileVault**  
  Вы можете *включить* полное шифрование диска с помощью XTS-AES 128 с FileVault на устройствах под управлением macOS 10.13 и более поздних версий.  
  - **Не настроено**.  
  - **Разрешить**  

  **По умолчанию**: Не настроено  

  - **Тип ключа восстановления**  
    Для устройств создаются *личные* ключи восстановления. Настройте следующие параметры для личного ключа.  

    - **Расположение личного ключа восстановления**. Введите короткое сообщение для пользователя, в котором объясняется, как и где можно получить личный ключ восстановления. Этот текст вставляется в сообщение, которое пользователь видит на экране входа в систему при появлении запроса на ввод личного ключа восстановления в случае, если пароль забыт.  
      
    - **Смена личного ключа восстановления**. Укажите частоту смены личного ключа восстановления для устройства. Можно выбрать значение по умолчанию **Не настроено** или значение от **1** до **12** месяцев.  

  - **Отключить запрос при выходе**  
    Запрет вывода запроса на включение FileVault при выходе пользователя из системы.  Если задано значение "Отключено", запрос при выходе будет отключен, и будет выводиться запрос при входе в систему.  
    - **Не настроено**.  
    - **Отключено**. Отключение запроса при выходе.

    **По умолчанию**: Не настроено  

  - **Число разрешенных пропусков**  
  Задайте, сколько раз пользователь может игнорировать запросы о включении FileVault, прежде чем оно станет обязательным для входа. 

    - **Не настроено**. На устройстве требуется включить шифрование, прежде чем будет разрешен следующий вход в систему.  
    - От **1** до **10**. Пользователь может игнорировать запрос от 1 до 10 раз, прежде чем требовать шифрования на устройстве.  
    - **Без ограничения, всегда запрашивать**. Выводится запрос на включение FileVault, но шифрование никогда не требуется.  
 
    **По умолчанию**: *Различается*. Если параметру *Отключить запрос при выходе* задано значение **Не настроено**, по умолчанию используется значение **Не настроено**. Если параметру *Отключить запрос при выходе* задано значение **Отключено**, по умолчанию используется значение **1**, а значение **Не настроено** не рассматривается.

Дополнительные сведения о FileVault см. в разделе [Ключи восстановления FileVault](encryption-monitor.md#filevault-recovery-keys).
