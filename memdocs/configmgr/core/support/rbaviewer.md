---
title: Средство ролевого администрирования
titleSuffix: Configuration Manager
description: Использование средства ролевого администрирования и аудита для моделирования и аудита ролей и областей безопасности в Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 6372ff17-7f56-4d7b-a21b-87fb8bdd6d3a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ff940db21711aabb5d57a45b05d90d04415639bb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707562"
---
# <a name="role-based-administration-and-auditing-tool"></a>Средство ролевого администрирования и аудита

*Область применения: Configuration Manager (Current Branch)*

Средство ролевого администрирования и аудита является одним из [средств Configuration Manager](tools.md). Оно применяется для выполнения следующих задач:

- моделирование ролей безопасности с определенными разрешениями;  

- аудит областей безопасности и ролей безопасности, назначенных другим пользователям.



## <a name="requirements"></a>Requirements (Требования)

- Средство следует запускать на компьютере с установленной консолью Configuration Manager.  

- У вас есть роль **Полный администратор**, **Аналитик с правами только для чтения** или **Администратор безопасности**.  

- Назначьте учетную запись области безопасности **Все** и всем коллекциям.  

- (*Необязательно*) Для анализа безопасности папки отчетов требуется доступ к SQL.  

- (*Необязательно*) Для анализа детализированных данных отчета это средство следует запускать на сервере системы сайта с ролью "Точка формирования отчетов".



## <a name="procedures"></a>Процедуры


### <a name="model-permissions-for-a-new-role"></a>Моделирование разрешений для новой роли

Следующая процедура предназначена для моделирования разрешений для новой роли, которую вы хотите создать. 

1. Запустите **RBAViewer.exe**.  

2. Выберите базовые роли безопасности в качестве основы или начните с пустого набора разрешений. Выберите необходимые разрешения.  

3. Нажмите кнопку **Анализировать**, чтобы открыть пользовательский интерфейс для этой настраиваемой роли.  

    > [!Note]  
    > Чтобы проверить наличие существующей роли безопасности, которая соответствует вашим требованиям, перейдите на вкладку **Подобия**.  

4. Нажмите кнопку **Экспорт**, чтобы сохранить роль в виде XML-файла. Затем импортируйте файл в консоль Configuration Manager. Дополнительные сведения см. в разделе [Создание настраиваемых ролей безопасности](../servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole).


### <a name="audit-existing-security-scopes"></a>Аудит существующих областей безопасности

Следующая процедура предназначена для аудита всех существующих пользователей, коллекций и областей безопасности в Configuration Manager.

1. Запустите **RBAViewer.exe**.  

2. На панели инструментов нажмите кнопку **Аудит RBA**.  

    1. Чтобы просмотреть связи, ограниченные коллекцией, в представлении в виде дерева, перейдите на вкладку **Сводка по коллекции**.  

    2. Чтобы просмотреть объекты, назначенные роли безопасности, перейдите на вкладку **Сводка по области**.  


### <a name="audit-a-specific-user"></a>Аудит определенного пользователя

Следующая процедура предназначена для аудита конфигурации ролевого администрирования для определенного пользователя.

1. Запустите **RBAViewer.exe**.  

2. На панели инструментов нажмите кнопку **Запуск от имени**.  

3. Введите имя пользователя, чтобы проверить разрешения для этой учетной записи.  

4. Средство отобразит роли безопасности, назначенные пользователю или группе безопасности, в которую он входит. Оно также выведет объекты, которые этот пользователь может видеть, и действия, которые он может выполнять в консоли.  



## <a name="see-also"></a>См. также

- [Основы ролевого администрирования](../understand/fundamentals-of-role-based-administration.md)
- [Настройка ролевого администрирования](../servers/deploy/configure/configure-role-based-administration.md)