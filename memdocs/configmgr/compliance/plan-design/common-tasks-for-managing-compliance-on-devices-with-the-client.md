---
title: Распространенные задачи управления соответствием
titleSuffix: Configuration Manager
description: Узнайте, как использовать параметры соответствия Configuration Manager при работе с некоторыми распространенными сценариями.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 1ccb0f0a042a0dd82817e030f96bbbc729e752f0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692222"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Распространенные задачи по управлению соответствия требованиям на устройствах с клиентом Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этой статье приводятся общие сведения об использовании параметров соответствия Configuration Manager и некоторые распространенные сценарии, с которыми вы можете столкнуться.  

 Если вы уже знакомы с параметрами соответствия, подробные сведения по всем используемым компонентам вы можете найти в статье об [элементах конфигурации для устройств, управляемых с помощью клиента Configuration Manager](../../compliance/deploy-use/create-configuration-items.md).  

 Прежде чем начать, прочтите статью [Приступая к работе с параметрами соответствия](../../compliance/get-started/get-started-with-compliance-settings.md), чтобы получить основные сведения о параметрах соответствия. Сведения о необходимых предварительных требованиях см. в статье [Планирование и настройка параметров соответствия](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

## <a name="general-information-for-each-scenario"></a>Общие сведения для каждого сценария  
 В каждом сценарии вы создадите элемент конфигурации, выполняющий определенную задачу. Чтобы открыть мастер создания элемента конфигурации и приступить к работе, выполните следующие действия.  

1.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Параметры соответствия** > **Элементы конфигурации**.  

1.  На вкладке **Главная** в группе **Создать** выберите **Создать элемент конфигурации**.  

1.  На странице **Общие** мастера создания элемента конфигурации, изображенного ниже, укажите имя и описание элемента. Затем выберите соответствующий тип элемента конфигурации для каждого сценария в этой статье.  

     ![Страница "Общие" в мастере создания элементов конфигурации](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Сценарий: отключение Bluetooth на устройствах Windows 10

 В этом сценарии ваш отдел безопасности решил, что канал связи Bluetooth на устройствах может использоваться для передачи конфиденциальных корпоративных данных организации за пределы организации. Вы недавно обновили все компьютеры до Windows 10. Вы решили отключить Bluetooth на этих устройствах.  

1. На странице **Общие** мастера создания элемента конфигурации выберите тип **Windows 10**, а затем нажмите кнопку **Далее**.  

2. На странице мастера **Поддерживаемые платформы** выберите все платформы Windows 10.  

3. На странице **Параметры устройства** выберите **Устройство** и нажмите кнопку **Далее**.  

4. На странице **Устройство** выберите значение **Запрещено** для параметра **Bluetooth**.  

5. Выберите **Исправлять несоответствующие параметры** , чтобы применить изменение ко всем устройствам Windows 10.  

6. Следуйте указаниям мастера, чтобы создать элемент конфигурации.  

 Теперь для развертывания созданной конфигурации на устройствах можно использовать информацию из статьи [Common tasks for creating and deploying configuration baselines with Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) (Типичные задачи, связанные с созданием и развертыванием конфигурационных баз с помощью Configuration Manager).  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Сценарий: исправление неправильного значения реестра на настольных компьютерах Windows

> [!NOTE] 
> На компьютерах Mac с запущенным клиентом Configuration Manager у вас есть два варианта для оценки соответствия:  
> - Оценка файла параметров (PLIST) Mac OS X.
> - Использование пользовательского сценария и оценка возвращенных им результатов.  
>
>Дополнительные сведения см. в статье [Создание элементов конфигурации для устройств Mac OS X, управляемых с помощью клиента Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 В этом сценарии вы обнаруживаете, что важное бизнес-приложение работает неправильно на некоторых компьютерах с Windows 8.1, которыми вы управляете. Как выяснится, это вызвано тем, что для раздела реестра с именем **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** на некоторых компьютерах задано значение **0**. Для успешного выполнения бизнес-приложения это значение должно быть равно **1**.  

 В этой процедуре вы создадите элемент конфигурации, который отслеживает и автоматически исправляет все неправильные значения разделов реестра.  

1. На странице **Общие** мастера создания элемента конфигурации выберите тип **Настольные компьютеры и серверы под управлением Windows (настраиваемые)** , а затем нажмите кнопку **Далее**.  

2. На странице **Поддерживаемые платформы** мастера выберите **Windows 8.1** (чтобы применить элемент конфигурации только к затронутым компьютерам).  

3. На странице **Параметры** выберите **Создать** для создания параметра.  

4. На вкладке **Общие** диалогового окна **Создание параметра** настройте такие параметры:  

   -   **Имя** > **Пример параметра**  

   -   **Тип параметра** > **Значение реестра**  

   -   **Тип данных** > **Целое** (так как значение содержит только число).  

   -   **Куст** > **HKEY_LOCAL_MACHINE**  

   -   **Раздел** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Значение** > **1** (обязательное значение)  

5. На вкладке **Правила соответствия** диалогового окна **Создание параметра** выберите **Создать**. В диалоговом окне **Создание правила** настройте следующие параметры.  

   -   **Имя** > **Пример правила**  

   -   **Выбранный параметр.** Убедитесь, что выбран параметр **Пример параметра**.

   -   **Тип правила** > **Значение**  

   -   **Этот параметр должен соответствовать следующему правилу.** Проверьте правильность имени параметра и укажите, что значение параметра должно быть равно **1**.  

   -   **Исправлять несоответствующие параметры, когда это возможно.** Установите этот флажок, чтобы Configuration Manager сбрасывал значение раздела реестра до правильного значения, если оно окажется неправильным.  

6. Следуйте указаниям мастера, чтобы создать элемент конфигурации.  

 Теперь для развертывания созданной конфигурации на устройства можно использовать информацию из статьи [Типичные задачи, связанные с созданием и развертыванием конфигурационных баз с помощью System Center Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md).  

## <a name="next-steps"></a>Дальнейшие шаги

[Создание и развертывание конфигурационных баз](common-tasks-for-creating-and-deploying-configuration-baselines.md)
