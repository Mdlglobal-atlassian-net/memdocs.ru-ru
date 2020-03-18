---
title: Устранение неполадок с политиками в Microsoft Intune в Azure | Документация Майкрософт
description: Узнайте, как использовать встроенное средство устранения неполадок, и ознакомьтесь с распространенными проблемами, возникающими при использовании политик соответствия требованиям и профилей конфигурации в Microsoft Intune, а также способами их решения.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 99fb6db6-21c5-46cd-980d-50f063ab8ab8
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3aaf2bf895082f3647f0a1ad6b9997a5e97baee
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "79364127"
---
# <a name="troubleshoot-policies-and-profiles-and-in-intune"></a>Устранение неполадок с политиками и профилями в Intune

В Microsoft Intune есть встроенные функции устранения неполадок. С их помощью можно устранять проблемы с политиками соответствия требованиям и профилями конфигурации в среде.

В этой статье перечислены некоторые стандартные способы устранения неполадок и описаны возможные проблемы.

## <a name="check-tenant-status"></a>Проверка состояния клиента

Проверьте [Состояние клиента](../fundamentals/tenant-status.md) и убедитесь, что подписка активна. Вы также можете просмотреть сведения об активных инцидентах и рекомендации, которые могут повлиять на развертывание политики или профиля.

## <a name="use-built-in-troubleshooting"></a>Использование встроенных функций устранения неполадок

1. В [центре администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) выберите раздел **Устранение неполадок и поддержка**:

    ![В Intune перейдите на страницу "Справка и поддержка" и выберите пункт "Устранение неполадок"](./media/troubleshoot-policies-in-microsoft-intune/help-and-support-troubleshoot.png)

2. Нажмите **Выберите пользователя**, выберите пользователя, у которого возникла проблема, а затем нажмите кнопку **Выбрать**.
3. Убедитесь в том, что поля **Лицензия Intune** и **Состояние учетной записи** отмечены зелеными галочками.

    ![В Intune выберите пользователя и убедитесь в том, что поля состояния "Состояние учетной записи" и "Лицензия Intune" отмечены зелеными галочками](./media/troubleshoot-policies-in-microsoft-intune/account-status-intune-license-show-green.png)

    **Полезные ссылки**:

    - [Назначение пользователям лицензий для регистрации устройств](../fundamentals/licenses-assign.md)
    - [Добавление пользователей в Intune](../fundamentals/users-add.md)

4. На панели **Устройства** найдите устройство, с которым связана проблема. Проверьте значения в различных столбцах.

    - **Управляется**: чтобы к устройству могли применяться политики соответствия требованиям или политики конфигурации, это свойство должно иметь значение **MDM** или **EAS/MDM**.

        - Если свойство **Управляется** имеет значение, отличное от **MDM** или **EAS/MDM**, устройство не зарегистрировано. Политики соответствия требованиям и политики конфигурации не будут применяться к нему, пока оно не будет зарегистрировано.

        - Политики защиты приложений (управление мобильными приложениями) не требуют регистрации устройств. Дополнительные сведения см. в статье [Как создать и назначить политики защиты приложений](../apps/app-protection-policies.md).

    - **Тип присоединения к Azure AD**: должно иметь значение **Рабочая область** или **AzureAD**.
 
        - Если в этом столбце указано значение **Не зарегистрировано**, возможно, имеются проблемы с регистрацией. Как правило, их удается решить путем отмены регистрации устройства и его повторной регистрации.

    - **Совместимость с Intune**: должно иметь значение **Да**. Значение **Нет** может свидетельствовать о проблеме с политиками соответствия требованиям или о том, что устройство не подключается к службе Intune. Например, устройство может быть выключено или не иметь подключения к сети. В конечном итоге устройство перестанет соответствовать требованиям (обычно через 30 дней).

        Дополнительные сведения см. в статье [Начало работы с политиками соответствия устройств](../protect/device-compliance-get-started.md).

    - **Совместимо с Azure AD**: должно иметь значение **Да**. Значение **Нет** может свидетельствовать о проблеме с политиками соответствия требованиям или о том, что устройство не подключается к службе Intune. Например, устройство может быть выключено или не иметь подключения к сети. В конечном итоге устройство перестанет соответствовать требованиям (обычно через 30 дней).

        Дополнительные сведения см. в статье [Начало работы с политиками соответствия устройств](../protect/device-compliance-get-started.md).

    - **Последний возврат**: значением должны быть недавние дата и время. По умолчанию проверка устройств выполняется в Intune каждые 8 часов.

        - Если со времени, указанного в столбце **Последний возврат**, прошло больше 24 часов, возможно, имеется проблема с устройством. Если устройство не проходит проверку, оно не может получать политики из Intune.

        - Чтобы пройти проверку принудительно, выполните указанные ниже действия.
            - На устройстве Android откройте приложение "Корпоративный портал", выберите пункт **Устройства**, выберите устройство в списке и нажмите **Проверить параметры устройства**.
            - На устройстве с iOS или iPadOS откройте приложение "Корпоративный портал", выберите пункт **Устройства**, выберите устройство в списке и нажмите элемент **Проверить параметры**.

        - На устройстве Windows последовательно выберите **Параметры** > **Учетные записи** > **Доступ к учетной записи места работы или учебного заведения**, выберите учетную запись или регистрацию в системе MDM, а затем нажмите **Информация** > **Синхронизировать**.

    - Выберите устройство, чтобы просмотреть сведения о политиках.

        На панели **Соответствие устройства политике** показано состояние политик соответствия требованиям, назначенных устройству.

        На панели **Конфигурация устройств** показано состояние политик конфигурации, назначенных устройству.

        Если на панели **Соответствие устройства политике** или **Конфигурация устройств** отсутствуют требуемые политики, значит, они настроены неправильно. Откройте политику и назначьте ее этому пользователю или устройству.

        **Состояния политики**:

        - **Неприменимо**. Эта политика не поддерживается на данной платформе. Например, политики iOS/iPadOS не работают в Android. Политики Samsung KNOX не работают на устройствах Windows.
        - **Конфликт**. На устройстве есть параметр, который служба Intune не может переопределить. Возможно также, что развернуты две политики с одним и тем же параметром, имеющим разные значения.
        - **Ожидание**: Устройство не связалось с Intune для получения политики. Возможно также, что устройство получило политику, но пока не сообщило Intune о своем состоянии.
        - **Ошибки**: сведения об ошибках и возможных способах их устранения см. в статье [Устранение неполадок, связанных с доступом к ресурсам компании](../fundamentals/troubleshoot-company-resource-access-problems.md).

        **Полезные ссылки**: 

        - [Способы развертывания политик соответствия устройств](../protect/device-compliance-get-started.md#ways-to-deploy-device-compliance-policies)
        - [Мониторинг политик соответствия устройств](../protect/compliance-policy-monitor.md)

## <a name="youre-unsure-if-a-profile-is-correctly-applied"></a>Вы не уверены, правильно ли применен профиль

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Последовательно выберите **Устройства** > **Все устройства**, выберите устройство и нажмите **Конфигурация устройств**. 

    Для каждого устройства приведен список профилей. У каждого профиля есть **состояние**. Состояние присваивается после применения к устройству всех назначенных профилей, включая требования и ограничения, связанные с оборудованием и операционной системой. Ниже перечислены возможные состояния.

    - **Соответствует**. Устройство получило профиль и сообщает Intune о соответствии заданному параметру.

    - **Неприменимо**. Параметр профиля неприменим. Например, параметры электронной почты для устройств с iOS или iPadOS не применяются к устройствам Android.

    - **Ожидание**: Профиль был отправлен на устройство, которое пока не сообщило Intune о своем состоянии. Например, для шифрования на устройствах Android требуется, чтобы пользователь включил соответствующую функцию, в результате чего может возникнуть состояние ожидания.

**Полезная ссылка**: [Мониторинг профилей устройств](../configuration/device-profile-monitor.md)

> [!NOTE]
> Если к одному устройству или пользователю применяются две политики с разными уровнями ограничений, используется более строгая политика.

## <a name="policy-troubleshooting-resources"></a>Ресурсы по устранению неполадок с политикой

- [Support tip: Troubleshooting iOS or Android policies not applying to devices](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-tip-Troubleshooting-iOS-or-Android-policies-not-applying/ba-p/280154) (Совет службы поддержки: устранение проблем с политиками iOS/iPadOS или Android, которые не применяются к устройствам) — откроется другой сайт Майкрософт.
- [Troubleshooting Windows 10 Intune Policy Failures](https://blogs.technet.microsoft.com/configmgrdogs/2018/08/09/troubleshooting-windows-10-intune-policy-failures/) (Устранение неполадок со сбоями политик Intune в Windows 10) — откроется блог.
- [Troubleshoot CSP custom settings for Windows 10](https://support.microsoft.com/en-us/help/4055338/troubleshoot-csp-setting-windows-10-computer-intune) (Устранение проблем с настраиваемыми параметрами CSP для Windows 10) — откроется другой сайт Майкрософт.
- [Windows 10 Group Policy vs. Intune MDM Policy who wins?](https://blogs.technet.microsoft.com/cbernier/2018/04/02/windows-10-group-policy-vs-intune-mdm-policy-who-wins/) (Групповая политика Windows 10 и политика Intune MDM) — откроется другой сайт Майкрософт.

## <a name="alert-saving-of-access-rules-to-exchange-has-failed"></a>Предупреждение: Не удалось сохранить правила доступа в Exchange

**Проблема**. В консоли администрирования появляется предупреждение **Не удалось сохранить правила доступа в Exchange**.

Если вы создаете политики в рабочей области локальной политики Exchange (в консоли администрирования), но используете Office 365, служба Intune не применяет настроенные параметры политики. Обратите внимание на источник политики в предупреждении. Удалите устаревшие правила в рабочей области локальной политики Exchange. Устаревшие правила — это глобальные правила Exchange в Intune для локальной службы Exchange, которые не относятся к Office 365. Затем создайте новую политику для Office 365.

Полезную информацию можно найти в статье [Устранение неполадок в работе соединителя Intune с локальной организацией Exchange](../protect/troubleshoot-exchange-connector.md).

## <a name="cant-change-security-policies-for-enrolled-devices"></a>Не удается изменить политики безопасности для зарегистрированных устройств

Устройства Windows Phone не поддерживают последующее снижение уровня безопасности для политик, настроенных с помощью MDM или EAS. Например, вы задали значение 8 для параметра **минимального числа символов в пароле**, а затем хотите уменьшить его до 4. К устройству уже применяется более строгая политика.

Устройства Windows 10 могут не удалять политики безопасности при отмене назначения политики (остановке развертывания). Может потребоваться оставить политику назначенной, а затем восстановить параметры безопасности по умолчанию.

Если вы хотите изменить политику на менее безопасную, то в зависимости от платформы устройства может потребоваться выполнить сброс политик безопасности.

Например, на рабочем столе Windows 8.1 проведите пальцем от правого края, чтобы открыть панель **чудо-кнопок**. Последовательно выберите **Параметры** > **Панель управления** > **Учетные записи пользователей**. На экране слева щелкните ссылку **Сбросить политики безопасности** и выберите **Сбросить политики**.

Чтобы применить менее строгую политику к другим платформам (например, Android, iOS/iPadOS и Windows Phone 8.1), скорее всего, потребуется снять платформу с учета и повторно зарегистрировать ее.

Полезную информацию можно найти в статье [Устранение проблем при регистрации устройств](../enrollment/troubleshoot-device-enrollment-in-intune.md).

## <a name="pcs-using-the-intune-software-client---classic-portal"></a>Компьютеры, на которых используется программный клиент Intune, — классический портал

> [!NOTE]
> Этот раздел относится к классическому порталу. 

### <a name="microsoft-intune-policy-related-errors-in-policyplatformlog"></a>Ошибки в policyplatform.log, связанные с политиками Microsoft Intune

Для компьютеров Windows под управлением клиентского программного обеспечения Intune ошибки политик в файле `policyplatform.log` могут быть вызваны тем, что параметрам контроля учетных записей Windows (UAC) на устройстве присвоены значения, отличные от стандартных. Некоторые отличные от используемых по умолчанию значения параметров UAC могут затрагивать установки клиента Microsoft Intune и выполнение политик.

#### <a name="resolve-uac-issues"></a>Устранение проблем с UAC

1. Снимите компьютер с учета. См. статью [Удаление устройств](../remote-actions/devices-wipe.md).

2. Подождите 20 минут для удаления клиентского программного обеспечения.

    > [!NOTE]
    > Не пытайтесь удалить клиент из раздела "Программы и компоненты".

3. Введите **UAC** в меню "Пуск", чтобы открыть параметры контроля учетных записей.

4. Переместите ползунок уведомлений в значение по умолчанию.

### <a name="error-cannot-obtain-the-value-from-the-computer-0x80041013"></a>ERROR: Не удается получить значение от компьютера, 0x80041013

Возникает, если рассинхронизация времени в локальной системе составляет пять и более минут. В случае рассинхронизации времени на локальном компьютере безопасные транзакции завершаются ошибкой из-за недопустимых меток времени.

Чтобы устранить эту проблему, установите время локальной системы как можно ближе ко времени в Интернете или времени, установленному в контроллерах домена в сети.

## <a name="next-steps"></a>Дальнейшие шаги

[Распространенные проблемы с профилями электронной почты и возможные решения](../configuration/troubleshoot-email-profiles-in-microsoft-intune.md)

Получите [поддержку от корпорации Майкрософт](../fundamentals/get-support.md) или обратитесь на [форумы сообщества](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).