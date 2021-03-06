---
title: Добавление скриптов PowerShell для устройств Windows 10 в Microsoft Intune — Azure | Документация Майкрософт
description: Создавайте и добавляйте скрипты PowerShell, назначайте политику скриптов группам Azure Active Directory, используйте отчеты для отслеживания скриптов и ознакомьтесь с инструкциями по удалению скриптов, добавленных для устройств Windows 10 в Microsoft Intune. Изучите распространенные проблемы и способы их устранения.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/06/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 768b6f08-3eff-4551-b139-095b3cfd1f89
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: a8d75208de7cc6697699d79e3a52df742f605fdb
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990729"
---
# <a name="use-powershell-scripts-on-windows-10-devices-in-intune"></a>Использование скриптов PowerShell для устройств Windows 10 в Intune

Используйте расширение управления Microsoft Intune, чтобы отправлять скрипты PowerShell в Intune для выполнения на устройствах Windows 10. Расширение управления предоставляет больше возможностей управления мобильными устройствами (MDM) Windows 10 и упрощает переход на современные средства управления.

Данная функция применяется к:

- Windows 10 и более поздних версий (кроме Windows 10 Домашняя)

> [!NOTE]
> Если выполняются предварительные условия, расширение управления Intune устанавливается автоматически, когда скрипт PowerShell либо приложение Win32 назначаются пользователю или устройству. Дополнительные сведения см. в разделе [Предварительные условия](../apps/intune-management-extension.md#prerequisites).

## <a name="move-to-modern-management"></a>Переход на современные принципы управления

Вычислительная среда конечного пользователя находится на этапе цифрового преобразования. Классические ИТ-системы работают по схеме, где используется одна платформа для устройств, применяются корпоративные устройства, пользователи занимаются своими обязанностями в офисе, а различные ИТ-процессы выполняются вручную и в оперативном режиме. Современные организации используют сразу несколько платформ как на личных, так и на корпоративных устройствах, позволяют пользователям работать из любого места, а также поддерживают автоматизированные и упреждающие ИТ-процессы.

Службы управления мобильными устройствами, например Microsoft Intune, могут контролировать работу мобильных и настольных устройств под управлением Windows 10. Встроенный клиент управления Windows 10 взаимодействует с Intune для реализации соответствующих задач на уровне предприятия. Возможно, вам потребуется выполнять такие задачи, как расширенная настройка или устранение неполадок. Вы можете управлять приложениями Win32 с помощью [соответствующей функции](app-management.md) на устройствах с Windows 10.

Расширение управления Intune дополняет встроенные возможности Windows 10 MDM. Вы можете создать скрипты PowerShell для выполнения на устройствах Windows 10. Например, создайте скрипт PowerShell, который задает расширенные конфигурации устройств. Затем отправьте скрипт в Intune, назначьте скрипт группе Azure Active Directory (AD) и запустите скрипт. Вы сможете отслеживать состояние выполнения скрипта от начала до конца.

## <a name="prerequisites"></a>Предварительные условия

Для расширения управления Intune требуется выполнить следующие условия. Если они выполняются, расширение управления Intune устанавливается автоматически, когда скрипт PowerShell или приложение Win32 назначаются пользователю или устройству.

- Устройства с ОС Windows 10 версии 1607 или более поздней. Если устройство зарегистрировано с помощью [массовой автоматической регистрации](../enrollment/windows-bulk-enroll.md), на нем должна выполняться Windows 10 версии 1709 или более поздней. Расширение управления Intune не поддерживается в Windows 10 в режиме S, так как режим S блокирует запуск приложений, не приобретенных в магазине. 
  
- Устройства, присоединенные к службам Azure Active Directory, включая:  
  
  - устройства с гибридным присоединением к Azure AD — устройства, присоединенные к Azure Active Directory (AD), а также присоединенные к локальной среде Active Directory (AD). Инструкции см. в разделе [Планирование реализации гибридного подключения к Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).
  
  > [!TIP]
  > Убедитесь, что устройства [присоединены к Azure AD](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network). Устройства, которые только [зарегистрированы](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) в Azure AD, не получат ваши скрипты.  

- Устройства, зарегистрированные в Intune, включая:

  - устройства, зарегистрированные в групповой политике (GPO). (инструкции см. в разделе [Enroll a Windows 10 device automatically using Group Policy](https://docs.microsoft.com/windows/client-management/mdm/enroll-a-windows-10-device-automatically-using-group-policy) (Автоматическая регистрация устройства Windows 10 с помощью групповой политики));
  
  - устройства, зарегистрированные в Intune вручную, то есть когда:
  
    - [Автоматическая регистрация в Intune](../enrollment/quickstart-setup-auto-enrollment.md) включена в Azure AD. Пользователь выполняет вход в устройство с использованием учетной записи локального пользователя, вручную присоединяет устройство к Azure AD, а затем выполняет вход в устройство, используя свою учетную запись Azure AD.
    
    ИЛИ  
    
    - пользователь выполняет вход на устройство с помощью своей учетной записи Azure AD и регистрирует его в Intune;

  - совместно управляемые устройства, использующие Configuration Manager и Intune. Убедитесь, что для рабочей нагрузки **Приложения** выбрано значение **Pilot Intune** (Пилотная версия Intune) или **Intune**. Дополнительные сведения см. в следующих статьях: 
  
    - [Что такое совместное управление?](https://docs.microsoft.com/configmgr/comanage/overview) 
    - [Клиентские приложения](https://docs.microsoft.com/configmgr/comanage/workloads#client-apps)
    - [Переключение рабочих нагрузок Configuration Manager на Intune](https://docs.microsoft.com/configmgr/comanage/how-to-switch-workloads)
  
> [!NOTE]
> Дополнительные сведения об использовании виртуальных машин Window 10 см. в разделе [Использование виртуальных машин Windows 10 с Intune](../fundamentals/windows-10-virtual-machines.md).

## <a name="create-a-script-policy-and-assign-it"></a>Создание и назначение политики скрипта

1. Войдите в [Центр администрирования Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Выберите **Устройства** > **Сценарии PowerShell** > **Добавить**.

    ![Добавление и использование скрипов PowerShell в Microsoft Intune](./media/intune-management-extension/mgmt-extension-add-script.png)

3. В разделе **Основные** укажите следующие свойства и нажмите **Далее**.
    - **Имя** — Введите имя скрипта PowerShell. 
    - **Описание**. Введите описание скрипта PowerShell. Этот параметр является необязательным, но мы рекомендуем его использовать.
4. В разделе **Параметры скрипта** укажите следующие свойства и нажмите **Далее**.
    - **Расположение скрипта**. Укажите расположение скрипта PowerShell. Размер скрипта не должен превышать 200 КБ (ASCII).
    - **Запускать сценарий по учетным данным**. Выберите **Да**, чтобы запускать скрипт с помощью учетных данных пользователя на устройстве. Выберите **Нет** (по умолчанию) для запуска скрипта в контексте системы. Многие администраторы выбирают **Да**. Выберите **Нет**, если скрипт требуется запускать в контексте системы.
    - **Принудительно проверить подпись сценария**. Выберите **Да**, если скрипт должен быть подписан доверенным издателем. Выберите **Нет** (по умолчанию), если требование к подписыванию скрипта отсутствует. 
    - **Запуск скрипта на 64-разрядном узле PowerShell**. Выберите **Да** для запуска скрипта на 64-разрядном узле PowerShell (PS) в 64-разрядной архитектуре клиента. Выберите **Нет** (по умолчанию) для запуска скрипта на 32-разрядном узле PowerShell.

      При выборе значения **Да** или **Нет** используйте следующую таблицу для нового и существующего поведения политики.

      | Запуск скрипта на 64-разрядном узле PS | Архитектура клиента | Новый скрипт PS | Существующий скрипт политики PS |
      | --- | --- | --- | --- | 
      | Нет | 32-разрядная система  | Поддерживается 32-разрядный узел PS | Скрипт запускается только на 32-разрядном узле PS, который работает в 32- и 64-разрядных архитектурах. |
      | Да | 64-разрядная система | Скрипт запускается на 64-разрядном узле PS для 64-разрядных архитектур. Если запуск выполнялся в 32-разрядной системе, скрипт запускается на 32-разрядном узле PS. | Скрипт запускается на 32-разрядном узле PS. При изменении значения этого параметра на 64-разрядную версию скрипт открывается (не запускается) на 64-разрядном узле PS и выводит результаты. Если запуск выполнялся в 32-разрядной системе, скрипт запускается на 32-разрядном узле PS. |

5. Щелкните **Область (теги)** . Теги области являются необязательными. Дополнительные сведения см. в разделе [Использование управления доступом на основе ролей (RBAC) и тегов области для распределенных ИТ](../fundamentals/scope-tags.md).

    Добавление тега области

    1. Щелкните **Выбрать теги области** > выберите в списке существующий тег области > **Выбрать**.

    2. Когда закончите, нажмите **Далее**.

6. Выберите пункты **Назначения** > **Выберите группы для включения**. Отобразится существующий список групп Azure AD.

    1. Выберите одну или несколько групп пользователей, чьи устройства получат скрипт. Щелкните **Выбрать**. Выбранные группы отображаются в списке и получат вашу политику.

        > [!NOTE]
        > Скрипты PowerShell в Intune могут назначаться группам безопасности устройств или группам безопасности пользователей Azure AD.

    2. Выберите **Далее**.

        ![Назначение или развертывание скрипта PowerShell для групп устройств в Microsoft Intune](./media/intune-management-extension/mgmt-extension-assignments.png)

7. В окне **Проверка и добавление** отображается сводка по настроенным параметрам. Выберите **Добавить**, чтобы сохранить сценарий. При нажатии кнопки **Добавить** политика развертывается в выбранных группах.

## <a name="important-considerations"></a>Важные замечания

- Если для скриптов задан пользовательский контекст и пользователь имеет права администратора, скрипт PowerShell по умолчанию запускается с правами администратора.

- Конечным пользователям не требуется выполнять вход на устройство для выполнения скриптов PowerShell.

- Агент расширения управления Intune сверяется с Intune каждый час и после каждой перезагрузки, чтобы получить новые скрипты или изменения. После назначения политики группам Azure AD выполняется скрипт PowerShell, после чего выводятся результаты выполнения. Последующее выполнение скрипта происходит только при изменении скрипта или политики. Если произойдет сбой выполнения скрипта, агент расширения управления Intune попытается трижды повторить запуск скрипта при трех следующих синхронизациях этого агента.

- Для общих устройств сценарий PowerShell выполняется для каждого нового пользователя, который входит в систему.

### <a name="failure-to-run-script-example"></a>Пример сбоя выполнения скрипта
08:00
  -  Синхронизация
  -  Запуск скрипта **ConfigScript01**
  -  Сбой выполнения скрипта

09:00
  -  Синхронизация
  -  Запуск скрипта **ConfigScript01**
  -  Сбой выполнения скрипта (число повторных попыток = 1)

10:00
  -  Синхронизация
  -  Запуск скрипта **ConfigScript01**
  -  Сбой выполнения скрипта (число повторных попыток = 2)
  
11:00
  -  Синхронизация
  -  Запуск скрипта **ConfigScript01**
  -  Сбой выполнения скрипта (число повторных попыток = 3)

12:00
  -  Синхронизация
  - Повторные попытки запуска скрипта **ConfigScript01** не выполнялись.
  - Если в скрипт не вносятся изменения, дальнейшие попытки его запуска не предпринимаются.


## <a name="monitor-run-status"></a>Отслеживание состояния выполнения

На портале Azure можно отслеживать состояние выполнения сценариев PowerShell для пользователей и устройств.

В области **Скрипты PowerShell** выберите скрипт для отслеживания, а затем **Монитор** и один из следующих отчетов:

- **Состояние устройства**
- **Состояние пользователя**

## <a name="intune-management-extension-logs"></a>Журналы расширения управления Intune

Журналы агентов на клиентском компьютере обычно находятся в папке `\ProgramData\Microsoft\IntuneManagementExtension\Logs`. Для просмотра этих файлов журналов можно использовать [CMTrace.exe](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Снимок экрана или пример журналов агента cmtrace в Microsoft Intune](./media/apps-win32-app-management/apps-win32-app-10.png)  

## <a name="delete-a-script"></a>Удаление скрипта

В области **Скрипты PowerShell** щелкните скрипт правой кнопкой мыши и выберите пункт **Удалить**.

## <a name="common-issues-and-resolutions"></a>Распространенные проблемы и способы их устранения

### <a name="issue-intune-management-extension-doesnt-download"></a>Проблема. Не удается скачать расширение управления Intune

**Возможные решения**:

- Устройство не присоединено к Azure AD. Убедитесь, что устройства соответствуют [предварительным требованиям](#prerequisites) (в этой статье). 
- Нет скрипта PowerShell или приложения Win32, назначенного группам, к которым принадлежит пользователь или устройство.
- Устройство не может зарегистрироваться в службе Intune из-за отсутствия доступа к Интернету, отсутствия доступа к службам push-уведомлений Windows (WNS) и т. д.
- Устройство находится в режиме S. Расширение управления Intune не поддерживается на устройствах, работающих в режиме S. 

Чтобы узнать, зарегистрировано ли устройство автоматически, можно сделать следующее.

  1. Откройте **Учетные записи** > **Учетные записи** > **Доступ к рабочей или учебной учетной записи**.
  2. Выберите присоединенную учетную запись и щелкните **Информация**.
  3. В разделе **Расширенный диагностический отчет** выберите **Создать отчет**.
  4. В веб-браузере откройте `MDMDiagReport`.
  5. Найдите свойство **MDMDeviceWithAAD**. Если свойство существует, устройство зарегистрировано автоматически. Если такое свойство не существует, значит устройство не регистрируется автоматически.

В статье [Включение автоматической регистрации Windows 10](../enrollment/windows-enroll.md#enable-windows-10-automatic-enrollment) приведены действия по настройке автоматической регистрации в Intune.

### <a name="issue-powershell-scripts-do-not-run"></a>Проблема. Скрипты PowerShell не выполняются

**Возможные решения**:

- Скрипты PowerShell не выполняются при каждом входе в систему. Они выполняются в следующих случаях:

  - когда скрипт назначается устройству;
  - когда вы изменяете скрипт, загружаете его и назначаете пользователю или устройству.
  
    > [!TIP]
    > **Расширение управления Intune Microsoft** — это служба, которая выполняется на устройстве, как и любая другая служба, указанная в приложении "Службы" (services.msc). После перезагрузки устройства эта служба может также перезапуститься и выполнить поиск назначенных скриптов PowerShell в службе Intune. Если для службы **Расширение управления Microsoft Intune** задан запуск вручную, то служба не может перезапуститься после перезагрузки устройства.

- Убедитесь, что устройства [присоединены к Azure AD](https://docs.microsoft.com/azure/active-directory/user-help/user-help-join-device-on-network). Устройства, которые присоединены только к вашему рабочему месту или организации ([зарегистрированы](https://docs.microsoft.com/azure/active-directory/user-help/user-help-register-device-on-network) в Azure AD), не получат скрипты.
- Клиент расширения управления Intune раз в час проверяет наличие изменений в скриптах или политиках Intune.
- Убедитесь, что расширение управления Intune скачано в папку `%ProgramFiles(x86)%\Microsoft Intune Management Extension`.
- Скрипты не выполняются в Surface Hub или в Windows 10 в режиме S.
- Проверьте журналы на наличие ошибок. См. раздел [Журналы расширения управления Intune](#intune-management-extension-logs) (в этой статье).
- Чтобы исключить проблемы с разрешениями, задайте `Run this script using the logged on credentials` в свойствах скрипта PowerShell. Также убедитесь, что выполнивший вход пользователь имеет нужные разрешения на выполнение скрипта.

- Чтобы определить проблемы со скриптами, сделайте следующее:

  - Проверьте конфигурацию выполнения PowerShell на устройствах. Инструкции см. в разделе [Политика выполнения PowerShell](https://docs.microsoft.com/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-6).
  - Запустите пример скрипта с помощью расширения управления Intune. Например, создайте каталог `C:\Scripts` и предоставьте всем полный доступ к нему. Выполните следующий сценарий:

    ```powershell
    write-output "Script worked" | out-file c:\Scripts\output.txt
    ```

    При успешном выполнении будет создан файл output.txt с текстом Script worked (Скрипт выполнен).

  - Чтобы проверить выполнение скриптов без Intune, запустите их в локальной системной учетной записи с помощью [средства psexec](https://docs.microsoft.com/sysinternals/downloads/psexec):

    `psexec -i -s`  
    
  - Если сообщается о выполнении скрипта, но скрипт не был выполнен, возможно, антивирусная служба изолирует AgentExecutor. Следующий скрипт всегда сообщает об ошибке в Intune. В качестве теста можно использовать следующий скрипт:
  
    ```powershell
    Write-Error -Message "Forced Fail" -Category OperationStopped
    mkdir "c:\temp" 
    echo "Forced Fail" | out-file c:\temp\Fail.txt
    ```

    Если сообщается о выполнении скрипта, проверьте `AgentExecutor.log`, чтобы подтвердить ошибку. При выполнении скрипта длина должна составлять > 2.

  - Для записи файлов .error и .output следующий фрагмент кода выполняет скрипт с помощью AgentExecutor для PSx86 (`C:\Windows\SysWOW64\WindowsPowerShell\v1.0`). При этом журналы сохраняются для проверки. Помните, что расширение управления Intune очищает журналы после выполнения скрипта:
  
    ```powershell
    $scriptPath = read-host "Enter the path to the script file to execute"
    $logFolder = read-host "Enter the path to a folder to output the logs to"
    $outputPath = $logFolder+"\output.output"
    $errorPath =  $logFolder+"\error.error"
    $timeoutPath =  $logFolder+"\timeout.timeout"
    $timeoutVal = 60000 
    $PSFolder = "C:\Windows\SysWOW64\WindowsPowerShell\v1.0"
    $AgentExec = "C:\Program Files (x86)\Microsoft Intune Management Extension\agentexecutor.exe"
    &$AgentExec -powershell  $scriptPath $outputPath $errorPath $timeoutPath $timeoutVal $PSFolder 0 0
    ```

## <a name="next-steps"></a>Дальнейшие шаги

[Мониторинг](../configuration/device-profile-monitor.md) и [устранение неполадок](../configuration/device-profile-troubleshoot.md) для профилей.
