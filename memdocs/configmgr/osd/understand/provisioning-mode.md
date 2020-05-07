---
title: Режим подготовки
titleSuffix: Configuration Manager
description: Сведения о режиме подготовки клиента во время выполнения последовательности задач Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 815b32ecf7e9cd315c2365cb5ed73004b2a48718
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708652"
---
# <a name="provisioning-mode"></a>Режим подготовки

*Область применения: Configuration Manager (Current Branch)*

Во время выполнения последовательности задач развертывания ОС Configuration Manager переводит клиент в режим подготовки. (Последовательность задач развертывания операционной системы включает обновление на месте до Windows 10). В этом состоянии клиент не обрабатывает политику с сайта. Таким образом устраняется риск того, что во время выполнения последовательности задач в клиенте будут выполняться другие развертывания. Когда последовательность задач завершается успешно или с обработанным сбоем, клиент выходит из режима подготовки.

Если последовательность задач завершается непредвиденным сбоем, клиент может остаться в режиме подготовки. Это происходит, например, если устройство перезапускается во время обработки последовательности задач и не может возобновить ее. Администратору необходимо вручную определить клиенты, находящиеся в таком состоянии, и исправить их.


## <a name="manually-remove-provisioning-mode"></a>Выход из режима подготовки вручную

Если клиент не выходит из режима подготовки, вы можете вручную вернуть клиента к нормальной работе следующим образом.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Одно из изменений, вносимых этим методом WMI, — задание значения реестра, но он также вносит другие изменения. Простое изменение значения реестра не приведет к полному выводу клиента из режима подготовки. Если вы измените реестр вручную, это может повлечь за собой непредвиденное поведение клиента.  


## <a name="client-provisioning-mode-timeout"></a>Тайм-аут в режиме подготовки клиентов

Начиная с версии 1902, когда последовательность задач переводит клиент в режим подготовки, устанавливается метка времени. Клиент в режиме подготовки каждые 60 минут проверяет время, прошедшее с метки времени. Если клиент находится в режиме подготовки более 48 часов, он автоматически выходит из него и перезапускает процесс.

48 часов — это значение тайм-аута по умолчанию для режима подготовки. Вы можете настроить таймер на устройстве, задав параметр **ProvisioningMaxMinutes** в следующем разделе реестра: `HKLM\Software\Microsoft\CCM\CcmExec`. Если этот параметр не существует или имеет значение `0`, клиент использует значение по умолчанию, равное 48 часам.

Метка времени **ProvisioningEnabledTime** находится в следующем разделе реестра: `HKLM\Software\Microsoft\CCM\CcmExec`. Ее значением является время последнего перехода компьютера в режим подготовки. Она имеет формат эпохи (метки времени Unix) и указывается в UTC.

Эта метка времени сбрасывается в текущее время, когда компьютер переводится в режим подготовки вручную с помощью следующей команды:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Технологическая схема

На этой схеме показана последовательность операций для последовательности задач и клиента.

### <a name="task-sequence"></a>Последовательность задач

На следующей схеме показано, как последовательность задач задает режим подготовки:

![Схема потока задания режима подготовки последовательностью задач](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Исправление клиентов

На следующей схеме показано, как клиент выходит из режима подготовки:

![Схема потока выхода клиента из режима подготовки](media/3197824-client-flow.png)


## <a name="see-also"></a>См. также

[Настройка Windows и Configuration Manager](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Обновление операционной системы](task-sequence-steps.md#BKMK_UpgradeOS)