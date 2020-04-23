---
title: Улучшенный протокол HTTP
titleSuffix: Configuration Manager
description: Используйте современные методы проверки подлинности, чтобы защитить обмен данными с клиентами без использования PKI-сертификатов.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703572"
---
# <a name="enhanced-http"></a>Улучшенный протокол HTTP

*Область применения: Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Эта функция появилась в версии 1806 [на стадии предварительного выпуска](../../servers/manage/pre-release-features.md). Начиная с версии 1810 эта функция больше не считается функцией предварительной версии.  

Майкрософт рекомендует использовать подключение по протоколу HTTPS для всех путей обмена данными Configuration Manager, но это может оказаться сложной задачей для некоторых клиентов из-за дополнительных расходов на управление сертификатами PKI.

Configuration Manager версии 1806 включает улучшения обмена данными между клиентами и системами сайтов. Основные цели этих улучшений две:  

- вы можете защитить обмен конфиденциальными данными с клиентами без использования PKI-сертификатов проверки подлинности сервера;  

- клиенты могут получать безопасный доступ к содержимому из точек распространения, не используя учетную запись доступа к сети, клиентский PKI-сертификат и проверку подлинности Windows.  

Весь обмен данными с клиентом осуществляется по протоколу HTTPS. Использование расширенной версии HTTP — это не то же самое что и включение HTTPS для обмена данными с клиентом или для системы сайта.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> Сертификаты PKI по-прежнему доступны для клиентов со следующими требованиями:  
>
> - Все взаимодействие с клиентом осуществляется по протоколу HTTPS.  
> - Расширенные функции управления инфраструктурой подписывания.
>
> Кроме того, если вы уже используете PKI, будет использоваться сертификат PKI, привязанный к службам IIS, даже если включен улучшенный протокол HTTP.



## <a name="scenarios"></a><a name="bkmk_scenario"></a> Сценарии

Эти улучшения будут особо полезны в описанных ниже сценариях.  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> Сценарий 1. Клиент для точки управления

<!--1356889-->
[Присоединенные к Azure Active Directory (Azure AD) устройства](/azure/active-directory/devices/concept-azure-ad-join) могут обмениваться данными с точкой управления, настроенной для протокола HTTP. На сервере сайта создается сертификат для точки управления, что позволяет ей обмениваться данными по защищенному каналу.

> [!Note]  
> Мы изменили это поведение в Configuration Manager начиная с текущей ветви версии 1802. Для этого сценария требовалась точка управления, настроенная для протокола HTTPS, для присоединенных к Azure AD клиентов, использующих для обмена данными шлюз управления облачными клиентами. Дополнительные сведения см. в статье [Включение точки управления для HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> Сценарий 2. Клиент для точки распространения

<!--1358228-->
Рабочая группа или клиент, присоединенный к Azure AD, могут пройти проверку подлинности и по защищенному каналу скачать содержимое из точки распространения, настроенной для протокола HTTP. Такие устройства также могут выполнять проверку подлинности и загружать содержимое из точки распространения, настроенной на HTTPS, не требуя PKI-сертификат на клиенте. Сложно добавить сертификат проверки подлинности клиента в рабочую группу или клиент, присоединенный к Azure AD.

Это поведение включает сценарии развертывания операционной системы с последовательностью задач, запускаемой с загрузочного носителя, PXE или центра программного обеспечения. Дополнительные сведения см. в разделе [Учетная запись доступа к сети](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> Сценарий 3. Удостоверение устройства Azure AD

<!--1358460-->
Устройство, присоединенное к Azure AD, или [гибридное устройство Azure AD](/azure/active-directory/devices/concept-azure-ad-join-hybrid) может обмениваться данными с назначенным сайтом в безопасном режиме. При этом не требуется, чтобы пользователь выполнял вход на устройство. Теперь удостоверения облачного устройства достаточно для аутентификации с использованием точки управления и CMG в сценариях, ориентированных на устройство. (Токен пользователя по-прежнему необходим для сценариев, ориентированных на пользователей.)  


## <a name="features"></a>Функции

Следующие возможности Configuration Manager поддерживают или требуют использовать расширенную версию HTTP:

- [Шлюз управления облаком](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Развертывание операционной системы без учетной записи для доступа к сети](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Включение совместного управления для новых устройств Windows 10 для Интернет клиентов](../../../comanage/tutorial-co-manage-new-devices.md)
- [Утверждение приложений по электронной почте](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Служба администрирования](../../../develop/adminservice/overview.md)
- [Просмотр сведений о недавно подключенных консолях](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Точка обновления программного обеспечения и связанные сценарии всегда поддерживали безопасный HTTP-трафик для клиентов и шлюза управления облачными клиентами. При этом используется механизм с точкой управления, который отличается от проверки подлинности на основе сертификата или маркера.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Предварительные условия  

- Точка управления, настроенная для клиентских подключений по протоколу HTTP. Установите этот параметр на вкладке **Общие** в свойствах роли точки управления.  

- Точка распространения, настроенная для клиентских подключений по протоколу HTTP. Установите этот параметр на вкладке **Связь** в свойствах роли точки распространения. Не устанавливайте флажок **Разрешить клиентам анонимное подключение**.  

- Интеграция сайта с Azure AD для управление облаком.  

    - Если это предварительное требование уже выполнено для вашего сайта, обновите приложение Azure AD. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Облачные службы** и выберите **Клиенты Azure Active Directory**. Выберите клиент Azure AD, укажите веб-приложение в области **приложений**, а затем щелкните **Обновить параметры приложения** на ленте.  

- *Только для [сценария 3](#bkmk_scenario3)* : клиент, на котором выполняется Windows 10 (версии 1803 или более поздней) и который присоединен к Azure AD. Клиенту требуется эта конфигурация для проверки подлинности устройства Azure AD.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Настройка сайта

1. В консоли Configuration Manager перейдите в рабочую область **Администрирование**, разверните узел **Конфигурация сайта** и выберите узел **Сайты**. Выберите сайт и щелкните **Свойства** на ленте.  

2. Перейдите на вкладку **Взаимодействие с клиентскими компьютерами**.

    > [!Note]
    > Начиная с версии 1906, эта вкладка называется **Communication Security** (Безопасность обмена данными).<!-- SCCMDocs#1645 -->  

    Выберите параметр для **HTTPS или HTTP**. Затем включите параметр **Использовать сертификаты, созданные с помощью Configuration Manager, для систем сайтов HTTP**.

> [!Tip]
> Получение и настройка нового сертификата для точки управления могут занять до 30 минут.

<!--3798957-->
Начиная с версии 1902, вы также можете включить расширенную версию HTTP для сайта центра администрирования. Используйте этот же процесс и откройте окно свойств сайта центра администрирования. Это действие включает только расширенный HTTP для ролей поставщика SMS на сайте центра администрирования. Это не глобальный параметр, который применяется ко всем сайтам в иерархии.

Эти сертификаты отобразятся в консоли Configuration Manager. Перейдите в рабочую область **Администрирование**, разверните узел **Безопасность** и выберите узел **Сертификаты**. Найдите корневой сертификат для **отправки SMS** и сертификаты роли сервера сайта, выданные корневым центром сертификации для отправки SMS.

Дополнительные сведения о взаимодействии клиента с точкой управления и точкой распространения в этой конфигурации см. в разделе [Обмен данными между клиентами и системами сайта и службами](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>См. также

- [Планирование безопасности](../security/plan-for-security.md)  

- [Безопасность и конфиденциальность клиентов Configuration Manager](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Настройка безопасности](../security/configure-security.md)  

- [Связь между конечными точками](communications-between-endpoints.md)  