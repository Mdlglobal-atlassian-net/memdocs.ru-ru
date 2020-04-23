---
title: Настройка инвентаризации программного обеспечения
titleSuffix: Configuration Manager
description: Настройте инвентаризацию программного обеспечения и исключите папки из инвентаризации программного обеспечения в Configuration Manager.
ms.date: 01/03/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f86559de-092a-4ce8-9b43-5d7530e0b763
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 74436eb95166ae9bc78d7ae22881b709349bf847
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695442"
---
# <a name="how-to-configure-software-inventory-in-configuration-manager"></a>Настройка инвентаризации программного обеспечения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Эта процедура позволяет настроить параметры клиентов, используемые по умолчанию для инвентаризации оборудования и применяемые ко всем компьютерам в иерархии. Если нужно применить эти параметры только к некоторым компьютерам, создайте настраиваемый параметр для клиента устройства и назначьте его коллекции. Дополнительные сведения о создании настраиваемых параметров устройства см. в статье [Настройка параметров клиента](../../../../core/clients/deploy/configure-client-settings.md).   

## <a name="to-configure-software-inventory"></a>Настройка инвентаризации программного обеспечения  

1. В консоли Configuration Manager последовательно выберите **Администрирование** > **Параметры клиента** **Параметры клиента по умолчанию**.  

2. На вкладке **Главная** в группе **Свойства** нажмите кнопку **Свойства**.  

3. В диалоговом окне **Параметры по умолчанию** щелкните пункт **Инвентаризация программного обеспечения**.  

4. В списке **Параметры устройства** настройте следующие значения.  

   -   **Включить инвентаризацию программного обеспечения для клиентов** — в раскрывающемся списке выберите **True**.  

   -   **Расписание инвентаризации программного обеспечения и сбора файлов** — настройка интервала сбора клиентами файлов и данных инвентаризации.   

5. Настройте требуемые параметры клиента. Список параметров клиента см. в разделе [Инвентаризация программного обеспечения](../../../../core/clients/deploy/about-client-settings.md#software-inventory) статьи [Сведения о параметрах клиента](../../../../core/clients/deploy/about-client-settings.md).  

   Заданные параметры будут применены к клиентским компьютерам при следующей загрузке политики клиента. Сведения об инициации получения политик для отдельного клиента см. в разделе [Управление клиентами](../../../../core/clients/manage/manage-clients.md).  

   > [!TIP]
   >   Код ошибки 80041006 в inventoryprovider.log означает, что поставщику WMI не хватает памяти. То есть достигнуто ограничение квоты памяти для поставщика, поэтому поставщик инвентаризации не может продолжить работу.
   > В этом случае агент инвентаризации создает отчет с 0 записей, так как элементы инвентаризации отсутствуют. <br/>
   > Возможное решение для этой ошибки заключается в сокращении области сбора данных при инвентаризации программного обеспечения. В ситуациях, когда эта ошибка возникает после ограничения области инвентаризации, нужный результат может дать увеличение свойства [MemoryPerHost](https://blogs.technet.microsoft.com/askperf/2008/09/16/memory-and-handle-quotas-in-the-wmi-provider-service/), определенного в классе [_ProviderHostQuotaConfiguration](https://msdn.microsoft.com/library/aa394671).

<!--SMS.480648 include WMI Out of memory tip -->


## <a name="to-exclude-folders-from-software-inventory"></a>Исключение папок из инвентаризации программного обеспечения  

1.  С помощью программы Notepad.exe создайте пустой файл с именем **Skpswi.dat**.  

2.  Щелкните правой кнопкой мыши файл **Skpswi.dat** и выберите пункт **Свойства**. В окне свойств файла Skpswi.dat выберите атрибут **Скрытый** .  

3.  Расположите файл **Skpswi.dat** в корне жесткого диска каждого клиента или структуры папок, которую требуется исключить из области инвентаризации ПО.  

> [!NOTE]  
>  Инвентаризация ПО не будет запускаться снова на диске клиентского компьютера, если этот файл будет присутствовать на нем.