---
title: Контрольный список администратора по управлению питанием
titleSuffix: Configuration Manager
description: Этот контрольный список администратора поможет вам спланировать и внедрить управление питанием в Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 94e42cbe-9df8-4228-a04e-0ad7626180ca
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 039ebf73fba9850b8479bfabab6ab928b7d6f2df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696662"
---
# <a name="administrator-checklist-for-power-management-in-configuration-manager"></a>Контрольный список администратора по управлению питанием в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Этот контрольный список администратора включает рекомендуемые действия для использования функций управления питанием Configuration Manager в организации.  

## <a name="configuring-power-management"></a>Настройка функций управления питанием  
 Чтобы настроить иерархию с целью сбора данных об управлении питанием с клиентских компьютеров, выполните описанные ниже действия.  

> [!IMPORTANT]  
>  Не применяйте схемы управления питанием к компьютерам иерархии до завершения сбора и анализа данных клиентских компьютеров. Применение схем управления питанием до анализа используемых параметров может привести к росту энергопотребления.  

|Задача|Сведения|  
|----------|-------------|  
|Ознакомьтесь с основными принципами управления питанием в библиотеке документации Configuration Manager.|См. раздел [Общие сведения об управлении питанием](introduction-to-power-management.md).|  
|Ознакомьтесь с необходимыми условиями для управления питанием в библиотеке документации Configuration Manager.|См. раздел [Необходимые условия для управления питанием](prerequisites-for-power-management.md).|  
|Ознакомьтесь с рекомендациями по использованию функций управления питанием.|См. раздел [Рекомендации по управлению питанием](best-practices-for-power-management.md).|  
|Настройте коллекции для управления энергопотреблением компьютеров в среде.|Используйте **коллекцию для отчетов с базовыми данными**, **коллекцию для отчетов с базовыми данными**, **коллекцию компьютеров, для которых управление питанием невозможно**, **коллекции компьютеров, к которым будут применяться схемы управления питанием**, **коллекции компьютеров, к которым будут применяться схемы управления питанием** и **коллекции компьютеров под управлением ОС Windows Server** для управления параметрами питания компьютеров в иерархии. Можно создать несколько коллекций и применять к ним различные схемы управления питанием.|  
|Включите функцию управления питанием.|Прежде чем вы сможете пользоваться функциями управления питанием, необходимо включить этот компонент и настроить соответствующие параметры клиента. Дополнительные сведения см. в разделе [Настройка управления питанием](configuring-power-management.md).|  
|Выполните сбор данных об управлении питанием с клиентских компьютеров.|Данные управления питанием передаются клиентами с помощью функций инвентаризации оборудования Configuration Manager. В зависимости от настроенной схемы инвентаризации сбор данных инвентаризации со всех компьютеров может занять определенное время.|  

## <a name="monitoring-and-planning-phase"></a>Этап мониторинга и планирования  

|Задача|Сведения|  
|----------|-------------|  
|Запустите отчет **Активность компьютеров**.|Отчет **Активность компьютера** содержит график, демонстрирующий активность мониторов, компьютеров и пользователей заданной коллекции за указанный период времени. Этот отчет связан с отчетом **Сведения об активности компьютеров**, содержащим сведения о возможностях перехода компьютеров выбранной коллекции в спящий режим и выхода из него. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Энергопотребление** или **Энергопотребление по дням**.|В отчетах **Энергопотребление** или **Энергопотребление по дням** отображается общее энергопотребление за месяц в кВт*ч для выбранной коллекции за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Воздействие на окружающую среду** или **Воздействие на окружающую среду по дням**.|Отчеты **Воздействие на окружающую среду** и **Воздействие на окружающую среду по дням** содержат графики, демонстрирующие уровень выброса углекислого газа (CO2), сокращенного благодаря снижению энергопотребления выбранной коллекции компьютеров за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Стоимость электроэнергии** или **Стоимость электроэнергии по дням**.|В отчетах **Стоимость электроэнергии** или **Стоимость электроэнергии по дням** отображаются расходы на электроэнергию за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Возможности электропитания**.|Отчет **Возможности электропитания** содержит перечень возможностей управления питанием компьютеров указанной коллекции. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Параметры питания**.|В отчете **Параметры управления питанием** отображается сводный список текущих параметров питания компьютеров указанной коллекции. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Исключите нужные коллекции компьютеров из получателей параметров управления питанием.|См. раздел [Настройка функций управления питанием](configuring-power-management.md).|  

> [!IMPORTANT]  
>  Убедитесь, что данные отчетов об управлении питанием, полученные на этапе мониторинга и планирования, сохранены. Эти данные пригодятся для сравнения с данными об управлении питанием на этапах применения и обеспечения соответствия требованиям. Такое сравнение позволит оценить сокращение энергопотребления, затрат на электроэнергию и влияния на окружающую среду после применения схем управления питанием к компьютерам иерархии.  

## <a name="enforcement-phase"></a>Этап применения параметров  

|Задача|Сведения|  
|----------|-------------|  
|Выберите для применения к коллекциям компьютеров имеющиеся схемы управления питанием или создайте новые.|См. раздел [Создание и применение схем управления питанием](create-and-apply-power-plans.md).|  
|Примените эти схемы управления питанием к компьютерам.|См. раздел [Создание и применение схем управления питанием](create-and-apply-power-plans.md).|  

## <a name="compliance-phase"></a>Этап обеспечения соответствия требованиям  

|Задача|Сведения|  
|----------|-------------|  
|Запустите отчет **Активность компьютеров**.|Отчет **Активность компьютера** содержит график, демонстрирующий активность мониторов, компьютеров и пользователей заданной коллекции за указанный период времени. Этот отчет связан с отчетом **Сведения об активности компьютеров**, содержащим сведения о возможностях перехода компьютеров выбранной коллекции в спящий режим и выхода из него. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Энергопотребление** или **Энергопотребление по дням**.|В отчетах **Энергопотребление** или **Энергопотребление по дням** отображается общее энергопотребление за месяц в кВт*ч для выбранной коллекции за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Воздействие на окружающую среду** или **Воздействие на окружающую среду по дням**.|Отчеты **Воздействие на окружающую среду** и **Воздействие на окружающую среду по дням** содержат графики, демонстрирующие уровень выброса углекислого газа (CO2), сокращенного благодаря снижению энергопотребления выбранной коллекции компьютеров за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|Запустите отчет **Стоимость электроэнергии** или **Стоимость электроэнергии по дням**.|В отчетах **Стоимость электроэнергии** или **Стоимость электроэнергии по дням** отображаются расходы на электроэнергию за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  

## <a name="troubleshooting"></a>Устранение неполадок  

|Задача|Сведения|  
|----------|-------------|  
|Если компьютеры иерархии не переходят в спящий режим или режим гибернации, для выяснения возможных причин запустите **Отчет о компьютерах без спящего режима**.|**Отчет о компьютерах без спящего режима** содержит список распространенных причин, препятствующих переходу компьютеров в спящий режим или режим гибернации, а также число компьютеров для каждой причины за указанный период времени. Дополнительные сведения см. в разделе [Отслеживание и планирование управления питанием](monitor-and-plan-for-power-management.md).|  
|При применении к компьютеру нескольких схем управления питанием используется менее ограничительная схема. Для просмотра списка компьютеров, к которым применено несколько схем управления питанием, запустите отчет **Компьютеры с несколькими схемами управления питанием**.|См. подраздел **Компьютеры с несколькими схемами управления питанием** в разделе [Отслеживание и планирование управления питанием в Configuration Manager](monitor-and-plan-for-power-management.md).|  
