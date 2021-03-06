---
title: Профили OneDrive для бизнеса
titleSuffix: Configuration Manager
description: Перенаправляйте известные папки Windows в OneDrive для бизнеса с помощью профиля OneDrive для бизнеса в Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 47d44c96e0ae63504278c58a5838c54648665505
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692312"
---
# <a name="onedrive-for-business-profiles"></a>Профили OneDrive для бизнеса

Начиная с Configuration Manager версии 1902 можно создавать профили OneDrive для бизнеса для перемещения известных папок Windows в OneDrive для бизнеса. К этим папкам относятся "Рабочий стол", "Документы" и "Изображения". В каждом профиле можно указать параметры для перемещения известных папок Windows. См. дополнительные сведения о OneDrive для бизнеса в статье [Redirect and move Windows known folders to OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders) (Перенаправление и перенос известных папок Windows в OneDrive). <!--3556021-->

## <a name="prerequisites"></a>Предварительные условия

- [Найдите свой идентификатор клиента Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Разверните версию клиента синхронизации OneDrive 18.111.0603.0004 или более позднюю. Дополнительные сведения см. в разделе [Развертывание приложений OneDrive с помощью Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> Перемещение известных папок Windows в OneDrive
<!--3556021-->
С помощью Configuration Manager можно переместить известные папки Windows в OneDrive для бизнеса. К этим папкам относятся "Рабочий стол", "Документы" и "Изображения". Чтобы упростить обновление до Windows 10, разверните эти параметры для клиентов с Windows 7, прежде чем развертывать последовательность задач. 

1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**, разверните узел **Параметры соответствия**, а затем выберите узел **Профили OneDrive для бизнеса**.  

   ![Узел профилей OneDrive для бизнеса](media/onedrive-for-business-profiles-node.png)
2. В ленте выберите **Создать профиль OneDrive для бизнеса**.  

3. Укажите имя для этой политики и нажмите кнопку **Далее**.  

4. Выберите платформы, которые будут подготовлены с помощью профиля OneDrive для бизнеса. Когда вы выберете платформы, нажмите кнопку **Далее**.

    ![Выбор платформ для профиля OneDrive для бизнеса](media/onedrive-for-business-profile-select-platforms.png) 

5. На странице **Параметры**:

    1. Укажите идентификатор клиента Office 365.  

    2. Выберите один из следующих параметров, чтобы переместить указанные папки в OneDrive:  

        - **Запрашивать у пользователей перемещение известных папок Windows в OneDrive** — этот параметр позволяет открыть для пользователя мастер для перемещения файлов. Если вы решите отложить или отклонить перемещение папок, из OneDrive будет периодически поступать напоминание.  

        - **Автоматически перемещать известные папки Windows в OneDrive** — если к устройству применяется эта политика, клиент OneDrive автоматически перенаправляет известные папки в OneDrive для бизнеса.  

            - **Показывать пользователям уведомление после перенаправления папок** — если этот параметр включен, клиент OneDrive уведомляет пользователя после перемещения папки.  

    3. **Запретить пользователям перенаправлять их известные папки Windows обратно на ПК** — отключает параметр в OneDrive для бизнеса в клиенте, позволяющий пользователям перемещать эти папки обратно на устройство.  

       ![Параметры перемещения известных папок в OneDrive для бизнеса](media/onedrive-for-business-profile-move-folder-settings.png)

6. Закройте мастер и разверните политику.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Развертывание профиля OneDrive для бизнеса

1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**, разверните узел **Параметры соответствия**, а затем выберите узел **Профили OneDrive для бизнеса**.  


2. Выберите профиль, а затем выберите **Развернуть** на ленте.

3. Укажите следующие параметры для развертывания:

   1. **Коллекция** — щелкните **Обзор...** и выберите коллекцию, для которой необходимо развернуть профиль.  
   1. **Создавать оповещение**.

      - **Когда соответствие ниже:**  — минимальный допустимый процент соответствия клиентов. Если фактический показатель ниже этого значения, создается оповещение.
      -  **Дата и время** — дата, когда впервые начали создаваться оповещения, касающиеся соответствия профиля.
      - **Создать оповещение System Center Operations Manager** — отправка оповещения, касающегося соответствия, в System Center Operations Manager.
   1. **Расписание**.

      - **Простое расписание** — по умолчанию этот параметр использует простое расписание с запуском оценки соответствия каждые семь дней.
      - **Настраиваемое расписание** — определяет, когда запускается оценка соответствия. Время запуска указывается с помощью локального времени компьютера, на котором выполняется консоль Configuration Manager, на момент создания расписания. Или же вы можете использовать UTC.
 
      ![Развертывание профиля OneDrive для бизнеса](media/onedrive-for-business-deploy-profile.png)

4. Щелкните **ОК**, чтобы развернуть профиль OneDrive для бизнеса.


## <a name="next-steps"></a>Дальнейшие действия

[Создание профилей удаленного подключения](create-remote-connection-profiles.md)
