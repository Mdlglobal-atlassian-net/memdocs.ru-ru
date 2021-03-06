---
title: Учебник. Пошаговое руководство по использованию Intune на портале Azure
titleSuffix: Microsoft Intune
description: Это обзорное руководство по Microsoft Intune поможет вам лучше понять, как выполнять стандартные задачи.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 11/06/2019
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: e892d8a3-7f74-498c-98d5-e968a8fbb049
Customer intent: As an Intune admin, I want to learn where to find the different features in Intune.
ms.reviewer: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22910604d19aecb37adef2452d01d46c1435f7ef
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79355261"
---
# <a name="tutorial-walkthrough-of-microsoft-intune-in-the-azure-portal"></a>Руководство. Пошаговое руководство по использованию Microsoft Intune на портале Azure

Платформа [Azure](https://docs.microsoft.com/learn/modules/welcome-to-azure) включает в себя более 100 служб для различных облачных сценариев и задач. Одна из них — Microsoft Intune. Intune помогает обеспечивать соответствие устройств, приложений и данных организации требованиям безопасности. Вы можете настроить требования, которые должны проверяться, и действия, выполняемые при их несоблюдении. [Портал Azure](https://portal.azure.com) — это ресурс, где можно найти службу Microsoft Intune. Знание возможностей Intune поможет вам в выполнении различных задач по управлению мобильными устройствами (MDM) и мобильными приложениями (MAM).

В этом руководстве выполняются следующие задачи:
> [!div class="checklist"]
> * Обзор Microsoft Intune
> * Настройка портала Azure

Если у вас нет подписки Intune, [зарегистрируйтесь для получения бесплатной пробной учетной записи](free-trial-sign-up.md).

## <a name="prerequisites"></a>Предварительные условия
Перед настройкой Microsoft Intune изучите следующие требования.

- [Поддерживаемые операционные системы и браузеры](supported-devices-browsers.md) 
- [Требования к конфигурации сети и ее пропускная способность](network-bandwidth-use.md)

## <a name="sign-up-for-a-microsoft-intune-free-trial"></a>Регистрация для использования бесплатной пробной версии Microsoft Intune

Пробная версия Intune предоставляется бесплатно на 30 дней. Если уже есть рабочая или учебная учетная запись, выполните **вход** под этой учетной записью и добавить в свою подписку Intune. Если же нет, [зарегистрируйте бесплатную пробную учетную запись](free-trial-sign-up.md) для использования Intune в своей организации.

> [!IMPORTANT]
> Зарегистрировав новую учетную запись, вы не сможете объединить ее с уже существующей рабочей или учебной учетной записью.

## <a name="tour-microsoft-intune"></a>Обзор Microsoft Intune

Чтобы ознакомиться с использованием Intune на портале Azure, следуйте приведенным ниже инструкциям. Завершив обзор, вы будете лучше понимать, как устроены некоторые из основных областей в Intune.

1. Откройте браузер и войдите на [портал Intune](https://aka.ms/intuneportal). Если вы только приступаете к работе с Intune, используйте бесплатную пробную подписку.

    ![Снимок экрана: портал Microsoft Intune](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-01.png)

    При открытии Intune или любой другой службы в Azure она отображается на панели. Вот некоторые рабочие нагрузки, с которых вы, скорее всего, начнете работу в Intune: **Устройства**, **Клиентские приложения**, **Пользователи** и **Группы**. Рабочая нагрузка — это попросту раздел службы. При выборе рабочей нагрузки соответствующая панель открывается на всю страницу. Другие открываемые панели разворачиваются из правой части панели и сворачиваются, открывая предыдущую панель. Панели также называются колонками. 

    По умолчанию при открытии Intune отображается панель **Обзор**. На ней в наглядной форме представлена общая информация о назначенных устройствах и состоянии соответствия требованиям, а также состоянии установки приложений.

2. В [Intune](https://aka.ms/intuneportal) выберите **Регистрация устройства**, чтобы просмотреть сведения о зарегистрированных устройствах в клиенте Intune. Если у вас новый клиент Intune, то зарегистрированных устройств пока нет. 

    ![Снимок экрана: панель "Регистрация устройства"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-02.png)
    
    Intune позволяет управлять устройствами и приложениями в рамках рабочего процесса, включая способ их доступа к корпоративным данным. Прежде чем использовать службу управления мобильными устройствами (MDM), зарегистрируйте устройства в Intune. После регистрации выдается сертификат MDM. Этот сертификат используется для обмена данными со службой Intune. 

    Есть несколько способов регистрации корпоративных устройств в Intune. Каждый способ зависит от типа владения (личное или корпоративное), типа устройства (iOS/iPadOS, Windows, Android) и требований к управлению (сброс, сопоставление, блокировка). Однако, прежде чем регистрировать устройства, необходимо настроить инфраструктуру Intune. В частности, для регистрации устройств нужно [настроить центр MDM](mdm-authority-set.md). Дополнительные сведения о подготовке среды (клиента) Intune см. в статье [Настройка Intune](setup-steps.md). Подготовив клиент Intune, вы можете регистрировать устройства. Дополнительные сведения о регистрации устройств см. в статье [Что такое регистрация устройств?](../enrollment/device-enrollment.md).

3. В [Intune](https://aka.ms/intuneportal) выберите **Соответствие устройства политике**, чтобы просмотреть сведения о соответствии устройств, находящихся под управлением Intune, требованиям. Откроется страница наподобие приведенной ниже.

    ![Снимок экрана: панель "Соответствие устройства политике"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-03.png)
    
    Требования соответствия — это, по сути, правила, такие как требование ПИН-кода устройства или требование шифрования устройства. Политики соответствия устройств определяют правила и параметры, которым должно соответствовать устройство, чтобы считаться соответствующим требованиям. Для использования политик соответствия устройств требуются следующие элементы:
    - служба Intune и подписка Azure Active Directory (Azure AD) Premium;
    - устройства с поддерживаемой платформой;
    - устройства должны быть зарегистрированы в Intune;
    - устройства, зарегистрированные для одного пользователя, или устройства без основного пользователя.
    
    Дополнительные сведения см. в статье [Начало работы с политиками соответствия устройств в Intune](../protect/device-compliance-get-started.md).

4. В [Intune](https://aka.ms/intuneportal) выберите **Конфигурация устройств**, чтобы просмотреть сведения о профилях устройств в Intune.

    ![Снимок экрана: панель "Конфигурация устройств"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-04.png)
    
    Intune содержит параметры и функции, которые можно включать или отключать на различных устройствах в вашей организации. Эти параметры и компоненты добавляются в "профили конфигурации". Вы можете создавать профили для различных устройств и платформ, включая iOS/iPadOS, Android и Windows. Затем с помощью Intune можно применять профили к устройствам в организации.   

    Дополнительные сведения о конфигурации устройств см. в статье [Применение параметров функций на устройствах с помощью профилей устройств в Microsoft Intune](../configuration/device-profiles.md).

5. В [Intune](https://aka.ms/intuneportal) выберите **Устройства**, чтобы просмотреть сведения об устройствах, зарегистрированных в клиенте Intune. Если у вас новый клиент Intune, то зарегистрированных устройств пока нет.

    ![Снимок экрана: панель "Регистрация устройства"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-05.png)

    На панели **Устройства** приводятся сведения об устройствах, зарегистрированных в клиенте. Вы можете щелкнуть пункт **Все устройства**, чтобы открыть список устройств, имеющихся в клиенте Intune.

6. В [Intune](https://aka.ms/intuneportal) выберите **Клиентские приложения**, чтобы просмотреть состояние установки приложений.

    ![Снимок экрана: панель "Клиентские приложения"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-06.png)

    Как ИТ-администратор, вы можете использовать Microsoft Intune для управления клиентскими приложениями, которые используют сотрудники организации. Эта функция дополняет возможности управления устройствами и защиты данных. Одна из основных задач администратора — убедиться в том, что пользователи имеют доступ к приложениям, необходимым им для работы. Кроме того, может потребоваться назначать приложения и управлять ими на устройствах, которые не зарегистрированы в Intune. Intune предлагает широкий набор возможностей, позволяющих получить нужные приложения на требуемых устройствах. Дополнительные сведения о добавлении и назначении приложений см. в статьях [Добавление приложений в Microsoft Intune](../apps/apps-add.md) и [Назначение приложений группам с помощью Microsoft Intune](../apps/apps-deploy.md).

7. В [Intune](https://aka.ms/intuneportal) выберите **Условный доступ**, чтобы просмотреть сведения о политиках доступа.

    ![Снимок экрана: панель "Условный доступ"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-07.png)

    Условный доступ — это способ управления устройствами и приложениями, которым разрешено подключаться к вашей электронной почте и ресурсам компании. Сведения об условном доступе для устройств и приложений, а также описание распространенных сценариев использования условного доступа в Intune см. в статье [Что такое условный доступ?](../protect/conditional-access.md)

8. В [Intune](https://aka.ms/intuneportal) выберите **Пользователи**, чтобы просмотреть сведения о пользователях, добавленных в Intune. Пользователи являются сотрудниками вашей организации.

    ![Снимок экрана: панель "Пользователи"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-08.png)

    Вы можете добавлять пользователей в Intune напрямую или синхронизировать их из локальной службы Active Directory. После добавления пользователи могут регистрировать устройства и получать доступ к ресурсам организации. Вы также можете предоставит пользователям дополнительные разрешения на доступ к Intune. Дополнительные сведения см. в статье [Добавление пользователей и предоставление административных разрешений для Intune](users-add.md).

9. В [Intune](https://aka.ms/intuneportal) выберите **Группы**, чтобы просмотреть сведения о группах Azure Active Directory (Azure AD), добавленных в Intune. Администраторы Intune используют группы для управления устройствами и пользователями.

    ![Снимок экрана: панель "Группы"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-09.png)

    Группы можно настраивать необходимым образом. Создавайте группы, чтобы упорядочить пользователей или устройства по географическому расположению, отделу или характеристикам оборудования. Используйте группы для управления задачами в требуемом масштабе. Например, вы можете настроить политики для многих пользователей или развернуть приложения для набора устройств. Дополнительные сведения о группах см. в статье [Добавление групп для организации пользователей и устройств](groups-add.md).

10. В [Intune](https://aka.ms/intuneportal) выберите **Справка и поддержка**, чтобы запросить помощь. ИТ-администратор может искать сведения о решении проблем, а также регистрировать обращения в службу поддержки, связанные с Intune, через Интернет, выбрав пункт **Справка и поддержка**. 

    ![Снимок экрана: панель "Справка и поддержка"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-10.png)

    Для создания обращения в службу поддержки вашей учетной записи должна быть назначена роль администратора в Azure Active Directory. Имеются следующие роли администраторов: **администратор Intune**, **глобальный администратор** и **администратор служб**. Дополнительные сведения см. в разделе [Как получить поддержку для Microsoft Intune](get-support.md).

11. В [Intune](https://aka.ms/intuneportal) выберите **Состояние клиента**, чтобы просмотреть сведения о клиенте Intune.

    ![Снимок экрана: панель "Состояние клиента"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-11.png)

    Здесь приводятся сведения о состоянии соединителя, состоянии работоспособности службы Intune, а также новости Intune. Если возникли проблемы с вашим клиентом или самой службой Intune, информация о них будет представлена на панели **Состояние клиента**. Дополнительные сведения см. в статье [Страница "Состояние клиента" Intune](tenant-status.md).

12. В [Intune](https://aka.ms/intuneportal) выберите **Устранение неполадок**, чтобы получить советы по устранению неполадок, обратиться в службу поддержки или проверить состояние Intune. Представленная информация связана с выбранным пользователем Intune.

    ![Снимок экрана: панель "Устранение неполадок"](./media/tutorial-walkthrough-intune-portal/tutorial-walkthrough-intune-portal-12.png)

Дополнительные сведения об устранении неполадок в службе Intune см. в статье [Использование портала диагностики для оказания помощи пользователям в вашей компании](help-desk-operators.md).

## <a name="configure-the-azure-portal"></a>Настройка портала Azure

Вы можете настроить внешний вид портала Azure.

### <a name="change-the-sidebar"></a>Изменение боковой панели

На **боковой панели** в левой части портала Azure отображается список всех доступных служб Azure. Вы можете изменить заданное по умолчанию представление списка, чтобы иметь в своем распоряжении постоянное представление важных для вас служб. Ниже Intune выступает в качестве примера службы, которая будет добавлена в начало списка.

![Пользователь, выполняющий поиск Microsoft Intune в списке "Дополнительные службы".](./media/tutorial-walkthrough-intune-portal/azure-add-intune1.png)

1. Выберите **Все службы** на боковой панели слева.
2. В поле фильтра введите условие поиска **Intune**.
3. Выберите **звездочку**, чтобы добавить Intune в нижнюю часть списка избранных служб.
4. Наведите указатель мыши на службу Intune. Перетащите Intune с помощью **трех вертикальных точек** справа от имени службы.

### <a name="change-the-dashboard"></a>Изменение панели мониторинга

**Панель мониторинга** является начальной страницей по умолчанию. На этой странице вы настраиваете плитки для отображения наиболее важных для вас сведений.

![Изображение универсальной новой панели мониторинга. На рисунке отображается боковая панель со всеми службами в левой части и основная панель мониторинга в центре. Кнопки изменения панели мониторинга находятся в верхней части. Там же располагаются плитки, которые предоставляют доступ к ресурсам, кратким руководствам, состоянию работоспособности и Azure Marketplace.](./media/tutorial-walkthrough-intune-portal/azure-default-dashboard.png)

Чтобы изменить текущую панели мониторинга, нажмите кнопку **Изменить панель мониторинга**. Если вы не хотите изменять панель мониторинга по умолчанию, можно создать **новую панель мониторинга**. При создании панели мониторинга вы получаете пустую закрытую панель мониторинга с **коллекцией плиток**. Вы можете добавлять плитки и менять их местами. Плитки можно найти по их категории **Общие**, по **типу**, с помощью функции **Поиск** и с помощью **группы ресурсов** или **тега**.

Можно также добавлять плитки напрямую на панели мониторинга, нажав кнопку с **многоточием** и выбрав **Закрепить на панели мониторинга**.

![Крупный план расположения "Пользователи и группы" > "Все группы" в Intune с параметром "Закрепить на панели мониторинга" в правой части группы.](./media/tutorial-walkthrough-intune-portal/azure-pin-to-dashboard.png)

Это действие будет более актуальным после добавления дополнительного содержимого, такого как группы и пользователи, в Intune.

## <a name="next-steps"></a>Дальнейшие шаги

Чтобы быстро приступить к работе с Microsoft Intune, ознакомьтесь с краткими руководствами, предварительно зарегистрировав бесплатную учетную запись Intune.

> [!div class="nextstepaction"]
> [Краткое руководство. Бесплатная пробная версия Microsoft Intune](free-trial-sign-up.md)
