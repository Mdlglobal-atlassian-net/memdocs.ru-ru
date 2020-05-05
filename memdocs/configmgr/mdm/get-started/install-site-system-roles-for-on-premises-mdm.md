---
title: Установка ролей для локальной системы MDM
titleSuffix: Configuration Manager
description: Установите необходимые роли системы сайта для локального управления мобильными устройствами (MDM) в Configuration Manager.
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f47d78eeafb745732d4917dd7abd80f752f4dd20
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724708"
---
# <a name="install-site-system-roles-for-on-premises-mdm-in-configuration-manager"></a>Установка ролей системы сайта для локального MDM в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

Для Configuration Manager локального управления мобильными устройствами (MDM) требуются следующие роли системы сайта на сайте Configuration Manager.

- Точка регистрации

- Прокси-точка регистрации.

- Точка распространения

- Точка управления устройствами, которая является точкой управления, которую вы разрешаете использовать для мобильных устройств.

## <a name="requirements-and-limitations"></a>Требования и ограничения

- Локальная система MDM требует включения ролей системы сайта для подключений по протоколу HTTPS. Дополнительные сведения см. [в статье Настройка сертификатов для доверенного взаимодействия в локальной системе MDM](set-up-certificates-on-premises-mdm.md).

- Текущая ветвь Configuration Manager поддерживает только подключения к *интрасети* с устройств к точкам распространения и точкам управления устройствами для локальной MDM. Тем не менее, если вы также управляете компьютерами macOS, для них требуется подключение к этим же ролям *через Интернет* . При настройке точки распространения и точки управления устройствами используйте параметр, чтобы **Разрешить подключения к интрасети и Интернету**.

- Для точек распространения, настроенных для подключений в интрасети, требуется настроить границы сайта. Configuration Manager поддерживает только границы диапазона IPv4 для локальной среды MDM. Дополнительные сведения см. в разделе [Определение границ сайта и групп границ](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

- Если вы используете [реплики базы данных](../../core/servers/deploy/configure/database-replicas-for-management-points.md) с точкой управления устройствами, то сначала не удастся подключиться к новым зарегистрированным устройствам. Это происходит из-за того, что реплика базы данных не имеет сведений о вновь зарегистрированном устройстве, необходимого для успешного подключения. Реплики синхронизируются каждые пять минут. Устройствам не удастся подключиться в течение первых пяти минут после регистрации. обычно это два попытки подключения. После этого устройства будут успешно подключены.

## <a name="add-roles"></a>Добавление ролей

Если вы добавляете локальное управление мобильными устройствами на сайт с большинством устройств, управляемых с помощью клиента Configuration Manager, возможно, некоторые из этих ролей уже установлены на сайте. Например, точка распространения является общей ролью, и для управления устройствами macOS требуется точка управления устройствами.

Дополнительные сведения о добавлении ролей на сайт см. в разделе [Добавление ролей системы сайта](../../core/servers/deploy/configure/install-site-system-roles.md).

## <a name="configure-roles"></a>Настройка ролей

Настройка новых или существующих ролей для управления мобильными устройствами. Выполните следующие действия, чтобы настроить точку распространения и точки управления устройствами для правильной работы в локальной системе MDM.

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта** и выберите узел **Серверы и роли системы сайта**.

1. Выберите сервер системы сайта с точкой распространения или точкой управления устройством, которые требуется настроить. Выберите сервер в списке, а затем выберите роль **системы сайта** в области сведения о ролях системы сайта. На вкладке **роль сайта** на ленте выберите **свойства**.

    > [!TIP]
    > На большом сайте можно ограничить область просмотра, чтобы отображались только серверы с конкретными ролями. Выбрав узел **серверы и роли системы сайта** , на ленте в теге Home выберите **серверы с ролью**. Затем выберите нужную роль в списке ролей, доступных в настоящее время на сайте.

    На вкладке **Общие** в **свойствах системы сайта**убедитесь, что **имя** является полным доменным именем (FQDN). Закройте свойства.

1. В списке консоли выберите сервер с ролью локальной точки распространения. Выберите роль **точка распространения** в области сведения о ролях системы сайта. На вкладке **роль сайта** на ленте выберите **свойства**. На вкладке **связь** в **свойствах точки распространения**выполните следующие действия.

    1. Выберите **HTTPS**и установите флажок **Разрешить подключения только через интрасеть**.

        > [!IMPORTANT]
        > Если вы также управляете macOS компьютерами с помощью клиента Configuration Manager, используйте вместо этого параметр **Разрешить подключения к интрасети и Интернету** .

    1. Включите параметр **разрешить мобильным устройствам подключаться к этой точке распространения**, а затем закройте свойства.

1. Откройте свойства для роли системы сайта **точки управления** .

    1. На вкладке **Общие** выберите **HTTPS**и установите флажок **Разрешить подключения только из интрасети**.

        > [!IMPORTANT]
        > Если вы также управляете macOS компьютерами с помощью клиента Configuration Manager, используйте вместо этого параметр **Разрешить подключения к интрасети и Интернету** .

    1. Включите параметр **Разрешить использовать эту точку управления на мобильных устройствах и компьютерах Mac**, а затем закройте свойства.

        > [!NOTE]
        > Этот параметр позволяет эффективно превратить точку управления в точку управления *устройствами* .  

## <a name="next-step"></a>Следующий шаг

После добавления и настройки ролей для управления мобильными устройствами необходимо настроить серверы в качестве доверенных конечных точек. Это отношение доверия позволяет ролям взаимодействовать с управляемыми устройствами и регистрировать их.

> [!div class="nextstepaction"]
> [Set up certificates for trusted communications](set-up-certificates-on-premises-mdm.md)