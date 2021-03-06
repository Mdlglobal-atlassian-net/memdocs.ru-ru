---
title: файловую репликацию
titleSuffix: Configuration Manager
description: Сведения об использовании Configuration Manager файловой репликации для передачи файловых данных между сайтами
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 65fcc1a8-214e-4dd9-8093-de4cd4a00442
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b7d7f1564057a7a942fc4a32064eb54cdbfa890d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703562"
---
# <a name="file-based-replication"></a>файловую репликацию

*Область применения: Configuration Manager (Current Branch)*

Configuration Manager использует файловую репликацию для передачи файловых данных между сайтами. Эти данные включают в себя приложения и пакеты, которые требуется развернуть в точках распространения на дочерних сайтах. Он также управляет необработанными записями данных обнаружения, передаваемых сайтом на родительский сайт, а затем обрабатывает их.  

При обмене файловыми данными между сайтами используется протокол *блока сообщений сервера* (SMB) с портом TCP/IP 445. Вы можете задать регулирование полосы пропускания и импульсный режим для контроля объема данных, передаваемых сайтом по сети. Используйте расписания для управления отправкой данных по сети.  

## <a name="routes"></a><a name="bkmk_routes"></a> Маршруты

Ниже приведены сведения о настройке и использовании маршрутов репликации файлов.  

### <a name="file-replication-route"></a>Маршрут репликации файлов

Каждый маршрут репликации файлов определяет конечный сайт, на который сайт передает файловые данные. Каждый сайт поддерживает один маршрут репликации файлов для конкретного конечного сайта.  

Для управления маршрутом репликации файлов, перейдите в рабочую область **Администрирование**. Разверните узел **Конфигурации иерархии** и выберите **Репликация файла**.  

Можно изменить следующие параметры маршрутов репликации файлов.  

#### <a name="file-replication-account"></a>Учетная запись репликации файлов

Эта учетная запись используется для подключения к конечному сайту и для записи данных в общий ресурс **SMS_Site** сайта. Записанные в этот ресурс данные обрабатываются получающим сайтом. По умолчанию при добавлении сайта в иерархию Configuration Manager назначает ему в качестве учетной записи репликации файлов учетную запись компьютера, служащего сервером новых сайтов. Затем эта учетная запись добавляется в `SMS_SiteToSiteConnection_<sitecode>` группу конечного сайта. Эта группа является локальной для компьютера, который предоставляет доступ к общему ресурсу SMS_Site. Эту учетную запись можно изменить на учетную запись пользователя Windows. При изменении учетной записи убедитесь, что новая учетная запись добавлена в `SMS_SiteToSiteConnection_<sitecode>` группу конечного сайта.  

> [!NOTE]  
> Вторичные сайты всегда используют учетную запись компьютера сервера вторичных сайтов со значением **Учетная запись репликации файлов**.  

#### <a name="schedule"></a>Расписание

Задайте расписание для каждого маршрута репликации файлов. Это действие позволяет ограничивать тип данных и время, когда данные могут быть переданы на конечный сайт.  

#### <a name="rate-limits"></a>Пределы скорости

Укажите пределы скорости для каждого маршрута репликации файлов. Это действие управляет пропускной способностью сети, используемой сайтом при передаче данных на конечный сайт:  

- **Импульсный режим**. Укажите размер блоков данных, отправляемых на конечный сайт. Можно также задать значение задержки между отправками каждого блока данных. Этот параметр используется при отправке данных на конечный сайт по медленному сетевому каналу.

    Например, существуют ограничения на отправку 1 КБ данных каждые пять секунд, но не по 1 КБ каждые три секунды. Это ограничение не зависит от скорости связи или ее использования в определенный момент времени.

- **Ограничено указанной максимальной скоростью передачи в час.** Сайт отправляет данные на конечный сайт, используя только указанный процент времени. Configuration Manager не определяет доступную пропускную способность сети. Вместо этого он делит время отправки данных на промежутки. После этого в течение короткого промежутка времени выполняется отправка данных, за которой следуют временные паузы, во время которых данные не отправляются.

    Например, в качестве максимальной скорости можно задать значение **50 %** . Configuration Manager передает данные в течение определенного времени, за которым следует точно такой же период, когда данные не отправляются. Он не управляет фактическим размером отправляемого блока данных. Сайт управляет только временем, в течение которого он отправляет данные.  

    > [!CAUTION]  
    > По умолчанию для передачи данных на конечный сайт можно использовать до трех **одновременных отправок** . Если для маршрута репликации файлов включены ограничения скорости, доступна только одна **одновременная отправка** для передачи данных на сайт. Это поведение применяется даже в том случае, если параметру **Ограничить доступную пропускную способность (%)** задано значение **100 %** . Использование заданных по умолчанию параметров для отправителя позволяет сократить скорость передачи на конечный сайт до трети от пропускной способности по умолчанию.  

#### <a name="routes-between-secondary-sites"></a>Маршруты между вторичными сайтами

Настройте маршрут репликации файлов между двумя вторичными сайтами для маршрутизации файлового содержимого между этими сайтами.  


### <a name="sender"></a>Отправитель

На каждом сайте есть один отправитель. Отправитель управляет сетевым подключением с одного сайта на конечный сайт. Он может устанавливать подключения к нескольким сайтам одновременно. Для подключения к сайту отправитель использует маршрут репликации файлов к сайту и определяет учетную запись, используемую для установки сетевого подключения. Отправитель также использует эту учетную запись для записи данных в общую папку SMS_Site конечного сайта.  

По умолчанию отправитель записывает данные на конечный сайт с помощью нескольких **одновременных отправок** или *потока*. Каждый поток может передавать на конечный сайт различные файловые объекты. Когда отправитель начинает отправлять объект, он продолжает записывать для него блоки данных вплоть до полной отправки. После отправки всех данных для этого объекта можно приступить к отправке нового объекта в том же потоке.  

Чтобы начать управление отправителем для сайта, в рабочей области **Администрирование** разверните узел **Конфигурация сайта**. Затем разверните узел **Сайты** и нажмите кнопку **Свойства** для сайта, которым требуется управлять. Откройте вкладку **Отправитель**, чтобы изменить параметры отправителя.  

Можно настроить следующие параметры для отправителя.  

#### <a name="maximum-concurrent-sendings"></a>Максимальное число одновременных отправок

По умолчанию каждый сайт использует пять одновременных отправок (потоков). Три из них можно использовать при отправке данных на любой конечный сайт. Увеличение этого числа приведет к увеличению скорости обмена данными между сайтами. Большее число потоков означает, что Configuration Manager может одновременно передавать больше файлов. Увеличение этого числа также приводит к увеличению потребляемой пропускной способности сети между сайтами.  

#### <a name="retry-settings"></a>Параметры повтора

По умолчанию каждый сайт два раза повторяет подключение с минутной задержкой между попытками. Число попыток подключений сайта и время ожидания между попытками можно изменить.  


## <a name="next-steps"></a>Дальнейшие шаги

[Database replication](database-replication.md)
