---
title: Развертывание в рабочую среду
titleSuffix: Configuration Manager
description: Руководство по развертыванию в рабочую группу Аналитики компьютеров.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 0a7ffe8eea1048e696ce7dd254d58364226efc58
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268796"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Развертывание в рабочую среду с помощью Аналитики компьютеров

После [развертывания в пилотную версию](deploy-pilot.md) и проверки состояния ресурсов вы можете обновить остальную часть рабочей среды.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Выполнение развертывания обновлений на рабочих устройствах состоит из трех основных частей:

1. [Проверка ресурсов, требующих принятия решения об обновлении](#bkmk_review). Чтобы подготовить устройства к рабочему развертыванию, в их ресурсах для решения об обновлении должно быть установлено значение **Готово** или **Ready, remediations required** (Готово, требуются исправления).  

2. [Развертывание на готовых устройствах](#bkmk_deploy). Используйте Configuration Manager для обновления готовых устройств. Аналитика компьютеров предоставляет список устройств, готовых к рабочему развертыванию, а также отчеты для мониторинга успешности развертывания.  

3. [Мониторинг состояния работоспособности обновленных устройств](#bkmk_monitor). По мере развертывания обновления следите за состоянием работоспособности важных ресурсов. Если некоторые из них требуют внимания, устраните неполадки и проблемы. Если решено, что проблемы не могут быть устранены, остановите развертывание на затронутых устройствах, установив для решения об обновлении значение **Не удалось**.  

> [!NOTE]  
> Если вы уверены в успешности пилотного развертывания, начните рабочее развертывание в любое время. Нет необходимости, чтобы все пилотные устройства сначала достигли "завершенного" состояния.  



## <a name="review-assets-that-need-an-upgrade-decision"></a><a name="bkmk_review"></a> Проверка ресурсов, требующих принятия решения об обновлении

Аналитика компьютеров поможет выполнить процесс проверки ресурсов для рабочего развертывания. На портале Azure перейдите к параметру **Планы развертывания**, выберите план развертывания, а затем в меню слева щелкните **Подготовка рабочей среды**.

![Снимок экрана: представление "Подготовка рабочей среды" в Аналитике компьютеров](media/prepare-production.png)

Просмотрите состояние приложений. Используйте эти сведения, чтобы установить решение об обновлении для каждого из этих ресурсов.

Используйте каждую из вкладок для просмотра состояния приложений. В каждом представлении со вкладками можно фильтровать результаты, чтобы отображать устройства, которые доступны для обновления, нуждаются во внимании, устройства со смешанными результатами, а также устройства в неопределенном состоянии.

Выберите **Цели выполняются**, чтобы отфильтровать представление для ресурсов, которые, вероятно, готовы к рабочему развертыванию на основе следующих критериев:

- Риск: предварительная оценка известных рисков для обновления устройств, на которых установлен этот ресурс.  

- Состояние работоспособности: оценка устройств после обновления в других развертываниях и определение того, не возникли ли у них проблемы после установки обновления. Дополнительные сведения о работоспособности см. в разделе об [отслеживании работоспособности обновленных устройств](#bkmk_monitor).  

Чтобы утвердить ресурс для обновления, выберите имя в списке, а затем выберите один из следующих параметров в списке **Решение об обновлении**:

- Выполняется проверка
- Готово
- Готово (с исправлениями)
- Не удалось
- Не проверено

Чтобы установить это значение для нескольких приложений одновременно, используйте первый столбец, чтобы **выбрать этот элемент**, а затем щелкните **Принять решение об обновлении**.

![Параметр "Принять решение об обновлении" на нескольких устройствах](media/prep-prod-set-upgrade-decision.png)

Выберите **Нет данных**, чтобы просмотреть ресурсы, которые не могут быть классифицированы. Обычно это ресурсы с недостаточным охватом для Аналитики компьютеров, чтобы выполнить анализ риска или состояния работоспособности. Чтобы улучшить охват, добавьте дополнительные устройства с этими ресурсами в пилотный проект или попросите пилотных пользователей опробовать эти ресурсы.

Ресурсы также могут быть в состоянии **Требуется внимание** или **Mixed Results** (Смешанные результаты). Перед принятием решения об обновлении ресурсов для них может потребоваться выполнение дополнительной проверки.

Проверьте все приложения. Как только для данного устройства будет принято положительное решение об обновлении для всех ресурсов, его состояние изменится на "готово к выпуску". Посмотрите текущий счет на главной странице для плана развертывания, выбрав третий шаг развертывания **Развернуть**.


## <a name="deploy-to-devices-that-are-ready"></a><a name="bkmk_deploy"></a> Развертывание на готовых устройствах

Configuration Manager использует данные из Аналитики компьютеров для создания коллекции для рабочего развертывания. Не развертывайте последовательность задач, используя традиционное развертывание. Используйте следующую процедуру для создания интегрированного развертывания Аналитики компьютеров:

Если вы выполнили рекомендуемый процесс [развертывания на пилотных устройствах](deploy-pilot.md#deploy-to-pilot-devices), поэтапное развертывание Configuration Manager готово. Когда вы помечаете ресурсы как *готовые*, Аналитика компьютеров автоматически синхронизирует эти устройства с Configuration Manager. Эти устройства затем добавляются в рабочую коллекцию. Когда поэтапное развертывание переходит ко второму этапу, эти рабочие устройства получают развертывание обновления.

Если для поэтапного развертывания вы настроили параметр **Вручную начать второй этап развертывания**, то вам нужно вручную переместить его на следующий этап. Дополнительные сведения см. в статье [Мониторинг поэтапных развертываний и управление ими](../osd/deploy-use/manage-monitor-phased-deployments.md#bkmk_move).

Если вы создали одно развертывание, интегрированное с Аналитикой компьютеров, в пилотной коллекции, необходимо повторить этот процесс для развертывания в рабочей коллекции.


### <a name="address-deployment-alerts"></a>Отправка оповещений о развертывании

Как и в случае пилотного развертывания, Аналитика компьютеров сообщает вам о любых проблемах, которые требуют внимания во время рабочего развертывания. В Аналитике компьютеров перейдите к плану развертывания и выберите **Состояние развертывания** в меню слева. В представлении состояния развертывания перечислены устройства в следующих категориях:  

- Не запущено
- Выполняется
- Completed
- Требует внимания — устройства (отсортировано по имени устройства).
- Требует внимания — проблемы (отсортировано по типу проблемы).

![Снимок экрана: состояние рабочего развертывания Аналитики компьютеров](media/prod-deployment-status.png)


## <a name="monitor-the-health-of-updated-devices"></a><a name="bkmk_monitor"></a> Отслеживание состояния работоспособности обновленных устройств

На странице **Подготовка рабочей среды** отображаются сведения, которые помогут принять решение об обновлении для ресурсов. На этой странице по умолчанию отображаются только те ресурсы, которые еще не находятся в состоянии **Готово**. На странице **Отслеживание работоспособности** отображаются проблемы с работоспособностью для любого значимого ресурса, даже для тех, состояние которых отмечено как **Готово**. Если будут обнаружены проблемы, вы можете исправить неполадки и устранить проблему или изменить состояние решения об обновлении на **Не удалось**. При изменении решения об обновлении это действие предотвращает будущие обновления на устройствах с этим ресурсом.

Отфильтруйте эту страницу по ресурсам со следующими состояниями работоспособности:

| Фильтр состояния работоспособности | Описание: |
|----------------------|-------------|
| **Требуется внимание** | (Фильтр по умолчанию) Аналитика компьютеров обнаруживает статистически значимую регрессию к некоторым показателям работоспособности для этого ресурса.
| **Цели выполняются** | Аналитика компьютеров не обнаруживает регрессии в поведении. |
| **Недостаточно данных** | Аналитика компьютеров не имеет достаточно данных об этом ресурсе, чтобы предоставлять какие-либо рекомендации. |
| **Нет данных** | Для этого ресурса еще нет данных об использовании. |

Чтобы отобразить нефильтрованное представление всех ресурсов, выберите текущий фильтр. Это действие удаляет этот фильтр.

> [!NOTE]  
> Чтобы уменьшить количество ресурсов с недостаточным объемом данных, Аналитика компьютеров отслеживает ресурсы на всех устройствах, которые были обновлены до целевой версии Windows, указанной в плане развертывания. Это устройства, которые не включены в конкретный план развертывания.  

Порядок сортировки по умолчанию определяется количеством устройств, на которых произошел инцидент с этим конкретным ресурсом, поэтому вы можете быстро просмотреть, какие из них вызывают наибольшее количество проблем. Например, при просмотре **приложений** происходит сортировка по **устройствам со сбоями приложений за последние две недели**.

Если вы хотите проверить работоспособность всех ресурсов, даже тех, у которых недостаточно данных для Аналитики компьютеров, чтобы сделать статистические выводы, используйте следующий процесс:

1. Выберите раскрывающийся список в столбце **Devices with incidents in last two weeks** (Устройства с инцидентами за последние две недели). Добавьте фильтр только к тем ресурсам, которые имели инциденты на некотором минимальном количестве интересующих устройств. Например, отображать элементы со значениями **больше 100**.  

2. Выберите раскрывающийся список в столбце **% Devices with incidents in the last two weeks** (% устройств с инцидентами за последние две недели) и выберите сортировку по **убыванию**.  

    В полученном представлении отображаются ресурсы с наивысшей частотой инцидентов при минимальном количестве инцидентов.  

3. Выберите ресурс, чтобы получить более подробные сведения или изменить его решение об обновлении.  

Дополнительные сведения см. в статье [Мониторинг состояния работоспособности в Аналитике компьютеров](health-status-monitoring.md).
