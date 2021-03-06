---
title: Регистрация устройства iOS в службе управления затратами на телекоммуникации с помощью Intune
description: Узнайте, как зарегистрировать устройство iOS в службе управления затратами на телекоммуникации.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/19/2017
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 6d8c6372-f2ce-4558-8886-1d7c1966699c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: sumitp
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: aeb1f6ae1ca666a96eca583d2e3be9c565013e7c
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83881314"
---
# <a name="enroll-your-ios-device-in-telecom-expense-management"></a>Регистрация устройства iOS в службе управления затратами на телекоммуникации

В организации может использоваться программное обеспечение для управления затратами на телекоммуникации, чтобы гарантировать, что тарифный и разговорный планы используются в допустимых пределах. После завершения регистрации устройства будет предложено выбрать для него наиболее подходящую категорию.

  ![Снимок экрана "Выбор наиболее подходящей категории для устройства" на устройстве iOS. На нем отображаются варианты корпоративной или персональной регистрации.](./media/ios-enroll-10-tem-select-best-category.png)

Выберите подходящий вариант, и вы получите уведомление для установки приложения [__Datalert__](https://itunes.apple.com/app/datalert/id771029268?mt=8) из Магазина приложений. С помощью приложения Datalert специалисты организации могут оценить использование данных. Если в вашей организации есть возможность регистрации с помощью рабочей или учебной учетной записи, вам потребуется войти в соответствующую учетную запись. Если учетная запись еще не включена, укажите свой номер телефона и проверьте свое устройство с помощью кода для регистрации в службе Datalert из приложения.

  ![Снимок экрана приветствия приложения Datalert с предложением перейти к следующему экрану, ознакомившись с краткими сведениями о том, как эффективнее использовать тарифный план с помощью Datalert.](./media/ios-enroll-11-tem-datalert-setup.png)

## <a name="enroll-into-datalert-using-your-microsoft-work-or-school-account"></a>Регистрация в Datalert с помощью рабочей или учебной учетной записи Майкрософт

> [!NOTE]
> Чтобы зарегистрировать устройство таким образом, установите и активируйте на своем телефоне приложение [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to).

1. Выберите __Enroll with Microsoft account__ (Регистрация с помощью учетной записи Майкрософт).

   ![Изображение экрана настроек приложения Datalert, на котором предлагается ввести номер телефона и выбрать регистрацию с помощью учетной записи Майкрософт, если у вас есть учетная запись Microsoft Office 365 и подписка Intune.](./media/ios-enroll-11a-tem-datalert-enroll-msft-account.png)

2. Вы получите уведомление __"Datalert" wants to open "Authenticator"__ (Приложение Datalert хочет открыть Authenticator). Выберите __Open__ (Открыть).

   ![Изображение всплывающего окна, которое предлагает пользователю открыть приложение Authenticator по запросу приложения Datalert.](./media/ios-enroll-11b-tem-datalert-open-authenticator.png)

3. Войдите с помощью своей __рабочей или учебной учетной записи Майкрософт__. Установка Datalert займет некоторое время. Выберите __Finish__ (Готово), когда установка завершится.

## <a name="enroll-into-datalert-using-your-phone-number"></a>Регистрация в Datalert с помощью номера телефона

1. Укажите номер телефона устройства.

   ![Снимок экрана с запросом номера телефона приложением Datalert.](./media/ios-enroll-12-tem-datalert-phone-number.png)

2. Затем вы получите SMS-сообщение с кодом проверки. Введите код и коснитесь __ОК__.

   ![Снимок экрана с запросом кода проверки в SMS приложением Datalert.](./media/ios-enroll-13-tem-datalert-sms.png)

3. После ввода кода проверки установка Datalert будет завершена. Коснитесь __Готово__. После этого вы сможете отслеживать данные в приложении Datalert.

   ![Снимок экрана приложения Datalert с мониторингом использования данных за сегодня.](./media/ios-enroll-14-tem-datalert-monitoring-active.png)

После регистрации сведения об использовании данных начнут появляться в приложении Datalert.

По-прежнему нужна помощь? Обратитесь в службу поддержки вашей компании. Его контактные данные доступны на [веб-сайте корпоративного портала](https://go.microsoft.com/fwlink/?linkid=2010980).
