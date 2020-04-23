---
title: Средство формирования сводных данных по контролю использования
titleSuffix: Configuration Manager
description: Используйте средство формирования сводных данных по контролю использования для активации задач формирования сводных данных по контролю использования программных продуктов в Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d27f88fe-817f-4af4-b290-c16f2e46cf31
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 599cc2f552b975fa9b40c94ea413f6b80b04a1a3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707542"
---
# <a name="run-meter-summarization-tool"></a>Средство формирования сводных данных по контролю использования

*Область применения: Configuration Manager (Current Branch)*

Средство формирования сводных данных по контролю использования является одним из [средств Configuration Manager](tools.md). Используйте его для немедленного запуска задач обслуживания для формирования сводных данных по контролю использования программных продуктов на первичных сайтах. По умолчанию эти задачи выполняются как запланированные в очереди задач **Обслуживание сайта**, которая запускается после 12:00 каждый день. 

Эти задачи формируют сводные данные в таблице SQL **MeterData** и записывают сводные результаты в таблицы **FileUsageSummary** и **MonthlyUsageSummary**. Затем сводный результат отображается в отчетах по контролю использования программных продуктов. Использовать это средство для формирования сводных данных может любой пользователь Configuration Manager с возможностью подключения к базе данных первичного сайта. 

Это средство позволяет выполнять задачи формирования сводных данных по контролю использования программных продуктов **Сводка об использовании файла** и **Ежемесячная сводка по использованию**. Оно обобщает все существующие данные об использовании без обычного 12-часового периода ожидания. Его следует запускать на экземпляре SQL Server, где размещается база данных сайта. При успешном формировании сводных данных код выхода получает значение `0`. Если произошла ошибка, код выхода имеет значение `1`.



## <a name="usage"></a>Использование

### <a name="command-line"></a>Командная строка

`runmetersumm  [sms database name]  <delay in hours for summarization <default=0>>`


### <a name="options"></a>Элемент Options

#### <a name="database-name"></a>Имя базы данных
Имя базы данных сайта на сервере SQL Server.

#### <a name="delay-in-hours-for-summarization"></a>Задержка (в часах) для формирования сводных данных
Средство формирует сводные данные по контролю использования программных продуктов, созданные до задержки. По умолчанию эта задержка равна нулю.


### <a name="example"></a>Пример

#### <a name="summarize-the-software-metering-usage-generated-12-hours-ago"></a>Формирование сводных данных по контролю использования программных продуктов, созданных 12 часов назад

`runmetersumm CCM_ABC <12>`



## <a name="see-also"></a>См. также

- [Задачи обслуживания](../servers/manage/maintenance-tasks.md)
- [Отслеживание применения приложений с помощью функции контроля использования программных продуктов](../../apps/deploy-use/monitor-app-usage-with-software-metering.md)