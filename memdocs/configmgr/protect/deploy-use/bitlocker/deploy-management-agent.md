---
title: Развертывание управления BitLocker
titleSuffix: Configuration Manager
description: Развертывание агента управления BitLocker для клиентов Configuration Manager и точек управления службы восстановления
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 39aa0558-742c-4171-81bc-9b1e6707f4ea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be5ecd02817d315da4a3bea1f21285eb5a77d77e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709362"
---
# <a name="deploy-bitlocker-management"></a>Развертывание управления BitLocker

*Область применения: Configuration Manager (Current Branch)*

<!--3601034-->

Управление BitLocker в Configuration Manager включает следующие компоненты.

- **Агент управления BitLocker**. Configuration Manager включает этот агент на устройстве при [создании политики](#create-a-policy) и [ее развертывании в коллекции](#deploy-a-policy).

- **Служба восстановления**. Серверный компонент, который получает данные восстановления BitLocker от клиентов. Дополнительные сведения см. в разделе [Служба восстановления](#recovery-service).

Перед созданием и развертыванием политик управления BitLocker выполните следующие действия.

- Проверка [предварительных требований](../../plan-design/bitlocker-management.md#prerequisites)

- При необходимости [зашифруйте ключи восстановления](encrypt-recovery-data.md) в базе данных сайта

## <a name="create-a-policy"></a>Создание политики

При создании и развертывании этой политики клиент Configuration Manager включает на устройстве агент управления BitLocker.

> [!NOTE]
> Для создания политики управления BitLocker требуется роль **Полный администратор** в Configuration Manager.

1. В консоли Configuration Manager перейдите в рабочую область **Активы и соответствие**, разверните узел **Endpoint Protection** и выберите узел **Управление BitLocker**.

1. В ленте выберите **Создать политику Управления BitLocker**.

1. В разделе **Общие** укажите имя и описание (необязательно). Выберите компоненты, которые нужно включить на клиентах с помощью этой политики:  

    - **Диск операционной системы**. Управление шифрованием диска операционной системы

    - **Фиксированный диск**. Управление шифрованием для дополнительных дисков данных на устройстве

    - **Съемный диск**. Управление шифрованием для дисков, которые можно удалить с устройства, например USB-ключ

    - **Управление клиентами**. Управление резервным копированием службы восстановления ключей для сведений о восстановлении шифрования диска BitLocker.  

1. На странице **Установка** настройте следующие глобальные параметры для шифрование диска BitLocker:

    > [!NOTE]
    > Configuration Manager применяет эти параметры при включении BitLocker. Если диск уже зашифрован или выполняется, любые изменения параметров политики не повлияют на шифрование диска на устройстве.
    >
    > Если вы отключаете или не настраиваете эти параметры, BitLocker использует метод шифрования по умолчанию (AES 128 бит).

    - Для устройств Windows 8.1 включите параметр **Метод шифрования диска и стойкость шифра**. Затем выберите метод шифрования.

    - Для устройств Windows 10 включите параметр **Метод шифрования диска и стойкость шифра (Windows 10)** . Затем по отдельности выберите метод шифрования для дисков ОС, фиксированных дисков с данными и съемных дисков с данными.

    Дополнительные сведения об этих и других параметрах на этой странице см. в разделе [Справочник по параметрам — настройка](../../tech-ref/bitlocker/settings.md#setup).

1. На странице **Диск операционной системы** укажите следующие параметры.  

    - **Параметры шифрования диска операционной системы**. Если этот параметр включен, пользователь должен защитить диск операционной системы, и BitLocker шифрует диск. Если он отключен, пользователь не может защитить диск.  

    На устройствах с совместимым модулем TPM для обеспечения дополнительной защиты зашифрованных данных при запуске могут использоваться два типа методов проверки подлинности. При запуске компьютера для проверки подлинности может использоваться только TPM или дополнительно может запрашиваться ввод персонального идентификационного номера (ПИН-кода). Настройте следующие параметры.

    - **Выберите предохранитель для диска операционной системы**. Настройте его, чтобы использовать доверенный платформенный модуль и ПИН-код или только доверенный платформенный модуль.

    - **Настроить минимальную длину ПИН-кода**. Если ПИН-код обязателен, это значение задает кратчайшую длину кода, который пользователь может указать. Пользователь вводит этот ПИН-код для разблокировки диска при загрузке компьютера. По умолчанию минимальная длина ПИН-кода составляет `4`.

    Дополнительные сведения об этих и других параметрах на этой странице см. в разделе [Справочник по параметрам — диск ОС](../../tech-ref/bitlocker/settings.md#os-drive).

1. На странице **Фиксированный диск** укажите следующие параметры.

    - **Шифрование фиксированного диска с данными**. Если этот параметр включен, BitLocker требует, чтобы пользователи защищали все фиксированные диски с данными. Затем он шифрует диски с данными. При включении этой политики включите автоматическую разблокировку или параметры для **политики паролей фиксированного диска с данными**.

    - **Настройка автоматического снятия блокировки для фиксированного диска с данными**. Разрешение или требование автоматической разблокировки любых зашифрованных дисков с данными с помощью BitLocker. Для использования автоматической разблокировки также требуется шифрование BitLocker для диска операционной системы.

    Дополнительные сведения об этих и других параметрах на этой странице см. в разделе [Справочник по параметрам — фиксированный диск](../../tech-ref/bitlocker/settings.md#fixed-drive).

1. На странице **Съемный диск** укажите следующие параметры.

    - **Шифрование съемного диска с данными**. Если включить этот параметр и разрешить пользователям применять защиту BitLocker, клиент Configuration Manager сохранит сведения о восстановлении съемных дисков в службе восстановления на точке управления. Такое поведение позволяет пользователям восстанавливать диск, если они забывают или теряют средство защиты (пароль).

    - **Разрешать пользователям применять защиту BitLocker на съемных дисках с данными**. Пользователи могут включить защиту BitLocker для съемного диска.

    - **Политика паролей для съемных дисков с данными**. Используйте эти параметры, чтобы задать ограничения для паролей для снятия блокировки съемных дисков, защищенных BitLocker.

    Дополнительные сведения об этих и других параметрах на этой странице см. в разделе [Справочник по параметрам — съемный диск](../../tech-ref/bitlocker/settings.md#removable-drive).

1. На странице **Управление клиентами** укажите следующие параметры.

    > [!IMPORTANT]
    > Если у вас нет точки управления с веб-сайтом с поддержкой HTTPS, не настраивайте этот параметр. Дополнительные сведения см. в разделе [Служба восстановления](#recovery-service).

    - **Настройка служб Управления BitLocker**. Если этот параметр включен, Configuration Manager автоматически создает резервную копию сведений о восстановлении ключей в базе данных сайта. Если вы отключаете или не настраиваете этот параметр политики, Configuration Manager не сохраняет сведения о восстановлении ключей.

        - **Выберите данные восстановления BitLocker для хранения**. Настройте параметр для задания пароля и ключа восстановления пакета или только пароля восстановления.

        - **Разрешить хранение сведений для восстановления в виде обычного текста**. Без сертификата шифрования управления BitLocker Configuration Manager хранит сведения о восстановлении ключей в виде обычного текста. Дополнительные сведения см. в статье [Шифрование данных восстановления](encrypt-recovery-data.md).

    Дополнительные сведения об этих и других параметрах на этой странице см. в разделе [Справочник по параметрам — управление клиентом](../../tech-ref/bitlocker/settings.md#client-management).

1. Завершите работу мастера.

Чтобы изменить параметры существующей политики, выберите ее в списке и нажмите **Свойства**.

При создании нескольких политик можно настроить их относительный приоритет. При развертывании нескольких политик на клиенте для определения его параметров используется значение приоритета.

## <a name="deploy-a-policy"></a>Развертывание политики

1. Выберите существующую политику в узле **Управление BitLocker**. На ленте щелкните **Развернуть**.

1. Выберите коллекцию устройств в качестве целевого объекта развертывания.

1. Если вы хотите, чтобы устройство могло шифровать или расшифровывать свои диски в любое время, выберите параметр **Разрешить исправление за пределами периода обслуживания**. Если коллекция содержит периоды обслуживания, она все равно исправляет эту политику BitLocker.

1. Настройте **простое** или **настраиваемое** расписание. По умолчанию клиент оценивает свое соответствие этой политике каждые 12 часов.

1. Выберите **ОК**, чтобы развернуть политику.

Можно создать несколько развертываний одной политики. Чтобы просмотреть дополнительные сведения о каждом развертывании, выберите политику в узле **Управление BitLocker**, а затем в области сведений перейдите на вкладку **Развертывания**.

## <a name="monitor"></a>Монитор

Просмотрите базовую статистику по соответствию для развертывания политики в области сведений узла **Управление BitLocker**.

- Количество соответствий
- Количество сбоев
- Количество несоответствий

Перейдите на вкладку **Развертывания**, чтобы увидеть процент соответствия и рекомендуемое действие. Выберите развертывание, а затем на ленте выберите **Просмотр состояния**. Это действие переключает представление на рабочую область **Мониторинг** в узле **Развертывания**. Подобно развертыванию других политик конфигурации можно просмотреть в этом представлении более подробное состояние соответствия.

Сведения о том, почему клиенты сообщают о несоответствии политике управления BitLocker, см. в разделе [Коды несоответствия](../../tech-ref/bitlocker/non-compliance-codes.md).

Дополнительные сведения об устранении неполадок см. в разделе [Устранение неполадок BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

Для мониторинга и устранения неполадок используйте следующие журналы.

### <a name="client-logs"></a>Журналы клиента

- Журнал событий MBAM: в средстве просмотра событий Windows перейдите к файлу "Приложения и службы" > Microsoft > Windows > MBAM.  Дополнительные сведения см. в разделе [Журналы событий BitLocker](../../tech-ref/bitlocker/about-event-logs.md) и [Журналы событий клиента](../../tech-ref/bitlocker/client-event-logs.md).

- **BitlockerMangementHandler.log** в пути журналов клиента, `%WINDIR%\CCM\Logs` по умолчанию

### <a name="management-point-logs-recovery-service"></a>Журналы точек управления (служба восстановления)

- Журнал событий службы восстановления: в средстве просмотра событий Windows перейдите к файлу "Приложения и службы" > Microsoft > Windows > MBAM-Web. Дополнительные сведения см. в разделе [Журналы событий BitLocker](../../tech-ref/bitlocker/about-event-logs.md) и [Журналы событий сервера](../../tech-ref/bitlocker/server-event-logs.md).

- Журналы трассировки службы восстановления: `<Default IIS Web Root>\Microsoft BitLocker Management Solution\Logs\Recovery And Hardware Service\trace*.etl`

## <a name="recovery-service"></a>Служба восстановления

Служба восстановления BitLocker — это серверный компонент, который получает данные восстановления BitLocker от клиентов Configuration Manager. Сайт развертывает службу восстановления при создании политики управления BitLocker. Configuration Manager автоматически устанавливает службу восстановления на каждой точке управления с помощью веб-сайта с поддержкой HTTPS.

Configuration Manager сохраняет сведения о восстановлении в базе данных сайта. Без сертификата шифрования управления BitLocker Configuration Manager хранит сведения о восстановлении ключей в виде обычного текста.

Дополнительные сведения см. в статье [Шифрование данных восстановления](encrypt-recovery-data.md).

## <a name="migration-considerations"></a>Вопросы миграции

Если в настоящее время вы используете Microsoft BitLocker Administration and Monitoring (MBAM), можно легко перенести управление в Configuration Manager. При развертывании политик управления BitLocker в Configuration Manager клиенты автоматически передают ключи и пакеты восстановления в службу восстановления Configuration Manager.

> [!IMPORTANT]
> При переходе с автономной службы MBAM на управление BitLocker в Configuration Manager, если требуются существующие функциональные возможности автономного MBAM, не используйте повторно автономные серверы или компоненты MBAM с управлением BitLocker в Configuration Manager. Если вы повторно используете эти серверы, автономная служба MBAM перестанет работать, когда управление BitLocker в Configuration Manager установит свои компоненты на этих серверах. Не запускайте сценарий MBAMWebSiteInstaller.ps1 для настройки порталов BitLocker на автономных серверах MBAM. При настройке управления BitLocker в Configuration Manager используйте отдельные серверы.

### <a name="group-policy"></a>Групповая политика

- Параметры управления BitLocker полностью совместимы с параметрами групповой политики MBAM. Если устройства получают параметры групповой политики и политики Configuration Manager, они должны совпадать.

- Configuration Manager не реализует все параметры групповой политики MBAM. При настройке дополнительных параметров в групповой политике агент управления BitLocker на клиентах Configuration Manager учитывает эти параметры.

### <a name="tpm-password-hash"></a>Хэш пароля TPM

- Предыдущие клиенты MBAM не передают хэш пароля TPM в Configuration Manager. Клиент отправляет хэш пароля TPM только один раз.

- Если необходимо перенести эти сведения в службу восстановления Configuration Manager, очистите TPM на устройстве. После перезапуска будет отправлен новый хэш пароля TPM в службу восстановления.

### <a name="re-encryption"></a>Повторное шифрование

Configuration Manager не выполняет повторное шифрование дисков, которые уже защищены с помощью шифрования диска BitLocker. При развертывании политики управления BitLocker, которая не соответствует текущей защите диска, она сообщает о несоответствии требованиям. Диск по-прежнему будет защищен.

Например, вы использовали MBAM для шифрования диска без защиты ПИН-кода, но для политики Configuration Manager требуется ПИН-код. Диск не соответствует политике, несмотря на то что он зашифрован.

Чтобы обойти это поведение, сначала отключите BitLocker на устройстве. Затем разверните новую политику с новыми параметрами.

## <a name="next-steps"></a>Дальнейшие шаги

[Настройка отчетов и порталов BitLocker](setup-websites.md)