---
title: Ошибки и коды состояний в Microsoft Intune в Azure | Документация Майкрософт
description: Здесь приводится список ошибок, кодов состояний, их описания и способы их устранения при использовании управляемых MDM устройств, получении доступа к ресурсам организации, ошибках на устройствах с iOS/iPadOS и ошибках в ответах OMA в Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 40622ced-6029-4abf-873e-b51d2b51934c
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91a0f717a8ed3d5574b731fe2f20a40c5494a160
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79355781"
---
# <a name="common-error-codes-and-descriptions-in-microsoft-intune"></a>Коды распространенных ошибок в Microsoft Intune и их описания

В этой статье перечислены распространенные ошибки, коды состояний, описания и возможные решения при доступе к ресурсам организации. Эти сведения можно использовать для устранения проблем доступа при использовании Microsoft Intune.

Если требуется поддержка, см. раздел [Получение поддержки для Microsoft Intune](get-support.md).

## <a name="status-codes-for-mdm-managed-windows-devices"></a>Коды состояния для устройств Windows, управляемых с помощью функции MDM

|Код состояния|Сообщение об ошибке|Предпринимаемые действия|
|---------------|-----------------|--------------|
|10 (APP_CI_ENFORCEMENT_IN_PROGRESS)|Идет установка||
|20 (APP_CI_ENFORCEMENT_IN_PROGRESS_WAITING_CONTENT)|Ожидание содержимого||
|30 (APP_CI_ENFORCEMENT_ERROR_RETRIEVING_CONTENT)|Получение содержимого|Возможная причина: состояние задания 30 указывает на сбой скачивания приложения пользователем.<br /><br />Наиболее вероятные причины:<br /><br />Устройство потеряло подключение к Интернету во время скачивания.<br /><br />Истек срок действия сертификата, выданного для устройства во время регистрации.<br /><br />Устранение:<br /><br />Запустите приложение "Приложения организации" на панели управления устройства, чтобы убедиться, что срок действия сертификата устройства еще не истек; если он истек, потребуется повторно зарегистрировать устройство.<br /><br />Убедитесь, что устройство подключено к Интернету, и попробуйте снова запросить приложение.|
|40 (APP_CI_ENFORCEMENT_IN_PROGRESS_CONTENT_DOWNLOADED)|Скачивание содержимого завершено||
|50 (APP_CI_ENFORCEMENT_IN_PROGRESS_INSTALLING)|Идет установка||
|60 (APP_CI_ENFORCEMENT_ERROR_INSTALLING)|Произошла ошибка установки|Не удалось установить приложение после скачивания.<br /><br />На устройстве отсутствует сертификат подписи кода, с помощью которого было подписано приложение.<br /><br />На устройстве не найдена установленная зависимость от платформы, от которой зависит приложение.<br /><br />Убедитесь, что на устройстве присутствует сертификат подписи кода, с помощью которого было подписано приложение, и получите подтверждение администратора, что такой сертификат был нацелен на все устройства Windows RT, зарегистрированных на предприятии.<br /><br />В случае сбоя установки из-за отсутствующей зависимости от платформы администратор должен повторно опубликовать приложение, упаковав платформу вместе с пакетом приложения.<br /><br />Скачанный пакет приложения не является допустимым, поврежден или несовместим с версией ОС на данном устройстве.|
|70 (APP_CI_ENFORCEMENT_SUCCEEDED)|Установка выполнена успешно||
|80 (APP_CI_ENFORCEMENT_IN_PROGRESS)|Выполняется удаление||
|90 (APP_CI_ENFORCEMENT_ERROR)|Произошла ошибка удаления||
|100 (APP_CI_ENFORCEMENT_SUCCEEDED)|Удаление выполнено успешно||
|110 (APP_CI_ENFORCEMENT_ERROR)|Несоответствие хэша содержимого||
|120 (APP_CI_ENFORCEMENT_ERROR)|SLK/загрузка неопубликованных приложений не включена||
|130 (APP_CI_ENFORCEMENT_ERROR)|Не удалось установить лицензию MSADP||
|Нет состояния (APP_CI_ENFORCEMENT_UNKNOWN)|н/д|В настоящее время состояние неизвестно.|

## <a name="company-resource-access-common-errors"></a>Доступ к ресурсам компании (распространенные ошибки)

|Код состояния|Шестнадцатеричный код ошибки|Сообщение об ошибке|
|---------------|--------------------------|-----------------|
|-2016281101|0x87D1FDF3|Запрос MDM CRP не найден|
|-2016281102|0x87D1FDF2|URL-адрес NDES не найден|
|-2016281103|0x87D1FDF1|Сведения о сертификате MDM CRP не найдены|
|-2016281104|0x87D1FDF0|Сведения о сертификате MDM CI не найдены|
|-2016281105|0x87D1FDEF|Не удалось проверить правило|
|-2016281106|0x87D1FDEE|Неприменимо, поскольку пропущено во время разрешения конфликта|
|-2016281107|0x87D1FDED|Источник обнаружения параметров не поддерживается|
|-2016281108|0x87D1FDEC|В элементе конфигурации не найден параметр, на который указывает ссылка|
|-2016281109|0x87D1FDEB|Не удалось выполнить преобразование типа данных|
|-2016281110|0x87D1FDEA|Недопустимое значение параметра CIM|
|-2016281111|0x87D1FDE9|Не применимо для этого устройства|
|-2016281112|0x87D1FDE8|Сбой исправления|
|-2016330905|0x87D13B67|Состояние приложения неизвестно|
|-2016330906|0x87D13B66|Приложение управляется, но было удалено пользователем|
|-2016330907|0x87D13B65|Устройство активирует код активации|
|-2016330908|0x87D13B64|Сбой установки приложения|
|-2016330909|0x87D13B63|Пользователь отклонил предложение обновить приложение|
|-2016330910|0x87D13B62|Пользователь отклонил предложение установить приложение|
|-2016330911|0x87D13B61|Пользователь установил приложение до установки управляемого приложения|
|-2016330912|0x87D13B60|Установка приложения запланирована, но для завершения транзакции требуется код активации|
|-2016341109|0x87D1138B|Устройство iOS возвращает ошибку|
|-2016341110|0x87D1138A|Устройство iOS отклонило команду из-за неправильного формата|
|-2016341111|0x87D11389|Устройство iOS возвращает непредвиденное состояние «Неактивен»|
|-2016341112|0x87D11388|Устройство iOS в настоящее время занято|

## <a name="errors-returned-by-iosipados-devices"></a>Ошибки, возвращенные устройствами с iOS или iPadOS

### <a name="company-portal-errors"></a>Ошибки на корпоративном портале

|Текст ошибки на корпоративном портале|Код состояния HTTP|Дополнительные сведения об ошибке|
|---|---|---|
|__Внутренняя ошибка сервера__ <br>Похоже, не удалось установить подключение из-за внутренней ошибки сервера. Повторите попытку, а затем обратитесь к ИТ-администратору, если проблема не будет устранена.|Ошибка 500|Эта ошибка, скорее всего, вызвана проблемой в службе Intune. Проблема должна быть решена на стороне службы Intune. Скорее всего, на стороне клиента проблемы нет.|
|__Служба временно недоступна__ <br>Похоже, не удалось установить подключение, так как наша служба временно недоступна. Повторите попытку, а затем обратитесь к ИТ-администратору, если проблема не будет устранена.|Ошибка 503|Это вызвано временной ошибкой службы Intune, например служба находится на обслуживании. Проблема должна быть решена на стороне службы Intune. Скорее всего, на стороне клиента проблемы нет.|
|__Не удается подключиться к серверу__ <br>Похоже, не удалось установить подключение. Повторите попытку, а затем обратитесь к ИТ-администратору, если проблема не будет устранена.|Не настроена связь с кодом состояния HTTP|Не удалось установить безопасное подключение к серверу. Скорее всего, причина проблемы в используемом сертификате SSL. Возможно, причина в том, что конфигурации клиента не соответствуют требованиям Apple к защите транспорта приложения.|
|__Произошла ошибка__ <br>Не удалось загрузить клиент корпоративного портала. Повторите попытку, а затем обратитесь к ИТ-администратору, если проблема не будет устранена.|Ошибка 400|Любая ошибка с кодом состояния HTTP, который начинается на 400. Если нет конкретных сведений, будет отображаться это сообщение. Эта ошибка в приложении "Корпоративный портал" для iOS или iPadOS произошла на стороне клиента.|
|__Сервер недоступен__ <br>Похоже, не удалось установить подключение. Повторите попытку, а затем обратитесь к ИТ-администратору, если проблема не будет устранена.|Ошибка 500|Любая ошибка с кодом состояния HTTP, который начинается на 500. Если нет конкретных сведений, будет отображаться это сообщение. Эта ошибка в службе Intune произошла на стороне службы.|

### <a name="service-errors"></a>Ошибки службы

|Код состояния|Шестнадцатеричный код ошибки|Сообщение об ошибке|
|---------------|--------------------------|-----------------|
|-2016299111|0x87D1B799|Внутренняя ошибка.|
|-2016299112|0x87D1B798|Внутренняя ошибка.|
|-2016300111|0x87D1B3B1|36001:(внутренняя ошибка)|
|-2016300112|0x87D1B3B0|36000: сотовое соединение уже настроено|
|-2016301110|0x87D1AFCA|35002:несколько шрифтов в одной полезной нагрузке|
|-2016301111|0x87D1AFC9|35001:сбой установки шрифтов|
|-2016301112|0x87D1AFC8|35000:недопустимые данные шрифтов|
|-2016302109|0x87D1ABE3|34003:недопустимое имя участника Kerberos|
|-2016302110|0x87D1ABE2|34002:имя участника Kerberos отсутствует|
|-2016302111|0x87D1ABE1|34001:недопустимый шаблон сопоставления URL-адресов|
|-2016302112|0x87D1ABE0|34000:недопустимый шаблон сопоставления идентификаторов приложений|
|-2016304112|0x87D1A410|32000:слишком много приложений|
|-2016305111|0x87D1A029|31001:не удается применить параметры|
|-2016305112|0x87D1A028|31000:не удается применить учетные данные|
|-2016306111|0x87D19C41|30001:время ожидания истекло|
|-2016306112|0x87D19C40|30000:сбой проверки подлинности|
|-2016307109|0x87D1985B|29003:неправильные данные сертификата|
|-2016307110|0x87D1985A|29002:|
|-2016307111|0x87D19859|29001:|
|-2016307112|0x87D19858|29000:устройство не защищено|
|-2016308110|0x87D19472|28002:не удается установить обои|
|-2016308111|0x87D19471|28001:неправильное изображение обоев|
|-2016308112|0x87D19470|28000:неизвестный элемент|
|-2016310111|0x87D18CA1|26001:шифрование на уровне файла не поддерживается|
|-2016310112|0x87D18CA0|26000:шифрование уровня блокировки не поддерживается|
|-2016311110|0x87D188BA|25002:не удается удалить|
|-2016311111|0x87D188B9|25001:не удается установить|
|-2016311112|0x87D188B8|25000:неправильный профиль|
|-2016312109|0x87D184D3|24003:неправильный итоговый профиль|
|-2016312110|0x87D184D2|24002:неправильная полезная нагрузка|
|-2016312111|0x87D184D1|24001:не удается подписать словарь атрибутов|
|-2016312112|0x87D184D0|24000:не удается создать словарь атрибутов|
|-2016313110|0x87D180EA|23002:недопустимый сертификат сервера|
|-2016313111|0x87D180E9|23001:неправильный ответ сервера|
|-2016313112|0x87D180E8|23000:неправильное удостоверение|
|-2016314099|0x87D17D0D|22013:недопустимый ответ на операцию PKI|
|-2016314100|0x87D17D0C|22012:не удается сохранить сертификат ЦС|
|-2016314101|0x87D17D0B|22011:не удается создать CSR|
|-2016314102|0x87D17D0A|22010:не удается сохранить временное удостоверение|
|-2016314103|0x87D17D09|22009:не удается создать временное удостоверение|
|-2016314104|0x87D17D08|22008:не удается создать удостоверение|
|-2016314105|0x87D17D07|22007:недопустимый подписанный сертификат|
|-2016314106|0x87D17D06|22006:недостаточно маркеров ЦС|
|-2016314107|0x87D17D05|22005:сетевая ошибка|
|-2016314108|0x87D17D04|22004:конфигурация сертификата не поддерживается|
|-2016314109|0x87D17D03|22003:недопустимый ответ RA|
|-2016314110|0x87D17D02|22002:недопустимый ответ ЦС|
|-2016314111|0x87D17D01|22001:не удается создать пару ключей|
|-2016314112|0x87D17D00|22000:недопустимое использование ключей|
|-2016315105|0x87D1791F|21007:не удается проверить учетную запись|
|-2016315106|0x87D1791E|21006:не удается расшифровать сертификат|
|-2016315107|0x87D1791D|21005:учетная запись не уникальна (профиль электронной почты уже существует на устройстве)|
|-2016315108|0x87D1791C|21004:не удается создать учетную запись|
|-2016315109|0x87D1791B|21003:отсутствует имя узла|
|-2016315110|0x87D1791A|21002:не удается соответствовать политике шифрования сервера|
|-2016315111|0x87D17919|21001:не удается соответствовать политике сервера|
|-2016315112|0x87D17918|21000:не удается получить политику сервера|
|-2016316110|0x87D17532|20002:учетная запись не является уникальной|
|-2016316111|0x87D17531|20001:отсутствует имя узла|
|-2016316112|0x87D17530|20000:не удается создать учетную запись|
|-2016317110|0x87D1714A|19002:учетная запись не является уникальной|
|-2016317111|0x87D17149|19001:отсутствует имя узла|
|-2016317112|0x87D17148|19000:не удается создать учетную запись|
|-2016318110|0x87D16D62|18002:недопустимые учетные данные|
|-2016318111|0x87D16D61|18001:невозможно достичь узла|
|-2016318112|0x87D16D60|18000:неизвестная ошибка|
|-2016319110|0x87D1697A|17002:учетная запись не является уникальной|
|-2016319111|0x87D16979|17001:отсутствует имя узла|
|-2016319112|0x87D16978|17000:не удается создать учетную запись|
|-2016320110|0x87D16592|16002:учетная запись не является уникальной|
|-2016320111|0x87D16591|16001:отсутствует имя узла|
|-2016320112|0x87D16590|16000:не удается создать подписку|
|-2016321109|0x87D161AB|15003:недопустимый сертификат|
|-2016321110|0x87D161AA|15002:не удается заблокировать конфигурацию сети|
|-2016321111|0x87D161A9|15001:не удается удалить VPN|
|-2016321112|0x87D161A8|15000:не удается установить VPN|
|-2016322110|0x87D15DC2|14002:облачная конфигурация уже существует|
|-2016322111|0x87D15DC1|14001:устройство заблокировано|
|-2016322112|0x87D15DC0|14000:недопустимое поле|
|-2016323107|0x87D159DD|13005:не удается настроить прокси-сервер|
|-2016323108|0x87D159DC|13004:не удается настроить EAP|
|-2016323109|0x87D159DB|13003:не удается создать конфигурацию Wi-Fi|
|-2016323110|0x87D159DA|13002:требуется пароль|
|-2016323111|0x87D159D9|13001:требуется имя пользователя|
|-2016323112|0x87D159D8|13000:не удается установить|
|-2016324070|0x87D1561A|12042:неизвестный код языкового стандарта|
|-2016324071|0x87D15619|12041:неизвестный код языка|
|-2016324072|0x87D15618|12040:необходимо войти в магазин iTunes|
|-2016324073|0x87D15617|12039:(не используется)|
|-2016324074|0x87D15616|12038:приложение не управляется|
|-2016324075|0x87D15615|12037:недопустимый код активации|
|-2016324076|0x87D15614|12036:не удается удалить приложение в текущем состоянии|
|-2016324077|0x87D15613|12035:не удается купить приложение|
|-2016324078|0x87D15612|12034:URL-адрес не является HTTPS|
|-2016324079|0x87D15611|12033:недопустимый манифест|
|-2016324080|0x87D15610|12032:слишком много приложений в манифесте|
|-2016324081|0x87D1560F|12031:установка приложения отключена|
|-2016324082|0x87D1560E|12030:недопустимый URL-адрес|
|-2016324083|0x87D1560D|12029:приложение не управляется|
|-2016324084|0x87D1560C|12028:отсутствует ожидание активации|
|-2016324085|0x87D1560B|12027:не является приложением|
|-2016324086|0x87D1560A|12026:приложение уже поставлено в очередь|
|-2016324087|0x87D15609|12025:приложение уже установлено|
|-2016324088|0x87D15608|12024:не удалось проверить манифест приложения|
|-2016324089|0x87D15607|12023:не удалось проверить ИД приложения|
|-2016324090|0x87D15606|12022:недопустимый раздел|
|-2016324091|0x87D15605|12021:недопустимый тип запроса|
|-2016324092|0x87D15604|12020:не авторизовано сервером|
|-2016324093|0x87D15603|12019:не удается скопировать депонированный секрет|
|-2016324094|0x87D15602|12018:не удается скопировать данные депонированной сумки с ключами|
|-2016324095|0x87D15601|12017:не удается создать депонированную сумку с ключами|
|-2016324096|0x87D15600|12016:отсутствует удостоверение|
|-2016324097|0x87D155FF|12015:не удается получить токен|
|-2016324098|0x87D155FE|12014:подготовка профиля не управляется|
|-2016324099|0x87D155FD|12013:профиль не управляется|
|-2016324100|0x87D155FC|12012:несоответствие замены MDM|
|-2016324101|0x87D155FB|12011:недопустимая конфигурация MDM|
|-2016324102|0x87D155FA|12010:внутренняя ошибка несоответствия|
|-2016324103|0x87D155F9|12009:недопустимый профиль замены|
|-2016324104|0x87D155F8|12008:неправильно оформленный запрос|
|-2016324105|0x87D155F7|12007:не авторизовано|
|-2016324106|0x87D155F6|12006:перенаправление отклонено|
|-2016324107|0x87D155F5|12005:не удается найти сертификат|
|-2016324108|0x87D155F4|12004:недопустимый сертификат push-уведомления|
|-2016324109|0x87D155F3|12003:недопустимый ответ на запрос|
|-2016324110|0x87D155F2|12002:не удается зарегистрироваться|
|-2016324111|0x87D155F1|12001:несколько экземпляров MDM|
|-2016324112|0x87D155F0|12000:недопустимые права доступа|
|-2016325111|0x87D15209|11001:пользовательское имя точки доступа уже установлено|
|-2016325112|0x87D15208|11000:не удается установить имя точки доступа|
|-2016326111|0x87D14E21|10001:недопустимое подписывающее лицо|
|-2016326112|0x87D14E20|10000:не удается установить значения по умолчанию|
|-2016327106|0x87D14A3E|9006:сертификат не является удостоверением|
|-2016327107|0x87D14A3D|9005:сертификат неправильно оформлен|
|-2016327108|0x87D14A3C|9004:не удается сохранить корневой сертификат|
|-2016327109|0x87D14A3B|9003:не удается сохранить данные WAPI|
|-2016327110|0x87D14A3A|9002:не удается сохранить сертификат|
|-2016327111|0x87D14A39|9001:слишком много сертификатов в полезной нагрузке|
|-2016327112|0x87D14A38|9000:недопустимый пароль|
|-2016328112|0x87D14650|8000:не удается установить веб-клип|
|-2016329105|0x87D1426F|7007:учетная запись протокола SMTP неправильно настроена|
|-2016329106|0x87D1426E|7006:учетная запись POP неправильно настроена|
|-2016329107|0x87D1426D|7005:учетная запись IMAP неправильно настроена|
|-2016329108|0x87D1426C|7004:неправильный сертификат SMIME|
|-2016329109|0x87D1426B|7003:сертификат SMIME не найден|
|-2016329110|0x87D1426A|7002:произошла неизвестная ошибка при проверке|
|-2016329111|0x87D14269|7001:недопустимые учетные данные|
|-2016329112|0x87D14268|7000:невозможно достичь узла|
|-2016330110|0x87D13E82|6002:не удается создать запрос|
|-2016330111|0x87D13E81|6001:пустая строка|
|-2016330112|0x87D13E80|6000:системная ошибка цепочки ключей|
|-2016331097|0x87D13AA7|5015:не удается задать период отсрочки|
|-2016331098|0x87D13AA6|5014:не удается задать секретный код|
|-2016331099|0x87D13AA5|5013:не удается очистить секретный код|
|-2016331100|0x87D13AA4|5012:(не используется)|
|-2016331101||5011:неправильный секретный код|
|-2016331102||5010:устройство заблокировано|
|-2016331103|0x87D13AA4|5009:(не используется)|
|-2016331104|0x87D13AA0|5008:секретный код недавно использовался|
|-2016331105|0x87D13A9F|5007:срок действия секретного кода истек|
|-2016331106|0x87D13AA3|5006:для секретного кода требуются текстовые символы|
|-2016331107|0x87D13A9D|5005:для секретного кода требуется число|
|-2016331108|0x87D13A9C|5004:секретный код содержит надстрочные и подстрочные символы|
|-2016331109|0x87D13A9B|5003:секретный код содержит повторяющиеся символы|
|-2016331110|0x87D13A9A|5002:слишком мало сложных символов|
|-2016331111|0x87D13A99|5001:слишком мало уникальных символов|
|-2016331112|0x87D13A98|5000:секретный код слишком короткий|
|-2016332093|0x87D136C3|4019:несколько полезных нагрузок блокировки приложения|
|-2016332094|0x87D136C2|4018:несколько имен точек доступа или полезных нагрузок сотовой сети|
|-2016332095|0x87D136C1|4017:несколько глобальных полезных нагрузок прокси-сервера HTTP|
|-2016332096|0x87D136C0|4016:(внутренняя ошибка)|
|-2016332097|0x87D136BF|4015:профиль замены не содержит полезную нагрузку MDM|
|-2016332098|0x87D136BE|4014:нет доступных удостоверений устройств|
|-2016332099|0x87D136BD|4013:сбой обновления|
|-2016332100|0x87D136BC|4012:невозможно обновить профиль|
|-2016332101|0x87D136BB|4011:итоговый профиль не является настраиваемым профилем|
|-2016332102|0x87D136BA|4010:идентификатор обновленного профиля отличается|
|-2016332103|0x87D136B9|4009:устройство заблокировано|
|-2016332104|0x87D136B8|4008:несовпадающие сертификаты|
|-2016332105|0x87D136B7|4007:неопознанный формат файла|
|-2016332106|0x87D136B6|4006:дата удаления профиля находится в прошлом|
|-2016332107|0x87D136B5|4005:секретный код не соответствует политике|
|-2016332108|0x87D136B4|4004:установка прервана пользователем|
|-2016332109|0x87D136B3|4003:установка профиля отсутствует в очереди|
|-2016332110|0x87D136B2|4002:повторяющийся UUID|
|-2016332111|0x87D136B1|4001:сбой установки|
|-2016332112|0x87D136B0|4000:не удается проанализировать профиль|
|-2016333111|0x87D132C9|3001:несоответствующий контроль сравнения значений (внутренняя ошибка)|
|-2016333112|0x87D132C8|3000:несоответствующий контроль ограничений (внутренняя ошибка)|
|-2016334108|0x87D12EE4|2004:неподдерживаемое значение поля|
|-2016334109|0x87D12EE3|2003:неправильный тип данных в поле|
|-2016334110|0x87D12EE2|2002:отсутствует обязательное поле|
|-2016334111|0x87D12EE1|2001:неподдерживаемая версия полезной нагрузки|
|-2016334112|0x87D12EE0|2000:неправильно оформленная полезная нагрузка|
|-2016335102|0x87D12B02|1010:неподдерживаемое значение поля|
|-2016335103|0x87D12B01|1009:сбой установки профиля|
|-2016335104|0x87D12B00|1008:идентификаторы полезной нагрузки не являются уникальными|
|-2016335105|0x87D12AFF|1007:UUID не являются уникальными|
|-2016335106|0x87D12AFE|1006:не удается расшифровать|
|-2016335107|0x87D12AFD|1005:пустой профиль|
|-2016335108|0x87D12AFC|1004:неправильная подпись|
|-2016335109|0x87D12AFB|1003:неправильный тип данных в поле|
|-2016335110|0x87D12AFA|1002:отсутствует обязательное поле|
|-2016335111|0x87D12AF9|1001:неподдерживаемая версия профиля|
|-2016335112|0x87D12AF8|1000:неправильно оформленный профиль|

## <a name="oma-response-codes"></a>Коды ответа OMA

|Код состояния|Шестнадцатеричный код ошибки|Сообщение об ошибке|
|---------------|--------------------------|-----------------|
|-2016344008|0x87D10838|(1404): отказано в доступе по сертификату.|
|-2016344009|0x87D10837|(1403): сертификат не найден.|
|-2016344010|0x87D10836|DCMO(1402): произошел сбой операции.|
|-2016344011|0x87D10835|DCMO(1401): пользователь не подтвердил операцию при появлении соответствующего приглашения.|
|-2016344012|0x87D10834|DCMO(1400): ошибка клиента.|
|-2016344108|0x87D107D4|DCMO(1204): возможность устройства отключена, но пользователю разрешено повторно включать ее.|
|-2016344109|0x87D107D3|DCMO(1203): возможность устройства отключена, и пользователю запрещено повторно включать ее.|
|-2016344110|0x87D107D2|DCMO(1202): Включение выполнено успешно, но возможность устройства в настоящее время отсоединена.|
|-2016344111|0xF3FB4D95|DCMO(1201): включение выполнено успешно, и возможность устройства в настоящее время присоединена.|
|-2016344112|0x87D107D0|DCMO(1200): операция выполнена успешно.|
|-2016345595|0x87D10205|Syncml(517): ответ на атомарную команду имеет слишком большой объем для одного сообщения.|
|-2016345596|0x87D10204|Syncml(516): команда выполнялась в элементе Atomic, в котором возникла ошибка. Не удалось выполнить откат этой команды.|
|-2016345598|0x87D10202|Syncml(514): выполнение команды SyncML не завершено, поскольку операция была отменена, прежде чем удалось обработать команду.|
|-2016345599|0x87D10201|Syncml(513): получатель не поддерживает или отказывается поддерживать указанную версию протокола синхронизации SyncML, которая используется в запросе сообщения SyncML.|
|-2016345600|0x87D10200|Syncml(512): ошибка приложения во время сеанса синхронизации.|
|-2016345601|0x87D101FF|Syncml(511): во время обработки запроса на сервере возникла серьезная ошибка.|
|-2016345602|0x87D101FE|Syncml(510): во время обработки запроса возникла ошибка. Эта ошибка связана с ошибкой хранилища данных получателя.|
|-2016345603|0x87D101FD|Syncml(509): Зарезервировано для использования в будущем.|
|-2016345604|0x87D101FC|Syncml(508): возникла ошибка, в результате которой необходимо обновить текущее состояние синхронизации клиента с сервером.|
|-2016345605|0x87D101FB|Syncml(507): из-за ошибки не удалось выполнить ни одну команду SyncML в элементе типа Atomic.|
|-2016345606|0x87D101FA|Syncml(506): ошибка приложения при обработке запроса.|
|-2016345607|0x87D101F9|Syncml(505): получатель не поддерживает или отказывается поддерживать определенную версию SyncML DTD, которая используется в запросе сообщения SyncML.|
|-2016345608|=0x87D101F8|Syncml(504): играя роль шлюза или прокси-сервера, получатель не получил своевременного ответа, необходимого для доступа при попытке выполнить запрос, от вышестоящего получателя, указанного в универсальном коде ресурса (например, HTTP, FTP, LDAP), или другого дополнительного получателя (например, DNS).|
|-2016345609|0x87D101F7|Syncml(503): получатель сейчас не может обработать запрос из-за временной перегрузки или обслуживания получателя.|
|-2016345610|0x87D101F6|Syncml(502): играя роль шлюза или прокси-сервера, получатель получил недопустимый ответ от вышестоящего получателя, к которому он обратился при попытке выполнить запрос.|
|-2016345611|0x87D101F5|Syncml(501): получатель не поддерживает команду, необходимую для выполнения запроса.|
|-2016345612|0x87D101F4|Syncml(500): получателем обнаружено непредвиденное условие, что помешало ему выполнить запрос|
|-2016345684|0x87D101AC|Syncml(428): не удалось выполнить перемещение.|
|-2016345685|0x87D101AB|Syncml(427): нельзя удалить родительский элемент, поскольку он содержит дочерние элементы.|
|-2016345686|0x87D101AA|Syncml(426): частичный элемент не принят.|
|-2016345687|0x87D101A9|Syncml(425): не удалось выполнить запрашиваемую команду, поскольку у отправителя нет необходимых разрешений контроля доступа на получателе.|
|-2016345688|0x87D101A8|Syncml(424): получен фрагментированный объект, но его размер не соответствует размеру, заявленному в первом фрагменте.|
|-2016345689|0x87D101A7|Syncml(423): не удалось выполнить запрашиваемую команду, поскольку обратимо удаленный элемент необратимо удален на сервере.|
|-2016345690|0x87D101A6|Syncml(422): не удалось выполнить на сервере запрашиваемую команду из-за неправильного формата сценария CGI в локальном универсальном коде ресурса.|
|-2016345691|0x87D101A5|Syncml(421): не удалось выполнить на сервере запрашиваемую команду из-за неизвестной грамматики указанного поискового запроса.|
|-2016345692|0x87D101A4|Syncml(420): на получателе отсутствует свободное дисковое пространство для оставшихся данных синхронизации.|
|-2016345693|0x87D101A3|Syncml(419): в результате запроса клиента возник конфликт, который разрешен благодаря успешному выполнению команды сервера.|
|-2016345694|0x87D101A2|Syncml(418): не удалось выполнить запрошенную команду Put или Add, поскольку целевой объект уже существует.|
|-2016345695|0x87D101A1|Syncml(417): в этот раз не удалось выполнить запрос. Инициатору следует повторить попытку позже.|
|-2016345696|0x87D101A0|Syncml(416): не удалось выполнить запрос, поскольку в нем указан слишком большой размер (в байтах).|
|-2016345697|0x87D1019F|Syncml(415): тип или формат носителя не поддерживается.|
|-2016345698|0x87D1019E|Syncml(414): не удалось выполнить команду, поскольку целевой универсальный код ресурса имеет слишком большую длину, чтобы получатель мог или был готов его обработать.|
|-2016345699|0x87D1019D|Syncml(413): получатель отказался выполнить запрашиваемую команду, поскольку запрашиваемый элемент больше, чем получатель может или готов обработать.|
|-2016345700|0x87D1019C|Syncml(412): не удалось обработать запрашиваемую команду на получателе, поскольку она сформирована не полностью или неправильно.|
|-2016345701|0x87D1019B|Syncml(411): для запрашиваемой команды также необходимо указать размер в байтах или сведения о длине элемента типа Meta.|
|-2016345702|0x87D1019A|Syncml(410): запрашиваемый целевой объект более не расположен на получателе, а универсальный код ресурса для пересылки неизвестен.|
|-2016345703|0x87D10199|Syncml(409): не удалось выполнить запрос из-за конфликта обновлений между версиями данных на клиенте и сервере.|
|-2016345704|0x87D10198|Syncml(408): ожидаемое сообщение не получено в течение необходимого периода.|
|-2016345705|0x87D10197|Syncml(407): не удалось выполнить запрашиваемую команду, поскольку инициатор должен пройти надлежащую проверку подлинности.|
|-2016345706|0x87D10196|Syncml(406): не удалось выполнить запрашиваемую команду, поскольку в запросе есть необязательный компонент, который не поддерживался.|
|-2016345707|0x87D10195|Syncml(405): выполнение запрашиваемой команды на целевом объекте не разрешено.|
|-2016345708|0x87D10194|Syncml(404): запрашиваемый целевой объект не найден.|
|-2016345709|0x87D10193|Syncml(403): не удалось выполнить запрашиваемую команду, но она была понята получателем.|
|-2016345710|0x87D10192|Syncml(402): не удалось выполнить запрашиваемую команду, поскольку требуется соответствующая оплата.|
|-2016345711|0x87D10191|Syncml(401): не удалось выполнить запрашиваемую команду, поскольку инициатор запроса должен пройти надлежащую проверку подлинности.|
|-2016345712|0x87D10190|Syncml(400): нельзя выполнить запрашиваемую команду из-за неправильного синтаксиса.|
|-2016345807|0x87D10131|Syncml(305): доступ к запрашиваемому целевому объекту необходимо получить с помощью указанного универсального кода ресурса прокси-сервера.|
|-2016345808|0x87D10130|Syncml(304):запрашиваемая команда SyncML не выполнена на целевом объекте.|
|-2016345809|0x87D1012F|Syncml(303): не удается найти запрашиваемый целевой объект на другом универсальном коде ресурса.|
|-2016345810|0x87D1012E|Syncml(302): запрашиваемый целевой объект временно перемещен на другой универсальный код ресурса.|
|-2016345811|0x87D1012D|Syncml(301): новый универсальный код ресурса запрашиваемого целевого объекта.|
|-2016345812|0x87D1012C|Syncml(300): запрашиваемый целевой объект является одним из нескольких альтернативных запрашиваемых целевых объектов.|
|-2016345896|0x87D100D8|Syncml(216): внутри элемента Atomic была команда, и в Atomic произошел сбой. Для команды успешно выполнен откат.|
|-2016345897|0x87D100D7|Syncml(215): команда не была выполнена из-за взаимодействия с пользователем, и пользователь отказался от принятия выбора.|
|-2016345898|0x87D100D6|Syncml(214): Операция отменена. Команда SyncML успешно выполнена, но в рамках сеанса другие команды не будут обрабатываться.|
|-2016345899|0x87D100D5|Syncml(213): блочный элемент принят и помещен в буфер.|
|-2016345900|0x87D100D4|Syncml(212): проверка подлинности принята. До завершения сеанса синхронизации не требуется дополнительной проверки подлинности. Этот код ответа можно использовать только в ответ на запрос, в котором указаны учетные данные.|
|-2016345901|0x87D100D3|Syncml(211): элемент не удален. Запрашиваемый элемент не найден. Возможно, он был удален ранее.|
|-2016345902|0x87D100D2|Syncml(210): удалить без архивации. Ответ означает, что запрашиваемые данные были успешно удалены, но не были предварительно заархивированы, так как эта НЕОБЯЗАТЕЛЬНАЯ возможность не поддерживалась реализацией.|
|-2016345903|0x87D100D1|конфликт разрешен созданием дубликата. Ответ означает, что из-за запроса возник конфликт обновления, который был разрешен с помощью дублирования данных клиента в базе данных сервера. Ответ включает целевой и исходный универсальные коды ресурса дубликата в элементе состояния. Помимо этого, в случае двусторонней синхронизации команда добавления возвращается с определением данных дублирования.|
|-2016345904|0x87D100D0|конфликт разрешен в пользу команды клиента. Ответ означает, что был конфликт обновления, который разрешился благодаря успешному выполнению команды клиента.|
|-2016345905|0x87D100CF|конфликт разрешен с помощью слияния. Ответ означает, что из-за запроса возник конфликт, который был разрешен с помощью слияния экземпляров данных клиента и сервера. Ответ включает целевой и исходный URL-адреса в элементе состояния. Помимо этого, команда перемещения возвращается с данными слияния.|
|-2016345906|0x87D100CE|ответ означает, что выполнена только часть команды. Если оставшуюся часть команды можно выполнить позднее, то после выполнения необходимо создать другой соответствующий код состояния запроса на выполнение.|
|-2016345907|0x87D100CD|НЕОБХОДИМО, чтобы источник обновил содержимое. Инициатору запроса сообщается, что его содержимое НЕОБХОДИМО синхронизировать, чтобы получить последнюю версию.|
|-2016345908|0x87D100CC|запрос был успешно выполнен, но никаких данных не возвращается. Код ответа также возвращается в ответ на команду Get, если у целевого объекта нет содержимого.|
|-2016345909|0x87D100CB|недостоверный ответ. Выполняет ответ на запрос со стороны сущности, отличной от целевой. Ответ возвращается, только если на запрос приходит код ответа 200 от достоверного целевого объекта.|
|-2016345910|0x87D100CA|принято к обработке. Запрос на удаленный запуск приложения или на оповещение пользователя о том, что приложение успешно выполнено.|
|-2016345911|0x87D100C9|запрашиваемый элемент был добавлен.|
|-2016345912|0x87D100C8|команда SyncML успешно выполнена.|
|-2016346011|0x87D10065|указанная команда SyncML выполняется, но ее выполнение еще не завершено.|

## <a name="next-steps"></a>Дальнейшие шаги

Обратитесь в службу поддержки Майкрософт, [чтобы получить поддержку для Microsoft Intune](get-support.md).