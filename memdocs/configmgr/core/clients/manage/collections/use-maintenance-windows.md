---
title: Использование периодов обслуживания
titleSuffix: Configuration Manager
description: Используйте коллекции и периоды обслуживания для эффективного управления клиентами в Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6c2128c9e26137c268577e68e5ee12e3a71f8513
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695462"
---
# <a name="how-to-use-maintenance-windows-in-configuration-manager"></a>Использование периодов обслуживания в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Периоды обслуживания позволяют определить период времени, когда в отношении коллекции устройств можно проводить операции Configuration Manager. Периоды обслуживания служат для внесения изменений в конфигурацию клиентов в то время, когда это не влияет на производительность работы. Начиная с Configuration Manager версии 1806 пользователи могут видеть следующие период обслуживания на вкладке **Состояние установки** в **Центре программного обеспечения**. <!--1358131-->

 Следующие операции поддерживают периоды обслуживания:  

- Развертывания программного обеспечения  

- Развертывания обновлений программного обеспечения  

- Развертывание и оценка параметров соответствия требованиям  

- Развертывания операционных систем  

- Развертывания последовательностей задач  

  Для периода обслуживания настраиваются дата начала, время начала и окончания, а также расписание повторений. Период должен продолжаться менее 24 часов. По умолчанию перезагрузки компьютера, вызванные развертыванием, разрешены только во время периода обслуживания, однако можно переопределить значение по умолчанию. Периоды обслуживания влияют только на время запуска программы развертывания. Приложения, настроенные для скачивания и запуска в локальном режиме, могут скачивать содержимое после окончания такого периода.  

  Если клиентский компьютер входит в коллекцию устройств с настроенным периодом обслуживания, программа развертывания запускается, только если максимально допустимое время выполнения не превышает заданной длительности периода. Если программа не запускается, создается оповещение и развертывание запускается повторно в течение следующего запланированного периода обслуживания с доступным временем.  

## <a name="using-multiple-maintenance-windows"></a>Использование нескольких периодов обслуживания  
 Если клиентский компьютер входит в несколько коллекций устройств с периодами обслуживания, действуют указанные ниже правила.  

- Если периоды обслуживания не пересекаются, они рассматриваются как два независимых периода обслуживания.  

- Если периоды обслуживания пересекаются, они рассматриваются как один период обслуживания, охватывающий время обоих периодов. Например, если два периода, каждый из которых длится час, пересекаются на 30 минут, эффективная продолжительность периода обслуживания будет составлять 90 минут.  

  Когда пользователь начинает установку приложения из центра программного обеспечения, приложение устанавливается незамедлительно независимо от периодов обслуживания.  

  Если развертывание приложения с целью **Необходимо** достигает крайнего срока установки в нерабочее время, настроенное пользователем в центре программного обеспечения, приложение будет установлено. 

### <a name="how-to-configure-maintenance-windows"></a>Настройка периодов обслуживания  

1.  В консоли Configuration Manager выберите **Активы и соответствие**>  **Коллекции устройств**.  

3.  В списке **Коллекции устройств** выберите коллекцию. Создать периоды обслуживания для коллекции **Все системы** невозможно.  

4.  На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  

5.  На вкладке **Периоды обслуживания** в диалоговом окне **Свойства &lt;имя коллекции\>** щелкните значок **Создать**.  

6.  Укажите сведения в диалоговом окне **&lt;новое\> расписание**.  

7.  Выберите значение в раскрывающемся списке **Применить это расписание к**.  

8.  Нажмите кнопку **ОК**, а затем закройте диалоговое окно **Свойства &lt;имя коллекции\>** .  
 
## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Использование PowerShell

PowerShell можно использовать для настройки периодов обслуживания.  Дополнительные сведения см. на странице

* [Set-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmmaintenancewindow)
* [Get-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmmaintenancewindow)
* [New-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmmaintenancewindow)
* [Remove-CMMaintenanceWindow](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmmaintenancewindow)
