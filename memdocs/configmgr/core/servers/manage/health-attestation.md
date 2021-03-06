---
title: Аттестация работоспособности
titleSuffix: Configuration Manager
description: Сведения о возможностях аттестации работоспособности устройств, доступных в консоли Configuration Manager.
ms.date: 10/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ed155fb61491a273732ed3b974b6ddb5ac29bc89
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904012"
---
# <a name="health-attestation-for-configuration-manager"></a>Подтверждение работоспособности в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Администраторы могут просматривать состояние [аттестации работоспособности устройств Windows 10 ](https://docs.microsoft.com/windows/security/threat-protection/protect-high-value-assets-by-controlling-the-health-of-windows-10-based-devices) в консоли Configuration Manager.  Аттестация работоспособности устройств позволяет администратору гарантировать, что на клиентских компьютерах включены следующие надежные конфигурации BIOS, модуля TPM и загрузочного программного обеспечения.  

-   Ранний запуск антивредоносной программы — ранний запуск антивредоносной программы (ELAM) обеспечивает защиту компьютера при запуске и до инициализации сторонних драйверов. [Как включить ELAM](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker — шифрование диска Windows BitLocker является программным обеспечением, позволяющим шифровать все данные, хранящиеся на томе операционной системы Windows.  [Как включить BitLocker](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   Безопасная загрузка — безопасная загрузка является стандартом безопасности, разработанным участниками компьютерной индустрии для того, чтобы гарантировать загрузку компьютера с использованием только программного обеспечения, которому доверяет производитель компьютера. [Дополнительные сведения о безопасной загрузке](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824987(v=win.10))  
-   Целостность кода — целостность кода является функцией, которая проверяет целостность файла драйвера или системного файла каждый раз, когда такой файл загружается в память. [Дополнительные сведения о целостности кода](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd348642(v=ws.10))  

Эта функция доступна для ПК и локальных ресурсов, управляемых с помощью Configuration Manager, и мобильных устройств, управляемых с помощью Microsoft Intune. Администраторы могут выбрать метод передачи отчетов — через облачную или локальную инфраструктуру. Локальный мониторинг для аттестации работоспособности устройств позволяет администратору отслеживать состояние клиентских компьютеров без доступа к Интернету.

## <a name="enable-health-attestation"></a>Включение аттестации работоспособности устройств

 **Требования:**  

-   Клиентские устройства под управлением Windows 10 версии 1607 или Windows Server 2016 версии 1607, на которых [включена аттестация работоспособности устройства](https://docs.microsoft.com/windows-server/security/device-health-attestation).
-   Устройства с поддержкой TPM 1.2 или TPM 2.
-   При использовании облачного управления наличие связи между агентом клиента Configuration Manager и точкой управления с *has.spserv.microsoft.com* (порт 443) службы аттестации работоспособности (для облачного управления). В локальной среде клиент должен иметь возможность взаимодействовать с точкой управления с поддержкой аттестации работоспособности устройства.

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Как включить связь со службой подтверждения работоспособности на клиентских компьютерах Configuration Manager

Эта процедура позволяет включить мониторинг для аттестации работоспособности устройств, подключенных к Интернету.

1.  В консоли Configuration Manager выберите **Администрирование** > **Обзор** > **Параметры клиента**.  Перейдите на вкладку параметров **агента компьютера** .  
2.  В диалоговом окне **Параметры по умолчанию** выберите **Агент компьютера** и прокрутите вниз до пункта **Разрешить связь со службой подтверждения работоспособности**.  
3.  Для параметра **Разрешить связь со службой подтверждения работоспособности** задайте значение **Да**, а затем нажмите кнопку **ОК**.  
4. Выберите коллекции устройств, которые должны сообщать о работоспособности устройств.

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Как включить связь с локальной службой подтверждения работоспособности на клиентских компьютерах Configuration Manager
Эта процедура позволяет включить мониторинг для аттестации работоспособности устройств, размещенных в локальной среде без подключения к Интернету.

Начиная с версии Configuration Manager 1702 вы можете настроить на точке управления URL-адрес локальной службы аттестации работоспособности устройств, чтобы работать с клиентскими устройствами без доступа к Интернету.

1. В консоли Configuration Manager перейдите в раздел **Администрирование** > **Обзор** > **Конфигурация сайта** > **Сайты**.
2. Щелкните правой кнопкой мыши первичный или вторичный сайт с точкой управления, поддерживающей локальные клиенты аттестации работоспособности устройств, а затем выберите **Настройка компонентов сайта** > **Точка управления**. Откроется страница **Свойства компонента точки управления**.
3. На вкладке **Дополнительные параметры** выберите действие **Добавить** и укажите допустимый локальный URL-адрес службы аттестации работоспособности устройств. Здесь можно добавить несколько URL-адресов. Если вы укажете несколько локальных URL-адресов, клиенты получать весь набор адресов и будут случайным образом выбирать один из них.
4.  В консоли Configuration Manager выберите **Администрирование** > **Обзор** > **Параметры клиента**.  Перейдите на вкладку параметров **агента компьютера** .  
5.  Прокрутите содержимое вниз до параметра **Разрешить связь со службой подтверждения работоспособности** и задайте для него значение **Да**.
7.  Выберите параметр **Использовать локальную службу подтверждения работоспособности** и задайте значение **Да**.
8. Выберите коллекции устройств, которые должны сообщать о работоспособности устройств, для которых установлены параметры агента клиента, разрешающие отчеты для аттестации работоспособности устройств.

Вы также можете **Изменить** или **Удалить** URL-адреса службы аттестации работоспособности устройств.

> [!NOTE]
> Если вы уже использовали аттестацию работоспособности устройств до обновления к версии Configuration Manager 1702, указанные в параметрах агента клиента локальные URL-адреса будут при обновлении автоматически перенесены в свойства точки управления. Локальные клиенты будут по-прежнему использовать URL-адрес, указанный в параметрах агента клиента, пока они не будут обновлены. После этого они перейдут на те URL-адреса, которые указаны для точки управления.

## <a name="monitor-device-health-attestation"></a>Мониторинг для аттестации работоспособности устройств

1.  Чтобы просмотреть представление аттестации работоспособности устройства, в консоли Configuration Manager перейдите в рабочую область **Мониторинг** , щелкните узел **Безопасность** , а затем щелкните **Аттестация работоспособности**.  
2.  Отобразятся результаты аттестации работоспособности устройства.  

Служба аттестации работоспособности устройств Configuration Manager выводит данные следующих мониторов.  

-   **Состояние аттестации работоспособности** — показывает, какая часть устройств находится в соответствующем, несоответствующем и неизвестном состоянии, а также в состоянии ошибки.  
-   **Устройства, передающие данные подтверждения работоспособности** — показывает процент устройств, которые передают данные о состоянии аттестации работоспособности.  
-   **Несовместимые устройства по типу клиента** — показывает, какая часть мобильных устройств и компьютеров является несоответствующей.  
-   **Наиболее часто отсутствующие параметры аттестации работоспособности** — показывает количество устройств, для которых отсутствуют параметры аттестации работоспособности, с отдельным списком для каждого параметра.
