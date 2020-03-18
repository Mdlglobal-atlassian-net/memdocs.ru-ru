---
title: Удаленное администрирование устройств в Microsoft Intune —Azure | Документы Майкрософт
description: Просмотрите необходимые роли для использования TeamViewer, рекомендации по установке соединителя TeamViewer и пошаговые инструкции для удаленного администрирования устройств с помощью Microsoft Intune на портале Azure
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 72cdd888-efca-46e6-b2e7-fb9696bb2fba
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b63dbf983872dbbb1c792e1f5d00bb136da973a1
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79348852"
---
# <a name="use-teamviewer-to-remotely-administer-intune-devices"></a>Используйте TeamViewer для удаленного администрирования устройств Intune

Устройства, управляемые Intune, можно администрировать удаленно с помощью [TeamViewer](https://www.teamviewer.com). TeamViewer — это программа стороннего производителя, которая приобретается отдельно. В этом разделе описано, как настроить TeamViewer в Intune и удаленно управлять устройством. 

## <a name="prerequisites"></a>Предварительные условия

- Необходимо поддерживаемое устройство. Профиль администратора устройства Android, рабочий профиль устройства Android, а также устройства Windows, iOS, iPadOS и macOS, управляемые с помощью Intune, поддерживают удаленное администрирование. TeamViewer может не поддерживать Windows Holographic (HoloLens), Windows Team (Surface Hub) или Windows 10 S. Актуальный список поддерживаемых устройств см. в разделе [TeamViewer](https://www.teamviewer.com).

> [!NOTE]
> Выделенные и полностью управляемые устройства Android не поддерживаются.

- Администратор Intune на портале Azure должен иметь следующие [роли Intune](../fundamentals/role-based-access-control.md):  

  - **Обновить удаленную помощь**: позволяет администраторам изменять параметры соединителя TeamViewer
  - **Запросить удаленную помощь**: позволяет администраторам начать новый сеанс удаленной помощи для любого пользователя. Пользователи с этой ролью не ограничиваются ролями Intune в пределах области. Кроме того, группы пользователей или устройств с ролью Intune в пределах области могут также запросить удаленную помощь. 

- Учетная запись [TeamViewer](https://www.teamviewer.com) с учетными данными для входа. Только некоторые лицензии TeamViewer поддерживают интеграцию с Intune. Конкретные потребности TeamViewer см. в разделе [Партнер по интеграции TeamViewer: Microsoft Intune](https://www.teamviewer.com/integrations/microsoft-intune/).

Используя TeamViewer, вы можете использовать соединитель TeamViewer для Intune для создания сеансов TeamViewer, чтения данных Active Directory и сохранения токена доступа к учетной записи TeamViewer.

## <a name="configure-the-teamviewer-connector"></a>Настройка соединителя TeamViewer

Чтобы предоставить удаленную поддержку для устройств, настройте соединитель TeamViewer для Intune, выполнив следующие действия:

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Администрирование клиента** > **Соединители и токены** > **Соединитель TeamViewer**.
3. Нажмите **Подключить** и примите условия лицензионного соглашения.
4. Нажмите **Войти в TeamViewer для авторизации**.
5. Откроется веб-страница сайта TeamViewer. Введите учетные данные лицензии TeamViewer и нажмите кнопку **Войти**.

## <a name="remotely-administer-a-device"></a>Удаленное администрирование устройства

После настройки соединителя вы можете удаленно управлять устройством. Выполните следующие шаги. 

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства**, а затем — **Все устройства**.
3. В списке выберите устройство для удаленного администрирования > **...**  > **Новый сеанс удаленного помощника**.
4. После того как Intune подключится к службе TeamViewer, появятся определенные сведения об устройстве. Выберите **Подключить**, чтобы начать удаленный сеанс.

![Удаленное администрирование устройства Android с помощью TeamViewer — пример](./media/teamviewer-support/android-teamviewer.png)

Когда вы запускаете удаленный сеанс, пользователь видит флажок уведомления на значке приложения "Корпоративный портал" на своем устройстве. Также уведомление отображается при открытии приложения. При необходимости пользователь может принять запрос удаленной помощи.

> [!NOTE]
> Устройства с ОС Windows, которые регистрируются без участия пользователей, например с помощью DEM и WCD, не отображают уведомление TeamViewer в приложении "Корпоративный портал". В этих случаях рекомендуется создать сеанс на портале TeamViewer.

В TeamViewer можно выполнить ряд действий на устройстве, включая возможность управления устройством. Подробные сведения о доступных возможностях см. в [Руководстве по TeamViewer](https://www.teamviewer.com/support/documents/).

После завершения сеанса закройте окно TeamViewer.