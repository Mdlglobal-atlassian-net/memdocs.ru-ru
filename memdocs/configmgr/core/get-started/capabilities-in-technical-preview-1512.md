---
title: Возможности технической версии 1512
titleSuffix: Configuration Manager
description: Сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f52d6956cf860de8e45ac4e532500d32bcf077ba
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074509"
---
# <a name="capabilities-in-technical-preview-1512-for-configuration-manager"></a>Возможности в Technical Preview 1512 для Configuration Manager

*Область применения: Configuration Manager (ветвь Technical Preview)*

В этой статье содержатся сведения о функциях, доступных в Technical Preview для Configuration Manager, версия 1512. Этот выпуск можно установить для обновления и добавления новых возможностей в ознакомительную техническую версию сайта Configuration Manager. Перед установкой этой версии прочтите вводную статью [Technical Preview для Configuration Manager](technical-preview.md), чтобы ознакомиться с общими требованиями и ограничениями на использование ознакомительной технической версии, а также узнать, как выполнять обновления и оставлять отзывы о возможностях этого выпуска.  

 Ниже перечислены новые возможности, доступные в этой версии.  

##  <a name="device-health-attestation"></a><a name="bkmk_devicehealth"></a> Аттестация работоспособности устройств  
 Начиная с Technical Preview 1512, администраторы могут просматривать состояние аттестации работоспособности устройств Windows 10 в консоли Configuration Manager.  Эта функция доступна для Configuration Manager и Configuration Manager с Microsoft Intune. Аттестация работоспособности устройств позволяет администратору гарантировать, что клиентские компьютеры имеют надежные конфигурации BIOS, модуля TPM и загрузочного программного обеспечения. Для поддержки аттестации работоспособности устройств клиентские устройства должны работать под управлением Windows 10 с включенным модулем TPM 2. Аттестация работоспособности устройств отображает количество устройств, которые включены для использования каждой из следующих функций:  

-   Ранний запуск защиты от вредоносных программ  

-   BitLocker  

-   Безопасная загрузка  

-   Целостность кода  

В консоли также отображаются основные отсутствующие настройки аттестации работоспособности с количеством устройств.  

Чтобы просмотреть представление аттестации работоспособности устройства, в консоли Configuration Manager перейдите в рабочую область **Мониторинг**, щелкните узел **Безопасность**, а затем **Аттестация работоспособности**.  

##  <a name="in-console-monitoring-for-terms-and-conditions"></a><a name="bkmk_viewterms"></a> Выполняемый в консоли мониторинг условий и положений  
Начиная с версии Technical Preview 1512, при интеграции Configuration Manager с Microsoft Intune можно использовать консоль Configuration Manager для просмотра того, какие пользователи приняли условия и положения, настроенные вашим ИТ-отделом, а какие — нет.  

**Просмотр сводных данных**  

-   В консоли Configuration Manager последовательно выберите **Мониторинг** > **Обзор** > **Развертывания** и выберите условия развертывания для просмотра.  

**Просмотр подробных сведений**  

1.  В консоли Configuration Manager последовательно выберите **Активы и соответствие** > **Обзор** > **Параметры соответствия** > **Условия**, а затем выберите условия для просмотра.  

2.  В нижней части консоли откройте вкладку **Развертывания**, выберите развертывание и щелкните **Просмотреть состояние**.  

##  <a name="improvements-to-endpoint-protection-policy-settings"></a><a name="bkmk_EPpolicy"></a> Усовершенствования параметров политики Endpoint Protection  
В Technical Preview 1512 мы добавили следующие новые параметры для политики защиты от вредоносных программ Endpoint Protection.  

-   Защита в режиме реального времени: **Блокировать потенциально нежелательные приложения при скачивании и до установки.**  

    -   Потенциально нежелательные приложения (PUA) — это классификация угроз на основе репутации и ориентированной на исследования идентификации. Чаще всего это средства увязки нежелательных приложений в пакеты или их упакованные приложения.  

    -   Параметр политики защиты включен по умолчанию (задано значение "Да"). Если параметр включен, он блокирует PUA при скачивании и установке. Тем не менее вы можете исключить определенные файлы или папки в соответствии с потребностями среды.  

-   Параметры проверки: **Проверять подключенные сетевые диски при выполнении полной проверки**  

    -   Этот параметр позволяет администраторам более тщательно выполнять проверки сетевых файлов по требованию без риска постоянной проверки подключенных сетевых дисков во время запланированной полной проверки.  

    -   Параметр **Проверять сетевые файлы** должен быть включен ("Да"), чтобы его можно было настроить.  

    -   По умолчанию значение "Нет" для этого параметра означает, что полная проверка не затронет подключенные сетевые диски.  

-   Параметры автоматической отправки примеров файлов  

     Модуль защиты от вредоносных программ может запросить примеры файлов, отправляемых в корпорацию Майкрософт для дальнейшего анализа. По умолчанию он всегда будет выводить запрос перед отправкой таких примеров. Теперь администраторы могут управлять следующими параметрами для настройки этого поведения.  

    -   Дополнительно: **Включить автоматическую отправку примеров файлов, чтобы помочь Майкрософт определить, являются ли некоторые обнаруженные элементы вредоносными**.  Изменение значения этого параметра на "Да", чтобы включить автоматическую отправку примеров файлов. По умолчанию задано значение "Нет", означающее, что автоматическая отправка примеров файлов отключена и пользователи будут получать запрос перед отправкой примеров.   (Этот параметр впервые появился в System Center 2012 R2 Configuration Manager с пакетом обновления 1 (SP1).)  

    -   Дополнительно: **Разрешить пользователям изменять параметры автоматической отправки примеров файлов**. Этот параметр определяет, может ли пользователь с правами локального администратора на устройстве изменять параметр автоматической отправки примера файла в интерфейсе клиента. По умолчанию этому параметру присвоено значение "Нет", означающее, что параметры можно изменять только в консоли Configuration Manager, а локальные администраторы устройства не могут изменять эту настройку.  

         Например, ниже показано, что администратор задал параметр Защитника Windows в Windows 10 как включенный, и пользователь не может изменить его.  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    Кроме того, существующий параметр **Исключить файлы и папки** в разделе "Параметры исключения" политики защиты от вредоносных программ Endpoint Protection усовершенствован и разрешает исключать устройства. Например, теперь можно указать следующее в качестве исключения: **\device\mvfs** (для файловой системы с несколькими версиями). Политика не проверяет путь к устройству. Политика Endpoint Potection доступна в модуле защиты от вредоносных программ на клиентском компьютере, который должен интерпретировать строки устройств.  

**Необходимые компоненты для использования политик Endpoint Protection**  

Перед использованием политик Endpoint Protection необходимо установить клиент Endpoint Protection и организовать управление им в помощью параметров клиента Endpoint Protection. Для этого используется клиент System Center Endpoint Protection для Windows 7, Windows 8, Windows 8.1 или управляемый Защитник Windows для Windows 10. См. [Endpoint Protection](../../protect/deploy-use/endpoint-protection.md).  
