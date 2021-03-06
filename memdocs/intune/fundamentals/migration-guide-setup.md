---
title: Базовая настройка Microsoft Intune
description: В этой статье описаны необходимые действия по настройке Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b7784d4ad86e3418259f85ca1c4577d2289dc86
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79358160"
---
# <a name="basic-setup"></a>Базовая настройка

После оценки среды можно переходить к установке Microsoft Intune.

## <a name="external-dependencies-for-an-intune-deployment"></a>Внешние зависимости развертывания Intune

### <a name="identity"></a>Удостоверение

Intune требуется Azure Active Directory (AAD) в качестве поставщика групп идентификаторов и пользователей. Дополнительные сведения

- [Требования к удостоверениям](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Требования к синхронизации каталогов](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [Многофакторная идентификация (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks)

- [Планирование групп пользователей и устройств](users-add.md)

- [Создание групп пользователей и устройств](groups-get-started.md)

Если ваша организация уже работает с Office 365, в Intune необходимо использовать ту же среду Azure Active Directory.

### <a name="pki-optional"></a>PKI (необязательно)

Если вы планируете использовать проверку подлинности на основе сертификатов с профилями VPN, Wi-Fi или электронной почты в Intune, следует убедиться в наличии поддерживаемой [инфраструктуры открытых ключей](../protect/certificates-configure.md), готовой к созданию и развертыванию профилей сертификатов. Дополнительные сведения о настройке сертификатов в Intune:

- [Настройка инфраструктуры сертификатов для SCEP](/intune/certificates-scep-configure).

- [Настройка инфраструктуры сертификатов для PFX](/intune/certficates-pfx-configure).

## <a name="task-list-for-an-intune-setup"></a>Список задач для настройки Intune

### <a name="task-1-intune-subscription"></a>Задача 1. Подписка Intune

Перед миграцией в Intune потребуется [подписка Intune](account-sign-up.md).

### <a name="task-2-assign-intune-user-licenses"></a>Задача 2. Назначение лицензий пользователя Intune

- Узнайте, как можно [назначить лицензии пользователя Intune](licenses-assign.md).

- Узнайте, как можно [создать пользователей или синхронизировать пользователя из локальной службы Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) (при создании клиента Azure Active Directory).

### <a name="task-3-set-your-mdm-authority-to-intune"></a>Задача 3. Установка Intune в качестве центра MDM

Для управления Intune рекомендуем использовать [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).

Укажите **Intune** в качестве центра MDM. При использовании другого центра MDM служба Intune может передать управление MDM альтернативной консоли управления Майкрософт. Но это случается редко.

> [!IMPORTANT]
> Если вы передаете управление мобильными устройствами службе Intune впервые, ее следует задать в качестве центра управления мобильными устройствами.

Узнайте, как [установить центр управления мобильными устройствами](mdm-authority-set.md).

## <a name="next-step"></a>Дальнейшие действия

[Настройка политик управления устройствами и приложениями](migration-guide-configure-policies.md).
