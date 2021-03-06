---
title: Удаленно выполняемые действия с использованием совместного управления
titleSuffix: Configuration Manager
description: Запуск удаленно выполняемых действий из Intune для совместно управляемых устройств
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075325"
---
# <a name="remote-actions-with-co-management"></a>Удаленно выполняемые действия с использованием совместного управления

Для вас важно, чтобы все управляемые устройства были всегда доступны, независимо от места и времени их подключения к сети. Также вам нужно предоставить каждому пользователю все необходимое для продуктивной работы и обеспечить защиту приложений и данных. Поддержка действий на устройствах в Intune позволяет удаленно выполнять эти критически важные функции.

В следующем видео руководитель программы Хайди Чен (Heidi Cheng) и старший менеджер программы Дэнни Гиллори (Danny Guillory) обсуждают и демонстрируют применение удаленных действий с совместным управлением:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Преимущества

Удаленно выполняемые действия с устройством позволяют управлять устройствами, не затрагивая персональные данные. Эти удаленно выполняемые действия с устройством позволяют: 
- удалять данные компании на утерянных или украденных устройствах;  
- переименовывать устройство;  
- перезапускать устройство;  
- проверять список устройств;  
- удаленно управлять устройством;  
- удалять предварительно установленные OEM-приложения с перезагрузкой "новый запуск";  
- выполнять сброс до заводских установок для любого устройства Windows 10.  

Эти функции предоставляют простые и важные методы для защиты корпоративных данных, хранящихся на устройствах, в том числе в электронной почте или на OneDrive.

Дополнительные сведения об этих действиях вы найдете в разделе [Доступные удаленные действия](#available-remote-actions). 



## <a name="case-studies"></a>Практические примеры

Глобальная консалтинговая фирма Avanade регулярно использует удаленные действия для управления устройствами, которые используются 30 000 сотрудниками. В недавней [записи блога](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/) директор Avanade по информационным технологиям отметил следующее:

> *Первым преимуществом от применения функций Intune стала возможность удаленно сбрасывать настройки Windows на компьютерах. Это важно в случае утери или кражи компьютеров, что случается нередко из-за высокой мобильности наших сотрудников.* 
> *Без этого нам пришлось бы реализовывать и поддерживать эту функциональную возможность в отдельном пользовательском пакете Configuration Manager.*

Дополнительные сведения об использовании этих удаленных действий вы найдете в разделе [Доступные удаленные действия](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Ценность предложения

Если для устройства Configuration Manager применяется совместное управление, сразу же становятся доступными все функции, которые не предоставляются в стандартной конфигурации Configuration Manager. Теперь вы сможете выполнять любое удаленное действие, которое поддерживается Intune. 

В сочетании с совместным управлением для устройств Configuration Manager будут доступны все функции обычных устройств под управлением Intune. Например, полный набор облачных функций и возможность доступа в любой момент, когда устройство имеет доступ к Интернету. Все эти действия можно выполнить без дополнительных сложностей, только включив совместное управление.

Так как процесс автоматической регистрации проходит незаметно для пользователя, он никак не влияет на продуктивность работы. Пользователю не нужно выполнять никаких действий.


### <a name="available-remote-actions"></a>Доступные удаленные действия

Вы можете выполнять из Intune следующие удаленные действия, [включив совместное управление](how-to-enable.md) в Configuration Manager.

#### <a name="remove-devices"></a>Удаление устройств
- **Прекратить использование**. Это действие удаляет управляемые приложения и их данные (если применимо), параметры и профили электронной почты, которые были назначены устройству. После этого устройство удаляется из системы управления Intune. Этот процесс будет выполнен в следующий раз, когда устройство проверит изменения и получит удаленное действие "Прекратить использование". Функция "Прекратить использование" не затрагивает персональные данные пользователя на устройстве.  

- **Очистка**. Это действие восстанавливает на устройстве заводские настройки. Если вы установите флажок **Сохранить состояние регистрации и учетную запись пользователя**, данные пользователя сохранятся на устройстве. В противном случае выполняется надежная очистка диска.  

- **Удалить**: Если вы намерены удалить устройства из Intune при помощи портала Azure, удалите их на соответствующей панели устройств. При следующей проверке изменений для устройства с него удаляются все сохраненные корпоративные данные.  

Дополнительные сведения см. в статье [Удаление устройств с помощью очистки, прекращения использования или ручной отмены регистрации устройства](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Выборочная очистка
<!--SCCMDocs issue 973-->
Если вы выберете вариант **Выборочная очистка приложений**, будут удалены только данные корпоративных приложений, но не персональные данные. Это действие полезно в тех случаях, когда устройство заявлено как потерянное или украденное. 

Дополнительные сведения см. в статье [Очистка только корпоративных данных в приложениях, управляемых с помощью Intune](../../intune/apps/apps-selective-wipe.md.

#### <a name="sync"></a>Синхронизация
Действие **Синхронизация** приводит к немедленной проверке изменений в Intune для выбранного устройства. При проверке изменений устройство получает все ожидающие действия или политики, которые вы ему назначили.

Эта функция позволяет сразу проверить назначенные политики и устранить возникшие с ними неполадки, не дожидаясь следующей плановой проверки изменений.

Дополнительные сведения см. в статье [Синхронизация устройств с Intune для получения последних политик и действий](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Перезапуск
Действие **Перезапуск** приводит к перезапуску выбранного устройства. Это полезно в тех случаях, когда требуется перезагрузка, но пользователь не может ее выполнить.

Дополнительные сведения см. в статье [Удаленный перезапуск устройств с помощью Intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Чистый запуск
Действие **Новый запуск** удаляет все приложения, установленные на устройстве под управлением Windows 10 версии 1703 или более поздней версии. Функция "Новый запуск" позволяет удалить все предварительно установленные OEM-приложения, которые обычно устанавливаются на новом устройстве.

Если вы не намерены сохранять данные пользователя, устройство восстанавливается до того состояния, в котором поступает от производителя. Также отменяется его регистрация в Azure AD и MDM.

Если вы предварительно задали стандарты, определяющие список приложений на устройстве, это действие удаляет все остальные приложения, то есть не соответствующие заданным критериям.

Дополнительные сведения см. в статье [Сброс устройств с Windows 10 с помощью функции нового запуска в Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Удаленное управление
Устройства под управлением Intune можно удаленно администрировать с помощью [TeamViewer](https://www.teamviewer.com/). TeamViewer — это программа стороннего производителя, которую нужно приобретать отдельно.

Дополнительные сведения см. в статье [Используйте TeamViewer для удаленного администрирования устройств Intune](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Настройка

Кроме удаленного управления с помощью TeamViewer, вам не потребуются дополнительные настройки для выполнения удаленных действий с устройством в Intune, после того как вы [включите совместное управление](how-to-enable.md).

Дополнительные сведения об использовании TeamViewer для удаленного управления устройствами в Intune см. в [этой статье](../../intune/remote-actions/teamviewer-support.md).
