---
title: Политика соответствия устройств для устройств Jamf
titleSuffix: Microsoft Intune
description: Политики соответствия Microsoft Intune с условным доступом Azure Active Directory можно использовать для защиты управляемых устройств Jamf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/18/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: c87fd2bd-7f53-4f1b-b985-c34f2d85a7bc
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9760029effc873b510bf37b779c054c9a0574a20
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79353155"
---
# <a name="enforce-compliance-on-macs-managed-with-jamf-pro"></a>Принудительное применение политик соответствия требованиям на компьютерах Mac под управлением Jamf

При [интеграции Jamf Pro с Intune](conditional-access-integrate-jamf.md) можно использовать политики условного доступа для обеспечения соответствия на устройствах Mac в рамках требований организации.  Эта статья поможет вам при выполнении следующих задач:  

- Создание политик условного доступа.
- Настройка Jamf Pro для развертывания приложения Корпоративного портала Intune на устройствах, управляемых с помощью Jamf.
- Настройка устройств для регистрации в Azure AD при входе пользователя устройства в приложение Корпоративного портала, запускаемого в приложении Jamf Self Service. При регистрации устройства создается удостоверение в Azure AD, которое позволяет оценивать устройство с помощью политик условного доступа к ресурсам компании.  
 
Для процедур, описанных в этой статье, требуется доступ к консолям Intune и Jamf Pro.

## <a name="set-up-device-compliance-policies-in-intune"></a>Настройка политик соответствия требованиям устройств в Intune

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Выберите **Устройства** > **Политики соответствия**. Если вы используете ранее созданную политику, выберите ее в консоли и перейдите к следующему шагу процедуры. Чтобы создать новую политику выберите **Создать политику**, а затем укажите сведения для политики *платформы* для **macOS**. Настройте *параметры* и *действия при несоответствии* в соответствии с требованиями организации, а затем нажмите кнопку **Создать**, чтобы сохранить политику.

3. На панели политики *Обзор* щелкните **Назначения**. Используйте доступные параметры, чтобы настроить, какие пользователи Azure Active Directory (Azure AD) и группы безопасности получают эту политику. Интеграция Jamf с Intune не поддерживает политику соответствия требованиям, ориентированную на группы устройств.

4. При нажатии кнопки **Сохранить** политика развертывается для пользователей.  

Развертываемые политики предназначены для устройств, используемых назначенными пользователями. Эти устройства оцениваются на соответствие требованиям. Соответствующие устройства помечены как соответствующие требованиям для параметра *Требовать, чтобы устройство было отмечено как соответствующее* в Azure AD.  

> [!NOTE]
> Intune требуется полное шифрование диска для соответствия.

## <a name="deploy-the-company-portal-app-for-macos-in-jamf-pro"></a>Развертывание приложения корпоративного портала для macOS в Jamf Pro

Создайте политику в Jamf Pro, чтобы развернуть Корпоративный портал Intune. Эта политика развертывает приложение корпоративного портала, чтобы оно было доступно в Jamf Self Service. Создайте эту политику, прежде чем создавать политику в Jamf Pro, чтобы пользователи могли регистрировать устройства в Azure AD.  

Чтобы выполнить следующую процедуру, требуется доступ к устройству macOS и порталу Jamf Pro. 

### <a name="to-deploy-the-company-portal-app"></a>Развертывание приложения корпоративного портала  

1. На устройстве macOS скачайте (но не устанавливайте) последнюю версию [приложения "Корпоративный портал" для macOS](https://go.microsoft.com/fwlink/?linkid=862280). Вам нужна только копия приложения, чтобы вы могли отправить приложение в Jamf Pro.  

2. Откройте Jamf Pro и выберите **Computer management** (Управление компьютером)  > **Packages** (Пакеты).

3. Создайте пакет с помощью приложения "Корпоративный портал" для macOS, а затем нажмите кнопку **Save** (Сохранить).

4. Выберите **Computers** (Компьютеры) > **Политики** (Policies), а затем нажмите кнопку **New** (Создать).

5. С помощью полезных данных **Общие** настройте параметры политики. В их число входят следующие:
   - Триггер: выберите **Регистрация завершена** и **Recurring Check-in** (Повторный возврат).
   - Периодичность выполнения: выберите **Once per computer** (Один раз на компьютере).

6. Выберите полезные данные **пакетов** и нажмите кнопку **Configure** (Настроить).

7. Нажмите кнопку **Add** (Добавить), чтобы выбрать пакет с помощью приложения "Корпоративный портал".

8. В контекстном меню **Action** (Действие) выберите **Install** (Установить).
9. Настройте параметры пакета.

10. Перейдите на вкладку **Scope** (Область), чтобы указать, на каких компьютерах требуется установить приложение "Корпоративный портал". Нажмите кнопку **Сохранить**. Политика запустит заданные в области устройства при следующей активации выбранного триггера на компьютере и установке параметров, указанных в **универсальных** полезных данных.

## <a name="create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory"></a>Создание политики в Jamf Pro для регистрации устройств пользователей в Azure Active Directory  

После [развертывания Корпоративного портала](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) для macOS с помощью Jamf Pro Self Service можно создать политику Jamf Pro, которая регистрирует устройство пользователя в Azure AD. 

Для регистрации устройства пользователю устройства необходимо вручную выбрать приложение Корпоративного портала Intune в Jamf Self Service. Мы рекомендуем вам [отправить пользователям](../fundamentals/end-user-educate.md) сообщения по электронной почте, оповещения Jamf Pro или воспользоваться любым другим способом, который ваша организация использует для выполнения этого действия, чтобы зарегистрировать устройства. 

> [!WARNING]
> При запуске приложения "Корпоративный портал" вручную (например, из папки Applications или Downloads) процесс регистрации будет невозможен. Если пользователь устройства запустит Корпоративный портал вручную, он увидит предупреждение **AccountNotOnboarded**.

### <a name="to-create-the-registration-policy"></a>Создание политики регистрации  

1. В Jamf Pro выберите **Computers** (Компьютеры) > **Policies** (Политики), а затем создайте политику регистрации устройств.

2. Настройте полезные данные **Microsoft Intune Integration**, в том числе триггер и периодичность выполнения.

3. Перейдите на вкладку **Scope** (Область) и привяжите к политике все целевые устройства.

4. Перейдите на вкладку **Self Service** (Самообслуживание), чтобы предоставить доступ к политике на портале самообслуживания Jamf. Включите политику в категорию **Соответствие устройства политике**. Нажмите кнопку **Сохранить**.

## <a name="validate-intune-and-jamf-integration"></a>Проверка интеграции Intune и Jamf  

Используйте консоль Jamf Pro, чтобы убедиться в успешном взаимодействии между Jamf Pro и Microsoft Intune. 

- В Jamf Pro последовательно выберите **Settings** (Параметры) > **Global Management** (Глобальное управление) > **Microsoft Intune Integration** (Интеграция Microsoft Intune), а затем нажмите кнопку **Test** (Тестировать).

    В консоли отобразится сообщение об успешном или неудачном подключении.  

Если проверка подключения из консоли Jamf Pro завершится сбоем, проверьте конфигурацию Jamf. 


## <a name="removing-a-jamf-managed-device-from-intune"></a>Удаление устройства под управлением Jamf из Intune

Чтобы удалить устройство, управляемое Jamf, откройте Центр администрирования Microsoft Endpoint Manager и выберите **Устройства** > **Все устройства**, затем выберите устройство и нажмите **Удалить**.  Чтобы выполнить массовое удаление устройств, выберите несколько устройств и нажмите **Удалить**.

Сведения об [удалении устройства под управлением Jamf см. в документации Jamf Pro](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). Чтобы получить дополнительную помощь, можно также отправить запрос в [службу поддержки Jamf](https://www.jamf.com/support/). 

## <a name="next-steps"></a>Дальнейшие шаги

- [Условный доступ в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [Начало работы с условным доступом в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)