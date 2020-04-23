---
title: Планы развертывания в Аналитике компьютеров
titleSuffix: Configuration Manager
description: Дополнительные сведения о планах развертывания в Аналитике компьютеров.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c14eb9127b096f7fc4e4680735867913ea877f54
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706632"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>О планах развертывания в Аналитике компьютеров

Аналитика компьютеров собирает и анализирует данные об устройстве, приложении и драйверах в вашей организации. На основе этих аналитических и входных данных в службе можно создавать планы развертывания для Windows 10. Планы развертывания обладают следующими характеристиками:  

- автоматические рекомендации устройств, которые следует включить в пилотные проекты;  

- выявление проблем совместимости и предложения по их устранению;  

- оценка работоспособности развертывания до, во время и после обновлений;  

- отслеживание хода выполнения развертывания.  

В рамках плана развертывания выполняются следующие действия:  

- определение версий Windows 10, которые требуется развернуть;  

- выбор группы устройств, для которых требуется выполнить развертывание;  

- создание правил готовности для развертывания;  

- определение важности приложений;  

- выбор пилотных устройств на основе автоматических рекомендаций;  

- выбор способа устранения проблем с приложениями на основе рекомендаций из Аналитики компьютеров.  

По умолчанию Аналитика компьютеров ежедневно обновляет данные плана развертывания. Обработка всех изменений, внесенных в план развертывания, таких как назначение важности приложению или выбор устройства, которое необходимо добавить в пилотный проект, занимает до 24 часов. Чтобы ускорить этот процесс, запросите обновление данных по требованию. Дополнительные сведения см. в статье с [вопросами и ответами по Аналитике компьютеров](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

После подключения Аналитики компьютеров к Configuration Manager выберите коллекции в планах развертывания. Эта интеграция позволит развернуть Windows в коллекцию на основе данных Аналитики компьютеров.



## <a name="readiness-rules"></a>Правила готовности

В планах развертывания доступны следующие правила готовности:

- Принимают ли устройства драйверы из Центра обновления Windows автоматически. Если устройства получают обновления драйверов из Центра обновления Windows, то все проблемы с драйверами, идентифицированные как часть оценки готовности, автоматически помечаются как **Готово**.  

- Низкое пороговое значение количества установок для приложений Windows. Если приложение установлено на более высоком проценте компьютеров, чем это пороговое значение, то план развертывания помечает приложение как **Заслуживающее внимание**. Этот тег означает, что вы можете решить, насколько важно проверить приложение на этапе пилотного проекта.  


## <a name="plan-assets"></a>Ресурсы плана

<!-- 4670224 -->

Хотя в области [Ресурсы](about-assets.md) также отображаются устройства и приложения, область **Ресурсы плана** в рамках определенного плана развертывания содержит дополнительные сведения.

### <a name="devices"></a>Устройства

Ознакомьтесь с разделом **Решение об обновлении Windows** для каждого устройства в плане развертывания.

Решение об обновлении Windows **Замена устройства** может быть вызвано одной из следующих причин:

- Произошел сбой требуемой проверки процессора Windows 10. Дополнительные сведения см. в статье о [минимальных требованиях к оборудованию](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Он содержит блокировку BIOS.
- В нем недостаточно памяти.
- В критическом для загрузки компоненте системы есть заблокированный драйвер.
- Невозможно обновить определенный тип и модель.
- Есть компонент класса отображения с драйвером-блоком, который имеет все следующие атрибуты:
    - Не выполняется переопределение.
    - В новой версии ОС нет драйвера.
    - Он еще не добавлен в Центр обновления Windows.
- В системе есть еще один самонастраивающийся компонент, который блокирует обновление.
- Есть компонент беспроводной связи, использующий драйвер с эмуляцией XP.
- Сетевой компонент с активным подключением потеряет свой драйвер. Иными словами, после обновления он может потерять подключение к сети.

Решение об обновлении Windows в режиме **переустановки** означает, что для такого обновления, в отличие от обновления на месте, потребуется переустановка. 

Принятие решения об обновлении Windows в **заблокированном** режиме может быть вызвано следующими причинами.

- Для решения об обновлении одного или нескольких ресурсов задан параметр **Невозможно**.

- Указаны неполные данные для этого устройства, и Аналитика компьютеров не может выполнить полную оценку совместимости.

### <a name="apps"></a>Приложения

Задайте параметры **Решение об обновлении** и **Важность** для этого приложения в этом плане развертывания. Дополнительные сведения см. в статье [Создание планов развертывания в Аналитике компьютеров](create-deployment-plans.md).

В сведениях о приложении можно также просмотреть следующую информацию: рекомендации, факторы риска совместимости и известные проблемы корпорации Майкрософт. Полученные сведения могут помочь настроить параметр **Решение об обновлении**. Дополнительные сведения см. в статье об [оценке совместимости](compat-assessment.md).

Приложения, которые отображаются в Аналитике компьютеров как *Заслуживающие внимания*, основаны на низком пороговом значении количества установок для правил готовности плана развертывания. Дополнительные сведения см. в разделе о [правилах готовности](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Дополнительные сведения о категории приложений "Неважное" см. в разделе [Решение автоматического обновления приложений системы и магазина](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->


### <a name="drivers"></a>драйверы,

Ознакомьтесь со списком драйверов, входящих в этот план развертывания. Задайте параметр **Решение об обновлении**, просмотрите рекомендации Майкрософт и ознакомьтесь с факторами риска совместимости.


## <a name="importance"></a>Важность

В рамках плана развертывания задайте *важность* приложений. Аналитика компьютеров распознает эти приложения как установленные на целевых устройствах. Этот параметр помогает Аналитике компьютеров определить, какие устройства включать на этапе пилотного проекта развертывания.

Если приложение установлено на менее чем 2 % целевых устройств, оно помечается как **Малое число установок**. 2 % — это значение, используемое по умолчанию. Для порогового значения в параметрах готовности можно задать значение от 0 % до 10 %. Аналитика компьютеров автоматически помечает эти приложения как **Готовы к обновлению**.  

Выберите для приложений уровень важности **Критическое**, **Важное** или **Неважное**. Если пометить одно из них как критическое или важное, Аналитика компьютеров добавит в пилотное развертывание некоторые устройства с этим приложением. Служба добавляет в пилотный проект больше экземпляров критического приложения. Если приложение помечается как неважное, Аналитика компьютеров автоматически задает для него значение **Готово к обновлению**.



## <a name="pilot-devices"></a>Устройства пилотного проекта

Аналитика компьютеров объединяет сведения о важности с глобальными настройками пилотного проекта. Затем создает рекомендацию, по которой устройства следует добавить в пилотное развертывание. Рекомендуемое пилотное развертывание включает в себя устройства с различными конфигурациями оборудования и одним или несколькими экземплярами критических и важных приложений. Если приложение помечено как критическое, служба рекомендует добавить в пилотный проект большее количество устройств с этим приложением.



## <a name="deployment-plans-in-configuration-manager"></a>Планы развертывания в Configuration Manager

После создания плана развертывания разверните продукты с помощью Configuration Manager. После запуска развертывания Аналитика компьютеров отслеживает развертывание на основе параметров плана.


## <a name="next-steps"></a>Дальнейшие шаги

- [Ознакомьтесь со сведениями о ресурсах в Аналитике компьютеров](about-assets.md): устройствах, драйверах и приложениях.  

- [Узнайте больше об обновлениях в Аналитике компьютеров](about-updates.md)  

- [Создайте план развертывания](create-deployment-plans.md).  