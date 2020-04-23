---
title: Общие сведения о запросах
titleSuffix: Configuration Manager
description: Создавать и отправлять запросы для поиска объектов в иерархии Configuration Manager, соответствующей выбранным условиям.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff98645c7892192f2f914a25102454b5e9415fee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694572"
---
# <a name="introduction-to-queries-in-configuration-manager"></a>Общие сведения о запросах в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Можно создавать и отправлять запросы для поиска объектов в иерархии Configuration Manager, соответствующей выбранным условиям. В число таких объектов входят определенные типы компьютеров или групп пользователей. Запросы позволяют возвращать большую часть типов объектов Configuration Manager, в том числе сайтов, коллекций, приложений и данных инвентаризации.  

## <a name="query-creation-overview"></a>Общие сведения о создании запроса

 При создании запроса необходимо указать не менее двух параметров: область поиска и предмет поиска. Например, чтобы найти сведения об объеме пространства на жестком диске, доступного на всех компьютерах сайта Configuration Manager, можно создать запрос для поиска класса атрибута **Логический диск** и атрибута **Свободно (МБ)** , определяющего свободное пространство.  

 После создания первоначального запроса можно указать дополнительные условия. Например, можно указать, чтобы в результаты запроса входили только компьютеры, назначенные определенному сайту. Кроме того, можно изменить способ отображения результатов для их просмотра в удобном для вас порядке. Например, можно указать, чтобы результаты сортировались по объему свободного пространства на жестком диске в порядке возрастания или убывания.  

 Созданный запрос он сохраняется Configuration Manager и отображается в узле **Запросы** в рабочей области **Мониторинг**. В этом расположении можно создавать новые запроси, а также выполнять, обновлять или обновлять существующие.  

 Можно также импортировать запрос в правило запроса коллекции Configuration Manager. Дополнительные сведения см. в статье [Создание коллекций](../../../core/clients/manage/collections/create-collections.md).  

## <a name="next-steps"></a>Дальнейшие шаги

 [Создание запросов](../../../core/servers/manage/create-queries.md)