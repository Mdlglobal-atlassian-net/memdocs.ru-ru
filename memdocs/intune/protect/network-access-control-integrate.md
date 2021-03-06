---
title: Интеграция управления доступом к сети в Microsoft Intune в Azure | Документы Майкрософт
description: Решения по управлению доступом к сети (NAC) используются для проверки состояния регистрации и соответствия устройств в Intune. В NAC поддерживаются определенные режимы и работа с условным доступом. Ознакомьтесь с действиями по адаптации и получению списка партнерских решений.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: aa7ecff7-8579-4009-8fd6-e17074df67de
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9302e2229b84519b46c9b2ade80488e7ca10aebf
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985015"
---
# <a name="network-access-control-nac-integration-with-intune"></a>Интеграция управления доступом к сети (NAC) с Intune

Intune интегрируется с партнерами по управлению доступом сети, чтобы помочь организациям защитить корпоративные данные, когда устройства пытаются обратиться к локальным ресурсам.

>[!IMPORTANT]
> NAC сейчас не поддерживается для выделенных устройств или полностью управляемых устройств Android Enterprise.

## <a name="how-do-intune-and-nac-solutions-help-protect-your-organization-resources"></a>Как решения NAC и Intune помогают защитить ресурсы вашей организации?

Решения NAC проверяют состояние регистрации и соответствия устройств в Intune для принятия решений по управлению доступом. Если устройство не зарегистрировано либо зарегистрировано, но не удовлетворяет политикам соответствия устройств Intune, его требуется перенаправить в Intune для регистрации или проверки соответствия.

### <a name="example"></a>Пример

Если устройство зарегистрировано и является соответствующим в рамках Intune, решение NAC должно предоставить ему доступ к корпоративным ресурсам. Например, можно разрешать или запрещать доступ пользователям, пытающимся обратиться к корпоративным ресурсам Wi-Fi или VPN.

## <a name="feature-behaviors"></a>Поведение функции

Устройства, которые активно синхронизируются с Intune, нельзя переключить из состояния **Соответствующее** / **Несоответствующее** в состояние **Несинхронизированное** (или **Неизвестное**). Состояние **Неизвестное** используется только для новых зарегистрированных устройств, которые еще не были проверены на предмет соответствия.

Если для устройств заблокирован доступ к ресурсам, служба блокировки должна перенаправлять всех пользователей [портала управления](https://portal.manage.microsoft.com), чтобы определить причину блокировки устройства.  Если пользователи посетят эту страницу, их устройства будут синхронно проверены на предмет соответствия.

## <a name="nac-and-conditional-access"></a>NAC и условный доступ

NAC использует условный доступ для принятия решений по управлению доступом. См. дополнительные сведения о [стандартных способах использования условного доступа с помощью Intune](conditional-access-intune-common-ways-use.md).

## <a name="how-the-nac-integration-works"></a>Принцип работы интеграции с NAC

Ниже описаны особенности интеграции NAC с Intune. В шагах 1–3 объясняется процесс подключения. Типичная работа после интеграции решения NAC с Intune описана в шагах 4–9.

![Схематическое изображение принципов работы NAC с Intune](./media/network-access-control-integrate/ca-intune-common-ways-2.png)

1. Зарегистрируйте партнерское решение NAC в Azure Active Directory (AAD) и предоставьте делегированные разрешения API Intune NAC.
2. Настройте партнерское решения NAC с помощью соответствующих параметров, включая URL-адрес обнаружения Intune.
3. Настройте партнерское решение NAC для проверки подлинности сертификата.
4. Пользователь подключается к корпоративной точке доступа Wi-Fi или выполняет запрос на VPN-подключение.
5. Партнерское решение NAC перенаправляет сведения об устройстве в Intune и запрашивает там состояние регистрации и соответствия устройства.
6. Если устройство не соответствует требованиям или не зарегистрировано, партнерское решение NAC просит пользователя зарегистрировать устройство или обеспечить его соответствие.
7. Устройство пытается повторно проверить свое состояние соответствия и регистрации.
8. После регистрации и обеспечения соответствия устройства партнерское решение NAC получает это состояние из Intune.
9. Устанавливается соединение, предоставляющее устройству доступ к корпоративным ресурсам.

## <a name="use-nac-for-vpn-on-your-iosipados-devices"></a>Использование NAC для VPN на устройствах с iOS и iPadOS

Служба NAC доступна для следующих виртуальных частных сетей без включения NAC в профиле VPN:

- NAC для Cisco Legacy AnyConnect
- F5 Access прежних версий
- Citrix VPN

NAC также поддерживается для Cisco AnyConnect, Citrix SSO и F5 Access.

### <a name="to-enable-nac-for-cisco-anyconnect-for-ios"></a>Включение NAC для Cisco AnyConnect для iOS

- Интегрируйте интегрированную среду сценариев с Intune для NAC, как описано в приведенной ниже ссылке.
- Установите для параметра профиля VPN **Включить управление сетевым доступом (NAC)** значение **Да**.

### <a name="to-enable-nac-for-citrix-sso"></a>Включение NAC для Citrix SSO

- Используйте Citrix Gateway 12.0.59 или более поздней версии.  
- Пользователям нужно использовать Citrix SSO 1.1.6 или более поздней версии.
- Выполните [интеграцию NetScaler с Intune для NAC](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html), как описано в документации по продуктам Citrix.
- В профиле VPN выберите **Базовые параметры** > **Включить управление сетевым доступом (NAC)** > выберите **Принять**.

### <a name="to-enable-nac-for-f5-access"></a>Включение NAC для F5 Access

- Используйте F5 BIG-IP 13.1.1.5 или более поздней версии.
- Интеграция BIG-IP с Intune для NAC. Эти шаги перечислены в руководстве F5 [Обзор: настройка APM для проверки состояния устройства с системами управления конечными точками](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-7-1-6/6.html#guid-0bd12e12-8107-40ec-979d-c44779a8cc89).
- В профиле VPN выберите **Базовые параметры** > **Включить управление сетевым доступом (NAC)** > выберите **Принять**.

VPN-подключение разрывается каждые 24 часа из соображений безопасности. VPN-подключение может сразу же быть переустановлено.

Мы с нашими партнерами работаем над выпуском решения NAC для этих клиентов. Когда решения будут готовы, в этой статье будет появляться дополнительная информация.

## <a name="next-steps"></a>Дальнейшие шаги

- [Интеграция Cisco ISE с Intune](https://www.cisco.com/c/en/us/td/docs/security/ise/2-1/admin_guide/b_ise_admin_guide_21/b_ise_admin_guide_20_chapter_01000.html)
- [Интеграция Citrix NetScaler с Intune](https://docs.citrix.com/en-us/netscaler-gateway/12/microsoft-intune-integration/configuring-network-access-control-device-check-for-netscaler-gateway-virtual-server-for-single-factor-authentication-deployment.html)
- [Интеграция F5 BIG-IP Access Policy Manager с Intune](https://support.f5.com/kb/en-us/products/big-ip_apm/manuals/product/apm-client-configuration-13-0-0/6.html)
- [Интеграция HP Aruba ClearPass с Intune](https://support.arubanetworks.com/Documentation/tabid/77/DMXModule/512/Command/Core_Download/Default.aspx?EntryId=31271)
- [Интеграция Squadra security Removable Media Manager (secRMM) с Intune](http://www.squadratechnologies.com/StaticContent/ProductDownload/secRMM/9.9.0.0/secRMMIntuneAccessControlSetupGuide.pdf)
