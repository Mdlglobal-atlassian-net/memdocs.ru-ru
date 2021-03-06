---
title: Мониторинг обновлений программного обеспечения
titleSuffix: Configuration Manager
description: На консоли Configuration Manager отображаются оповещения и сведения о состоянии, необходимые для отслеживания обновлений и соответствия требованиям.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 9afd7b0f-5c8e-48bc-9a65-1f7d74103688
ms.openlocfilehash: aa17e58f2687a48895502d1062a22d0c8630aea3
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110378"
---
# <a name="monitor-software-updates-in-configuration-manager"></a>Мониторинг обновлений программного обеспечения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В Configuration Manager существует много способов наблюдения за объектами обновления ПО, процессами и данными соответствия требованиям. В следующих разделах содержатся сведения о мониторинге обновлений программного обеспечения.

## <a name="software-updates-dashboard"></a>Панель мониторинга "Обновления программного обеспечения"

*(Представлено в версии 1610)*

Начиная с версии Configuration Manager 1610 с помощью новой панели мониторинга "Обновления программного обеспечения" можно просматривать текущее состояние соответствия устройств требованиям в организации и быстро анализировать данные, чтобы определять устройства, находящиеся под угрозой. Чтобы открыть эту панель мониторинга, выберите **Наблюдение** > **Обзор** > **Безопасность** > **Панель мониторинга обновлений программного обеспечения**.

## <a name="drill-through-required-updates"></a>Детализация необходимых обновлений
<!--4224414-->
*(Представлено в версии 1906)*

Статистика по соответствию поддерживает детализацию, позволяющую определить, на каких устройствах требуется конкретное обновление программного обеспечения "Приложения Microsoft 365 для предприятий". Чтобы просмотреть список устройств, требуется разрешение на просмотр обновлений и коллекций, к которым относятся устройства. Чтобы детализировать список устройств, сделайте следующее.

1. Выберите **Библиотека программного обеспечения** > **Обновления программного обеспечения** > **Все обновления программного обеспечения**.
1. Выберите любое обновление, которое требуется по крайней мере на одном устройстве.
1. Перейдите на вкладку **Сводка** и найдите круговую диаграмму в разделе **Статистика**.
1. Для детализации по списку устройств щелкните гиперссылку **Просмотреть обязательные** рядом с круговой диаграммой.
1. В результате откроется временный узел в разделе **Устройства**, в котором представлены устройства, требующие обновления. В узле также можно выполнить такие действия, как создание коллекции на основе списка.


##  <a name="alerts-for-software-updates"></a><a name="BKMK_SUAlerts"></a> Оповещения для обновлений программного обеспечения  
 Настройте оповещения для обновлений программного обеспечения, чтобы извещать пользователей с правами администраторов, если показатель соответствия обновлений требованиям становится ниже заданного процента. Можно настроить оповещения для развертываний обновлений ПО в следующих местах.  

-   Параметр ADR: можно настроить параметры оповещений в мастере настройки правил автоматического развертывания и в свойствах ADR.  

-   Параметры развертывания. Можно настроить параметры оповещений в мастере развертывания обновлений программного обеспечения и в свойствах развертывания.  

Если параметры оповещений настроены, то при наступлении указанных условий Configuration Manager создает оповещение. Можно просмотреть оповещения об обновлениях ПО в следующих местах.  

1.  Просмотрите последние оповещения в узле **Обновления программного обеспечения** в рабочей области **Обновления программного обеспечения** .  

2.  Управление настроенными оповещениями осуществляется в узле **Оповещения** в рабочей области **Мониторинг** .  

##  <a name="software-updates-synchronization-status"></a><a name="BKMK_SUSyncStatus"></a> состояние синхронизации обновлений программного обеспечения;  
 Запущенный процесс синхронизации для всех точек обновления программного обеспечения в иерархии можно отслеживать с консоли Configuration Manager. Выполните следующую процедуру для мониторинга процесса синхронизации обновлений программного обеспечения.  

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>Мониторинг процесса синхронизации обновлений программного обеспечения  

- В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Состояние синхронизации точки обновления программного обеспечения**.  

    Точки обновления программного обеспечения в иерархии Configuration Manager отображаются в области результатов. В этом представлении можно выполнять мониторинг состояния синхронизации всех точек обновления программного обеспечения. Чтобы получить более подробные сведения о процессе синхронизации, изучите файл wsyncmgr.log, расположенный в каталоге <*путь_установки_Configuration_Manager*>\Logs на каждом сервере сайта.  

##  <a name="software-update-deployment-status"></a><a name="BKMK_SUDeployStatus"></a> состояние развертывания обновлений программного обеспечения;  
 После развертывания обновлений программного обеспечения в группе обновления программного обеспечения или развертывания отдельного обновления можно осуществлять мониторинг состояния развертывания. Следующая процедура позволяет осуществлять мониторинг состояния группы обновления программного обеспечения или обновления программного обеспечения.  

#### <a name="to-monitor-deployment-status"></a>Мониторинг состояния развертывания  

1.  В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Развертывания**.  

2.  Щелкните группу обновления программного обеспечения или обновление программного обеспечения, состояние которого требуется узнать.  

3.  На вкладке **Главная** в группе **Развертывание** нажмите кнопку **Просмотр состояния**.  

##  <a name="software-updates-reports"></a><a name="BKMK_SUReports"></a> Отчеты обновления программного обеспечения  
 Сообщения о состоянии обновления программного обеспечения содержат сведения о соответствии обновлений требованиям, а также данные оценки и состояние применения развертываний обновления. Запуск отчетов обновлений программного обеспечения для отображения сообщений состояния. Предусмотрено более 30 предварительно определенных отчетов об обновлении ПО. Они распределены по нескольким категориям и могут использоваться для создания отчетов по конкретным сведениям, связанным с обновлениями и развертываниями ПО. Помимо предустановленных отчетов можно также создавать настраиваемые отчеты об обновлении программного обеспечения, адаптированные под нужды предприятия. Дополнительные сведения см. в статье [Использование и обслуживание для отчетов](../../core/servers/manage/operations-and-maintenance-for-reporting.md).  

### <a name="recommended-software-updates-reports"></a>Рекомендуемые отчеты об обновлении программного обеспечения
Ниже представлены некоторые отчеты, которые могут быть полезны при выявлении возможных проблем. 

#### <a name="compliance-9---overall-health-and-compliance-starting-in-version-1806"></a>Соответствие 9. Общая работоспособность и соответствие (начиная с версии 1806)
Отчет состоит из следующих частей.

- **Отношение работоспособных клиентов к общему числу клиентов**. На этой линейчатой диаграмме сопоставляется число "работоспособных" клиентов, которые выходили на связь с сайтом за установленный промежуток времени, и общее количество клиентов в выбранной коллекции.
- **Общие сведения о соответствии**. На этой круговой диаграмме показано общее состояние соответствия для определенной группы обновлений программного обеспечения для активных клиентов в указанной коллекции.
- **Пять основных несоответствующих обновлений по коду статьи**. На этой линейчатой диаграмме отображаются пять обновлений программного обеспечения из выбранной группы, для которых зарегистрировано больше всего несоответствий в активных клиентах в указанной коллекции.
- В нижней части отчета содержится таблица с дополнительными сведениями, в том числе со списком обновлений программного обеспечения для указанной группы.

#### <a name="management-2---updates-required-but-not-deployed"></a>Управление 2 — необходимые, но не развернутые обновления

В этом отчете отображаются зависящие от поставщика обновления программного обеспечения, относящиеся к определенной категории, которые были обнаружены как обязательные для клиентов, но не были развернуты в указанной коллекции. 

#### <a name="troubleshooting-2---deployment-errors"></a>Устранение неполадок 2 — ошибки развертывания

В этом отчете представлены сведения об ошибках развертывания на сайте и число компьютеров для каждой ошибки. 


##  <a name="monitor-content"></a><a name="BKMK_MonitorContent"></a> Мониторинг содержимого  
 Вы можете отслеживать содержимое в консоли Configuration Manager для анализа состояния всех типов пакетов и связанных с ними точек распространения. Имеется возможность контроля состояния проверки содержимого пакета, состояния содержимого, назначенного конкретной группе точек распространения, состояния содержимого, назначенного конкретной точке распространения и состояния дополнительных функций по каждой из точек распространения (проверка содержимого, PXE и многоадресная рассылка).  

###  <a name="content-status-monitoring"></a><a name="BKMK_ContentStatus"></a> Мониторинг состояния содержимого  
 Узел **Состояние содержимого** в рабочей области **Мониторинг** содержит сведения о пакетах содержимого. Можно просмотреть общие сведения о пакете, состояние распространения пакета, а также детальные сведения о состоянии пакета. Для просмотра состояния содержимого следует использовать следующую процедуру.  

#### <a name="to-monitor-content-status"></a>Мониторинг состояния содержимого  

1.  В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Состояние развертывания** > **Состояние содержимого**. Отобразятся пакеты.  

2.  Выберите пакет, сведения о состоянии которого требуется получить.  

3.  На вкладке **Главная** щелкните **Просмотр состояния**. Отобразятся подробные сведения о состоянии пакета.  

###  <a name="distribution-point-group-status"></a><a name="BKMK_DPGroupStatus"></a> Состояние группы точек распространения  
 Узел **Состояние группы точек распространения** в рабочей области **Мониторинг** содержит сведения о группах точек распространения. Здесь также можно просмотреть дополнительные сведения о группе точек распространения, например состояние и степень соответствия группы точек распространения, а также подробные сведения о ее состоянии. Следующая процедура предназначена для просмотра состояния группы точек распространения.  

#### <a name="to-monitor-distribution-point-group-status"></a>Мониторинг состояния группы точек распространения  

1.  В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Состояние развертывания** > **Состояние группы точек распространения**. Отобразятся группы точек распространения.  

2.  Выберите группу точек распространения, сведения о состоянии которой требуется получить.  

3.  На вкладке **Главная** щелкните **Просмотр состояния**. Отобразятся подробные сведения для группы точек распространения.  

###  <a name="distribution-point-configuration-status"></a><a name="BKMK_DPConfigStatus"></a> Состояние конфигурации точки распространения  
 Узел **Состояние конфигурации точек распространения** в рабочей области **Мониторинг** содержит сведения о точке распространения. Вы можете анализировать включенные для точки распространения атрибуты, такие как PXE, многоадресная рассылка и проверка содержимого. Кроме того, можно отобразить подробные сведения о состоянии точки распространения. Следующая процедура предназначена для просмотра состояния конфигурации точки распространения.  

#### <a name="to-monitor-distribution-point-configuration-status"></a>Мониторинг состояния конфигурации точки распространения  

1.  В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Состояние развертывания** > **Состояние конфигурации точек распространения**. Отобразятся точки распространения.  

2.  Выберите точку распространения, сведения о состоянии которой требуется отобразить.  

3.  В области результатов откройте вкладку **Подробности** . Здесь отображаются сведения о состоянии точки распространения.  

## <a name="next-steps"></a>Дальнейшие шаги

- [Файлы журналов для обновлений программного обеспечения](../../core/plan-design/hierarchy/log-files.md#BKMK_SU_NAPLog)

- [Технический документ по управлению обновлением программного обеспечения](https://www.microsoft.com/download/confirmation.aspx?id=44578)
