---
title: Аудит изменений и событий в Microsoft Intune в Azure | Документация Майкрософт
description: Вы узнаете, как просмотреть журналы аудита, в которые записываются действия Microsoft Intune.
keywords: ''
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 03/18/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6ee841cc-5694-4ba1-8f66-1d58edec30a4
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 923a7c192121530d84ca2034b2ca8a4be3cc32d6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990761"
---
# <a name="use-audit-logs-to-track-and-monitor-events-in-microsoft-intune"></a>Использование журналов аудита для отслеживания событий в Microsoft Intune

В журналы аудита записываются действия, которые генерируют изменения в Microsoft Intune. Создание, обновление (редактирование), удаление, назначение и удаленные действия приводят к созданию событий аудита, которые администратор может просмотреть для большинства рабочих нагрузок Intune. По умолчанию для всех клиентов включен аудит. Его невозможно отключить.

> [!NOTE]
> Запись событий аудита начата с выпуска соответствующих компонентов в декабре 2017 г. Предыдущие события недоступны.

## <a name="who-can-access-the-data"></a>Кто имеет доступ к данным?

Журналы аудита могут просматривать пользователи со следующими разрешениями:

- глобальный администратор
- администратор службы Intune;
- администраторы, которым назначена роль Intune с разрешениями **Данные аудита** - **Чтение**.

## <a name="audit-logs-for-intune-workloads"></a>Журналы аудита для рабочих нагрузок Intune

Вы можете просматривать журналы аудита для каждой рабочей нагрузки Intune в группе мониторинга:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Администрирование клиента** > **Журналы аудита**.
3. Чтобы отфильтровать результаты, выберите **Фильтр** и уточните результаты, используя следующие параметры.
    - **Категория**: такие как **Соответствие**, **Устройство** и **Роль**.
    - **Действия**: указанные здесь параметры ограничены выбором в разделе **Категория**.
    - **Диапазон дат**: можно выбрать журналы за предыдущий месяц, неделю или день.
4. Нажмите кнопку **Применить**.
4. Выберите элемент в списке, чтобы просмотреть сведения об активности.

## <a name="route-logs-to-azure-monitor"></a>Отправка журналов в Azure Monitor

Журналы аудита и операционные журналы можно также перенаправить в Azure Monitor. Выберите команду **Экспортировать параметры данных** в разделе **Журналы аудита**.

![Экспорт данных журнала в Azure Monitor путем выбора параметров экспорта данных в Intune](./media/monitor-audit-logs/audit-logs-export-data-settings.png)

> [!NOTE]
> Дополнительные сведения об этой функции и предварительных требованиях для ее использования см. в разделе [Отправка данных журнала в хранилище, концентраторы событий или на анализ журналов](review-logs-using-azure-monitor.md).

> [!NOTE]
> Поле **Кем инициировано (субъект)** включает сведения о том, кто запустил задачу и где она была запущена. Например, если вы запустили действие в Intune на портале Azure, в разделе **Приложение** обязательно будет содержаться **расширение портала Microsoft Intune** и для **идентификатора приложения** всегда будет использоваться тот же GUID.
>
> Раздел **Целевые объекты** содержит несколько целевых объектов и свойств, которые были изменены.  

## <a name="use-graph-api-to-retrieve-audit-events"></a>Использование API Graph для получения событий аудита

Дополнительные сведения о том, как использовать API Graph для получения событий аудита за период до одного года, см. в статье о [списке auditEvents](https://docs.microsoft.com/graph/api/intune-auditing-auditevent-list?view=graph-rest-1.0).

## <a name="next-steps"></a>Дальнейшие действия

[Отправка данных журнала в хранилище, концентраторы событий или Log Analytics](review-logs-using-azure-monitor.md)

[Просмотр журналов защиты клиентских приложений](../apps/app-protection-policy-settings-log.md)
