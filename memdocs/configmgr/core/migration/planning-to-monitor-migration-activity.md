---
title: Мониторинг миграции
titleSuffix: Configuration Manager
description: Узнайте, как использовать консоль Configuration Manager для отслеживания хода выполнения и успешности заданий миграции.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9d1766a374c7abd8b13f503c3c7a64e35a5ac2c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693402"
---
# <a name="planning-to-monitor-migration-activity-in-configuration-manager"></a>Планирование наблюдения за действиями миграции в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В Configuration Manager вы можете отслеживать миграцию в консоли Configuration Manager, которая подключена к конечной иерархии. В консоли Configuration Manager в рабочей области **Администрирование** можно использовать узел **Миграция** для наблюдения за ходом выполнения и успешностью заданий миграции. Вы можете просмотреть сводные данные по каждому заданию миграции, определяющему перенесенные объекты, объекты, которые еще не перенесены, и число объектов, исключенных из задания миграции. Вы также увидите подробные сведения обо всех проблемах миграции.  

## <a name="view-migration-progress"></a>Просмотр процесса миграции  
 Чтобы просмотреть ход выполнения задания миграции, выполните одно из следующих действий.  

-   В рабочей области **Администрирование** консоли Configuration Manager разверните узел **Задания миграции**, выберите задание миграции, а затем откройте вкладку **Объекты в задании**.  

-   Используйте файлы журналов Configuration Manager для анализа процесса миграции или определения каких-либо проблем. Диспетчер миграции — это процесс Configuration Manager, отслеживающий действия миграции и регистрирующий их в файле migmctrl.log, сохраняемом в папке **\&lt;путь_установки\>\\LOGS** на сервере сайта.  

    > [!NOTE]  
    >  Если задание миграции не выполнено, как можно скорее просмотрите сведения в файле migmctrl.log. Записи журнала миграции непрерывно добавляются в файл и перезаписывают старую информацию. Если записи перезаписаны, возможно, вы не сможете определить, связаны ли с миграцией какие-либо проблемы, возникающие с перенесенными объектами. Действия миграции регистрируются на сайте \-верхнего уровня в иерархии независимо от сайта, к которому подключается консоль Configuration Manager при настройке миграции.  

-   Используйте отчеты Configuration Manager. В Configuration Manager есть несколько встроенных \-отчетов о миграции, которые можно использовать как есть или изменить в соответствии со своими требованиями. Дополнительные сведения об отчетах Configuration Manager см. в разделе [Введение в отчеты](../servers/manage/introduction-to-reporting.md).  