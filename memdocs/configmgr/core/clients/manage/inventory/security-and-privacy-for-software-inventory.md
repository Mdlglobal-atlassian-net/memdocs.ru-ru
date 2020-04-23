---
title: Безопасность и конфиденциальность инвентаризации программного обеспечения
titleSuffix: Configuration Manager
description: Сведения об обеспечении безопасности и конфиденциальности инвентаризации программного обеспечения в Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8e68e1fb-a8ec-4543-bb8a-cbbaf184a418
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: d64fd2ac98996a6a1ccadae78e5f9cc576b55444
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690092"
---
# <a name="security-and-privacy-for-software-inventory-in-configuration-manager"></a>Безопасность и конфиденциальность инвентаризации программного обеспечения в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

В этом разделе содержатся сведения об обеспечении безопасности и конфиденциальности инвентаризации программного обеспечения в Configuration Manager.  

##  <a name="security-best-practices-for-software-inventory"></a><a name="BKMK_Security_HardwareInventory"></a> Рекомендации по обеспечению безопасности для инвентаризации программного обеспечения  
 Примите во внимание следующие рекомендации по обеспечению безопасности при сборе данных инвентаризации программного обеспечения с клиентов.  

|Рекомендация по безопасности|Дополнительные сведения|  
|----------------------------|----------------------|  
|Данные инвентаризации необходимо подписывать и шифровать.|Когда клиенты обмениваются данными с точками управления по протоколу HTTPS, для всех передаваемых данных используется SSL-шифрование. Тем не менее, когда клиентские компьютеры используют протокол HTTP для обмена данными с точками управления в интрасети, данные инвентаризации клиентов и собранные файлы могут отправляться незашифрованными и неподписанными. Убедитесь, что требование подписывания и шифрования настроено для сайта. Кроме того, если клиенты поддерживают алгоритм шифрования SHA-256, настройте обязательное использование SHA-256.|  
|Не используйте функцию сбора файлов для сбора критических файлов или конфиденциальной информации.|Функция инвентаризации программного обеспечения Configuration Manager использует все права учетной записи LocalSystem, которой разрешено выполнять сбор копий критически важных системных файлов, таких как данные реестра или базы данных учетных записей безопасности. Если такие файлы доступны на сервере сайта, пользователь с правами на чтение ресурсов или правами NTFS на доступ к расположению, где хранятся файлы, может проанализировать содержимое файлов и выяснить важные сведения о клиентах, что позволит ему нарушить их безопасность.|  
|Ограничьте права локального администратора на клиентских компьютерах|Пользователь с правами локального администратора может отправить недопустимые данные в качестве данных инвентаризации.|  

### <a name="security-issues-for-software-inventory"></a>Проблемы безопасности инвентаризации программного обеспечения  
 Со сбором данных инвентаризации связано несколько потенциальных уязвимостей. Злоумышленники могут сделать следующее:  

- отправить недопустимые данные, которые могут быть приняты точкой управления, даже если параметр клиента инвентаризации программного обеспечения отключен, и сбор файлов не активирован;  

- отправлять слишком большие объемы данных в одном файле или в большом числе файлов, реализуя атаку типа "отказ в обслуживании";  

- получать доступ к данным инвентаризации в момент их передачи в Configuration Manager.  

  Если пользователям известно, что они могут создать скрытый файл с именем **Skpswi.dat** и поместить его в корневую папку жесткого диска клиента, чтобы исключить его из инвентаризации программного обеспечения, вам не удастся выполнить сбор данных с этого компьютера.  

  Так как пользователь с правами локального администратора может отправлять любые сведения в качестве данных инвентаризации, нельзя считать данные инвентаризации, собираемые Configuration Manager, достоверными.  

  Функция инвентаризации программного обеспечения включена по умолчанию в качестве параметра клиента.  

##  <a name="privacy-information-for-software-inventory"></a><a name="BKMK_Privacy_HardwareInventory"></a> Сведения о конфиденциальности инвентаризации программного обеспечения  
 Функция инвентаризации оборудования позволяет извлекать любые данные, хранимые в реестре и инструментарии WMI на клиентах Configuration Manager. Функция инвентаризации программного обеспечения позволяет обнаруживать все файлы указанного типа или выполнять сбор всех указанных файлов с клиентов. Аналитика активов оптимизирует возможности инвентаризации, расширяя набор данных инвентаризации оборудования и программного обеспечения и дополняя их новыми функциями управления лицензиями.  

 Инвентаризация оборудования включена по умолчанию в качестве параметра клиента. Набор собираемых данных инструментария WMI определяется заданными администратором параметрами. Функция инвентаризации программного обеспечения включена по умолчанию, однако сбор файлов по умолчанию не выполняется. Сбор данных аналитики активов включается автоматически, однако можно выбрать, какие именно классы отчетов инвентаризации оборудования будут включены.  

 Данные инвентаризации не передаются в корпорацию Майкрософт. Данные инвентаризации хранятся в базе данных Configuration Manager. Когда клиенты используют протокол HTTPS для подключения к точкам управления, отправляемые ими на сайт данные шифруются во время передачи. Если клиент использует для подключения к точкам управления протокол HTTP, шифрование данных инвентаризации можно настроить специально. Данные инвентаризации не хранятся в зашифрованном виде в базе данных. Сведения хранятся в базе данных, пока не будут удалены задачей обслуживания сайта **Удаление устаревших данных инвентаризации** или **Удаление устаревших собранных файлов** (интервал по умолчанию составляет 90 дней). Можно настроить интервал удаления.  

 Перед настройкой инвентаризации оборудования и программного обеспечения, сбора файлов или сбора данных аналитики активов примите во внимание требования к конфиденциальности.  