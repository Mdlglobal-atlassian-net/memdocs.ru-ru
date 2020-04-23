---
title: Расположение источника содержимого
titleSuffix: Configuration Manager
description: Сведения о параметрах Configuration Manager, которые позволяют клиентам находить содержимое в медленной сети.
ms.date: 01/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 70b5cbc0-64ba-49bd-8b34-fb4c09b2b95b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9d58138380263a7e7c3305ab2ad663a5246098b4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703662"
---
# <a name="content-source-location-scenarios-in-configuration-manager"></a>Сценарии расположения источника содержимого в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

До версии 1610 Configuration Manager поддерживал несколько параметров, которые в сочетании друг с другом определяют, как и когда клиенты находят содержимое в медленной сети. Возможные сочетания определяют расположение содержимого, применяемое клиентами, а также возможность использования резервного расположения в случае, если предпочтительный источник содержимого недоступен.  

> [!IMPORTANT]  
> **Если на ваших сайтах используется версия 1511, 1602 или 1606**, сведения в этом разделе относятся к вашей инфраструктуре. Сведения, относящиеся к группам границ в этих версиях Configuration Manager, см. в разделе [Группы границ для версий 1511,1602 и 1606](../../servers/deploy/configure/boundary-groups-for-1511-1602-and-1606.md).
>
> **Если на ваших сайтах используется версия 1610 или более поздняя**, обратитесь к разделу [Определение границ сайта и групп границ для Configuration Manager](../../servers/deploy/configure/define-site-boundaries-and-boundary-groups.md), чтобы получить сведения о том, как клиенты находят точки распространения с доступным содержимым.





**Перечисленные ниже три параметра определяют поведение при запросе содержимого клиентами.**

- **Разрешить использовать резервный источник содержимого** (включено или отключено). Этот параметр можно включить на вкладке **Группы границ** точки распространения. Он позволяет клиенту использовать точку распространения, настроенную в качестве резервного расположения, когда содержимое в предпочтительной точке распространения недоступно.  

  - **Поведение развертывания для скорости сетевого подключения**. Каждое развертывание настраивается с помощью одного из перечисленных ниже вариантов поведения, которые применяются при низкой скорости подключения к точке распространения.  

    -   **Загружать содержимое из точки распространения и запустить его локально**  

    -   **Не загружать содержимое**. Этот вариант используется только в том случае, если для получения содержимого клиент использует резервное расположение.  

    Скорость подключения для точки распространения настраивается на вкладке **Ссылки** группы границ и относится к этой группе границ.  

  - **Распространение пакета по запросу** (в предпочтительные точки распространения). Эта функция включается при выборе параметра **Распространять содержимое этого пакета в предпочтительные точки распространения** на вкладке **Параметры распространения** свойств пакета или приложения. Если включить этот параметр, то Configuration Manager будет автоматически копировать содержимое в предпочтительную точку распространения, в которой еще нет содержимого, после того, как клиент запросит это содержимое из этой точки распространения.  


 **Во всех сценариях действуют указанные ниже требования.**


-   Содержимое доступно на резервной точке распространения.  

-   Точки распространения находятся в сети и доступны.  


## <a name="scenario-1"></a>Сценарий 1.  
 Применяется при наличии следующих конфигураций.  

-   **Содержимое доступно в предпочтительной точке распространения**  

-   **Разрешить откат**. Не включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Все конфигурации  


**Подробные сведения:** (конфигурация с распространением пакета по запросу не подходит для данного сценария).  

1.  Клиент отправляет в точку управления запрос на содержимое.  

2.  Клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения с содержимым.  

3.  Клиент загружает содержимое из предпочтительной точки распространения в списке.  

## <a name="scenario-2"></a>Сценарий 2.  
 Имеются следующие конфигурации.  

-   **Содержимое доступно в предпочтительной точке распространения**  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Не скачивать содержимое  


**Подробные сведения:** (конфигурация с распространением пакета по запросу не подходит для данного сценария).  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым.  

3.  Клиент загружает содержимое из предпочтительной точки распространения в списке.  

## <a name="scenario-3"></a>Сценарий 3  
 Имеются следующие конфигурации.  

-   **Содержимое доступно в предпочтительной точке распространения**  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Скачивать и устанавливать содержимое  


**Подробные сведения:** (конфигурация с распространением пакета по запросу не подходит для данного сценария).  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым.  

3.  Клиент загружает содержимое из предпочтительной точки распространения в списке.  

## <a name="scenario-4"></a>Сценарий 4  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** не включен  

-   **Разрешить откат**. Не включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Все конфигурации  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое.  

2.  Клиенту с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения с содержимым. В списке нет предпочтительных точек распространения.  

3.  Происходит сбой клиента с отображением сообщения **Содержимое недоступно** , после чего клиент переходит в режим повторного выполнения. Новый запрос содержимого выполняется каждый час.  

## <a name="scenario-5"></a>Сценарий 5  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** не включен  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Не скачивать содержимое  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым. Предпочтительные точки распространения с содержимым отсутствуют, однако присутствует как минимум одна резервная точка распространения, в которой есть содержимое.  

3.  Содержимое не загружается, так как свойство развертывания, которое отвечает за использование клиентом резервной точки распространения, имеет значение **Не скачивать содержимое** (используется, когда клиенты обращаются к резервному расположению для получения содержимого). Происходит сбой клиента с отображением сообщения **Содержимое недоступно** , после чего клиент переходит в режим повторного выполнения. Клиент отправляет запрос на новое содержимое каждый час.  

## <a name="scenario-6"></a>Сценарий 6  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** не включен  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Скачивать и устанавливать содержимое  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым. Предпочтительные точки распространения с содержимым отсутствуют, однако присутствует как минимум одна резервная точка распространения, в которой есть содержимое.  

3.  Содержимое скачивается с резервной точки распространения из списка, поскольку свойству развертывания для клиента, использующего резервную точку распространения, задано значение **Загрузить и установить содержимое**.  

## <a name="scenario-7"></a>Сценарий 7  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** включен.  

-   **Разрешить откат**. Не включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Все конфигурации  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое.  

2.  Клиенту с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения с содержимым. Нет предпочтительных точек распространения с содержимым.  

3.  Происходит сбой клиента с отображением сообщения **Содержимое недоступно** , после чего клиент переходит в режим повторного выполнения. Новый запрос содержимого выполняется каждый час.  

4.  Точка управления создает для диспетчера распространения триггер, инициирующий распространение содержимого во все предпочтительные точки распространения для клиента, который создал запрос на содержимое.  

5.  Диспетчер распространения распространяет содержимое во все предпочтительные точки распространения. В большинстве случаев содержимое успешно распространяется в предпочтительные точки распространения в течение часа.  

6.  Клиент отправляет в точку управления новый запрос содержимого.  

7.  Клиенту с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения с содержимым. Клиент загружает содержимое из предпочтительной точки распространения в списке.  

## <a name="scenario-8"></a>Сценарий 8  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** включен.  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Не скачивать содержимое  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым. Предпочтительные точки распространения с содержимым отсутствуют, однако присутствует как минимум одна резервная точка распространения, в которой есть содержимое.  

3.  Содержимое не загружается, поскольку свойство развертывания, которое отвечает за использование клиентом резервной точки распространения, имеет значение **Не загружать содержимое**. Происходит сбой клиента с отображением сообщения **Содержимое недоступно** , после чего клиент переходит в режим повторного выполнения. Клиент отправляет запрос на новое содержимое каждый час.  

4.  Точка управления создает для диспетчера распространения триггер, инициирующий распространение содержимого во все предпочтительные точки распространения для клиента, который создал запрос на содержимое.  

5.  Диспетчер распространения распространяет содержимое во все предпочтительные точки распространения. В большинстве случаев содержимое успешно распространяется в предпочтительные точки распространения в течение часа.  

6.  Клиент отправляет в точку управления новый запрос содержимого.  

7.  Клиенту с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения с содержимым.  

8.  Клиент загружает содержимое из предпочтительной точки распространения в списке.  

## <a name="scenario-9"></a>Сценарий 9  
 Имеются следующие конфигурации.  

-   **Содержимое недоступно в предпочтительной точке распространения**  

-   Параметр **Распространять содержимое этого пакета в предпочтительные точки распространения** включен.  

-   **Разрешить откат**. Включено  

-   **Поведение при развертывании с медленным сетевым подключением**. Скачивать и устанавливать содержимое  


**Подробные сведения:**  

1.  Клиент отправляет в точку управления запрос на содержимое. Клиент указывает в запросе флаг, который означает, что разрешены резервные точки распространения.  

2.  На клиент с точки управления возвращается список расположений содержимого, где указаны предпочтительные точки распространения и резервные точки распространения с содержимым. Предпочтительные точки распространения с содержимым отсутствуют, однако присутствует как минимум одна резервная точка распространения, в которой есть содержимое.  

3.  Содержимое скачивается с резервной точки распространения из списка, поскольку свойству развертывания для клиента, использующего резервную точку распространения, задано значение **Загрузить и установить содержимое**. Этот параметр развертывания позволяет клиенту, которому необходимо использовать резервное расположение содержимого, получать содержимое из этого расположения.  

4.  Точка управления создает для диспетчера распространения триггер, инициирующий распространение содержимого во все предпочтительные точки распространения для клиента, который создал запрос на содержимое.  

5.  Диспетчер распространения распространяет содержимое во все предпочтительные точки распространения, что позволяет дополнительным клиентам получать содержимое без использования резервной точки распространения.  