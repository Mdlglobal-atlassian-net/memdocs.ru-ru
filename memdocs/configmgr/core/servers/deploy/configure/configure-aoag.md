---
title: Настройка групп доступности
titleSuffix: Configuration Manager
description: Настройка и управление группами доступности SQL Server Always On с помощью Configuration Manager
ms.date: 09/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 12753b3800b3b304bd13c992b57d22bf9e1bfad8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704802"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Настройка групп доступности SQL Server AlwaysOn для Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Используйте информацию в этой статье для настройки и управления группами доступности, используемыми в Configuration Manager.

Перед началом работы  

- См. дополнительные сведения о [подготовке к использованию групп доступности SQL Server AlwaysOn с помощью Configuration Manager](sql-server-alwayson-for-a-highly-available-site-database.md).
- Ознакомьтесь с документацией по SQL Server, где описывается использование групп доступности и связанные процедуры. Эти сведения необходимы для выполнения следующих сценариев.


## <a name="create-and-configure-an-availability-group"></a><a name="bkmk_create"></a> Создание и настройка группы доступности

Создайте группу доступности, выполнив инструкции ниже, и переместите в нее копию базы данных сайта.

1. Чтобы остановить сайт Configuration Manager, используйте следующую команду:

    `preinst.exe /stopsite`

    Дополнительные сведения см. в разделе [Средство обслуживания иерархии](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Измените модель резервного копирования базы данных сайта с **ПРОСТАЯ** на **ПОЛНАЯ**:

    ```sql
    ALTER DATABASE [CM_xxx] SET RECOVERY FULL;
    ```

    Группы доступности поддерживают только модель полного резервного копирования. Дополнительные сведения см. в разделе [Просмотр или изменение режима восстановления базы данных](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

3. Используйте SQL Server для создания полной резервной копии базы данных сайта. Выберите один из следующих вариантов.

    - **Сервер будет членом группы доступности**: Если сервер используется как член начальной первичной реплики группы доступности, восстанавливать копию базы данных сайта на этом или другом сервере в группе не потребуется. База данных уже размещена на первичной реплике. На более позднем этапе SQL Server реплицирует базу данных на вторичные реплики.  

    - **Сервер не будет членом группы доступности**: Восстановите копию базы данных сайта на сервере с первичной репликой группы.

    Дополнительные сведения см. в следующих статьях документации по SQL Server.

    - [Создание полной резервной копии базы данных](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server)
    - [Восстановление резервной копии базы данных с помощью SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)

    > [!NOTE]  
    > Если вы планируете перейти из группы доступности в отдельную группу на существующей реплике, сначала удалите базу данных из группы доступности.

4. На сервере, где будет размещена начальная первичная реплика группы, с помощью [мастера создания групп доступности](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) создайте группу доступности. В мастере выполните следующее.

    - На странице **Выбор базы данных** выберите базу данных для сайта Configuration Manager.  

    - На странице **Указание реплик** настройте следующие параметры.

        - **Реплики**. Укажите серверы, на которых будут размещены вторичные реплики.

        - **Прослушиватель**. Укажите **DNS-имя прослушивателя** в качестве полного DNS-имени, например `<listener_server>.fabrikam.com`. Когда вы настраиваете Configuration Manager на использование базы данных в группе доступности, он использует это имя.

    - На странице **Выбор начальной синхронизации данных** выберите **Полная**. Создав группу доступности, мастер выполнит архивацию базы данных-источника и журнала транзакций. Затем мастер восстановит их на каждом сервере, на котором размещена вторичная реплика.

        > [!Note]  
        > Если вы не используете этот шаг, восстановите копию базы данных сайта на каждом сервере, на котором размещена вторичная реплика. Затем вручную присоедините эту базу данных к группе.

5. Проверьте конфигурацию для каждой реплики.

    1. Убедитесь, что учетная запись компьютера сервера сайта входит в локальную группу **Администраторы** на каждом компьютере, входящем в группу доступности.  

    2. Запустите [скрипт проверки ](sql-server-alwayson-for-a-highly-available-site-database.md#prerequisites), чтобы убедиться, что база данных сайта на каждой реплике настроена правильно.

    3. Если необходимо настроить конфигурации во вторичных репликах, прежде чем продолжить, вручную перейдите с первичной реплики на вторичную. Базу данных можно настроить только в первичной реплике. Дополнительную информацию см. в [Планированный ручной обход отказа группы доступности](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) в документации SQL Server.

6. Если все реплики соответствует требованиям, группа доступности готова к использованию с Configuration Manager.


## <a name="configure-a-site-to-use-the-availability-group"></a><a name="bkmk_configure"></a> Настройка сайта для использования группы доступности

[Создав и настроив группы доступности](#bkmk_create), выполните обслуживание сайта Configuration Manager, чтобы настроить его для использования базы данных, размещенной в группе доступности.

Установка нового сайта с базой данных в группе доступности не поддерживается. Например, при использовании базового носителя установите сайт при помощи одного экземпляра SQL Server. После установки сайта, базу данных можно переместить в группу доступности.

1. Запустите **программу установки Configuration Manager**: `\BIN\X64\setup.exe`из папки установки сайта Configuration Manager.

2. На странице **Приступить к работе** выберите **Выполнить обслуживание или сброс параметров этого сайта**, а затем нажмите кнопку **Далее**.

3. Выберите **Изменить конфигурацию SQL Server**, а затем нажмите кнопку **Далее**.

4. Измените конфигурацию следующих параметров базы данных сайта:

    - **Имя SQL Server**. Введите виртуальное имя для *прослушивателя* группы доступности. Вы настроили прослушивателя при создании группы доступности. Виртуальное имя должно представлять собой полное DNS-имя, например `<Listener_Server>.fabrikam.com`.  

    - **Экземпляр**. Это поле должно быть пустым, чтобы указать экземпляр по умолчанию для *прослушивателя* группы доступности. Если текущая база данных сайта выполняется на именованном экземпляре, очистите текущий именованный экземпляр.

    - **База данных**. Оставьте отображенное имя. Это имя является текущей базой данных сайта.

5. После ввода сведений для нового расположения базы данных завершите установку и настройку обычным образом.


## <a name="synchronous-replica-members"></a><a name="bkmk_sync"></a> Синхронные члены реплики  

Если база данных сайта размещена в группе доступности, для добавления или удаления элементов синхронных реплик выполните следующие инструкции. Дополнительные сведения о поддерживаемом типе и количестве реплик см. в разделе [Конфигурация групп доступности](sql-server-alwayson-for-a-highly-available-site-database.md#availability-group-configurations).

### <a name="add-a-new-synchronous-replica-member"></a><a name="bkmk_sync-add"></a>Добавление нового элемента синхронной реплики

<!--3127336-->
Начиная с версии 1906 запустите программу установки Configuration Manager, чтобы добавить новый синхронный элемент реплики.

1. Добавьте вторичную реплику с помощью процедур SQL Server.

    1. См. сведения о [добавлении вторичной реплики в группу доступности Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

    1. Следите за статусом в SQL Management Studio. Дождитесь, пока группа доступности вернется к полному состоянию работоспособности.

1. Запустите программу установки Configuration Manager и выберите соответствующий параметр, чтобы изменить сайт.

1. Укажите имя прослушивателя группы доступности в качестве имени базы данных. Если прослушиватель использует нестандартный сетевой порт, укажите его также. Это действие заставляет программу установки убедиться, что каждый узел настроен соответствующим образом. Оно также запускает процесс восстановления базы данных.

Программа установки Configuration Manager использует операцию перемещения базы данных SQL и проверяет правильность настройки узлов.

Дополнительные сведения о том, как выполнить этот процесс вручную в версии 1902 или более ранней, см. в разделе [ConfigMgr 1702. Добавление нового узла (вторичной реплики) в существующую группу SQL AO AG](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configmgr-1702-adding-a-new-node-secondary-replica-to-an/ba-p/339960).

### <a name="remove-a-replica-member"></a>Удаление элемента реплики

Начиная с версии 1906, чтобы удалить элемент реплики можно использовать программу установки Configuration Manager. Используйте тот же процесс для [добавления нового синхронного элемента реплики](#bkmk_sync-add).

Дополнительные сведения о том, как выполнить этот процесс вручную в версии 1902 или более ранней, см. в разделе [Удаление вторичной реплики из группы доступности](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server).  


## <a name="asynchronous-replicas"></a><a name="bkmk_async"></a> Асинхронные реплики

Вы можете использовать асинхронную реплику в группе доступности, которая используется с Configuration Manager. Не нужно запускать скрипты конфигурации, необходимые для настройки синхронной реплики, так как асинхронная реплика не поддерживается для базы данных сайта.

### <a name="configure-an-asynchronous-commit-replica"></a>Настройка реплики с асинхронной фиксацией

Дополнительные сведения см. в разделе [Добавление вторичной реплики в группу доступности](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Использование асинхронных реплик для восстановления сайта

Использование асинхронных реплик для восстановления базы данных сайта.

1. Остановите основной активный сайт, чтобы предотвратить дополнительные операции записи в базу данных сайта. Чтобы остановить сайт используйте [средство обслуживания иерархии](../../manage/hierarchy-maintenance-tool-preinst.exe.md): `preinst.exe /stopsite`

1. После завершения работы сайта используйте асинхронную реплику вместо [базы данных, восстановленной вручную](../../manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered).


## <a name="stop-using-an-availability-group"></a><a name="bkmk_stop"></a>Прекращение использования группы доступности

Используйте следующую процедуру, если больше не требуется размещать базу данных сайта в группе доступности. С помощью этого процесса можно переместить базу данных сайта обратно в один экземпляр SQL Server.

1. Чтобы остановить сайт Configuration Manager, выполните следующую команду: `preinst.exe /stopsite`. Дополнительные сведения см. в разделе [Средство обслуживания иерархии](../../manage/hierarchy-maintenance-tool-preinst.exe.md).

2. Используйте SQL Server для создания полной резервной копии базы данных сайта из первичной реплики. Дополнительные сведения см. в статье [Создание полной резервной копии базы данных](https://docs.microsoft.com/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server).

3. Используйте SQL Server для восстановления резервной копии базы данных сайта на сервере, на котором будет размещена база данных сайта. Дополнительные сведения см. в статье [Восстановление резервной копии базы данных с помощью SSMS](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

    > [!Note]  
    > Если основной сервер реплики для группы доступности будет содержать единственный экземпляр базы данных сайта, пропустите этот шаг.

4. На сервере, где будет размещаться база данных сайта, измените модель резервного копирования базы данных сайта с **FULL** (Полная) на **SIMPLE** (Простая). Дополнительные сведения см. в разделе [Просмотр или изменение режима восстановления базы данных](https://docs.microsoft.com/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server).

5. Запустите **программу установки Configuration Manager**: `\BIN\X64\setup.exe`из папки установки сайта Configuration Manager.

6. На странице **Приступить к работе** выберите **Выполнить обслуживание или сброс параметров этого сайта**, а затем нажмите кнопку **Далее**.  

7. Выберите **Изменить конфигурацию SQL Server**, а затем нажмите кнопку **Далее**.  

8. Измените конфигурацию следующих параметров базы данных сайта:

    - **Имя SQL Server**. Укажите имя сервера, на котором теперь размещена база данных сайта.

    - **Экземпляр**. Укажите именованный экземпляр, на котором размещена база данных сайта. Если база данных находится в экземпляре по умолчанию, оставьте это поле пустым.

    - **База данных**. Оставьте отображенное имя. Это имя является текущей базой данных сайта.

9. После ввода сведений для нового расположения базы данных завершите установку и настройку обычным образом. После завершения программы установки сайт перезапускается и начинает использовать новое расположение базы данных.

10. Чтобы очистить серверы, которые входили в группу доступности, следуйте указаниям в разделе [Удаление группы доступности](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server).