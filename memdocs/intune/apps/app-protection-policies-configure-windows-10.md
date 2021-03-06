---
title: Настройка политик защиты приложений для Windows 10
titleSuffix: Microsoft Intune
description: В этом разделе описывается настройка политик защиты приложений (APP) для устройств с Windows 10.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 949fddec-5318-4c9a-957e-ea260e6e05be
ms.reviewer: joglocke
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 83eccdddd1cc38f72c949c80c4a1488b09920f94
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988705"
---
# <a name="get-ready-for-windows-information-protection-in-windows-10"></a>Подготовка к Windows Information Protection в Windows 10 

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Включите управление мобильными приложениями (MAM) для Windows 10, указав поставщик MAM в Azure AD. После этого можно определять состояние регистрации при создании новой политики Windows Information Protection (WIP) с помощью Intune. Есть два состояния регистрации — MAM и управление мобильными устройствами (MDM).

## <a name="to-configure-the-mam-provider"></a>Настройка поставщика MAM

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Все службы**, а затем **M365 Azure Active Directory**, чтобы переключить панели мониторинга.
3. Выберите **Azure Active Directory**.
4. Выберите **Мобильность (MDM и MAM)** в группе **Управление**.
5. Выберите **Microsoft Intune**.
6. Настройте параметры в группе **Восстановить URL-адреса MAM по умолчанию** на панели **Настройка**.

   **Область пользователя MAM**  
   Используйте автоматическую регистрацию MAM для управления корпоративными данными на устройствах Windows сотрудников вашей компании. Автоматическая регистрация MAM будет настроена для сценариев с использованием собственного устройства.<ul><li>**Нет**<br>Укажите, если никто из пользователей не может зарегистрироваться в MAM.</li><li>**Некоторые**<br>Выберите группы Azure AD, которые содержат пользователей для регистрации в MAM.</li><li>**Все**<br>Укажите, могут ли все пользователи зарегистрироваться в MAM.</li></ul>

   **URL-адрес условий использования MAM**  
   URL-адрес условий использования MAM не поддерживается в Microsoft Intune. Для применения политик защиты это поле ввода следует оставить пустым.

   **URL-адрес обнаружения MAM**  
   URL-адрес конечной точки регистрации службы MAM. Конечная точка регистрации используется для регистрации устройств для управления с помощью службы MAM.

   **URL-адрес соответствия требованиям MAM**  
   URL-адрес соответствия требованиям MAM не поддерживается в Microsoft Intune. Для применения политик защиты это поле ввода следует оставить пустым. 

7. Нажмите кнопку **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия

[Создание политики WIP](windows-information-protection-policy-create.md)
