---
title: Использование и обслуживание отчетов
titleSuffix: Configuration Manager
description: Сведения об управлении отчетами и подписками на отчеты в Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 5e154f2859a7541ac8f67b8588da7dfb8877c940
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694422"
---
# <a name="operations-and-maintenance-for-reporting-in-configuration-manager"></a>Использование и обслуживание отчетов в Configuration Manager

*Область применения: Configuration Manager (Current Branch)*

После создания инфраструктуры отчетов в Configuration Manager можно выполнить ряд операций, которые обычно используются для управления отчетами и подписками на отчеты.

> [!NOTE]
> В этой статье рассматриваются отчеты в SQL Server Reporting Services. Начиная с версии 2002, можно интегрировать отчеты с сервером отчетов Power BI. Дополнительные сведения см. в статье [Интеграция с сервером отчетов Power BI](powerbi-report-server.md).

## <a name="run-a-report-from-reporting-services"></a>Запуск отчета из Reporting Services

Configuration Manager использует службы SQL Server Reporting Services для хранения отчетов. Отчет получает данные из базы данных сайта Configuration Manager. Можно воспользоваться отчетами на консоли Configuration Manager или с помощью диспетчера отчетов с доступом через веб-браузер. Вы можете открывать отчеты в веб-браузере на любом компьютере, который имеет доступ к точке служб отчетов, если у пользователя достаточно прав для просмотра отчетов. Для запуска отчетов необходимо иметь права **Чтение** для разрешения **Сайт**, а также разрешение **Выполнить отчет** для определенных объектов.

При запуске отчета его название, описание и категория отображаются на языке локальной операционной системы. Дополнительные сведения см. в разделе [Языки отчетов](configuring-reporting.md#-languages-for-reports).

> [!NOTE]  
> Диспетчер отчетов — это веб-средство доступа к отчетам и управления ими. Его можно использовать для администрирования отдельного экземпляра сервера отчетов через HTTPS-соединение. Диспетчер отчетов можно использовать для таких задач, как просмотр отчетов, изменение свойств отчета, а также управление связанными подписками на отчет. В этой статье описаны действия по просмотру отчета и изменению свойств отчета в диспетчере отчетов. Дополнительные сведения о других возможностях диспетчера отчетов см. в разделе [Что такое диспетчер отчетов?](https://docs.microsoft.com/sql/reporting-services/report-manager-ssrs-native-mode)

Используйте следующие процедуры для запуска отчета Configuration Manager.

### <a name="run-a-report-in-the-configuration-manager-console"></a>Запуск отчета в консоли Configuration Manager

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**. Разверните **Отчетность** и выберите **Отчеты**. В этом узле перечислены доступные отчеты.

    > [!TIP]
    > Если отчеты в нем отсутствуют, убедитесь, что точка служб отчетов установлена и настроена. Дополнительные сведения см. в статье о [настройке отчетов](configuring-reporting.md).

1. Выберите отчет, который необходимо запустить. На вкладке ленты **Главная** в разделе **Группа отчетов** выберите **Выполнить**, чтобы открыть отчет.

1. Если есть обязательные параметры, укажите их, после чего щелкните **Просмотреть отчет**.

### <a name="run-a-report-in-a-web-browser"></a>Запуск отчета в веб-браузере

1. В браузере введите URL-адрес диспетчера отчетов, например `https://Server1/Reports`. Этот адрес есть на странице **URL-адрес диспетчера отчетов** в диспетчере конфигурации служб отчетов.

1. В диспетчере отчетов щелкните папку отчетов для Configuration Manager, например **ConfigMgr_CAS**.

    > [!TIP]
    > Если отчеты в диспетчере отчетов отсутствуют, убедитесь, что точка служб отчетов установлена и настроена. Дополнительные сведения см. в статье о [настройке отчетов](configuring-reporting.md).

1. Выберите категорию отчетов, содержащую требуемый отчет, после чего щелкните нужный отчет. Отчет откроется в диспетчере отчетов.

1. Если есть обязательные параметры, укажите их, после чего щелкните **Просмотреть отчет**.

## <a name="modify-the-properties-of-a-report"></a>Изменение свойств отчета

Свойства отчета включают имя и описание отчета. Вы можете просмотреть свойства отчета в консоли Configuration Manager.

Чтобы изменить свойства, используйте диспетчер отчетов.

1. В браузере введите URL-адрес диспетчера отчетов, например `https://Server1/Reports`.

1. В диспетчере отчетов щелкните папку отчетов для Configuration Manager, например **ConfigMgr_CAS**.

1. Выберите категорию отчета, а затем выберите конкретный отчет. Отчет откроется в диспетчере отчетов.

1. Выберите вкладку **Свойства**. Измените имя и описание отчет, а затем выберите **Применить**.

Диспетчер отчетов сохраняет свойства отчета на сервере отчетов. В консоли Configuration Manager отображаются обновленные свойства отчета.

## <a name="edit-a-report"></a><a name="bkmk_edit"></a> Изменение отчета

Если существующий отчет Configuration Manager не извлекает нужные сведения, измените его в построитель отчетов. Можно также использовать построитель отчетов для изменения макета или дизайна отчета. Хотя отчет по умолчанию можно редактировать напрямую, его лучше клонировать. Откройте отчет для изменения и выберите **Сохранить как**.

Чтобы изменить отчет, необходимы разрешения **Изменить сайт** и **Изменить отчет** для конкретных объектов отчета.

> [!IMPORTANT]
> При обновлении сайта встроенные отчеты сохраняются. При изменении стандартного отчета и обновлении сайта отчет переименовывается с добавлением символа подчеркивания в качестве префикса (`_`). Такое поведение гарантирует, что при обновлении сайта измененный отчет не перезапишется стандартным.
>
> При изменении предварительно определенных отчетов перед установкой обновления сайта создайте резервную копию пользовательских отчетов. После обновления восстановите отчет в Reporting Services. Если в предустановленный отчет вносятся значительные изменения, рекомендуется вместо этого создать новый отчет. Новые отчеты, созданные перед обновлением сайта, не перезаписываются.

Выполните следующую процедуру, чтобы изменить свойства отчета Configuration Manager.

1. В консоли Configuration Manager перейдите в рабочую область **Мониторинг**. Разверните **Отчетность** и выберите узел **Отчеты**.

1. Выберите отчет, который необходимо изменить. На вкладке ленты **Главная** в разделе **Группа отчетов** выберите **Изменить**. Может появиться запрос на ввод учетных данных. Если построитель отчетов не установлен на компьютере, Configuration Manager предложит установить его. Построитель отчетов необходим для изменения и создания отчетов.

1. В построителе отчетов измените соответствующие параметры отчета. Нажмите кнопку **Сохранить** для сохранения отчета на сервере отчетов.

## <a name="create-reports"></a>создание отчетов

Можно создавать отчеты двух типов.

- **Отчет на основе модели** позволяет интерактивно выбирать элементы, которые требуется включить в отчет. Дополнительные сведения о создании моделей отчетов см. в статье [Создание моделей пользовательских отчетов для Configuration Manager в службах SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).

- **Отчет на основе SQL** позволяет принимать данные, основанные на выражении SQL.

> [!IMPORTANT]
> Вашей учетной записи необходимо разрешение на **Изменение сайтов**, чтобы создать новый отчет. Вы можете создавать отчеты только в папках, для которых у вас есть разрешение на **Изменение отчетов**.

### <a name="create-a-model-based-report"></a>Создание отчета на основе модели

Ниже приведена процедура создания и отчета Configuration Manager на основе модели.

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты**, и выберите узел **Отчеты**.

1. На вкладке **Главная** на ленте в разделе **Создать** выберите **Создать отчет**. Это действие открывает **мастер создания отчетов**.

1. На странице **Сведения** настройте следующие параметры.

    - **Тип** — выберите **Отчет на основе модели**.

    - **Имя** — Укажите имя отчета.

    - **Описание**. Укажите описание отчета.

    - **Сервер**. Отображает имя сервера отчетов, на котором создается этот отчет.

    - **Путь**. Щелкните **Обзор**, чтобы указать папку, в которой будет сохранен отчет.

1. На странице **Выбор модели** выберите в списке доступную модель для создания этого отчета. В разделе **Предварительный обзор** отображаются представления SQL Server и сущности, доступные в этой модели отчета.

1. Завершите работу мастера создания отчетов.

1. Откройте построитель отчетов, чтобы настроить параметры отчета. Дополнительные сведения см. в статье [Запуск отчета Configuration Manager](#bkmk_edit).

1. В построителе отчетов можно создать макет отчета, выбрать данные в списке доступных представлений SQL Server и добавить параметры отчета.

1. Нажмите кнопку **Запустить**, чтобы выполнить отчет. Убедитесь, что отчет содержит ожидаемые сведения. При необходимости выберите **Проектирование**, чтобы изменить отчет.

1. Нажмите кнопку **Сохранить** для сохранения отчета на сервере отчетов.

### <a name="create-a-sql-based-report"></a>Создание отчета на основе SQL

При создании SQL-оператора для настраиваемого отчета не используйте прямые ссылки на таблицы SQL Server. Всегда ссылайтесь на поддерживаемые представления отчетов SQL Server из базы данных сайта. Эти представления имеют имена, начинающиеся с `v_`. Дополнительные сведения см. в разделе [Создание пользовательских отчетов с помощью представлений SQL Server в Configuration Manager](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

Можно также ссылаться на общие хранимые процедуры из базы данных сайта. Эти хранимые процедуры имеют имена, начинающиеся с `sp_`.

Ниже приведена процедура создания и отчета Configuration Manager на основе SQL.

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты**, и выберите узел **Отчеты**.

1. На вкладке **Главная** на ленте в разделе **Создать** выберите **Создать отчет**. Это действие открывает **мастер создания отчетов**.

1. На странице **Сведения** настройте следующие параметры.

    - **Тип** — выберите **Отчет на основе SQL**.

    - **Имя** — Укажите имя отчета.

    - **Описание**. Укажите описание отчета.

    - **Сервер**. Отображает имя сервера отчетов, на котором создается этот отчет.

    - **Путь**. Щелкните **Обзор**, чтобы указать папку, в которой будет сохранен отчет.

1. Завершите работу мастера создания отчетов.

1. Откройте построитель отчетов, чтобы настроить параметры отчета. Дополнительные сведения см. в статье [Запуск отчета Configuration Manager](#bkmk_edit).

1. В построителе отчетов укажите инструкцию SQL для отчета. Можно также создать инструкцию SQL, используя столбцы в доступных представлениях. При необходимости добавьте параметры в отчет.

1. Нажмите кнопку **Запустить**, чтобы выполнить отчет. Убедитесь, что отчет содержит ожидаемые сведения. При необходимости выберите **Проектирование**, чтобы изменить отчет.

1. Нажмите кнопку **Сохранить** для сохранения отчета на сервере отчетов.

## <a name="manage-report-subscriptions"></a><a name="bkmk_subscription"></a> Управление подписками на отчеты

Подписки на отчеты в SQL Server Reporting Services позволяют настраивать автоматическую доставку указанных отчетов по электронной почте или в хранилище файлов в соответствии с установленными временными интервалами. Используйте **мастер создания подписки** в Configuration Manager для настройки подписок на отчеты.

### <a name="create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Создание подписки на отчет для доставки отчета в общую папку

При создании подписки на отчет с целью доставки отчета в общую папку службы Reporting Services копируют отчет в указанном формате в назначенную общую папку. Можно подписаться и запросить доставку только для одного отчета.

При создании подписки, использующей общую папку, укажите в качестве папки назначения существующую общую папку. Сервер отчетов не создает обычную или сетевую папку. При указании папки назначения в подписке следует использовать UNC-путь, который не должен содержать символов обратной косой черты (`\`). Например, правильный UNC-путь папки назначения может иметь следующий вид: `\\server\reportfiles\operations\2001`.

> [!NOTE]
> При создании подписки необходимо указать имя пользователя и пароль. Этой учетной записи требуется доступ к этой общей папке с разрешением на **запись** в целевую папку.

Службы Reporting Services могут формировать отчеты в различных форматах файлов. Например, MHTML или Excel. Формат выбирается при создании подписки. Хотя можно выбрать любой поддерживаемый формат, некоторые форматы больше подходят для сохранения отчетов в файл, чем другие.

### <a name="limitations-for-report-subscriptions-to-a-file-share"></a>Ограничения для подписки на отчеты в общей папке

В следующем списке перечислены ограничения подписок на отчеты в общей папке.

- В отличие от отчетов, размещаемых на сервере отчетов и управляемых им, службы Reporting Services доставляют отчеты в общую папку в виде статических файлов.

- Интерактивные функции отчета для отчетов, хранящихся в виде файлов, не работают. Отчет представляет все интерактивные функции в виде статических элементов.

- Если отчет включает диаграммы, используется представление по умолчанию.

- Если в отчете есть ссылка на другой отчет, она отображается в виде статичного текста.

Чтобы сохранить интерактивные возможности в доставляемом отчете, используйте доставку по электронной почте. Дополнительные сведения см. в разделе [Создание подписки на отчет с доставкой по электронной почте](#bkmk_subscription-email).

### <a name="process-to-create-a-report-subscription-for-a-file-share"></a>Процесс создания подписки на отчет в общей папке

Следующая процедура позволяет создать подписку на отчет с целью доставки отчета в общую папку.  

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты**, и выберите узел **Отчеты**.

1. Выберите папку отчетов, а затем выберите отчет, на который необходимо подписаться. На вкладке ленты **Главная** в разделе **Группа отчетов** выберите **Создать подписку**. Это действие открывает **мастер создания подписки**.

1. На странице **Доставка подписки** настройте следующие параметры.  

    - **Способ доставки отчета**. Выберите **Общая папка Windows**.

    - **Имя файла**. Укажите имя файла для отчета. По умолчанию у имени файла отчета отсутствует расширение. Выберите **Добавлять расширение файла при создании**, чтобы автоматически добавлять расширение имени файла в зависимости от формата.

    - **Путь**. Укажите UNC-путь к существующей папке, в которую должен доставляться отчет. Например, `\\server\reportfiles\operations`.

    - **Формат отображения**. Укажите один из следующих форматов файла отчета:

      - **XML-файл с данными отчета**
      - **CSV-файл (разделители-запятые)**
      - **TIFF-файл**
      - **Файл Acrobat (PDF)**
      - **HTML 4.0**
        > [!NOTE]
        > Если в отчете есть изображения, формат HTML 4,0 не включает их.
      - **MHTML (веб-архив)**
      - **Модуль подготовки RPL** (макет страницы отчета)
      - **Excel**
      - **Word**

    - **Имя пользователя**. Укажите учетную запись пользователя Windows с разрешениями на *запись* для указанного **пути**.

    - **Пароль**. Введите пароль указанной учетной записи пользователя Windows.

    - **Параметр перезаписи**. Выберите один из следующих параметров для настройки поведения в случае, если в конечной папке уже есть файл с указанным именем.

      - **Перезаписать существующий файл более новым**
      - **Не перезаписывать существующий файл**
      - **Дополнять имена файлов числами при добавлении более новых версий**. Этот параметр добавляет номер к имени файла нового отчета, чтобы отличать его от более ранних версий.

    - **Описание**. При необходимости укажите дополнительные сведения об этой подписке на отчет.

1. На странице **Расписание подписки** выберите один из следующих вариантов расписания доставки для подписки на отчет.

    - **Использовать общее расписание**. Общее расписание — это заранее определенное расписание, которое может использоваться другими подписками на отчеты. При выборе этого параметра также выбирается общее расписание. Если общие расписания отсутствуют, выберите этот параметр, чтобы создать новое расписание.

    - **Создать новое расписание**. Настройте расписание, в соответствии с которым запускается этот отчет. Расписание включает интервал, дату и время начала, а также дату окончания для подписки. По умолчанию новая подписка создает новое расписание для ежечасного запуска начиная с текущей даты и времени.

1. На странице **Свойства подписки** укажите параметры отчета, необходимые при его автоматическом выполнении. Если в отчете нет параметров, мастер не отображает эту страницу.

1. Завершите работу мастера.

1. Убедитесь, что Configuration Manager успешно создал подписку на отчет. Чтобы просмотреть и изменить подписки на отчеты, выберите узел **Подписки**.

### <a name="create-a-report-subscription-to-deliver-a-report-by-email"></a><a name="bkmk_subscription-email"></a> Создание подписки на отчет для доставки отчета по электронной почте

При создании подписки на отчет с доставкой по электронной почте Reporting Services отправляют сообщение электронной почты указанным получателям. Сообщение электронной почты включает отчет в виде вложения. Сервер отчетов не проверяет адреса электронной почты и не получает их с почтового сервера. Отчеты можно направлять на любые действительные адреса внутри или за пределами организации.

> [!NOTE]
> Чтобы включить параметр подписки **Электронная почта**, необходимо настроить параметры электронной почты в Reporting Services. Дополнительные сведения см. в разделе [Доставка по электронной почте в службах Reporting Services](https://docs.microsoft.com/sql/reporting-services/subscriptions/e-mail-delivery-in-reporting-services).

Можно выбрать один или оба варианта доставки по электронной почте.

- Отправьте уведомление со ссылкой на созданный отчет.

- Отправьте внедренный или прикрепленный отчет. Формат визуализации и браузер определяют, является ли отчет внедренным или прикрепленным.

  - Если браузер поддерживает HTML 4.0 и MHTML и выбран вариант визуализации **MHTML (веб-архив)** , отчет внедряется в сообщение.
  - Все остальные форматы доставляют отчеты в виде вложений.
  - Службы Reporting Services не проверяют размер вложения и сообщения перед отправкой. Если размер вложения или сообщения превышает максимальный предел, разрешенный почтовым сервером пользователя, отчет доставлен не будет.

Следующая процедура позволяет создать подписку на отчет с целью доставки отчета по электронной почте.  

1. В консоли Configuration Manager перейдите к рабочей области **Наблюдение**, разверните пункт **Отчеты**, и выберите узел **Отчеты**.

1. Выберите папку отчетов, а затем выберите отчет, на который необходимо подписаться. На вкладке ленты **Главная** в разделе **Группа отчетов** выберите **Создать подписку**. Это действие открывает **мастер создания подписки**.

1. На странице **Доставка подписки** настройте следующие параметры.  

    - **Способ доставки отчета**. Выберите **Электронная почта**.

    - **Кому**. Укажите допустимый адрес электронной почты получателя.

        > [!NOTE]
        > Можно указать несколько получателей, разделив их адреса точкой с запятой (`;`).

    - **Копия**. При необходимости укажите адрес электронной почты для получения копии этого отчета.

    - **Скрытая копия**. При необходимости укажите адрес электронной почты для получения скрытой копии этого отчета.

    - **Ответить**. Укажите адрес ответа. Если пользователь ответит на сообщение, ответ будет отправлен на этот адрес.

    - **Тема**. Укажите тему сообщения электронной почты о подписке.

    - **Приоритет**. Установите флаг приоритета для этого сообщения электронной почты. **Низкий**, **нормальный** или **высокий**. Microsoft Exchange использует этот флаг, чтобы указать важность сообщения электронной почты.

    - **Комментарий**. Укажите текст сообщения о подписке.

    - **Описание**. При необходимости укажите дополнительные сведения об этой подписке на отчет.

    - **Включить ссылку**. Включите URL-адрес этого отчета в текст сообщения электронной почты.

    - **Включить отчет**. Присоединение отчета к сообщению электронной почты. Используйте параметр **Формат отображения**, чтобы указать формат отчета для присоединения.

    - **Формат отображения**. Выберите один из следующих форматов вложенного файла отчета.

      - **XML-файл с данными отчета**
      - **CSV-файл (разделители-запятые)**
      - **TIFF-файл**
      - **Файл Acrobat (PDF)**
      - **MHTML (веб-архив)**
      - **Excel**
      - **Word**

1. На странице **Расписание подписки** выберите один из следующих вариантов расписания доставки для подписки на отчет.

    - **Использовать общее расписание**. Общее расписание — это заранее определенное расписание, которое может использоваться другими подписками на отчеты. При выборе этого параметра также выбирается общее расписание. Если общие расписания отсутствуют, выберите этот параметр, чтобы создать новое расписание.

    - **Создать новое расписание**. Настройте расписание, в соответствии с которым запускается этот отчет. Расписание включает интервал, дату и время начала, а также дату окончания для подписки. По умолчанию новая подписка создает новое расписание для ежечасного запуска начиная с текущей даты и времени.

1. На странице **Свойства подписки** укажите параметры отчета, необходимые при его автоматическом выполнении. Если в отчете нет параметров, мастер не отображает эту страницу.

1. Завершите работу мастера.

1. Убедитесь, что Configuration Manager успешно создал подписку на отчет. Чтобы просмотреть и изменить подписки на отчеты, выберите узел **Подписки**.