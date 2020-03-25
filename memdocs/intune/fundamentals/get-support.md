---
title: Получение поддержки для Microsoft Intune
titleSuffix: Microsoft Intune
description: Получите поддержку по платной или пробной версии Microsoft Intune онлайн или по телефону.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/22/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 7fc95d17-098e-4da5-8a09-a96476569dd9
ms.reviewer: srik
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: b746317ef15065af246cfd977f6e9d745ef4dea7
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79362684"
---
# <a name="how-to-get-support-for-microsoft-intune"></a>Получение поддержки для Microsoft Intune

Для каждой подписки Microsoft Intune Майкрософт предлагает услуги глобальной, технической и предпродажной поддержки, а также поддержки по выставлению счетов и продлению подписки. Для оплаченных и пробных подписок доступна поддержка в Интернете и по телефону. Техническая поддержка в Интернете доступна на английском и японском языках. Поддержка по телефону и поддержка выставления счетов по сети доступны на дополнительных языках.

Администратор Intune может отправить запрос в службу поддержки, связанный с Intune, через Интернет на портале Azure, выбрав пункт **Справка и поддержка**. Для создания инцидента в службе поддержки и управления им учетной записи должна быть назначена роль Azure Active Directory (Azure AD), включающая *действие* **microsoft.office365.supportTickets**. Сведения о ролях и разрешениях Azure AD, необходимых для создания запроса в службу поддержки, см. в статье [Administrator role permissions in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) (Разрешения роли администратора в Azure Active Directory).

>[!IMPORTANT]
> Чтобы получить техническую поддержку для продуктов, используемых с Intune, от сторонних разработчиков (например, SaaSwedo, Cisco или Lookout), сначала попробуйте обратиться к поставщику продукта. Прежде чем обращаться в службу поддержки Intune, проверьте, правильно ли настроен этот сторонний продукт.
>
> Сведения об устранении неполадок, связанных с Microsoft Intune, см. в разделе [Устранение неполадок](help-desk-operators.md) документации Intune.


## <a name="help-and-support-experience"></a>Интерфейс справки и поддержки

Справка и поддержка для Intune доступна в [Центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) и во всех колонках (и на всех страницах) в Intune на портале Azure.

Новый интерфейс *Справка и поддержка* похож на интерфейс в [Центре администрирования Microsoft 365](https://admin.microsoft.com/) и заменяет предыдущий интерфейс *Справка + поддержка*, который будет доступен для других служб в Azure.

> [!TIP]
> Начиная с 18 ноября 2019 г. обновленный и усовершенствованный интерфейс в консоли для получения справки и поддержки начнет распространятся на клиентов. Новый интерфейс пока недоступен, но он скоро появится.

### <a name="options-to-access-help-and-support"></a>Параметры для доступа к Справке и поддержке

При использовании только что созданного клиента для Intune раздел *Справка и поддержка* может не открыться и вернется следующее сообщение:

- *We encountered an unknown problem. Please refresh the page but if the problem persists, please create a case through [M365 Admin Center](https://admin.microsoft.com) and reference the session ID provided* (Возникла неизвестная проблема. Обновите страницу, но если проблема не исчезнет, создайте обращение в Центре администрирования M365 и укажите предоставленный идентификатор сеанса).

Сведения об ошибке включают в себя *идентификатор сеанса*, *информацию о расширении* и многое другое. 
 
Эта проблема возникает, если вы еще не выполнили проверку подлинности для новой учетной записи клиента в **Центре администрирования M365** по адресу https://admin.microsoft.com или **на портале Office 365** по адресу https://portal.office.com. Чтобы устранить эту проблему, щелкните ссылку для *Центра администрирования M365* в сообщении или перейдите на портал https://portal.office.com и выполните вход. После выполнения проверки подлинности на каком-либо из этих сайтов раздел *Справка и поддержка* для Intune станет доступным.


**Чтобы получить доступ к разделу справки и поддержки**:

- **На портале Azure:**

  - Щелкните **Справка и поддержки** в любой колонке или на странице Intune.

  > [!NOTE]  
  > Если ваш экземпляр Intune размещен в вычислительном облаке для государственных организаций, также известном как национальное облако, например Azure для государственных организаций, см. раздел [Поддержка частного облака для государственных организаций в Intune](#intune-support-for-private-cloud-for-government) далее в этой статье. *Справка и поддержка* Intune не будут доступны в частном облаке для государственных организаций до следующего года.

- **Из Центра администрирования Microsoft Endpoint Manager**
  - Выбрав область функций для Intune, выберите пункт **Справка и поддержка**.
  - В любом узле Центра администрирования Microsoft Endpoint Manager выберите значок **?** в правом верхнем углу, а затем в раскрывающемся списке выберите службу, для которой требуется помощь. Значок **?** Значок в Центре администрирования Microsoft Endpoint Manager поддерживает несколько служб. Вам нужно выбрать конкретную службу, для которой вам требуется помощь.  

    ![Выбор своей службы](./media/get-support/select-a-service.png)

    Выбрав службу, вы увидите страницу *Справка и поддержка* для этой службы, где вы можете уточнить сведения, чтобы [найти решения](#find-solutions) для конкретной проблемы.

    Если результаты поиска не соответствуют ожиданиям, убедитесь, что выбрана правильная служба. Выбранная служба появится сразу под разделом *Справка и поддержка*.  Если вы не выбрали нужную службу, щелкните *Выберите службу*, чтобы вернуться в раскрывающийся список выбора службы.

    ![Подтверждение выбора службы](./media/get-support/confirm-your-service-selection.png)

###  <a name="the-support-experience"></a>Интерфейс поддержки

  При открытии раздела "Справка и поддержка" на портале отображается окно **Требуется помощь?** .

  ![Просмотр окна "Требуется помощь?"](./media/get-support/need-help.png)

  В левом верхнем углу находятся три значка, которые можно щелкнуть, чтобы открыть нужную панель в окне *Требуется помощь?* . Панель, которую вы просматриваете, обозначается подчеркиванием.

  У клиентов с планами **Premier** или **Единая поддержка** есть [дополнительные варианты](#premier-and-unified-support-customers) получения поддержки. Также для них отображается баннер на странице *Требуется помощь?* , который напоминает следующее изображение: ![Баннер для клиентов с планом поддержки Premier](./media/get-support/premier-banner.png)

  На странице *Нужна помощь?* открывается область *Поиск решений*. Но если у вас есть активный запрос в службу поддержки, в окне откроется область *Запросы на обслуживание*, где можно просмотреть сведения об активных и закрытых обращениях в службу поддержки.

#### <a name="find-solutions"></a>Поиск решений

![Выбор области поиска решений](./media/get-support/find-solutions.png)

В области *Поиск решений* укажите сведения об ошибке в соответствующем текстовом поле. На основе вводимого текста область заполнится аналитическими сведениями, которые представляют потенциальные совпадения. Вы также получите ссылки на рекомендуемые статьи, которые могут помочь вам устранить проблему.

Если для указанных сведений найдено строгое соответствие, советы по устранению неполадок могут появиться прямо в окне *Требуется помощь?* .

Например, вы можете ввести **ошибки синхронизации паролей**. Результаты содержат инструкции по устранению неполадок непосредственно в области, а также ссылки на рекомендуемые статьи из нашей библиотеки с документацией.

![Просмотр аналитических сведений об устранении неполадок](./media/get-support/troubleshooting-insights.png)

#### <a name="contact-support"></a>Обратитесь в службу поддержки.

![Выбор области "Обращение в службу поддержки"](./media/get-support/contact-support.png)

В области *Обращение в службу поддержки* можно отправить запрос на помощь. Эта область становится доступной после предоставления некоторых основных ключевых слов в области *Поиск решений*.

При запросе на получение поддержки предоставьте сведения о проблеме с требуемым объемом детализации.  После подтверждения номера телефона и адреса электронной почты выберите предпочтительный метод связи. В этом окне отображается предположительное время ответа для каждого метода связи. Перед отправкой запроса вложите такие файлы, как журналы или снимки экрана, которые предоставят дополнительные сведения об ошибке.

![Форма обращения в службу поддержки](./media/get-support/contact-support-form.png)

Заполнив необходимые сведения, щелкните **Связаться со мной**, чтобы отправить запрос.

#### <a name="service-requests"></a>Запросы на обслуживание

![Выбор области "Запросы на обслуживание"](./media/get-support/service-requests.png)

В области *Запросы на обслуживание* отображается журнал обращений. Активные обращения находятся в верхней части списка. Там же можно просмотреть закрытые обращения.

![Просмотр списка запросов на обслуживание](./media/get-support/service-requests-pane.png)

Если у вас есть номер активного обращения в службу поддержки, его можно ввести здесь, чтобы перейти к этой проблеме. Также вы можете выбрать любой инцидент в списке активных и закрытых инцидентов, чтобы просмотреть дополнительные сведения о нем.

Просмотрев сведения об инциденте, щелкните стрелку влево в верхней части окна запроса на обслуживание над тремя значками в области *Требуется помощь?* . Стрелка назад отображает список открытых инцидентов.

#### <a name="premier-and-unified-support-customers"></a>Клиенты с планами Premier и Единая поддержка

Клиенты с планами **Premier** или **Единая поддержка** могут указать серьезность проблемы и запланировать обратный вызов поддержки в указанные день и время. Эти параметры доступны при открытии или отправке новой проблемы, а также при изменении активного обращения в службу поддержки.

**Серьезность** — параметры для определения серьезности проблемы зависят от контракта на поддержку.

- *Premier:* уровень серьезности A, B или C.
- *Единая поддержка:* критический или некритический.

Выбор уровня серьезности **А** или **Критический** ограничивается обращением в службу поддержки по телефону — самый быстрый вариант получения поддержки.

**Расписание обратного вызова** — вы можете запросить обратный вызов в указанные день и время.

## <a name="azure-help--support-experience"></a>Интерфейс справки и поддержки Azure

Вы не сможете больше получать доступ к интерфейсу *Справка и поддержка* в Azure для получения помощи в Intune, если ваша подписка не находится в частном облаке для государственных организаций.
Если ваш экземпляр Intune не работает в частном облаке для государственных организаций, навигация на странице *Справка и поддержка* Azure будет перенаправлять вас в раздел *Справка и поддержка* Intune для создания обращений в службу поддержки и управления ими:

Используя область навигации слева **Справка + поддержка** или значок **?** для открытия области *Справка* и выбора пункта **Справка и поддержка**, вы сможете открыть страницу *Справка и поддержка* Azure. 


На этой странице щелкните **+Создать запрос на поддержку**, чтобы открыть вкладку *Основные* на странице *Справка и поддержка — новый запрос на поддержку*.

![Справка + поддержка](./media/get-support/help-plus-support.png)

На этой странице:

- В качестве *типа проблемы* укажите **Техническая**.
- В качестве *службы* укажите **Microsoft Intune**.

  Вы получите ссылку, которая перенаправит вас на страницу [справки и поддержки Intune](https://aka.ms/intunehelpsupport).
  
  ![Новый запрос на поддержку](./media/get-support/new-request.png)


## <a name="intune-support-for-private-cloud-for-government"></a>Поддержка частного облака для государственных организаций в Intune

Если ваша подписка Intune размещена в частном облаке для государственных организаций, которое также называется национальным облаком, например Azure для государственных организаций, у вас еще нет доступа к обновленному интерфейсу справки и поддержки Intune.  Вместо этого используйте следующую информацию, чтобы получить поддержку в Intune.

### <a name="create-an-online-support-ticket"></a>Создание запроса в службу поддержки в Интернете

>[!IMPORTANT]
> Так как интерфейс *Справка и поддержка* переходит на новую систему, которая еще не была доступна для частного облака для государственных организаций, при создании обращения в службу поддержки портал определяет обращение с помощью идентификационного номера из 15 цифр. Когда создается обращение с 15-значным номером, создается его зеркальная версия для использования службой поддержки Майкрософт. Это зеркальное обращение создается в новой системе поддержки с 8-значным идентификатором и используется службами поддержки для наблюдения за всеми взаимодействиями по этому обращению. Вскоре после создания обращения с 15-значным номером вы получите сообщение электронной почты с указанием 8-значного идентификатора зеркального варианта обращения, используемого службами поддержки.
>
> Персонал службы поддержки работает с обращением с 8-значным идентификатором и использует только эту версию для регистрации сообщений и отслеживания хода обработки обращения. Таким образом, вы будете получать электронные обновления об обращении с 8-значным идентификатором, которые будут выступать в качестве записей для отслеживания обработки обращения. Для обращения в службу поддержки с 15-значным идентификатором не будут записываться сведения. Когда служба поддержки завершает обращение с 8-значным идентификатором, это состояние отражается в обращении с 15-значным идентификатором, которое можно просмотреть на портале Azure.  Никакие другие обновления и изменения состояния не должны появляться в варианте обращения с 15-значным идентификатором.
>
> Позже, когда в этом году завершатся переходы между средствами поддержки, интерфейс Intune, размещенный в облаке для государственных организаций, будет похож на интерфейс *справки и поддержки* по умолчанию, который в настоящее время доступен для подписок Intune, размещенных в общедоступном облаке.

1. Войдите на портал Azure (<https://portal.azure.us>), используя свои учетные данные администратора Intune, и выберите значок **?** в правом верхнем углу, а затем выберите **Справка и поддержка** для перехода на страницу [справки и поддержки Azure](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

   ![Изображение: выделенные ссылка с вопросительным знаком и ссылка "Справка и поддержка"](./media/get-support/azure-get-support.png)

2. На странице **Справка и поддержка** Azure выберите **Новый запрос в службу поддержки**.

   ![Изображение: страница справки и поддержки с выделенной ссылкой "Новый запрос в службу поддержки"](./media/get-support/azure-support-ticket-link.png)

3. На вкладке **Основные сведения** выберите для большинства вопросов по технической поддержке Intune следующие параметры:
   - **Тип проблемы**: **Техническая**.
   - **Подписка**: <*ваша подписка*>.
   - **Служба**. **Microsoft Intune**
   - **Тип проблемы**: выберите тип проблемы в раскрывающемся меню.
   - **Подтип проблемы**: выберите подтип проблемы в раскрывающемся меню.
   - **Тема**. Кратко опишите проблему, в решении которой вам требуется помощь.

   ![Изображение: вкладка "Основные сведения" на странице "Справка и поддержка" — "Новый запрос в службу поддержки"](./media/get-support/help-new-support-case-basics.png)

   Выберите **Далее: решения**, чтобы продолжить.
4. На вкладке **Решения** просмотрите рекомендуемые действия, которые могут помочь решить вашу проблему без подачи заявки в службу. Если после этого вы по-прежнему хотите создать запрос в службу поддержки, щелкните **Далее: сведения**.

   ![Изображение: вкладка "Решения" на странице "Справка и поддержка" — "Новый запрос в службу поддержки"](./media/get-support/help-new-support-case-solutions.png)
5. На вкладке **Сведения** укажите сведения о вашей проблеме, метод поддержки, ваши контактные данные, а затем щелкните **Далее: отзыв и создание**.

   ![Изображение: вкладка "Сведения" на странице "Справка и поддержка" — "Новый запрос в службу поддержки"](./media/get-support/help-new-support-case-details.png)
6. Проверьте сведения, убедитесь, что они правильные, а затем выберите **Создать**, чтобы отправить запрос в службу поддержки.

   ![Изображение: вкладка "Отзыв и создание" на странице "Новый запрос в службу поддержки"](./media/get-support/help-new-support-case-create.png)

>[!IMPORTANT]
>Если у вас возник вопрос о выставлении счетов или о подписке, вы можете сделать обращение для получения поддержки через [Центр администрирования Microsoft 365](https://admin.microsoft.com/Support/SupportEntry.aspx).

### <a name="view-support-requests"></a>Просмотр запросов на поддержку  

Запросы в службу поддержки можно просмотреть на портале Azure. Однако доступны ограниченные сведения.  Чтобы просмотреть обращения:

1. Войдите в Azure (<https://portal.azure.com>), используя свои учетные данные администратора Intune, и выберите значок **?** в правом верхнем углу, а затем выберите **Справка и поддержка** для перехода на страницу [справки и поддержки Azure](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview).

2. На странице **Справка и поддержка** можно просмотреть список **недавних запросов в службу поддержки**.

   > [!IMPORTANT]  
   > Пользователи частного облака для государственных организаций могут просматривать только обращения в службу поддержки с 15-значным номером и состояние инцидента. Все сообщения и оповещения касательно обращения отправляются по электронной почте и ссылаются на обращение с 8-значным номером, созданное в консоли Intune в виде зеркальной версии изначального обращения.

## <a name="additional-resources"></a>Дополнительные ресурсы  

- [Поддержка по вопросам выставления счетов и управления подписками](https://support.office.com/article/Contact-Office-365-for-business-support-Admin-Help-32a17ca7-6fa0-4870-8a8d-e25ba4ccfd4b)
- [Корпоративное лицензирование](https://go.microsoft.com/fwlink/p/?LinkID=282015)
- [Устранение неполадок, связанных с Intune](help-desk-operators.md)