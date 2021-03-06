---
title: Какие сведения доступны моей организации после регистрации устройства?
description: Поясняет, какие сведения доступны и недоступны ИТ-администратору на управляемом устройстве.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/31/2019
ms.topic: article
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: 12655728-a1af-4d89-97bc-925fe36c0dc4
searchScope:
- User help
ROBOTS: ''
ms.reviewer: esmich
ms.suite: ems
ms.collection: ''
ms.openlocfilehash: ed3f9f6f01c8dc2df3a89daee991d9f8c61056b9
ms.sourcegitcommit: f94cdca69981627d6a3471b04ac6f0f5ee8f554f
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "82210321"
---
# <a name="what-information-can-my-organization-see-when-i-enroll-my-device"></a>Какие сведения становятся доступными для моей организации при регистрации устройства?

Ваша организация не может просматривать ваши персональные данные, когда вы регистрируете устройство в Microsoft Intune. При регистрации устройства вы предоставляете своей организации разрешение на просмотр определенных фрагментов информации на этом устройстве, например модели и серийного номера. Ваша организация использует эти сведения для защиты корпоративных данных на устройстве.

**Данные, недоступные вашей организации**

- Журнал вызовов и журнал браузера
- Почтовые сообщения и SMS
- "Контакты"
- "Календарь"
- Пароли
- Рисунки, включая фотографии и галерею камеры
- Файлы

**Данные, доступные вашей организации**

- Модель устройства, например Google Pixel
- Изготовитель устройства, например корпорация Майкрософт
- Название и версия операционной системы, например iOS 12.0.1
- Перечень и названия приложений, например Microsoft Word. На личных устройствах для организации доступен только перечень управляемых приложений. На корпоративных устройствах организации доступен перечень всех приложений.
- Владелец устройства.
- Имя устройства
- Серийный номер устройства
- IMEI

 > [!NOTE]
 > Для полностью управляемых и выделенных устройств с Android для бизнеса не будет отображаться список всех приложений.    
    
**Данные, которые могут быть доступны вашей организации**

- Номер телефона. Если это корпоративное устройство, может быть доступен полный номер телефона. Если же это личное устройство, организации доступны только последние четыре цифры номера телефона. Вы можете узнать тип владения для каждого отдельного устройства, открыв страницу **Сведения об устройстве**.
- Доступное место на устройстве. Если вам не удается установить требуемое приложение, организация может просмотреть сведения о доступном пространстве на устройстве, чтобы узнать, достаточно ли на нем места.  
- Расположение: Организации недоступны данные о расположении устройств. Исключение составляют защищенные устройства iOS, которые были утеряны. Дополнительные сведения о защищенных устройствах см. в [документации по Apple iOS](https://go.microsoft.com/fwlink/?linkid=853816).  
- Перечень сведений о приложениях. Если в организации используется решение Mobile Threat Defense, то ей будут доступны дополнительные сведения о приложениях, имеющихся на вашем устройстве iOS. Дополнительные сведения о [Mobile Threat Defense](set-up-mobile-threat-defense.md). На личных устройствах для организации доступен только перечень управляемых приложений. На корпоративных устройствах организации доступен перечень всех приложений.
- Сведения о сети. Сведения о сетевых подключениях для устройств Android могут быть доступны для службы поддержки вашей организации. Например, если организации требуется, чтобы устройства оставались в пределах определенного здания, устройство идентифицирует сеть, к которой оно подключено. 
