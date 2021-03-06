---
title: Руководство по пакету SDK для приложений Intune для разработчиков под Android
description: Пакет SDK для приложений Microsoft Intune для Android позволяет встроить в ваше приложение Android функции управления мобильными приложениями (MAM).
keywords: Пакет SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/02/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 0100e1b5-5edd-4541-95f1-aec301fb96af
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 71d5efbf8b61c08e9a2edbc5312c61279571339e
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "80620560"
---
# <a name="microsoft-intune-app-sdk-for-android-developer-guide"></a>Руководство по пакету SDK для приложений Intune для разработчиков под Android

> [!NOTE]
> При желании прочтите статью [Обзор пакета SDK для приложений Intune](app-sdk.md), в которой рассмотрены актуальные функции пакета SDK и описана подготовка к интеграции на каждой поддерживаемой платформе.
>
> Инструкции по скачиванию пакета SDK см. в [этой статье](../developer/app-sdk-get-started.md#download-the-sdk-files).

Пакет SDK для приложений Microsoft Intune для Android позволяет встроить в ваше собственное приложение для Android **политики защиты приложений — APP** (или политики управления мобильными приложениями — MAM). В управляемое приложение Intune интегрирован пакет SDK для приложений Intune. Администраторы Intune могут развертывать политики защиты приложений в вашем управляемом приложении Intune, когда Intune активно управляет им.


## <a name="whats-in-the-sdk"></a>Состав пакета SDK

Пакет SDK для приложений Intune состоит из следующих файлов:

* **Microsoft.Intune.MAM.SDK.aar**. Компоненты пакета SDK, за исключением JAR-файлов библиотеки поддержки.
* **Microsoft.Intune.MAM.SDK.Suppилиt.v4.jar**: Обязательные классы для включения MAM в приложениях, использующих библиотеку поддержки Android версии 4.
* **Microsoft.Intune.MAM.SDK.Suppилиt.v7.jar**: Обязательные классы для включения MAM в приложениях, использующих библиотеку поддержки Android версии 7.
* **Microsoft.Intune.MAM.SDK.Support.v17.jar**. Обязательные классы для включения MAM в приложениях, использующих библиотеку поддержки Android версии 17. 
* **Microsoft.Intune.MAM.SDK.Support.Text.jar**. Обязательные классы для включения MAM в приложениях, использующих классы библиотеки поддержки Android в пакете `android.support.text`.
* **Microsoft.Intune.MAM.SDK.DownlevelStubs.aar**. Этот AAR-файл содержит заглушки для системных классов Android, которые имеются только на новых устройствах, но на которые ссылаются методы `MAMActivity`. Более новые устройства будут пропускать эти классы заглушек. Этот AAR-файл необходим только в том случае, если приложение выполняет отражение в классах, производных от `MAMActivity`, и его не требуется включать в большинство приложений. AAR содержит правила ProGuard для исключения всех его классов.
* **com.microsoft.intune.mam.build.jar**. Подключаемый модуль Gradle, который [помогает в интеграции пакета SDK](#build-tooling).
* **CHANGELOG.txt**. Содержит сведения об изменениях во всех версиях пакета SDK.
* **THIRDPARTYNOTICES.TXT**.  Примечание об атрибуции, где указан сторонний код и (или) код OSS, который будет скомпилирован в вашем приложении.

## <a name="requirements"></a>Requirements (Требования)

### <a name="android-versions"></a>Версии Android
Пакет SDK поддерживает API Android от версии 19 (Android 4.4+) до версии 28 (Android 9.0).

### <a name="company-portal-app"></a>Приложение корпоративного портала
Для включения политик защиты приложений пакету SDK для приложений Intune для Android требуется наличие на устройстве приложения [корпоративного портала](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). Корпоративный портал извлекает политики защиты приложения из службы Intune. При инициализации приложения политики и код загружаются для реализации этой политики на корпоративном портале.

> [!NOTE]
> Если приложение корпоративного портала отсутствует на устройстве, управляемое приложение Intune будет работать так же, как обычное приложение, не поддерживающее политики защиты приложений Intune.

Чтобы включить защиту приложений без регистрации устройства, пользователю _**не**_ нужно регистрировать устройство с помощью приложения корпоративного портала.

## <a name="sdk-integration"></a>Интеграция пакета SDK

### <a name="sample-app"></a>Пример приложения
Пример того, как правильно интегрировать пакет SDK для приложений Intune, доступен на [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Android-App). В этом примере используется [подключаемый модуль сборки Gradle](#gradle-build-plugin).

### <a name="referencing-intune-app-libraries"></a>Ссылки на библиотеки приложений Intune

Пакет SDK для приложений Intune — это стандартная библиотека Android без внешних зависимостей. **Microsoft.Intune.MAM.SDK.aar** содержит оба интерфейса, необходимых для включения политики защиты приложений, а также код, требующийся для взаимодействия с приложением "Корпоративный портал" Microsoft Intune.

**Microsoft.Intune.MAM.SDK.aar** нужно указать как ссылку на библиотеки Android. Чтобы сделать это, откройте проект приложения в Android Studio и выберите **File > New > New module** (Файл > Создать > Новый модуль), а затем щелкните **Import .JAR/.AAR Package** (Импорт пакета .JAR/AAR). После этого выберите наш пакет Android с архивом Microsoft.Intune.MAM.SDK.aar, чтобы создать модуль для AAR. Щелкните правой кнопкой мыши модуль или модули, содержащие код приложения, и выберите **Параметры модуля** > **Вкладка "Зависимости"**  > **Значок +**  > **Зависимость модуля**, а затем выберите только что созданный модуль AAR пакета SDK для MAM и нажмите кнопку **OK**. Это обеспечит компиляцию модуля с пакетом SDK для MAM при сборке проекта.

Кроме того, библиотеки **Microsoft.Intune.MAM.SDK.Support.XXX.jar**, содержат варианты Intune соответствующих библиотек `android.support.XXX`. Они не встраиваются в Microsoft.Intune.MAM.SDK.aar, если приложение не должно зависеть от библиотек поддержки.

#### <a name="proguard"></a>ProGuard

Если на этапе сборки используется [ProGuard](http://proguard.sourceforge.net/) (или любой другой механизм сжатия или маскировки), пакет SDK содержит дополнительные правила настройки, которые должны быть включены. При включении AAR-файлов в сборку наши правила автоматически применяются при использовании ProGuard, а необходимые файлы классов сохраняются.

Для библиотек ADAL могут быть предусмотрены собственные ограничения ProGuard. Если приложение включает ADAL, необходимо следовать инструкциям из документации по ADAL в отношении этих ограничений.

### <a name="policy-enforcement"></a>Принудительное применение политик
Пакет SDK для приложений Intune представляет собой библиотеку Android, благодаря которой приложение может поддерживать применение политик Intune и участвовать в этом процессе. 

Для применения некоторых политик требуется [явное участие приложения](#enable-features-that-require-app-participation), однако большинство политик применяется полуавтоматически.
Если вы выполняете интеграцию с источником или используете средства сборки для интеграции, необходимо закодировать политики, требующие явного участия.

Для политик, которые применяются автоматически, требуется, чтобы приложения заменили наследование от нескольких базовых классов Android на наследование от эквивалентных классов MAM, а также требуется аналогичная замена вызовов определенных классов системных служб Android на вызовы эквивалентных классов MAM. Конкретные требуемые замены подробно описаны [ниже](#class-and-method-replacements) и могут быть выполнены вручную при интеграции с источником или автоматически с помощью средств сборки.

### <a name="build-tooling"></a>Средства разработки
Пакет SDK предоставляет средства сборки (подключаемый модуль для сборок Gradle и средство командной строки для сборок, отличных от Gradle), которые осуществляют замены на эквивалентные классы MAM автоматически. Эти средства преобразуют файлы классов, созданные компиляцией Java, и не изменяют первоначальный исходный код.

Средства выполняют только [прямые замены](#class-and-method-replacements). Они не реализуют сложные интеграции пакета SDK, такие как [сохранение в виде политики](#enable-features-that-require-app-participation), [множественные удостоверения](#multi-identity-optional), [регистрация App-WE](#app-protection-policy-without-device-enrollment), [изменения AndroidManifest](#manifest-replacements) или [конфигурация ADAL](#configure-azure-active-directory-authentication-library-adal), поэтому эти процедуры должны быть завершены до включения полной поддержки приложения в Intune. Внимательно изучите остальную часть этой документации, посвященную точкам интеграции для приложения.

> [!NOTE]
> Рекомендуется запускать средства в проекте, в котором уже выполнена частичная или полная интеграция пакета SDK для MAM путем замен вручную. Проект по-прежнему должен содержать пакет SDK для MAM как зависимость.

### <a name="gradle-build-plugin"></a>Подключаемый модуль сборки Gradle
Если сборка приложения выполняется без Gradle, перейдите к разделу [Интеграция с помощью средства командной строки](#command-line-build-tool). 

Подключаемый модуль пакета SDK для приложений распространяется в составе пакета SDK в виде **GradlePlugin/com.microsoft.intune.mam.build.jar**. Чтобы Gradle мог найти подключаемый модуль, его необходимо добавить в путь к классу buildscript. Подключаемый модуль зависит от [Javassist](https://jboss-javassist.github.io/javassist/), который также необходимо добавить. Чтобы добавить их в путь к классу, добавьте следующее в корневой каталог `build.gradle`

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.javassist:javassist:3.22.0-GA"
        classpath files("$PATH_TO_MAM_SDK/GradlePlugin/com.microsoft.intune.mam.build.jar")
    }
}
```

Затем в файле `build.gradle` проекта APK просто примените этот подключаемый модуль как
```groovy
apply plugin: 'com.microsoft.intune.mam'
```

По умолчанию подключаемый модуль будет работать **только** с зависимостями `project`.
Проверка компиляции не затрагивается. Может предоставляться конфигурация для перечисления следующих компонентов:
*  исключаемые проекты;
*  [включаемые внешние зависимости](#usage-of-includeexternallibraries); 
*  определенные классы, которые следует исключить из обработки;
*  варианты, исключаемые из обработки. Они могут ссылаться на полное имя варианта или на один вкус. Например:
     * если приложение имеет типы сборки `debug` и `release` с вкусами {`savory`, `sweet`} и {`vanilla`, `chocolate`}, можно указать
     * `savory`, чтобы исключить все варианты с пикантным вкусом, или `savoryVanillaRelease`, чтобы исключить только именно этот вариант.

#### <a name="example-partial-buildgradle"></a>Пример частичного build.gradle

```groovy

apply plugin: 'com.microsoft.intune.mam'

dependencies {
    implementation project(':product:FooLib')
    implementation project(':product:foo-project')
    implementation fileTree(dir: "libs", include: ["bar.jar"])
    implementation fileTree(dir: "libs", include: ["zap.jar"])
    implementation "com.contoso.foo:zap-artifact:1.0.0"
    implementation "com.microsoft.bar:baz:1.0.0"
    implementation "com.microsoft.qux:foo:2.0"

    // Include the MAM SDK
    implementation files("$PATH_TO_MAM_SDK/Microsoft.Intune.MAM.SDK.aar")
}
intunemam {
    excludeProjects = [':product:FooLib']
    includeExternalLibraries = ['bar.jar', "com.contoso.foo:zap-artifact", "com.microsoft.*", "!com.microsoft.qux*"]
    excludeClasses = ['com.contoso.SplashActivity']
    excludeVariants=['savory']
}
```

Будут получены следующие результаты:
* `:product:FooLib` не переписывается, так как он включен в `excludeProjects`;
* `:product:foo-project` переписывается, за исключением `com.contoso.SplashActivity`, который пропускается, так как находится в `excludeClasses`;
* `bar.jar` переписывается, так как он включен в `includeExternalLibraries`;
* `zap.jar`**не** переписывается, так как он не является проектом и не включен в `includeExternalLibraries`;
* `com.contoso.foo:zap-artifact:1.0.0` переписывается, так как он включен в `includeExternalLibraries`;
* `com.microsoft.bar:baz:1.0.0` переписывается, так как он включен в `includeExternalLibraries` с помощью подстановочного знака (`com.microsoft.*`).
* `com.microsoft.qux:foo:2.0` не перезаписывается, несмотря на то, что он соответствует тому же подстановочному знаку, что и предыдущий элемент, так как он явно исключен через шаблон отрицания.

#### <a name="usage-of-includeexternallibraries"></a>Использование includeExternalLibraries

Поскольку подключаемый модуль работает только с зависимостями проекта (обычно предоставляемыми функцией `project()`) по умолчанию, все зависимости, указанные `fileTree(...)` или полученные из Maven или других источников пакетов (например, "`com.contoso.bar:baz:1.2.0`"), должны быть представлены свойству `includeExternalLibraries`, если требуется обработка MAM на основе условий, описанных ниже. Поддерживаются подстановочные знаки ("*"). Элемент, начинающийся с `!`, является отрицанием и позволяет исключить библиотеки, которые в противном случае должны быть включены с помощью подстановочного знака.

При указании внешних зависимостей с помощью нотации артефакта рекомендуется пропустить компонент версии в значении `includeExternalLibraries`. Если вы указываете версию, она должна быть точной. Динамические спецификации версий (например, `1.+`) не поддерживаются.

Общее правило, используемое для определения необходимости включения библиотеки в `includeExternalLibraries`, основано на двух вопросах:
1. Есть ли в библиотеке классы, для которых существуют эквиваленты MAM? Примеры: `Activity`, `Fragment`, `ContentProvider`, `Service` и т. д.
2. Если да, используются ли эти классы в приложении?

Если на оба вопроса дан ответ "Да", необходимо включить эту библиотеку в `includeExternalLibraries`. 

| Сценарий | Нужно включать? |
|--|--|
| Вы включаете библиотеку средства просмотра PDF-файлов в свое приложение и используете средство просмотра `Activity` в приложении, когда пользователи пытаются просматривать PDF-файлы. | Да |
| Вы включаете библиотеку HTTP в приложение для повышения веб-производительности. | Нет |
| Вы включаете библиотеку, например React Native, которая содержит классы, производные от `Activity`, `Application` и `Fragment`, и используете или далее наследуете эти классы в приложении. | Да |
| Вы включаете библиотеку, например React Native, которая содержит классы, производные от `Activity`, `Application` и `Fragment`, но используете только статические вспомогательные классы или служебные классы. | Нет |
| Вы включаете библиотеку, которая содержит классы представления, производные от `TextView`, и используете или далее наследуете эти классы в приложении. | Да |

#### <a name="reporting"></a>Отчеты
Подключаемый модуль сборки может создать HTML-отчет об изменениях, которые он создает. Чтобы запросить создание этого отчета, укажите `report = true` в блоке конфигурации `intunemam`. Если отчет создан, он будет записываться в `outputs/logs` в каталоге сборки.

```groovy
intunemam {
    report = true
}
```

#### <a name="verification"></a>Проверка
Подключаемый модуль сборки может выполнить дополнительную проверку, чтобы найти возможные ошибки в классах обработки. Чтобы запросить эту операцию, укажите `verify = true` в блоке конфигурации `intunemam`. Обратите внимание, что в результате задача подключаемого модуля может выполняться дольше на несколько секунд.

```groovy
intunemam {
    verify = true
}
```

#### <a name="incremental-builds"></a>Инкрементные сборки
Чтобы включить поддержку инкрементной сборки, укажите `incremental = true` в блоке конфигурации `intunemam`.  Это экспериментальная функция, предназначенная для повышения производительности сборки путем обработки только тех входных файлов, которые были изменены.  Конфигурация по умолчанию — `false`.

```groovy
intunemam {
    incremental = true
}
```

#### <a name="dependencies"></a>Зависимости

Подключаемый модуль Gradle имеет зависимость от [Javassist](https://jboss-javassist.github.io/javassist/), которая должна быть доступна для разрешения зависимостей Gradle (как описано выше). Javassist используется исключительно во время сборки при работе подключаемого модуля. Код Javassist в приложение не добавляется.

> [!NOTE] 
> Необходимо использовать подключаемый модуль Android Gradle версии 3.0 или более поздней и Gradle версии 4.1 или более поздней.

### <a name="command-line-build-tool"></a>Средство сборки из командной строки
Если в сборке используется Gradle, перейдите к [следующему разделу](#class-and-method-replacements).

Средство сборки из командной строки доступно в папке `BuildTool` пакета SDK. Оно выполняет ту же функцию, что и описанный выше подключаемый модуль Gradle, но может быть интегрировано в пользовательские системы сборки или сборки, отличные от Gradle. Поскольку средство является более универсальным, его вызов более сложен, поэтому при возможности следует использовать подключаемый модуль Gradle.

#### <a name="using-the-command-line-tool"></a>Использование средства командной строки

Средство командной строки можно вызывать, используя вспомогательные сценарии, расположенные в каталоге `BuildTool\bin`.

Средство ожидает следующие параметры.

| Параметр | Описание: |
| -- | -- |
| `--input` | Разделенный точкой с запятой список JAR-файлов и каталогов файлов классов, подлежащих изменению. Здесь необходимо указать все JAR-файлы и каталоги, которые следует переписать. |
| `--output` | Разделенный точкой с запятой список JAR-файлов и каталогов для хранения измененных файлов. Для каждой входной записи должна быть указана одна выходная запись. Их следует указывать по порядку. |
| `--classpath` | Путь к классу сборки. Он может содержать JAR-файлы и каталоги классов. |
| `--excludeClasses`| Разделенный точкой с запятой список, содержащий имена классов, которые должны быть исключены из переписи. |

Все параметры являются обязательными, за исключением `--excludeClasses`.

> [!NOTE]
> В Unix-подобных системах точка с запятой является разделителем команд. Во избежание разделения команд оболочки экранируйте все точки с запятой как '\' или заключите весь параметр в кавычки.

#### <a name="example-command-line-tool-invocation"></a>Пример вызова средства командной строки

``` batch
> BuildTool\bin\BuildTool.bat --input build\product-foo-project;libs\bar.jar --output mam-build\product-foo-project;mam-build\libs\bar.jar --classpath build\zap.jar;libs\Microsoft.Intune.MAM.SDK\classes.jar;%ANDROID_SDK_ROOT%\platforms\android-27\android.jar --excludeClasses com.contoso.SplashActivity
```

Будут получены следующие результаты:

* каталог `product-foo-project` переписывается в `mam-build\product-foo-project`;
* `bar.jar` переписывается в `mam-build\libs\bar.jar`;
* `zap.jar`**не** переписывается, так как он только указывается в `--classpath`;
* класс `com.contoso.SplashActivity`**не** переписывается, даже если он находится в `--input`.

> [!NOTE] 
> Сейчас средство сборки не поддерживает AAR-файлы. Если система сборки еще не извлекла `classes.jar` при работе с AAR-файлами, это потребуется сделать перед вызовом средства сборки.


## <a name="class-and-method-replacements"></a>Замены классов и методов

Чтобы включить управление Intune, базовые классы Android необходимо заменить соответствующими эквивалентами MAM. Классы пакета SDK располагаются между базовым классом Android и производной версией этого класса в самом приложении. Например, результатом выполнения действия может быть иерархия наследования, которая выглядит следующим образом: `Activity` > `MAMActivity` >
`AppSpecificActivity`. Фильтры уровня MAM выполняют вызовы системных операций, чтобы предоставить приложению управляемое представление мира.

Помимо базовых классов, некоторые классы, используемые приложением без наследования (например, `MediaPlayer`) также имеют обязательные эквиваленты MAM, и [некоторые вызовы методов также должны быть заменены](#wrapped-system-services). Более подробные сведения приведены ниже.

> [!NOTE] 
> Если приложение интегрируется со [средствами разработки ](#build-tooling) пакета SDK, следующие замены класса и метода выполняются автоматически.

| Базовый класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.app.Activity | MAMActivity |
| android.app.ActivityGroup | MAMActivityGroup |
| android.app.AliasActivity | MAMAliasActivity |
| android.app.Application | MAMApplication |
| android.app.Dialog | MAMDialog |
| android.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| android.app.DialogFragment | MAMDialogFragment |
| android.app.ExpandableListActivity | MAMExpandableListActivity |
| android.app.Fragment | MAMFragment |
| android.app.IntentService | MAMIntentService |
| android.app.LauncherActivity | MAMLauncherActivity |
| android.app.ListActivity | MAMListActivity |
| android.app.ListFragment | MAMListFragment |
| android.app.NativeActivity | MAMNativeActivity |
| android.app.PendingIntent | MAMPendingIntent (см. подраздел [Pending Intent](#pendingintent)) |
| android.app.Service | MAMService |
| android.app.TabActivity | MAMTabActivity |
| android.app.TaskStackBuilder | MAMTaskStackBuilder |
| android.app.backup.BackupAgent | MAMBackupAgent |
| android.app.backup.BackupAgentHelper | MAMBackupAgentHelper |
| android.app.backup.FileBackupHelper | MAMFileBackupHelper |
| android.app.backup.SharePreferencesBackupHelper | MAMSharedPreferencesBackupHelper |
| android.content.BroadcastReceiver | MAMBroadcastReceiver |
| android.content.ContentProvider | MAMContentProvider |
| android.os.Binder | MAMBinder (требуется, только если модуль привязки на основе интерфейса AIDL не создан) |
| android.media.MediaPlayer | MAMMediaPlayer |
| android.media.MediaMetadataRetriever | MAMMediaMetadataRetriever |
| android.provider.DocumentsProvider | MAMDocumentsProvider |
| android.preference.PreferenceActivity | MAMPreferenceActivity |
| android.support.multidex.MultiDexApplication | MAMMultiDexApplication |
| android.widget.TextView | MAMTextView |
| android.widget.AutoCompleteTextView |    MAMAutoCompleteTextView |
| android.widget.CheckedTextView | MAMCheckedTextView |
| android.widget.EditText | MAMEditText |
| android.inputmethodservice.ExtractEditText | MAMExtractEditText |
| android.widget.MultiAutoCompleteTextView | MAMMultiAutoCompleteTextView |

> [!NOTE]
> Даже если приложению не требуется собственный производный класс `Application`, [см. подраздел `MAMApplication` ниже](#mamapplication).

### <a name="microsoftintunemamsdksupportv4jar"></a>Microsoft.Intune.MAM.SDK.Support.v4.jar:

| Класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.support.v4.app.DialogFragment | MAMDialogFragment
| android.support.v4.app.FragmentActivity | MAMFragmentActivity
| android.support.v4.app.Fragment | MAMFragment
| android.support.v4.app.JobIntentService | MAMJobIntentService
| android.support.v4.app.TaskStackBuilder | MAMTaskStackBuilder
| android.support.v4.content.FileProvider | MAMFileProvider
| android.support.v4.content.WakefulBroadcastReceiver | MAMWakefulBroadcastReceiver

### <a name="microsoftintunemamsdksupportv7jar"></a>Microsoft.Intune.MAM.SDK.Support.v7.jar:

|Класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.support.v7.app.AlertDialog.Builder | MAMAlertDialogBuilder |
| android.support.v7.app.AppCompatActivity | MAMAppCompatActivity |
| android.support.v7.widget.AppCompatAutoCompleteTextView |    MAMAppCompatAutoCompleteTextView |
| android.support.v7.widget.AppCompatCheckedTextView | MAMAppCompatCheckedTextView |
| android.support.v7.widget.AppCompatEditText | MAMAppCompatEditText |
| android.support.v7.widget.AppCompatMultiAutoCompleteTextView | MAMAppCompatMultiAutoCompleteTextView |
| android.support.v7.widget.AppCompatTextView | MAMAppCompatTextView |

### <a name="microsoftintunemamsdksupportv17jar"></a>Microsoft.Intune.MAM.SDK.Support.v17.jar:
|Класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.support.v17.leanback.widget.SearchEditText | MAMSearchEditText |

### <a name="microsoftintunemamsdksupporttextjar"></a>Microsoft.Intune.MAM.SDK.Support.Text.jar:
|Класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.support.text.emoji.widget.EmojiAppCompatEditText | MAMEmojiAppCompatEditText |
| android.support.text.emoji.widget.EmojiAppCompatTextView | MAMEmojiAppCompatTextView |
| android.support.text.emoji.widget.EmojiEditText | MAMEmojiEditText |
| android.support.text.emoji.widget.EmojiTextView | MAMEmojiTextView |

### <a name="renamed-methods"></a>Переименованные методы
Часто метод, доступный в классе Android, отмечается как окончательный в замещающем классе MAM. В этом случае замещающий класс MAM предоставляет метод с таким же именем (обычно добавляется суффикс `MAM`), который должен быть переопределен вместо исходного. Например, при наследовании от `MAMActivity` вместо переопределения `onCreate()` и вызова `super.onCreate()` объекту `Activity` необходимо переопределить `onMAMCreate()` и вызвать `super.onMAMCreate()`. Компилятор Java должен налагать окончательные ограничения во избежание случайного переопределения исходного метода вместо его эквивалента MAM.

### <a name="mamapplication"></a>MAMApplication
Если приложение создает подкласс `android.app.Application`, вы **должны** вместо этого создать подкласс `com.microsoft.intune.mam.client.app.MAMApplication`. Если приложение не создает подкласс `android.app.Application`, то вы **должны** задать `"com.microsoft.intune.mam.client.app.MAMApplication"` в качестве атрибута `"android:name"` в своем теге `<application>` для AndroidManifest.xml.

### <a name="pendingintent"></a>PendingIntent
Вместо `PendingIntent.get*` следует использовать метод `MAMPendingIntent.get*`. После этого можно использовать полученный `PendingIntent` обычным образом.

### <a name="wrapped-system-services"></a>Упакованное системные службы
Для некоторых классов системных служб необходимо вызывать статический метод в классе-оболочке MAM, а не напрямую вызывать нужный метод в экземпляре службы. Например, вызов `getSystemService(ClipboardManager.class).getPrimaryClip()` должен стать вызовом `MAMClipboardManager.getPrimaryClip(getSystemService(ClipboardManager.class)`. Не рекомендуется выполнять эти замены вручную. Это должен делать BuildPlugin.

| Класс Android | Аналог в пакете SDK для приложений Intune |
|--|--|
| android.content.ClipboardManager | MAMClipboard |
| android.content.ContentProviderClient | MAMContentProviderClientManagement |
| android.content.ContentResolver | MAMContentResolverManagement |
| android.content.pm.PackageManager | MAMPackageManagement |
| android.app.DownloadManager | MAMDownloadManagement |
| android.print.PrintManager | MAMPrintManagement |
| Android.support.v4.Print.PrintHelper | MAMPrintHelperManagement |
| android.view.View | MAMViewManagement |
| android.view.DragEvent | MAMDragEventManagement |
| android.app.NotificationManager | MAMNotificationManagement |
| android.support.v4.app.NotificationManagerCompat | MAMNotificationCompatManagement |

Некоторые классы заключают большую часть своих методов в оболочку, например, `ClipboardManager`, `ContentProviderClient`, `ContentResolver` и `PackageManager`, хотя другие классы имеют только один или два метода в оболочке, например, `DownloadManager`, `PrintManager`, `PrintHelper`, `View`, `DragEvent`, `NotificationManager` и `NotificationManagerCompat`. Обратитесь к API-интерфейсам, предоставляемым эквивалентными классами MAM, чтобы уточнить конкретный метод, если вы не используете BuildPlugin.

### <a name="manifest-replacements"></a>Замены в манифесте
Может потребоваться выполнить некоторые описанные выше замены класса в манифесте и коде Java. Примечание.
* Ссылки на манифест `android.support.v4.content.FileProvider` необходимо заменить `com.microsoft.intune.mam.client.support.v4.content.MAMFileProvider`.

## <a name="androidx-libraries"></a>Библиотеки AndroidX
С выходом Android P компания Google объявила о новом (переименованном) наборе библиотек поддержки AndroidX. А версия 28 является последним основным выпуском существующих библиотек android.support.

В отличие от библиотек поддержки Android, мы не предоставляем варианты MAM библиотек AndroidX. AndroidX следует считать внешней библиотекой и настроить для переписи с помощью инструмента или подключаемого модуля сборки. Для сборок Gradle это можно сделать, включив `androidx.*` в поле `includeExternalLibraries` файла конфигурации подключаемого модуля. Вызовы средства командной строки должны явным образом указывать все JAR-файлы.

### <a name="pre-androidx-architecture-components"></a>Компоненты архитектуры до AndroidX
Многие компоненты архитектуры Android, включая Room, ViewModel и WorkManager, были переупакованы для AndroidX. Если приложение использует варианты этих библиотек до AndroidX, убедитесь, что перезапись применяется, включив `android.arch.*` в поле `includeExternalLibraries` конфигурации подключаемого модуля. Также можно обновить библиотеки до их эквивалентов AndroidX.

## <a name="sdk-permissions"></a>Разрешения пакета SDK

Пакету SDK для приложений Intune требуются три [разрешения системы Android](https://developer.android.com/guide/topics/security/permissions.html) в отношении приложений, в которые он интегрируется:

* `android.permission.GET_ACCOUNTS` (запрашивается во время выполнения при необходимости)

* `android.permission.MANAGE_ACCOUNTS`

* `android.permission.USE_CREDENTIALS`

Эти разрешения требуются библиотеке проверки подлинности Active Directory Azure ([ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/)) для проверки подлинности через посредника. Если эти разрешения приложению не предоставлены или отменены пользователем, потоки проверки подлинности, которым требуется брокер (приложение корпоративного портала), будут отключены.

## <a name="logging"></a>Logging

Чтобы получить максимальную пользу из регистрируемых данных, ведение журнала нужно инициализировать как можно раньше. Как правило, `Application.onMAMCreate()` — это наилучший вариант для инициализации ведения журнала.

Для получения журналов MAM в приложении, создайте [обработчик Java](https://docs.oracle.com/javase/7/docs/api/java/util/logging/Handler.html) и добавьте его в `MAMLogHandlerWrapper`. Это будет вызывать `publish()` в обработчике приложения для каждого сообщения журнала.

```java
/**
 * Global log handler that enables fine grained PII filtering within MAM logs.  
 *
 * To start using this you should build your own log handler and add it via
 * MAMComponents.get(MAMLogHandlerWrapper.class).addHandler(myHandler, false);  
 *
 * You may also remove the handler entirely via
 * MAMComponents.get(MAMLogHandlerWrapper.class).removeHandler(myHandler);
 */
public interface MAMLogHandlerWrapper {
    /**
     * Add a handler, PII can be toggled.
     *
     * @param handler handler to add.
     * @param wantsPII if PII is desired in the logs.    
     */
    void addHandler(final Handler handler, final boolean wantsPII);

    /**
     * Remove a handler.
     *
     * @param handler handler to remove.
     */
    void removeHandler(final Handler handler);
}
```

## <a name="enable-features-that-require-app-participation"></a>Включение функций, требующих содействия со стороны приложения

Есть несколько политик защиты приложений, которые пакет SDK не может реализовать самостоятельно. Приложение может управлять своим поведением для выполнения этих функций, используя несколько интерфейсов API, которые находятся в указанном ниже интерфейсе `AppPolicy`. Чтобы извлечь экземпляр `AppPolicy`, используйте `MAMPolicyManager.getPolicy`.

```java
/**
 * External facing application policies.
 */
public interface AppPolicy {

/**
 * Restrict where an app can save personal data.
  * This function is now deprecated. Use getIsSaveToLocationAllowed(SaveLocation, String) instead
 * @return True if the app is allowed to save to personal data stores; false otherwise.
 */
@Deprecated
boolean getIsSaveToPersonalAllowed();

/**
 * Check if policy prohibits saving to a content provider location.
 *
 * @param location
 *            a content URI to check
 * @return True if location is not a content URI or if policy does not prohibit saving to the content location.
 */
boolean getIsSaveToLocationAllowed(Uri location);

/**
 * Determines if the SaveLocation passed in can be saved to by the username associated with the cloud service.
 *
 * @param service
 *           see {@link SaveLocation}.
 * @param username
 *           the username/email associated with the cloud service being saved to. Use null if a mapping between
 *           the AAD username and the cloud service username does not exist or the username is not known.
 * @return true if the location can be saved to by the identity, false if otherwise.
 */
boolean getIsSaveToLocationAllowed(SaveLocation service, String username);

/**
 * Checks whether any activities which could handle the given intent are allowed by policy. Returns false only if all
 * activities which could otherwise handle the intent are blocked. If there are no activities which could handle the intent
 * regardless of policy, returns true. If some activities are allowed and others blocked, returns true. Note that it is not
 * necessary to use this method for policy enforcement. If your app attempts to launch an intent for which there are no
 * allowed activities, MAM will display a dialog explaining the situation to the user.
 *
 * @param intent
 *         intent to check
 *
 * @return whether any activities which could handle this intent are allowed.
*/
boolean areIntentActivitiesAllowed(Intent intent);

/**
 * Whether the SDK PIN prompt is enabled for the app.
 *
 * @return True if the PIN is enabled. False otherwise.
 */
boolean getIsPinRequired();

/**
 * Whether the Intune Managed Browser is required to open web links.
 * @return True if the Managed Browser is required, false otherwise
 */
boolean getIsManagedBrowserRequired();

/**
 * Check if policy allows taking screenshots.
 *
 * @return True if screenshots will be blocked, false otherwise
 */
boolean getIsScreenCaptureAllowed();

/**
 * Check if policy allows Contact sync to local contact list.
 *
 * @return True if Contact sync is allowed to save to local contact list; false otherwise.
 */
boolean getIsContactSyncAllowed();

/**
 * Get the notification restriction. If {@link NotificationRestriction#BLOCKED BLOCKED}, the app must not show any notifications
 * for the user associated with this policy. If {@link NotificationRestriction#BLOCK_ORG_DATA BLOCK_ORG_DATA}, the app must show
 * a modified notification that does not contain organization data. If {@link NotificationRestriction#UNRESTRICTED
 * UNRESTRICTED}, all notifications are allowed.
 *
 * @return The notification restriction.
 */
NotificationRestriction getNotificationRestriction();

/**
 * This method is intended for diagnostic/telemetry purposes only. It can be used to discover whether file encryption is in use.
 * File encryption is transparent to the app and the app should not need to make any business logic decisions based on this.
 * @return True if file encryption is in use.
 */
boolean diagnosticIsFileEncryptionInUse();

/**
 * Return the policy in string format to the app.
 *  
 * @return The string representing the policy.
 */
String toString();

}
```

> [!NOTE]
> `MAMPolicyManager.getPolicy` всегда будет возвращать политику приложений, отличную от NULL, даже если устройство или приложение не управляются Intune.

### <a name="example-determine-if-pin-is-required-for-the-app"></a>Пример: Настройка обязательного использования ПИН-кода в приложении

Если в приложении есть соответствующий интерфейс, вы можете отключить необходимость ввода ПИН-кода, если ИТ-администратор настроил это в пакете SDK. Чтобы определить, развернул ли ИТ-администратор политику использования ПИН-кода в приложении для текущего пользователя, вызовите следующий метод:

```java

MAMPolicyManager.getPolicy(currentActivity).getIsPinRequired();
```

### <a name="example-determine-the-primary-intune-user"></a>Пример: Определение основного пользователя Intune

В дополнение к API-интерфейсам, предоставляемых в AppPolicy, имя участника-пользователя (**UPN**) также предоставляется API `getPrimaryUser()`, определенным в интерфейсе `MAMUserInfo`. Чтобы получить имя участника-пользователя, вызовите следующее:

```java
MAMComponents.get(MAMUserInfo.class).getPrimaryUser();
```

Полное определение интерфейса MAMUserInfo приведено ниже:

```java
/**
 * External facing user information.
 *
 */
public interface MAMUserInfo {
       /**
        * Get the primary user name.
        *
        * @return the primary user name or null if neither the device nor app is enrolled.
        */
       String getPrimaryUser();
}
```

### <a name="example-determine-if-saving-to-device-or-cloud-storage-is-permitted"></a>Пример: Определение разрешения на сохранение данных на устройстве или в облачном хранилище

Во многих приложениях реализованы функции, позволяющие конечным пользователям сохранять файлы локально или в облачном хранилище. Пакет SDK для приложений Intune позволяет ИТ-администраторам защититься от утечки данных за счет применения ограничений политик, уместных для их организации.  Одной из политик, которой может управлять администратор, является возможность конечного пользователя сохранять данные в личном хранилище. Сюда входит сохранение в локальной папке, на SD-карте или в сторонних службах резервного копирования.

**Для включения этой функции требуется содействие со стороны приложения.** Если приложение позволяет сохранять данные в личное или облачное расположение непосредственно из приложения, необходимо реализовать эту функцию, чтобы предоставить ИТ-администратору возможность разрешать сохранение в расположение. Указанные ниже API позволяют приложению узнать, разрешено ли в текущей политике администрирования Intune сохранение в личном хранилище. После этого приложение может применить политику, так как ему известно о том, что хранилище личных данных доступно конечному пользователю через это приложение.  

Чтобы определить, применяется ли политика, выполните следующий вызов:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(
SaveLocation service, String username);
```

Параметру `service` нужно задать одно из следующих значений `SaveLocation`:


- `SaveLocation.ONEDRIVE_FOR_BUSINESS`
- `SaveLocation.SHAREPOINT`
- `SaveLocation.LOCAL`
- `SaveLocation.OTHER`

`username` задает имя участника-пользователя или имя пользователя и адрес электронной почты, связанные с облачной службой, где сохраняются данные (*не*обязательно те же, что и у пользователя, владеющего сохраняемым документом). Используйте значение NULL, если отсутствует сопоставление между AAD UPN и именем пользователя облачной службы или имя пользователя неизвестно. `SaveLocation.LOCAL` не является облачной службой и поэтому всегда должен использоваться с параметром имени пользователя `null`.

Предыдущий метод, с помощью которого можно определить, разрешает ли пользовательская политика сохранять данные в разных расположениях, представлен `getIsSaveToPersonalAllowed()` в рамках того же класса **AppPolicy**. Эта функция сейчас является **устаревшей** и не должна больше использоваться; следующий вызов эквивалентен `getIsSaveToPersonalAllowed()`:

```java
MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(SaveLocation.LOCAL, null);
```

>[!NOTE]
> Используйте `SaveLocation.OTHER`, если рассматриваемое расположение не включено в перечисление **SaveLocations**.

### <a name="example-determine-if-notifications-with-organization-data-need-to-be-restricted"></a>Пример: Определение необходимости ограничения уведомлений с данными организации

Если приложение отображает уведомления, сначала необходимо проверить политику ограничения уведомлений для пользователя, связанного с уведомлением. Чтобы определить, применяется ли политика, выполните следующий вызов.

```java
NotificationRestriction notificationRestriction =
    MAMPolicyManager.getPolicyForIdentity(notificationIdentity).getNotificationRestriction();
```

Если установлено ограничение `BLOCKED`, приложение не должно отображать уведомления для пользователя, связанного с этой политикой. Если установлено ограничение `BLOCK_ORG_DATA`, приложение должно отображать измененное уведомление, которое не содержит данных организации. Если `UNRESTRICTED`, все уведомления разрешены.

Если `getNotificationRestriction` не вызывается, пакет SDK MAM постарается автоматически ограничивать уведомления для приложений с одним удостоверением. Если включена автоматическая блокировка и установлено `BLOCK_ORG_DATA`, уведомление не будет отображаться совсем. Для более точного управления проверьте значение `getNotificationRestriction` и измените уведомления приложений соответствующим образом.

## <a name="register-for-notifications-from-the-sdk"></a>Регистрация для получения уведомлений из пакета SDK

### <a name="overview"></a>Обзор
Пакет SDK для приложений Intune позволяет приложению управлять поведением определенных политик, включая политики выборочной очистки, развернутых ИТ-администратором. Когда ИТ-администратор развертывает такую политику, служба Intune отправляет уведомление пакету SDK.

Ваше приложение следует зарегистрировать для получения уведомлений из пакета SDK. Для этого нужно создать класс `MAMNotificationReceiver` и зарегистрировать его с помощью `MAMNotificationReceiverRegistry`. Для этого укажите получателя, а также тип необходимых уведомлений в `App.onCreate`, как показано в следующем примере:

```java
@Override
public void onCreate() {
  super.onCreate();
  MAMComponents.get(MAMNotificationReceiverRegistry.class)
    .registerReceiver(
      new ToastNotificationReceiver(),
      MAMNotificationType.WIPE_USER_DATA);
  }
```

### <a name="mamnotificationreceiver"></a>MAMNotificationReceiver

Интерфейс `MAMNotificationReceiver` просто получает уведомления из службы Intune. Некоторые уведомления обрабатываются непосредственно пакетом SDK, другие требуют участия со стороны приложения. Приложение **должно** возвращать для уведомления значение true или false. Оно должно всегда возвращать значение true, за исключением случаев, когда какое-либо действие, которое приложение пыталось выполнить в результате уведомления, завершилось со сбоем.

* Этот сбой может быть зарегистрирован в службе Intune. Подобная ситуация может возникнуть, например, в случае, если приложение не смогло очистить данные пользователя после того, как ИТ-администратор запустил очистку.

>[!NOTE]
> Можно безопасно осуществить блокировку в `MAMNotificationReceiver.onReceive`, так как его обратный вызов не выполняется в потоке пользовательского интерфейса.

Интерфейс `MAMNotificationReceiver`, как определено в пакете SDK, включен ниже.

```java
/**
 * The SDK is signaling that a MAM event has occurred.
 *
 */
public interface MAMNotificationReceiver {

    /**
     * A notification was received.
     *
     * @param notification
     *            The notification that was received.
     * @return The receiver should return true if it handled the
     *   notification without error (or if it decided to ignore the
     *   notification). If the receiver tried to take some action in
     *   response to the notification but failed to complete that
     *   action it should return false.
     */
    boolean onReceive(MAMNotification notification);
}
```

### <a name="types-of-notifications"></a>Типы уведомлений

Следующие уведомления отправляются в приложение, и некоторые из них могут потребовать содействия со стороны приложения:

* **WIPE_USER_DATA**. Это уведомление отправляется в классе `MAMUserNotification`. При получении этого уведомления приложение *должно* удалить все данные, связанные с управляемым удостоверением (из `MAMUserNotification.getUserIdentity()`). Уведомление может возникнуть по различным причинам, в том числе когда приложение вызывает `unregisterAccountForMAM`, когда ИТ-администратор инициирует очистку или если не удовлетворены обязательные политики условного доступа администратора. Если приложение не зарегистрировано для этого уведомления, будет выполняться очистка по умолчанию. Поведение по умолчанию приведет к удалению всех файлов для приложения с одним удостоверением или всех файлов, помеченных как управляемое удостоверение для приложения с несколькими удостоверениями. Это уведомление никогда не будет отправляться в потоке пользовательского интерфейса.

* **WIPE_USER_AUXILIARY_DATA**. Приложения могут регистрироваться на получение этого уведомления, если пакет SDK для приложений Intune должен выполнять обычную выборочную очистку, но приложение будет одновременно с этим удалять некоторые другие данные. Это уведомление недоступно для приложений с одним удостоверением, оно будет отправляться только для приложений с множественной идентификацией. Это уведомление никогда не будет отправляться в потоке пользовательского интерфейса.

* **REFRESH_POLICY**. Это уведомление отправляется в `MAMUserNotification`. При получении этого уведомления все кэшированные вашим приложением решения по политикам Intune должны быть признаны недействительными и обновлены. Если приложение не сохраняет никаких предположений политики, его не требуется регистрировать для этого уведомления. Нет никаких гарантий в отношении потока, в который будет отправляться это уведомление.

* **REFRESH_APP_CONFIG**. Это уведомление отправляется в `MAMUserNotification`. При получении этого уведомления все кэшированные данные конфигурации приложений должны быть признаны недействительными и обновлены. Нет никаких гарантий в отношении потока, в который будет отправляться это уведомление.

* **MANAGEMENT_REMOVED**. Это уведомление отправляется в `MAMUserNotification` и сообщает приложению о переходе в неуправляемое состояние. Перейдя в неуправляемое состояние, приложение больше не сможет читать зашифрованные файлы и данные, зашифрованные с использованием MAMDataProtectionManager, а также взаимодействовать с зашифрованным буфером обмена или состоять в экосистеме управляемого приложения. См. дополнительные сведения ниже. Это уведомление никогда не будет отправляться в потоке пользовательского интерфейса.

* **MAM_ENROLLMENT_RESULT**. Это уведомление отправляется в `MAMEnrollmentNotification` для оповещения приложения о завершении попытки регистрации APP-WE и содержит сведения о состоянии этой попытки. Нет никаких гарантий в отношении потока, в который будет отправляться это уведомление.

* **COMPLIANCE_STATUS**. Это уведомление отправляется в `MAMComplianceNotification` для информирования приложения о результате попытки исправления соответствия. Нет никаких гарантий в отношении потока, в который будет отправляться это уведомление.

> [!NOTE]
> Одновременно регистрировать приложение для получения уведомлений `WIPE_USER_DATA` и `WIPE_USER_AUXILIARY_DATA` нельзя.

### <a name="management_removed"></a>MANAGEMENT_REMOVED

Уведомление `MANAGEMENT_REMOVED` указывает, что пользователь, который ранее находился под управлением политики, больше не будет регулироваться с помощью политики Intune MAM. Это не требует очистки пользовательских данных или выхода пользователя (если очистка нужна, будет отправлено уведомление `WIPE_USER_DATA`). Во многих приложениях может не требоваться обработка этого уведомления; тем не менее приложения, которые используют `MAMDataProtectionManager`, должны [особо учитывать это уведомление](#data-protection).

Когда MAM вызывает метод получателя `MANAGEMENT_REMOVED` в приложении, будут выполняться следующие условия:
* MAM уже расшифрует зашифрованные файлы (но не защищенные данные буферов), относящиеся к приложению. Файлы в открытых расположениях на SD-карте, которые не принадлежат непосредственно приложению (например, папки "Документы" или "Загрузки"), не расшифровываются.
* Новые файлы или буферы защищенных данных, создаваемые методом получателя (или любым другим кодом, выполняемым после запуска получателя), не шифруются.
* Приложение по-прежнему имеет доступ к ключам шифрования, поэтому такие операции, как расшифровка буферов данных, будут успешными.

После возвращения получателя приложение больше не будет иметь доступ к ключам шифрования.

## <a name="configure-azure-active-directory-authentication-library-adal"></a>Настройка библиотеки проверки подлинности Azure Active Directory (ADAL)

Во-первых, следует ознакомиться с рекомендациями по интеграции ADAL, доступными в [репозитории ADAL в GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android).

Для [аутентификации](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) пакет SDK использует библиотеки [ADAL](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) и сценарии условного запуска. Для этого в приложении должна быть определенная конфигурация [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/). Значения конфигурации передаются в пакет SDK с метаданными AndroidManifest.

Чтобы настроить приложение и включить надлежащий тип аутентификации, добавьте следующий код в узел приложения в AndroidManifest.xml. Некоторые из этих конфигураций нужны, только если приложение использует библиотеку ADAL для общей аутентификации. В этом случае вам потребуются эти конкретные значения, используемые вашим приложением для регистрации в AAD. Это позволяет предотвратить ситуацию, когда пользователь получает два запроса на аутентификацию, так как AAD распознает два отдельных значения регистрации: одно из приложения и одно из пакета SDK.

```xml
<meta-data
    android:name="com.microsoft.intune.mam.aad.Authority"
    android:value="https://AAD authority/" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.ClientID"
    android:value="your-client-ID-GUID" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.NonBrokerRedirectURI"
    android:value="your-redirect-URI" />
<meta-data
    android:name="com.microsoft.intune.mam.aad.SkipBroker"
    android:value="[true | false]" />
```

### <a name="adal-metadata"></a>Метаданные ADAL

* **Authority** — это используемый центр AAD. Если это значение отсутствует, используется общая среда AAD.
    > [!NOTE]
    > Не устанавливайте значение в этом поле, если ваше приложение поддерживает национальное облако.

* **ClientID** — это используемый идентификатор ClientID AAD (также называемый идентификатором приложения). Вы должны использовать ClientID своего приложения, если оно зарегистрировано в Azure AD, или [регистрацию по умолчанию](#default-enrollment-optional), если оно не интегрировано с ADAL.

* **NonBrokerRedirectURI** — это URI перенаправления AAD, используемый в ситуациях без брокера. Если это значение не указано, используется стандартное значение `urn:ietf:wg:oauth:2.0:oob`. Это значение подходит для большинства приложений.

  * NonBrokerRedirectURI используется только в том случае, когда значение SkipBroker равно true.

* **SkipBroker** позволяет переопределить поведение по умолчанию для участия единого входа ADAL. SkipBroker должен быть определен только для приложений, которые указывают ClientID **и** не поддерживают проверку подлинности через брокер или единый вход в масштабе всего устройства. В этом случае он должен иметь значение true. Большинству приложений не следует задавать параметр SkipBroker.

  * ClientID **необходимо** указать в манифесте, чтобы указать значение SkipBroker.

  * Если указан параметр ClientID, значение по умолчанию — false.

  * NonBrokerRedirectURI используется только в том случае, когда значение SkipBroker равно true. Приложения, которые не интегрируются с ADAL (и, следовательно, не имеют ClientID), также по умолчанию будут использовать true.

### <a name="common-adal-configurations"></a>Распространенные конфигурации ADAL

Ниже приведены стандартные способы настройки приложения с использованием ADAL. Определите конфигурацию приложения и присвойте параметрам метаданных ADAL (см. выше) необходимые значения. В любом случае Authority можно указать для нестандартных сред. Если параметр не указан, будет использоваться общедоступный рабочий центр AAD.

#### <a name="1-app-does-not-integrate-adal"></a>1. Приложение не интегрируется с ADAL
Метаданные ADAL **не должны** присутствовать в манифесте.

#### <a name="2-app-integrates-adal"></a>2. Приложение интегрируется с ADAL

|Обязательный параметр ADAL| Значение |
|--|--|
| ClientID | Идентификатор ClientID приложения (созданный в Azure AD при регистрации приложения). |

Центр может быть указан при необходимости.

Необходимо зарегистрировать приложение в Azure AD и предоставить вашему приложению доступ к службе политики защиты приложений.
* Дополнительные сведения о регистрации приложения в Azure AD см. [здесь](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).
* Убедитесь, что вы предоставили приложению Android права доступа к службе политики защиты приложений (APP). Инструкции см. в [Приступая к работе с руководством по пакету SDK для Intune](https://docs.microsoft.com/intune/app-sdk-get-started#next-steps-after-integration) в разделе «предоставить вашему приложению доступ к Intune защиты службы приложений (необязательно). 

Кроме того, ознакомьтесь с требованиями для [условного доступа](#conditional-access) ниже.


#### <a name="3-app-integrates-adal-but-does-not-support-brokered-authenticationdevice-wide-sso"></a>3. Приложение включает ADAL, но не поддерживает аутентификацию и единый вход с помощью брокера на уровне устройства.

|Обязательный параметр ADAL| Значение |
|--|--|
| ClientID | Идентификатор ClientID приложения (созданный в Azure AD при регистрации приложения). |
| SkipBroker | **True** |

При необходимости можно указать Authority и NonBrokerRedirectURI.

### <a name="conditional-access"></a>Условный доступ
Условный доступ — это [функция](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer) Azure Active Directory, которую можно использовать для управления доступом к ресурсам AAD. [Администраторы Intune могут определить правила условного доступа](https://docs.microsoft.com/intune/conditional-access), которые разрешают доступ к ресурсам только с устройств или из приложений, управляемых Intune. Чтобы убедиться, что приложение может обратиться к ресурсам, когда это необходимо, нужно выполнить указанные ниже действия. Если приложение не получает токены доступа AAD или обращается к ресурсам, которые невозможно защитить с помощью условного доступа, вы можете пропустить эти шаги.

1. Выполните [рекомендации по интеграции ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android#how-to-use-this-library). 
   Особое внимание уделите шагу 11 по использованию брокера.
2. [Зарегистрируйте приложение в Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration). 
   URI перенаправления можно найти в рекомендациях по интеграции ADAL выше.
3. Задайте параметры метаданных манифеста, как описано в пункте 2 раздела [Распространенные конфигурации ADAL](#common-adal-configurations) выше.
4. Проверьте правильность настройки всех компонентов, включив [условный доступ на основе устройств](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use) на [портале Azure](https://portal.azure.com/#blade/Microsoft_Intune_DeviceSettings/ExchangeConnectorMenu/aad/connectorType/2) и убедившись в следующем:
    - после входа в приложение выдается запрос на установку и регистрацию корпоративного портала;
    - после регистрации вход в приложение выполняется успешно.
5. Реализовав интеграцию своего приложения с пакетом SDK для приложений Intune, нужно обратиться по адресу msintuneappsdk@microsoft.com для включения в список утвержденных приложений для [условного доступа на основе приложений](https://docs.microsoft.com/intune/conditional-access-intune-common-ways-use#app-based-conditional-access).
6. После добавления приложения в утвержденный список проверьте работу, [настроив условный доступ на основе приложений](https://docs.microsoft.com/intune/app-based-conditional-access-intune-create), и убедитесь, что вход в приложение выполняется успешно.

## <a name="app-protection-policy-without-device-enrollment"></a>Политика защиты приложений без регистрации устройства

### <a name="overview"></a>Обзор
Политика защиты приложений без регистрации устройств Intune, также известная как APP-WE или MAM-WE, позволяет управлять приложениями с помощью Intune без необходимости регистрации устройств в Intune MDM. APP-WE работает с регистрацией устройств и без нее. Корпоративный портал по-прежнему должен быть установлен на устройстве, но пользователю не нужно входить на портал компании и регистрировать это устройство.

> [!NOTE]
> Все приложения должны поддерживать политику защиты приложений без регистрации устройства.

### <a name="workflow"></a>Рабочий процесс

Когда приложение создает учетную запись пользователя, оно должно зарегистрировать учетную запись для управления с использованием пакета SDK для приложений Intune. Пакет SDK будет обрабатывать сведения о регистрации приложения в службе APP-WE. В случае ошибки процесс регистрации повторится через определенные промежутки времени.

Приложение также может обратиться к пакету SDK для приложений Intune, запросив статус зарегистрированного пользователя. Это нужно, чтобы определить, будет ли пользователю заблокирован доступ к корпоративному содержимому. Хотя для управления можно зарегистрировать несколько учетных записей, одновременно зарегистрировать с использованием службы APP-WE можно только одну учетную запись. Это означает, что политика защиты приложения может одновременно применяться только к одной учетной записи в приложении.

Для приложения необходимо выполнить обратный вызов, чтобы получить маркер доступа из библиотеки ADAL от имени пакета SDK. Предполагается, что приложение уже использует ADAL для аутентификации пользователей и получения маркеров доступа.

Для учетной записи, полностью удаляемой приложением, необходимо отменить регистрацию. Так приложение больше не будет применять политику для этого пользователя. Для зарегистрированного в службе MAM пользователя регистрация будет отменена, а приложение будет очищено.

### <a name="overview-of-app-requirements"></a>Обзор требований приложения

Чтобы реализовать интеграцию APP-WE, приложение должно зарегистрировать учетную запись пользователя с помощью пакета SDK для MAM:

1. Приложение _должно_ реализовать и зарегистрировать экземпляр интерфейса `MAMServiceAuthenticationCallback`. Экземпляр обратного вызова должен быть зарегистрирован как можно раньше в жизненном цикле приложения (обычно в методе `onMAMCreate()` класса приложения).

2. Когда учетная запись пользователя будет создана, а сам пользователь войдет с использованием ADAL, приложение _должно_ вызвать `registerAccountForMAM()`.

3. Когда учетная запись пользователя удаляется, приложение должно вызвать `unregisterAccountForMAM()`, чтобы удалить эту учетную запись из системы управления Intune.

    > [!NOTE]
    > Если пользователь временно выходит из приложения, приложению не нужно вызывать `unregisterAccountForMAM()`. Вызов может инициировать очистку для полного удаления корпоративных данных для пользователя.


### <a name="mamenrollmentmanager"></a>MAMEnrollmentManager
Все необходимые процедуры аутентификации и регистрации API-интерфейсов можно найти в интерфейсе `MAMEnrollmentManager`. Ссылку на `MAMEnrollmentManager` можно получить так:

```java
MAMEnrollmentManager mgr = MAMComponents.get(MAMEnrollmentManager.class);

// make use of mgr
```

Возвращаемый экземпляр `MAMEnrollmentManager` гарантированно не будет иметь нулевое значение. Методы API можно разделить на две категории: **аутентификация** и **регистрация учетной записи**.

```java
package com.microsoft.intune.mam.policy;

public interface MAMEnrollmentManager {
    public enum Result {
        AUTHORIZATION_NEEDED,
        NOT_LICENSED,
        ENROLLMENT_SUCCEEDED,
        ENROLLMENT_FAILED,
        WRONG_USER,
        MDM_ENROLLED,
        UNENROLLMENT_SUCCEEDED,
        UNENROLLMENT_FAILED,
        PENDING,
        COMPANY_PORTAL_REQUIRED;
    }

    //Authentication methods
    interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
    }
    void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
    void updateToken(String upn, String aadId, String resourceId, String token);

    //Registration methods
    void registerAccountForMAM(String upn, String aadId, String tenantId);
    void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
    void unregisterAccountForMAM(String upn);
    Result getRegisteredAccountStatus(String upn);
}
```

### <a name="account-authentication"></a>Аутентификация учетной записи
В этом разделе описываются методы аутентификации API в `MAMEnrollmentManager` и способы их использования.

```java
interface MAMServiceAuthenticationCallback {
        String acquireToken(String upn, String aadId, String resourceId);
}
void registerAuthenticationCallback(MAMServiceAuthenticationCallback callback);
void updateToken(String upn, String aadId, String resourceId, String token);
```

1. Приложение должно реализовать интерфейс `MAMServiceAuthenticationCallback`, позволяющий пакету SDK запрашивать маркер ADAL для определенного пользователя и идентификатора ресурсов. Экземпляр обратного вызова должен предоставляться `MAMEnrollmentManager` при вызове его метода `registerAuthenticationCallback()`. Маркер может понадобиться на раннем этапе жизненного цикла приложения для повторных попыток регистрации или проверок обновления политики защиты приложений. Поэтому лучше всего регистрировать обратный вызов в методе `onMAMCreate()` подкласса `MAMApplication` приложения.

2. Метод `acquireToken()` должен получить маркер доступа для запрошенного идентификатора ресурса для определенного пользователя. Если он не может получить запрошенный маркер, должно быть возвращено нулевое значение.

    > [!NOTE]
    > Убедитесь, что приложение использует параметры `resourceId` и `aadId`, передаваемые в `acquireToken()`, чтобы получить правильный токен.

    ```java
    class MAMAuthCallback implements MAMServiceAuthenticationCallback {
        public String acquireToken(String upn, String aadId, String resourceId) {
            return mAuthContext.acquireTokenSilentSync(resourceId, ClientID, aadId).getAccessToken();
        }
    }
    ```

3. Если приложению не удается предоставить маркер, когда пакет SDK вызывает `acquireToken()` (например, если происходит сбой автоматической аутентификации, и это несвоевременно для отображения пользовательского интерфейса), приложение может сделать это позже, вызвав метод `updateToken()`. Запрошенные предыдущим вызовом `acquireToken()` идентификаторы имени участника-пользователя, AAD и ресурсов должны быть переданы `updateToken()` вместе с полученным маркером. Приложение, получившее нулевое значение из предоставленного обратного вызова, должно вызвать этот метод как можно быстрее.

    > [!NOTE]
    > Пакет SDK будет периодически вызывать `acquireToken()`, чтобы получить маркер, поэтому вызов `updateToken()` не является обязательным. Тем не менее это рекомендуемая процедура, которая помогает своевременно завершить проверки регистрации и применения политики защиты приложений.


### <a name="account-registration"></a>Регистрация учетной записи
В этом разделе описываются методы регистрации API в `MAMEnrollmentManager` и способы их использования.

```java
void registerAccountForMAM(String upn, String aadId, String tenantId);
void registerAccountForMAM(String upn, String aadId, String tenantId, String authority);
void unregisterAccountForMAM(String upn);
Result getRegisteredAccountStatus(String upn);
```

1. Чтобы зарегистрировать учетную запись для управления, приложение должно вызвать `registerAccountForMAM()`. Учетная запись пользователя идентифицируется по его имени участника-пользователя и идентификатора пользователя AAD. Идентификатор клиента также требуется для связывания данных регистрации с пользовательским клиентом AAD. Кроме того, могут быть предоставлены полномочия пользователя, чтобы разрешить регистрацию в отдельных национальных облаках (см. руководство по [регистрации в национальных облаках](#sovereign-cloud-registration)).  Пакет SDK может попытаться зарегистрировать приложение для определенного пользователя в службе MAM. В случае сбоя регистрации он будет периодически повторять эту процедуру, пока регистрация учетной записи не будет отменена. Интервал повторных попыток обычно составляет 12–24 ч. Пакет SDK предоставляет сведения о состоянии попыток регистрации асинхронно с помощью уведомлений.

2. Так как аутентификация AAD обязательна, лучше всего регистрировать учетную запись после того, как пользователь вошел в приложение и прошел аутентификацию с использованием ADAL. Идентификатор пользователя AAD и идентификатор клиента возвращаются из вызова аутентификации ADAL как часть объекта [`AuthenticationResult`](https://github.com/AzureAD/azure-activedirectory-library-for-android).
    * Идентификатор клиента предоставляется из метода `AuthenticationResult.getTenantID()`.
    * Сведения о пользователе находятся в дочернем объекте типа `UserInfo`, который предоставляется вместе с `AuthenticationResult.getUserInfo()`, а идентификатор пользователя AAD извлекается из этого объекта при вызове `UserInfo.getUserId()`.

3. Чтобы отменить регистрацию учетной записи в системе управления Intune, приложение должно вызвать `unregisterAccountForMAM()`. Если учетная запись зарегистрирована и является управляемой, пакет SDK отменит ее регистрацию и очистит связанные данные. Периодические повторные попытки регистрации учетной записи будут остановлены. Пакет SDK предоставляет сведения о состоянии запроса на отмену регистрации асинхронно с помощью уведомлений.

### <a name="sovereign-cloud-registration"></a>Регистрация в национальных облаках
Приложения, [поддерживающие национальные облака](https://www.microsoft.com/trustcenter/cloudservices/nationalcloud), **должны** предоставлять `authority` для `registerAccountForMAM()`.  Для этого можно предоставить `instance_aware=true` в acquireToken extraQueryParameters ADAL [1.14.0+](https://github.com/AzureAD/azure-activedirectory-library-for-android/releases/tag/v1.14.0), а затем вызвать `getAuthority()` для AuthenticationCallback AuthenticationResult.

```java
mAuthContext.acquireToken(this, RESOURCE_ID, CLIENT_ID, REDIRECT_URI, PromptBehavior.FORCE_PROMPT, "instance_aware=true",
        new AuthenticationCallback<AuthenticationResult>() {
            @Override
            public void onError(final Exception exc) {
                // authentication failed
            }

            @Override
            public void onSuccess(final AuthenticationResult result) {
                mAuthority = result.getAuthority();
                // handle other parts of the result
            }
        });
```

> [!NOTE]
> Не задавайте метаданные `com.microsoft.intune.mam.aad.Authority` в AndroidManifest.xml.

> [!NOTE]
> Убедитесь, что центр правильно задан в методе `MAMServiceAuthenticationCallback::acquireToken()`.

#### <a name="currently-supported-sovereign-clouds"></a>Поддерживаемые сейчас национальные облака

1. Облако Azure для государственных организаций США

### <a name="important-implementation-notes"></a>Примечания, связанные с реализацией

#### <a name="authentication"></a>Проверка подлинности
* Когда приложение вызывает метод `registerAccountForMAM()`, вскоре после этого оно может получить обратный вызов в своем интерфейсе `MAMServiceAuthenticationCallback` в другом потоке. В идеале приложение получает собственный токен из ADAL до регистрации учетной записи для ускорения процесса получения запрошенного токена. Если приложение возвращает действительный токен из обратного вызова, регистрация продолжится, и приложение получит результат в уведомлении.

* Если приложение не возвращает допустимый токен AAD, результатом попытки регистрации будет `AUTHENTICATION_NEEDED`. Если приложение получает этот результат в уведомлении, процесс регистрации настоятельно рекомендуется ускорить. Для этого нужно получить токен для пользователя и ресурса, ранее запрошенного из `acquireToken()`, и вызвать метод `updateToken()`, что снова инициирует процесс регистрации.

* Зарегистрированные `MAMServiceAuthenticationCallback` приложения также будут вызываться для получения маркера для периодической проверки обновления политики защиты приложений. Если приложению не удается предоставить маркер при запросе, оно не получит уведомление. Такое приложение должно попытаться получить маркер и вызвать `updateToken()` в удобное для этого время, чтобы ускорить процесс проверки. Если маркер не предоставлен, обратный вызов будет осуществляться при следующей попытке.

* Для поддержки национальных облаков требуется предоставить центр.

#### <a name="registration"></a>Регистрация
* Для удобства методы регистрации являются идемпотентными. Например, `registerAccountForMAM()` только зарегистрирует учетную запись и попытается зарегистрировать приложение, если учетная запись еще не зарегистрирована, а `unregisterAccountForMAM()` только отменит регистрацию учетной записи, если она уже зарегистрирована. Последующие вызовы не являются операциями, поэтому эти методы можно вызывать многократно. Кроме того, не гарантируется ни соответствие между вызовами этих методов, ни отправка уведомлений о результатах. То есть если `registerAccountForMAM()` вызывается для удостоверения, которое уже зарегистрировано, уведомление для этого удостоверения может больше не отправляться. Вполне возможно, что отправленные уведомления просто не соответствуют вызовам этих методов, так как пакет SDK может периодически повторять попытки регистрации в фоновом режиме, а отмена регистрации может инициироваться запросами на очистку, полученными от службы Intune.

* Методы регистрации могут вызываться для любого числа различных удостоверений, но сейчас зарегистрировать можно только одну учетную запись пользователя. Если одновременно (или почти одновременно) регистрируется несколько учетных записей, лицензированных для использования Intune и предназначенных для применения политики защиты приложения, нельзя предсказать, какая из этих учетных записей будет в итоге зарегистрирована.

* В итоге вы можете выполнить запрос `MAMEnrollmentManager`, чтобы узнать, зарегистрирована ли определенная учетная запись, и получить сведения о ее текущем состоянии с помощью метода `getRegisteredAccountStatus()`. Если предоставленная учетная запись не зарегистрирована, этот метод вернет значение **null**. Если учетная запись зарегистрирована, этот метод вернет состояние учетной записи как одного из членов перечисления `MAMEnrollmentManager.Result`.

### <a name="result-and-status-codes"></a>Коды результатов и состояния
При первой регистрации учетной записи она находится в состоянии `PENDING`. Это состояние указывает на то, что первоначальная попытка регистрации службы MAM не завершена. Когда попытка регистрации будет завершена, будет отправлено уведомление с одним из кодов результатов, перечисленных в таблице ниже. Кроме того, метод `getRegisteredAccountStatus()` вернет состояние учетной записи. Так приложение всегда сможет определить, заблокирован ли доступ к корпоративному содержимому для этого пользователя. Если попытка регистрации учетной записи не удается, состояние учетной записи может меняться по мере того, как пакет SDK будет совершать попытки регистрации в фоновом режиме.

|Код результата | Описание |
| -- | -- |
| `AUTHORIZATION_NEEDED` | Этот результат показывает, что зарегистрированный экземпляр приложения `MAMServiceAuthenticationCallback` не предоставил токен или предоставил недопустимый токен.  Приложение должно получить действительный маркер и вызвать метод `updateToken()`, если это возможно. |
| `NOT_LICENSED` | Пользователь не лицензирован для использования Intune или не удалось связаться со службой Intune MAM.  Приложение должно продолжать работу в неуправляемом (обычном) состоянии, а пользователь не должен быть заблокирован.  Попытки регистрации будут периодически повторяться, если у пользователя в будущем появится лицензия . |
| `ENROLLMENT_SUCCEEDED` | Попытка регистрации выполнена или пользователь уже зарегистрирован.  В случае успешной регистрации уведомление об обновлении политики будет отправлено до отправки этого уведомления.  Должен быть разрешен доступ к корпоративным данным. |
| `ENROLLMENT_FAILED` | Попытка регистрации не удалась.  Дополнительные сведения см. в журналах устройства.  Приложение не должно разрешать доступ к корпоративным данным в этом состоянии, так как ранее было обнаружено, что у пользователя есть лицензия для Intune.|
| `WRONG_USER` | Только один пользователь устройства может зарегистрировать приложение с использованием службы MAM. Этот результат означает, что пользователь, для которого был доставлен этот результат (второй пользователь), подчиняется политике MAM, но другой пользователь уже зарегистрирован. Так как политика MAM не может быть применена ко второму пользователю, приложение не должно разрешать доступ к данным этого пользователя (возможно, путем удаления пользователя из приложения), пока для этого пользователя не будет выполнена успешная попытка регистрации. Параллельно предоставлению этого результата `WRONG_USER` MAM предложит удалить существующую учетную запись. Если пользователь согласится, можно будет зарегистрировать второго пользователя чуть позже. Пока второй пользователь остается зарегистрированным, MAM будет периодически повторять попытку регистрации. |
| `UNENROLLMENT_SUCCEEDED` | Отмена регистрации выполнена.|
| `UNENROLLMENT_FAILED` | Отмена регистрации не удалась.  Дополнительные сведения см. в журналах устройства. Как правило, это не происходит, пока приложение передает допустимое имя участника-пользователя (не null или пустое). Приложение не может использовать прямое и надежное исправление. Если это значение получено при отмене регистрации действительного имени участника-пользователя, сообщите об ошибке команде Intune MAM.|
| `PENDING` | Идет попытка первоначальной регистрации для пользователя.  Приложение может заблокировать доступ к корпоративным данным, пока не станет известен результат регистрации, но это не обязательно. |
| `COMPANY_PORTAL_REQUIRED` | У пользователя есть лицензия на использование Intune, но приложение нельзя зарегистрировать до установки приложения корпоративного портала на устройстве. Пакет SDK для приложений Intune попытается заблокировать доступ к приложению для определенного пользователя, предлагая установить приложение корпоративного портала (см. ниже). |


### <a name="company-portal-requirement-prompt-override-optional"></a>Переопределение строки запроса для требований корпоративного портала (необязательно)
Если получен результат `COMPANY_PORTAL_REQUIRED`, пакет SDK будет блокировать действия, использующие удостоверение, для которого запрошена регистрация. Вместо этого пакет SDK вызовет для этих действий отображение строки запроса на скачивание корпоративного портала. Чтобы предотвратить такое поведение в приложении, действия могут реализовать `MAMActivity.onMAMCompanyPortalRequired`.

Этот метод вызывается до того, как пакет SDK отобразит стандартный пользовательский интерфейс блокировки. Если приложение изменяет удостоверение действия или отменяет регистрацию пользователя, пытающегося зарегистрироваться, пакет SDK не будет блокировать действия. В этом случае приложение отвечает за предотвращение утечки корпоративных данных. Только приложения с множественной идентификацией (см. ниже) смогут изменить удостоверение действия.

Если вы явно не наследуете `MAMActivity` (так как это изменение будет выполнено средствами сборки), но по-прежнему хотите обрабатывать это уведомления, можно реализовать `MAMActivityBlockingListener`.

### <a name="notifications"></a>Уведомления
Если приложение регистрируется для получения уведомлений типа **MAM_ENROLLMENT_RESULT**, будут отправляться `MAMEnrollmentNotification` для уведомления приложения о завершении запроса на регистрацию. `MAMEnrollmentNotification` будет получен через интерфейс `MAMNotificationReceiver`, как описано в разделе [Регистрация для получения уведомлений из пакета SDK](#register-for-notifications-from-the-sdk).

```java
public interface MAMEnrollmentNotification extends MAMUserNotification {
    MAMEnrollmentManager.Result getEnrollmentResult();
}
```

Метод `getEnrollmentResult()` возвращает результат запроса на регистрацию.  Так как `MAMEnrollmentNotification` расширяет `MAMUserNotification`, также будет доступно удостоверение пользователя, для которого выполнена попытка регистрации. Приложение должно реализовать интерфейс `MAMNotificationReceiver` для получения этих уведомлений. Дополнительные сведения см. в разделе [Регистрация для получения уведомлений из пакета SDK](#register-for-notifications-from-the-sdk).

Состояние учетной записи зарегистрированного пользователя может измениться при получении уведомления о регистрации, но в некоторых случаях это не происходит. Например, если уведомление `AUTHORIZATION_NEEDED` будет получено после возврата более информативного результата (`WRONG_USER`), такой результат будет использоваться в качестве состояния учетной записи.  После успешной регистрации учетной записи состояние будет оставаться как `ENROLLMENT_SUCCEEDED`, пока учетная запись не будет разрегистрирована или очищена.

## <a name="app-ca-with-policy-assurance"></a>Условный доступ к политикам защиты приложений с Policy Assurance

### <a name="overview"></a>Обзор
С помощью условного доступа к политикам защиты приложений с Policy Assurance для доступа к ресурсам используются условия из политик защиты приложений Intune.  AAD следит за этим, требуя для приложения регистрации и управления политиками защиты приложений перед предоставлением токена для условного доступа к политикам защиты приложений с помощью ресурса, защищенного Policy Assurance.  Приложение должно использовать брокер ADAL для получения токена; настройка проводится так же, как описано выше в разделе [Условный доступ](#conditional-access).

### <a name="adal-changes"></a>Изменения в ADAL
Библиотека ADAL содержит новый код ошибки, говорящий приложению о том, что сбой при получении токена вызван несоответствием управлению политиками защиты приложений.  Если приложение получает этот код ошибки, ему необходимо вызвать метод пакета SDK, чтобы попытаться устранить несоответствие путем регистрации приложения и применения политики. Исключение будет получено методом `onError()` в ADAL `AuthenticationCallback` и иметь код ошибки `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED`.  В этом случае исключение может быть приведено в `IntuneAppProtectionPolicyRequiredException`, откуда можно извлечь дополнительные параметры для устранения соответствия (см. пример кода ниже). После успешного завершения исправления приложение может повторно попытаться получить токен через ADAL.

> [!NOTE]
> Этот новый код ошибки и прочая поддержка условного доступа к политикам защиты приложений с помощью Policy Assurance требуют библиотеку ADAL версии 1.15.0 (или более позднюю).

### <a name="mamcompliancemanager"></a>MAMComplianceManager
Интерфейс `MAMComplianceManager` используется при получении ошибки необходимой политики из ADAL.  Он содержит метод `remediateCompliance()`, который должен быть вызван, чтобы попытаться привести приложение в состояние соответствия. Ссылку на `MAMComplianceManager` можно получить так:

```java
MAMComplianceManager mgr = MAMComponents.get(MAMComplianceManager.class);

// make use of mgr
```

Возвращаемый экземпляр `MAMComplianceManager` гарантированно не будет иметь нулевое значение.

```java
package com.microsoft.intune.mam.policy;

public interface MAMComplianceManager {
    void remediateCompliance(String upn, String aadId, String tenantId, String authority, boolean showUX);
}
```

Вызывается метод `remediateCompliance()`, чтобы попытаться перевести приложение под управление, чтобы оно удовлетворяло условиям предоставления запрошенного токена для AAD.  Первые четыре параметра могут быть извлечены из исключения, полученного ADAL в методе `AuthenticationCallback.onError()` (см. пример кода ниже).  Последний параметр — это логическое значение, которое определяет, отображается ли пользовательский интерфейс во время попытки исправления соответствия.  Это простой блокирующий ход выполнения интерфейс, который используется по умолчанию для приложений, у которых нет необходимости отображения настраиваемого пользовательского интерфейса во время этой операции.  Интерфейс будет заблокирован на время исправления соответствия и не отобразит окончательный результат.  Приложению необходимо зарегистрировать приемник уведомлений для обработки успешной попытки исправления соответствия (см. ниже).

Метод `remediateCompliance()` может выполнять регистрацию MAM как часть обеспечения соответствия.  Приложение может получать уведомления о регистрации, если оно зарегистрировано как получатель уведомлений о регистрации.  Зарегистрированный приложением `MAMServiceAuthenticationCallback` будет получать вызовы метода `acquireToken()` для получения токена при регистрации MAM. `acquireToken()` будет вызываться, прежде чем приложение получит собственный токен, поэтому все задачи учета или создания учетных записей, которые приложение выполняет после успешного получения токена, пока еще не могут выполняться.  Функция обратного вызова должна иметь возможность получить токен в данном случае.  Если не удается вернуть токен из `acquireToken()`, попытка исправления соответствия не удастся.  При вызове метода `updateToken()` позже с допустимым токеном для запрошенного ресурса исправление соответствия будет немедленно повторено с заданным токеном.

> [!NOTE]
> Автоматическое получение токена по-прежнему возможно в `acquireToken()`, так как пользователь уже получил указание установить брокер и зарегистрировать устройство перед сообщением об ошибке `ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED`.  Это приводит к тому, что брокер имеет действительный токен обновления в своем кэше, позволяя успешно получить запрошенный токен автоматически.

Ниже приведен пример получения ошибки требования политики в методе `AuthenticationCallback.onError()` и вызова метода `MAMComplianceManager` для обработки ошибки.

```java
public void onError(@Nullable Exception exc) {
    if (exc instanceof AuthenticationException && 
        ((AuthenticationException) exc).getCode() == ADALError.AUTH_FAILED_INTUNE_POLICY_REQUIRED) {

        final IntuneAppProtectionPolicyRequiredException policyRequiredException = 
            (IntuneAppProtectionPolicyRequiredException) ex;

        final String upn = policyRequiredException.getAccountUpn();
        final String aadId = policyRequiredException.getAccountUserId();
        final String tenantId = policyRequiredException.getTenantId();
        final String authority = policyRequiredException.getAuthorityURL();

        MAMComplianceManager complianceManager = MAMComponents.get(MAMComplianceManager.class);
        complianceManager.remediateCompliance(upn, aadId, tenantId, authority, showUX);
    }
}
```

### <a name="status-notifications"></a>Уведомления о состоянии
Если приложение регистрируется для получения уведомлений типа **COMPLIANCE_STATUS**, `MAMComplianceNotification` будут отправляться для информирования приложения о конечном состоянии попытки исправления соответствия. `MAMComplianceNotification` будет получен через интерфейс `MAMNotificationReceiver`, как описано в разделе [Регистрация для получения уведомлений из пакета SDK](#register-for-notifications-from-the-sdk).

```java
public interface MAMComplianceNotification extends MAMUserNotification {
    MAMCAComplianceStatus getComplianceStatus();
    String getComplianceErrorTitle();
    String getComplianceErrorMessage();
}
```

Метод `getComplianceStatus()` возвращает результат попытки исправления соответствия в виде значения из перечисления `MAMCAComplianceStatus`.

|Код состояния | Описание |
| -- | -- |
| UNKNOWN | Состояние неизвестно. Это может означать непредвиденную ошибку. Дополнительные сведения см. в журналах корпоративного портала. |
| COMPLIANT | Исправление соответствия выполнено успешно, и приложение теперь соответствует требованиям политики. Следует повторить получение токена ADAL. |
| NOT_COMPLIANT | Не удалось исправить соответствие.  Приложение не соответствует требованиям, и получение токена ADAL не нужно повторять, пока вы не устраните ошибку.  Дополнительные сведения об ошибке отправляются вместе с MAMComplianceNotification. |
| SERVICE_FAILURE | Произошел сбой при попытке получить данные о соответствии из службы Intune. Дополнительные сведения см. в журналах корпоративного портала. |
| NETWORK_FAILURE | Ошибка подключения к службе Intune. Приложению следует попытаться получить токен еще раз, когда сетевое подключение будет восстановлено. |
| CLIENT_ERROR | Исправить несоответствие не удалось по некоторым причинам, относящимся к клиенту.  Например, нет токена или неправильно указан пользователь. Дополнительные сведения об ошибке отправляются вместе с MAMComplianceNotification. |
| PENDING | Исправить соответствие не удалось, так как ответ о состоянии еще не был получен от службы при превышении предела времени. Приложению следует повторить попытку получения токена позже. |
| COMPANY_PORTAL_REQUIRED | Корпоративный портал должен быть установлен на устройстве для успешного устранения проблем соответствия требованиям.  Если на устройстве уже установлен корпоративный портал, необходимо перезапустить приложение.  В этом случае отображается диалоговое окно с запросом на перезапуск приложения. |

Если состояние соответствия — `MAMCAComplianceStatus.COMPLIANT`, приложение должно повторно начать получение токена (для своего собственного ресурса). Если попытка исправления соответствия терпит сбой, методы `getComplianceErrorTitle()` и `getComplianceErrorMessage()` возвращают локализованные строки, которые приложение может отобразить для конечного пользователя, если нужно.  В большинстве случаев ошибка не может быть устранена приложением, поэтому в общем случае может быть оптимально завершить ошибкой создание учетной записи или вход и разрешить пользователю повторить попытку позже.  Если ошибка не устраняется, журналы MAM могут помочь определить причину.  Конечный пользователь может отправить журналы с помощью инструкций, приведенных [здесь](https://docs.microsoft.com/mem/intune/user-help/send-logs-to-your-it-admin-by-email-android "Отправка журналов по электронной почте в службу поддержки вашей компании").

Так как `MAMComplianceNotification` расширяет `MAMUserNotification`, также будет доступно удостоверение пользователя, для которого выполнена попытка исправления.

Ниже приведен пример регистрации получателя с помощью анонимного класса для реализации интерфейса MAMNotificationReceiver:

```java
final MAMNotificationReceiverRegistry notificationRegistry = MAMComponents.get(MAMNotificationReceiverRegistry.class);
// create a receiver
final MAMNotificationReceiver receiver = new MAMNotificationReceiver() {
    public boolean onReceive(MAMNotification notification) {
        if (notification.getType() == MAMNotificationType.COMPLIANCE_STATUS) {
            MAMComplianceNotification complianceNotification = (MAMComplianceNotification) notification;
            
            // take appropriate action based on complianceNotification.getComplianceStatus()
            
            // unregister this receiver if no longer needed
            notificationRegistry.unregisterReceiver(this, MAMNotificationType.COMPLIANCE_STATUS);
        }
        return true;
    }
};
// register the receiver
notificationRegistry.registerReceiver(receiver, MAMNotificationType.COMPLIANCE_STATUS);
```

> [!NOTE]
> Получатель уведомлений должен быть зарегистрирован перед вызовом `remediateCompliance()` во избежание состязания, которое может привести к пропуску уведомления.

### <a name="implementation-notes"></a>Примечания по реализации
> [!NOTE]
> **Важное изменение!**  <br>
> Метод приложения `MAMServiceAuthenticationCallback.acquireToken()` должен передать значение *false* для нового флага `forceRefresh` в `acquireTokenSilentSync()`.
> Ранее мы рекомендовали передать значение *true*, чтобы устранить ошибку обновления токенов от брокера, но была обнаружена проблема с ADAL, которая могла препятствовать получению токенов в некоторых сценариях, если этот флаг имеет значение *true*.
```java
AuthenticationResult result = acquireTokenSilentSync(resourceId, clientId, userId, /* forceRefresh */ false);
```

> [!NOTE]
> Если вы хотите показать пользовательский интерфейс блокировки во время попытки исправления, следует передать *false* в параметре showUX для `remediateCompliance()`. Необходимо убедиться, что вы выводите ваш интерфейс, и зарегистрировать прослушиватель уведомлений перед вызовом `remediateCompliance()`.  Это устранит условие конкуренции, когда уведомления могут быть пропущены, если `remediateCompliance()` очень быстро завершается ошибкой.  Например, метод `onCreate()` или `onMAMCreate()` подкласса Activity — это идеальное место для регистрации прослушивателя уведомлений и последующего вызова `remediateCompliance()`.  Параметры `remediateCompliance()` могут передаваться в ваш пользовательский интерфейс как дополнения Intent.  При получении уведомления о состоянии соответствия требованиям можно отобразить результат или просто завершить работу.

> [!NOTE]
> `remediateCompliance()` зарегистрирует учетную запись и произведет попытку регистрации.  Как только основной токен будет получен, вызывать `registerAccountForMAM()` необязательно, но от этого не будет никакого вреда. С другой стороны, если приложение не сможет получить токен и желает удалить учетную запись пользователя, оно должен вызвать `unregisterAccountForMAM()`, чтобы удалить учетную запись и предотвратить повторные попытки регистрации в фоновом режиме.

## <a name="protecting-backup-data"></a>Защита данных резервной копии
Начиная с Android Marshmallow (API 23), система Android предоставляет два способа резервного копирования данных приложением. Каждый вариант доступен в приложении и требует разных действий для правильного обеспечения защиты данных Intune. Действия, необходимые для защиты данных, указаны в приведенной ниже таблице.  Дополнительные сведения о способах резервного копирования см. в [справочнике по API Android](https://developer.android.com/guide/topics/data/backup.html).

### <a name="auto-backup-for-apps"></a>Автоматическое резервное копирование для приложений
Начиная с устройств Android Marshmallow, система Android начала предлагать [автоматическое полное резервное копирование](https://developer.android.com/guide/topics/data/autobackup.html) приложений Диска Google независимо от целевого API. Если в файле AndroidManifest.xml задать для атрибута `android:allowBackup` значение **false**, Android не будет добавлять приложение в очереди на резервное копирование, а корпоративные данные останутся в приложении. В этом случае никаких дополнительных действий не требуется.

Однако по умолчанию атрибут `android:allowBackup` имеет значение true, даже если `android:allowBackup` не указан в файле манифеста. Это означает, что для всех приложений автоматически создаются резервные копии в учетной записи пользователя на диске Google, т. е. используется поведение по умолчанию, связанное с **риском утечки данных**. В связи с этим для защиты данных в пакет SDK необходимо внести описанные ниже изменения.  Если вы хотите, чтобы ваше приложение работало на устройствах Android Marshmallow, выполните представленные ниже рекомендации по защите клиентских данных.  

Intune позволяет использовать все [функции автоматической архивации](https://developer.android.com/guide/topics/data/autobackup.html), доступные в системе Android, включая возможность настройки правил в формате XML, однако для защиты данных необходимо выполнить следующие действия:

1. Если приложение **не** использует собственный агент BackupAgent, разрешите полное автоматическое резервное копирование, соответствующее политике Intune, с помощью MAMBackupAgent по умолчанию. В манифесте приложения должно быть следующее:

    ```xml
    android:fullBackupOnly="true"
    android:backupAgent="com.microsoft.intune.mam.client.app.backup.MAMDefaultBackupAgent"
    ```
    
2. **[Необязательно]** Если реализуется необязательный пользовательский агент BackupAgent, необходимо использовать MAMBackupAgent или MAMBackupAgentHelper. См. следующие разделы. Попробуйте использовать агент Intune **MAMDefaultFullBackupAgent** (см. шаг 1), который обеспечивает простое и удобное резервное копирование в Android версии M и выше.

3. Выберите тип полного резервного копирования для своего приложения (без фильтра, с фильтром или нет), задав для атрибута `android:fullBackupContent` значение true или false либо указав XML-ресурс в своем приложении.

4. Затем вы _**должны**_ скопировать все, что необходимо вставить в атрибут `android:fullBackupContent`, в тег метаданных с именем `com.microsoft.intune.mam.FullBackupContent`.

    **Пример 1**. Если приложение должно иметь полные резервные копии без исключений, присвойте атрибуту `android:fullBackupContent` и тегу метаданных `com.microsoft.intune.mam.FullBackupContent` значение **true**:

    ```xml
    android:fullBackupContent="true"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="true" />  
    ```

    **Пример 2**. Если приложение должно использовать пользовательский агент BackupAgent, не прибегая к полному и совместимому с политиками Intune автоматическому резервному копированию, необходимо присвоить атрибуту и тегу метаданных значение **false**:

    ```xml
    android:fullBackupContent="false"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:value="false" />  
    ```

    **Пример 3**. Если приложение должно иметь полные резервные копии в соответствии с пользовательскими правилами, определенными в XML-файле, укажите атрибут и тег метаданных в одном ресурсе XML:

    ```xml
    android:fullBackupContent="@xml/my_scheme"
    ...
    <meta-data android:name="com.microsoft.intune.mam.FullBackupContent" android:resource="@xml/my_scheme" />  
    ```

### <a name="keyvalue-backup"></a>Резервные копии "ключ-значение"
Параметр [Резервные копии "ключ-значение"](https://developer.android.com/guide/topics/data/keyvaluebackup.html) доступен для всех API-интерфейсов версии 8 и выше. Он позволяет передавать данные приложения в [службу резервного копирования Android](https://developer.android.com/google/backup/index.html). Объем данных для каждого пользователя приложения ограничен 5 МБ. При использовании резервных копий "ключ-значение" необходимо использовать **BackupAgentHelper** или **BackupAgent**.

### <a name="backupagenthelper"></a>BackupAgentHelper
Реализовать BackupAgentHelper гораздо проще, чем BackupAgent. Это относится как к собственным функциям Android, так и к интеграции Intune MAM. BackupAgentHelper позволяет разработчику регистрировать целые файлы и общие настройки в **FileBackupHelper** или **SharedPreferencesBackupHelper** соответственно, которые затем добавляются в BackupAgentHelper при создании. Выполните следующие действия, чтобы использовать BackupAgentHelper с Intune MAM:

1. Для использования резервного копирования с множественной идентификацией с помощью BackupAgentHelper ознакомьтесь с руководством по [расширению BackupAgentHelper в Android](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgentHelper).

2. Обеспечьте расширение класса эквивалента MAM для BackupAgentHelper, FileBackupHelper и SharedPreferencesBackupHelper.

|Класс Android | Эквивалент MAM |
|--|--|
|BackupAgentHelper |MAMBackupAgentHelper |
|FileBackupHelper | MAMFileBackupHelper
|SharedPreferencesBackupHelper| MAMSharedPreferencesBackupHelper|

Следуя этим рекомендациям, вы выполните резервное копирование и восстановление с множественной идентификацией.

### <a name="backupagent"></a>BackupAgent

Агент BackupAgent позволяет явно определить, какие именно данные следует копировать. Так как за реализацию отвечает разработчик, нужно выполнить дополнительные шаги для обеспечения защиты данных из Intune. Большая часть работы возложена на вас как разработчика, поэтому интеграция Intune играет более важную роль.

**Интеграция MAM**

1. Внимательно прочитайте руководство по [резервному копированию пар "ключ-значение"](https://developer.android.com/guide/topics/data/keyvaluebackup.html) в Android, уделив особое внимание сведениям о [расширении BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent). Так вы обеспечите соответствие вашей реализации BackupAgent рекомендациям Android.

2. Обеспечьте расширение класса `MAMBackupAgent`.

**Резервное копирование с множественной идентификацией**

1. Перед началом резервного копирования нужно определить, **разрешено ли ИТ-администратору создавать резервные копии** необходимых файлов или буферов данных в сценариях с использованием множественной идентификации. Для этого мы предоставляем функцию `isBackupAllowed` в `MAMFileProtectionManager` и `MAMDataProtectionManager`. Если для файла или буфера данных нельзя создавать резервную копию, вы не сможете использовать эти ресурсы в ходе резервного копирования.

2. Если в определенный момент во время резервного копирования вам нужно создать резервную копию удостоверений для файлов, проверенных на шаге 1, вызовите `backupMAMFileIdentity(BackupDataOutput data, File … files)` с файлами, из которых вы планируете извлекать данные. При этом автоматически создаются новые сущности резервного копирования, которые записываются в `BackupDataOutput` . Эти сущности будут автоматически использоваться при восстановлении.

**Восстановление с множественной идентификацией**

Руководство по резервному копированию данных определяет общий алгоритм для восстановления данных приложения и содержит пример кода в разделе о [расширении агента BackupAgent](https://developer.android.com/guide/topics/data/keyvaluebackup.html#BackupAgent). Для реализации успешного восстановления с множественной идентификацией вам нужно придерживаться общей структуры, представленной в примере кода. Также учтите следующее:

1. Необходимо использовать цикл `while(data.readNextHeader())` для обработки сущностей резервного копирования. В предыдущем коде `data` — это имя локальной переменной для **MAMBackupDataInput** (передается в приложение после восстановления).

2. Необходимо вызвать `data.skipEntityData()`, если `data.getKey()` не соответствует ключу, созданному в `onBackup`. Без выполнения этого шага восстановление может завершиться ошибкой. В предыдущем коде `data` — это имя локальной переменной для **MAMBackupDataInput** (передается в приложение после восстановления).

3. Старайтесь не возвращать результат при использовании сущностей резервного копирования в конструкции `while(data.readNextHeader())`, так как эти автоматически записываемые сущности будут утеряны. В предыдущем коде `data` — это имя локальной переменной для **MAMBackupDataInput** (передается в приложение после восстановления).

## <a name="multi-identity-optional"></a>Использование нескольких удостоверений (необязательно)

### <a name="overview"></a>Обзор
По умолчанию пакет SDK для приложений Intune применяет политику для всего приложения. Множественная идентификация — это дополнительная функция защиты приложений Intune, которую можно включить, чтобы разрешить применение политики на уровне удостоверения. Для этого требуется намного больше действий со стороны приложения, чем при использовании других функций защиты приложений.

> [!NOTE]
> Если приложение не участвует должным образом во взаимодействии, возможна утечка данных или другие проблемы с безопасностью.

Когда приложение или устройство будет зарегистрировано пользователем, пакет SDK будет использовать это удостоверение, считая его основным управляемым удостоверением Intune. Другие пользователи в приложении будут рассматриваться как неуправляемые и не имеющие ограничений для параметров политик.

> [!NOTE]
> Сейчас поддерживается только одно управляемое удостоверение Intune на устройство.

Удостоверение определяется как строка. Удостоверения задаются **без учета регистра**, а запросы удостоверения, направляемые к пакету SDK, могут возвращать удостоверения с использованием другого регистра.

Приложение *обязано* уведомить пакет SDK о том, что оно собирается сменить активное удостоверение. В некоторых случаях пакет SDK также будет уведомлять приложение, когда удостоверение требуется заменить. В большинстве случаев MAM не может знать, какие данные сейчас отображаются в пользовательском интерфейсе или используются в потоке, и при задании удостоверения полагается на приложение, чтобы избежать утечки данных. В следующих разделах будут отмечен ряд сценариев, в которых требуется действие от приложений.

### <a name="enabling-multi-identity"></a>Включение множественного удостоверения
По умолчанию все приложения считаются приложениями с одним удостоверением. Вы можете объявить для приложения поддержку множественной идентификации, добавив следующие метаданные в AndroidManifest.xml.

```xml
  <meta-data
    android:name="com.microsoft.intune.mam.MAMMultiIdentity"
    android:value="true" />
```

### <a name="setting-the-identity"></a>Задание удостоверения
Разработчики могут определять удостоверение пользователя приложения на следующих уровнях (в порядке убывания):

  1. Уровень потока.
  2. Уровень `Context` (обычно `Activity`)
  3. Уровень процесса.

Удостоверение, заданное на уровне потока, заменяет удостоверение, заданное на уровне `Context`, которое, в свою очередь, заменяет удостоверение, заданное на уровне процесса. Удостоверение, заданное в контексте `Context`, используется только в соответствующих связанных сценариях. Например, с операциями ввода-вывода файлов никакой контекст `Context` не связан. Чаще всего приложения задают удостоверение `Context` для `Activity`. Приложение *не должно* отображать данные для управляемого удостоверения, если оно не совпадает с удостоверением `Activity`. В общем случае удостоверение уровня процесса помогает, только если приложение в любой момент работает только с одним пользователем во всех потоках. Во многих приложениях это не требуется.

Если приложение использует контекст `Application` для получения системных служб, убедитесь, что задано удостоверение потока или процесса либо удостоверение пользовательского интерфейса у контекста `Application` вашего приложения.

Для обработки особых случаев при обновлении удостоверения пользовательского интерфейса с помощью `setUIPolicyIdentity` или `switchMAMIdentity` в оба метода может передаваться набор значений `IdentitySwitchOption`.

* `IGNORE_INTENT`: используется, если запрашивается переключение удостоверения, которому следует игнорировать намерения, связанные с текущим действием.
  Пример.

  1. Приложение получает объект намерения от управляемого удостоверения, содержащего управляемый документ, и приложение отображает документ.
  2. Пользователь переходит на использование своих личных учетных данных, поэтому приложение запрашивает замену удостоверений пользовательского интерфейса. В личном удостоверении приложение больше не отображает документ, поэтому используется `IGNORE_INTENT` при запросе переключения удостоверения.

  Если оно не задано, пакет SDK предполагает, что последнее намерение по-прежнему используется в приложении. В результате политика получения для нового удостоверения обрабатывает намерение как входящие данные и использует его идентификатор.

>[!NOTE]
> Так как `CLIPBOARD_SERVICE` используется для операций пользовательского интерфейса, в пакете SDK используется удостоверение пользовательского интерфейса переднего плана для операций `ClipboardManager`.
> Вы можете использовать следующие методы в `MAMPolicyManager`, чтобы определить удостоверение и получить значения удостоверений, определенные ранее.

```java
public static void setUIPolicyIdentity(final Context context, final String identity, final MAMSetUIIdentityCallback mamSetUIIdentityCallback, final EnumSet<IdentitySwitchOption> options);

  public static String getUIPolicyIdentity(final Context context);

  public static MAMIdentitySwitchResult setProcessIdentity(final String identity);

  public static String getProcessIdentity();

  public static MAMIdentitySwitchResult setCurrentThreadIdentity(final String identity);

  public static String getCurrentThreadIdentity();

/**
   * Get the current app policy. This does NOT take the UI (Context) identity into account.
   * If the current operation has any context (e.g. an Activity) associated with it, use the overload below.
   */
  public static AppPolicy getPolicy();

  /**
  * Get the current app policy. This DOES take the UI (Context) identity into account.
   * If the current operation has any context (e.g. an Activity) associated with it, use this function.
   */
  public static AppPolicy getPolicy(final Context context);


  public static AppPolicy getPolicyForIdentity(final String identity);

  public static boolean getIsIdentityManaged(final String identity);
  ```

>[!NOTE]
> Удостоверение приложения можно сбросить, присвоив ему нулевое значение.
>
> В качестве удостоверения можно использовать пустую строку. В этом случае политики защиты приложений применяться больше не будут.

#### <a name="results"></a>Результаты
Все методы определения удостоверений возвращают соответствующие значения с помощью атрибута `MAMIdentitySwitchResult`. Возвращаться могут четыре значения:

| Возвращаемое значение | Сценарий |
|--            |--        |
| `SUCCEEDED`    | Удостоверение изменено. |
| `NOT_ALLOWED`  | Изменение удостоверения запрещено. Это происходит при попытке задать удостоверение на уровне пользовательского интерфейса (`Context`), когда указано другое удостоверение для текущего потока. |
| `CANCELLED`    | Пользователь отменил изменение удостоверения. Обычно это делается при нажатии кнопки возврата в запросе ввести PIN-код или выполнить аутентификацию. |
| `FAILED`       | Изменить удостоверение не удалось по неизвестной причине.|

Приложение обязано проверить, что удостоверение заменено, прежде чем отображать или использовать корпоративные данные. Замена удостоверений процессов и потоков сейчас всегда будет выполняться для приложений с поддержкой нескольких удостоверений, но мы оставляем за собой право добавить условия для сбоев. Эта процедура может завершиться сбоем из-за недопустимых аргументов или конфликта с удостоверением потока либо если пользователь не выполнит условные требования для запуска (например, нажмет кнопку "Назад" на экране для ввода PIN-кода). Поведение по умолчанию для параметра удостоверения пользовательского интерфейса со сбоем в действии заключается в завершении действия (см. `onSwitchMAMIdentityComplete` ниже).

Если удостоверение задается на уровне `Context` с помощью `setUIPolicyIdentity`, результаты передаются асинхронно. Если `Context` является `Activity`, пакет SDK не сможет проверить изменение удостоверения, пока не будет выполнен условный запуск. Для этого пользователю может потребоваться ввести PIN-код или данные корпоративной учетной записи. Приложение может реализовать `MAMSetUIIdentityCallback` для получения этого результата или передать значение NULL для объекта обратного вызова. Обратите внимание, что если выполняется вызов `setUIPolicyIdentity`, в то время как результат предыдущего вызова `setUIPolicyIdentity` *в том же контексте* еще не доставлен, новый обратный вызов заменит старый, а исходный обратный вызов никогда не получит результат.

```java
    public interface MAMSetUIIdentityCallback {
        void notifyIdentityResult(MAMIdentitySwitchResult identitySwitchResult);
  }
```

Удостоверения на уровне действия можно также задать, не вызывая `MAMPolicyManager.setUIPolicyIdentity`, а с помощью метода в `MAMActivity`. Используйте для этого следующий метод:

```java
     public final void switchMAMIdentity(final String newIdentity, final EnumSet<IdentitySwitchOption> options);
```

Приложения могут также переопределять метод в `MAMActivity`, чтобы получать уведомления о результатах попыток изменения удостоверений на уровне действия.

``` java
    public void onSwitchMAMIdentityComplete(final MAMIdentitySwitchResult result);
```

Если не переопределить `onSwitchMAMIdentityComplete` (или не вызвать `super` метод), сбой переключения удостоверений в действии приведет к его завершению. При переопределении метода необходимо соблюдать осторожность, чтобы корпоративные данные не отображались после неудачного переключения удостоверений.

>[!NOTE]
> Для переключения удостоверения может потребоваться повторно создать действие. В этом случае обратный вызов `onSwitchMAMIdentityComplete` осуществляется в новый экземпляр действия.


### <a name="implicit-identity-changes"></a>Неявные изменения удостоверений
Задать удостоверение может не только приложение. Удостоверение на уровне потока или контекста может быть изменено на основе данных, поступивших из другого управляемого приложения Intune с политикой защиты приложений.

#### <a name="examples"></a>Примеры
1. Если действие запускается из `Intent` при отправке другому приложению MAM, удостоверение этого действия определяется с учетом удостоверения, действующего в другом приложении на момент отправки `Intent`.

2. Для служб удостоверение на уровне потока определяется аналогично на время вызова метода `onStart` или `onBind`. Вызовы в `Binder`, возвращенные из `onBind`, также временно определяют удостоверение на уровне потока.

3. Вызовы в `ContentProvider` задают удостоверение на уровне потока на время своего действия аналогичным образом.


    Кроме того, взаимодействие пользователя с действием может вызвать неявное переключение удостоверения.

    **Пример.** Если пользователь нажмет кнопку отмены в запросе на аутентификацию во время выполнения `Resume`, произойдет неявное переключение на пустое удостоверение.

    Приложение сможет узнавать о таких изменениях, а в некоторых случаях и запрещать их при необходимости. `MAMService` и `MAMContentProvider` предоставляют следующий метод, который подклассы могут переопределять:

    ```java
    public void onMAMIdentitySwitchRequired(final String identity,
      final AppIdentitySwitchResultCallback callback);
    ```

    При использовании класса `MAMActivity` в метод добавляется еще один параметр:

    ```java
    public void onMAMIdentitySwitchRequired(final String identity,
      final AppIdentitySwitchReason reason,
      final AppIdentitySwitchResultCallback callback);
    ```

    * `AppIdentitySwitchReason` фиксирует источник неявного переключения и может принимать значения `CREATE`, `RESUME_CANCELLED` и `NEW_INTENT`.  Если действие Resume вызывает отображение запроса PIN-кода, проверки подлинности или других элементов пользовательского интерфейса, связанных с соответствием, а пользователь пытается их отменить (обычно используя кнопку возврата), используется причина `RESUME_CANCELLED`.


    * `AppIdentitySwitchResultCallback` выглядит так:

      ```java
      public interface AppIdentitySwitchResultCallback {
          /**
            * @param result
            *            whether the identity switch can proceed.
            */
          void reportIdentitySwitchResult(AppIdentitySwitchResult result);
        }
        ```

      Здесь ```AppIdentitySwitchResult``` имеет значение `SUCCESS` или `FAILURE`.

Метод `onMAMIdentitySwitchRequired` вызывается для всех неявных изменений удостоверения, кроме связанных с возвратом средства привязки из `MAMService.onMAMBind`. Стандартные реализации `onMAMIdentitySwitchRequired` вызываются сразу же:

* `reportIdentitySwitchResult(FAILURE)`, если причиной является `RESUME_CANCELLED`.

* `reportIdentitySwitchResult(SUCCESS)` — во всех остальных случаях.

  Предполагается, что большинству приложений не требуется блокировать или откладывать переключение удостоверений каким-либо другим образом. Но если это не так, следует принимать во внимание следующие моменты:

  * Если переключение удостоверения заблокировано, результат аналогичен случаю, когда параметры общего доступа `Receive` запрещают входящие данные.

  * Если служба работает в основном потоке, `reportIdentitySwitchResult` **необходимо** вызывать асинхронно, иначе пользовательский интерфейс может зависнуть.

  * Для создания **`Activity`** параметр `onMAMIdentitySwitchRequired` будет вызываться до вызова метода `onMAMCreate`. Если приложение должно отображать интерфейс пользователя, чтобы определить, необходимо ли разрешить переключение удостоверения, интерфейс необходимо отображать, используя *другое* действие.

  * Если **`Activity`** запрашивает переключение на пустое удостоверение по причине `RESUME_CANCELLED`, приложение должно изменить возобновленное действие таким образом, чтобы отобразить данные, связанные с переключением удостоверения.  Если это невозможно, приложение должно запретить переключение и отобразить повторный запрос в соответствии с политикой возобновления удостоверения (например, отобразить экран для ввода PIN-кода).

    > [!NOTE]
    > Приложение с несколькими удостоверениями всегда получает входящие данные как из управляемых, так и из неуправляемых приложений. Приложение должно обрабатывать данные из управляемых удостоверений управляемым образом.

  Если запрошенное удостоверение является управляемым (используйте `MAMPolicyManager.getIsIdentityManaged` для проверки), но приложение не может использовать эту учетную запись (например, потому что учетные записи, такие как учетные записи электронной почты, должны быть сначала настроены в приложении), в переключении удостоверения будет отказано.

#### <a name="build-plugin--tool-considerations"></a>Особенности использования средства или подключаемого модуля сборки
Если вы явным образом не наследуете от `MAMActivity`, `MAMService` или `MAMContentProvider` (так как это изменение будет выполняться с помощью средства сборки), но по-прежнему хотите обрабатывать параметры удостоверений, можно реализовать `MAMActivityIdentityRequirementListener` (для `Activity`) или `MAMIdentityRequirementListener` (для `Service` или `ContentProviders`).
Для доступа к поведению по умолчанию для `MAMActivity.onMAMIdentitySwitchRequired` можно использовать вызов статического метода `MAMActivity.defaultOnMAMIdentitySwitchRequired(activity, identity,
reason, callback)`.

Аналогичным образом, если необходимо переопределить `MAMActivity.onSwitchMAMIdentityComplete`, можно реализовать `MAMActivityIdentitySwitchListener` без явного наследования от `MAMActivity`.

### <a name="preserving-identity-in-async-operations"></a>Сохранение удостоверений в асинхронных операциях
Обычно операции в потоке пользовательского интерфейса отправляют фоновые задачи в другой поток. В приложении с несколькими удостоверениями эти фоновые задачи должны выполняться с соответствующим удостоверением, которое часто совпадает с удостоверением, используемым отправившим его действием. Пакет SDK для MAM предоставляет `MAMAsyncTask` и `MAMIdentityExecutors` для удобства при сохранении удостоверений.
Необходимо использовать их, если асинхронная операция записывает корпоративные данные в файл или может взаимодействовать с другими приложениями.

#### <a name="mamasynctask"></a>MAMAsyncTask
Чтобы использовать класс `MAMAsyncTask`, просто унаследуйте его вместо `AsyncTask` и замените переопределения `doInBackground` и `onPreExecute` на `doInBackgroundMAM` и `onPreExecuteMAM`, соответственно. Конструктор `MAMAsyncTask` принимает контекст действия. Пример.

```java
  AsyncTask<Object, Object, Object> task = new MAMAsyncTask<Object, Object, Object>(thisActivity) {

    @Override
    protected Object doInBackgroundMAM(final Object[] params) {
        // Do operations.
    }

    @Override
    protected void onPreExecuteMAM() {
        // Do setup.
    };
}
```

### <a name="mamidentityexecutors"></a>MAMIdentityExecutors
`MAMIdentityExecutors` позволяет упаковывать существующий экземпляр `Executor` или `ExecutorService` как сохраняющий удостоверения `Executor`/`ExecutorService` с помощью методов `wrapExecutor` и `wrapExecutorService`. Например:

```java
  Executor wrappedExecutor = MAMIdentityExecutors.wrapExecutor(originalExecutor, activity);
  ExecutorService wrappedService = MAMIdentityExecutors.wrapExecutorService(originalExecutorService, activity);
```

### <a name="file-protection"></a>Защита файлов
При создании каждого файла к нему привязывается удостоверение потока или процесса. Оно будет использоваться и для шифрования файлов, и для выборочной очистки. Шифруются только те файлы, удостоверение которых управляется и имеет политику, которая требует шифрования. Функция выборочной очистки пакета SDK по умолчанию удаляет только файлы, связанные с управляемым удостоверением, для которого запрошена очистка. Приложение может запросить или изменить удостоверение файла с помощью класса `MAMFileProtectionManager`.

```java
public final class MAMFileProtectionManager {

   /**
    * Protect a file or directory. This will synchronously trigger whatever protection is required for the file, and will tag the
    * file for future protection changes. If an identity is set on a directory, it is set recursively on all files and
    * subdirectories. New files or directories will inherit their parent directory's identity. If MAM is operating in offline mode,
    * this method will silently do nothing.
    *
    * @param identity
    *         Identity to set.
    * @param file
    *         File to protect.
    *
    * @throws IOException
    *         If the file cannot be protected.
    */
   public static void protect(final File file, final String identity) throws IOException;

   /**
     * Protect a file obtained from a content provider. This is intended to be used for
     * sdcard (whether internal or removable) files accessed through the Storage Access Framework.
     * It may also be used with descriptors referring to private files owned by this app.
     * It is not intended to be used for files owned by other apps and such usage will fail. If
     * creating a new file via a content provider exposed by another MAM-integrated app, the new
     * file identity will automatically be set correctly if the ContentResolver in use was
     * obtained via a Context with an identity or if the thread identity is set.
     *
     * This will synchronously trigger whatever protection is required for the file, and will tag
     * the file for future protection changes. If an identity is set on a directory, it is set
     * recursively on all files and subdirectories. If MAM is operating in offline mode, this
     * method will silently do nothing.
     *
     * @param identity
     *            Identity to set.
     * @param file
     *            File to protect.
     *
     * @throws IOException
     *             If the file cannot be protected.
     */
    public static void protect(final ParcelFileDescriptor file, final String identity) throws IOException;

   /**
    * Get the protection info on a file.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final File file) throws IOException;

   /**
    * Get the protection info on a file.
    *
    * @param file
    *            File or directory to get information on.
    * @return File protection info, or null if there is no protection info.
    * @throws IOException
    *             If the file cannot be read or opened.
    */
    public static MAMFileProtectionInfo getProtectionInfo(final ParcelFileDescriptor file) throws IOException;

}

public interface MAMFileProtectionInfo {
    String getIdentity();
}
 ```

#### <a name="app-responsibility"></a>Ответственность приложения
MAM не может автоматически определить связь между читаемыми файлами и отображаемыми данными в `Activity`. Приложения *обязаны* должным образом задать удостоверение пользовательского интерфейса, прежде чем отображать корпоративные данные. Это относится и к данным, прочитанным из файлов. Если файл получен извне приложения (из `ContentProvider` или прочитан из общего доступного для записи расположения), приложение *обязано* попытаться определить удостоверение файла (с использованием `MAMFileProtectionManager.getProtectionInfo`), прежде чем отображать прочитанные из файла сведения. Если `getProtectionInfo` сообщает о ненулевом и непустом удостоверении, удостоверение пользовательского интерфейса *обязано* быть назначено таким же (с использованием `MAMActivity.switchMAMIdentity` или `MAMPolicyManager.setUIPolicyIdentity`). Если замена удостоверения не сработает, данные из файла *не должны* отображаться.

Пример рабочего потока:
* Пользователь выбирает документ, который нужно открыть в приложении.
  * В ходе потока открытия, перед чтением данных с диска приложение подтверждает удостоверение, которое следует использовать для отображения содержимого:

    ```java
    MAMFileProtectionInfo info = MAMFileProtectionManager.getProtectionInfo(docPath)
    if (info != null)
        MAMPolicyManager.setUIPolicyIdentity(activity, info.getIdentity(), callback, EnumSet.noneOf<IdentitySwitchOption.class>)
    ```

  * Приложение ожидает отправки результата в обратный вызов.
  * Если происходит сбой отправленного результата, приложение не отображает документ.
* Приложение открывает и обрабатывает файл.
  
#### <a name="single-identity-to-multi-identity-transition"></a>Переход от единой идентификации к множественной
Если приложение, выпущенное ранее с интеграцией Intune с одним удостоверением, интегрируется с множественной идентификацией, ранее установленные приложения должны будут произвести переход (не отображается для пользователя, не связан с интерфейсом). Приложению не *требуется* делать что-либо явно для такого перехода. Все файлы, созданные до перехода, будут по-прежнему рассматриваться как управляемые (поэтому они остаются зашифрованными, если включена политика шифрования). При желании можно обнаружить обновление и использовать `MAMFileProtectionManager.protect`, чтобы пометить определенные файлы или каталоги пустым удостоверением (что удалит шифрование, если они были зашифрованы).

#### <a name="offline-scenarios"></a>Автономные сценарии
Удостоверение файла маркируется как чувствительное к автономному режиму. Необходимо учитывать следующее:

* Если корпоративный портал не установлен, удостоверения файлов маркировать нельзя.

* Если корпоративный портал установлен, но приложение не имеет политику Intune MAM, надежная маркировка удостоверений для файлов невозможна.

* Если маркировка удостоверений файлов становится доступной, все созданные ранее файлы считаются личными или неуправляемыми (относящимися к удостоверению с пустой строкой). Но если приложение установлено как управляемое приложение с одним удостоверением, такие файлы будут считаться принадлежащими зарегистрированному пользователю.

### <a name="directory-protection"></a>Защита каталога
Каталоги можно защищать с помощью того же метода `protect`, используемого для защиты файлов. Защита каталога применяется рекурсивно ко всем файлам и подкаталогам, содержащимся в каталоге, а также к файлам, создаваемым в каталоге. Так как защита каталога применяется рекурсивно, вызов `protect` может занять некоторое время для больших каталогов. По этой причине при применении защиты для каталога, который содержит большое число файлов приложения, может потребоваться асинхронный запуск `protect` в фоновом потоке.

### <a name="data-protection"></a>Защита данных
Маркировать файл как принадлежащий нескольким удостоверениям нельзя. Приложения, которые должны сохранять принадлежащие разным пользователям данные в один файл, могут делать это с помощью функций, предоставляемых `MAMDataProtectionManager`. Он позволяет приложению шифровать данные и привязывать их к определенному пользователю. Зашифрованные данные можно сохранять на диск в файле. Вы можете запросить данные, связанные с удостоверением, и расшифровать их позднее.

Приложения, использующие `MAMDataProtectionManager`, должны реализовать получатель для уведомления `MANAGEMENT_REMOVED`. Когда обработка уведомления будет выполнена, защищенные с помощью этого класса буферы больше не будут доступными для чтения, если при применении защиты буферов было включено шифрование файлов. Приложение может решить эту проблему, вызвав `MAMDataProtectionManager.unprotect` для всех буферов при обработке этого уведомления. Вызывать защиту во время обработки этого уведомления также безопасно, если нужно сохранить сведения об удостоверении. Во время обработки удостоверения шифрование будет отключено.

```java

public final class MAMDataProtectionManager {
    /**
     * Protect a stream. This will return a stream containing the protected
     * input.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect, read sequentially. This function
     *            will change the position of the stream but may not have
     *            read the entire stream by the time it returns. The
     *            returned stream will wrap this one. Calls to read on the
     *            returned stream may cause further reads on the original
     *            input stream. Callers should not expect to read directly
     *            from the input stream after passing it to this method.
     *            Calling close on the returned stream will close this one.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static InputStream protect(final InputStream input, final String identity);

    /**
     * Protect a byte array. This will return protected bytes.
     *
     * @param identity
     *            Identity to set.
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be protected
     */
    public static byte[] protect(final byte[] input, final String identity) throws IOException;

    /**
     * Unprotect a stream. This will return a stream containing the
     * unprotected input.
     *
     * @param input
     *            Input data to protect, read sequentially.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static InputStream unprotect(final InputStream input) throws IOException;

    /**
     * Unprotect a byte array. This will return unprotected bytes.
     *
     * @param input
     *            Input data to protect.
     * @return Protected input data.
     * @throws IOException
     *             If the data could not be unprotected
     */
    public static byte[] unprotect(final byte[] input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input stream to get information on. Either this input
     *            stream must have been returned by a previous call to
     *            protect OR input.markSupported() must return true.
     *            Otherwise it will be impossible to get protection info
     *            without advancing the stream position. The stream must be
     *            positioned at the beginning of the protected data.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final InputStream input) throws IOException;

    /**
     * Get the protection info on a stream.
     *
     * @param input
     *            Input bytes to get information on. These must be bytes
     *            returned by a previous call to protect() or a copy of
     *            such bytes.
     * @return Data protection info, or null if there is no protection
     *            info.
     * @throws IOException
     *             If the input cannot be read.
     */
    public static MAMDataProtectionInfo getProtectionInfo(final byte[] input) throws IOException;
}
```

### <a name="content-providers"></a>Поставщики содержимого
Если приложение предоставляет корпоративные данные, отличные от `ParcelFileDescriptor` через `ContentProvider`, приложение должно вызвать метод `isProvideContentAllowed(String)` в `MAMContentProvider`, передав идентификатор владельца UPN (имя участника-пользователя) для содержимого. Если эта функция возвращает значение false, содержимое *не должно* возвращаться вызывающему. Дескрипторы файлов, возвращенные с помощью поставщика содержимого, обрабатываются автоматически, исходя из удостоверения файла.

Если вы не наследуете `MAMContentProvider` явным образом и вместо этого разрешите средствам сборки внести это изменение, можно вызывать статическую версию метода: `MAMContentProvider.isProvideContentAllowed(provider,
contentIdentity)`.

### <a name="selective-wipe"></a>Выборочная очистка
Если приложение с множественной идентификацией регистрирует уведомление `WIPE_USER_DATA`, такое приложение отвечает за очистку всех данных удаляемого пользователя, включая все файлы, которые были отмечены в удостоверении как принадлежащие этому пользователю. Если приложение удаляет пользовательские данные из файла, но хочет оставить там другие данные, оно *должно* изменить удостоверение файла (посредством `MAMFileProtectionManager.protect` на личное удостоверение пользователя или пустое удостоверение). Если используется политика шифрования, все оставшиеся файлы, принадлежащие удаляемому пользователю, не расшифровываются и станут недоступными для приложения после очистки.

Если приложение регистрируется для `WIPE_USER_DATA`, стандартная выборочная очистка, выполняемая пакетом SDK, будет для него недоступна. Для приложений с поддержкой множественной идентификации это может быть существенно, так как стандартная выборочная очистка MAM по умолчанию удаляет только файлы, удостоверение которых предполагает такую очистку. Если для приложения с поддержкой множественной идентификации требуется стандартная выборочная очистка MAM, которая, тем не менее, должна выполняться _**самостоятельно**_ , такое приложение необходимо зарегистрировать для использования уведомлений `WIPE_USER_AUXILIARY_DATA`. Такие уведомления будут отправляться пакетом SDK непосредственно перед выполнением стандартной выборочной очистки MAM. Одновременно регистрировать приложение для получения уведомлений `WIPE_USER_DATA` и `WIPE_USER_AUXILIARY_DATA` нельзя.

Выборочная очистка по умолчанию корректно закроет приложение, завершит действия и процесс приложения. Если приложение переопределяет выборочную очистку по умолчанию, рекомендуется закрыть приложение вручную, чтобы запретить пользователям доступ к данным в памяти после очистки.

## <a name="enabling-mam-targeted-configuration-for-your-android-applications-optional"></a>Включение целевой конфигурации MAM для приложений Android (необязательно)
Вы можете настроить в консоли Intune пары "ключ-значение" для конкретных приложений [MAM-WE](https://docs.microsoft.com/intune/app-configuration-policies-managed-app) и [Android Enterprise](https://docs.microsoft.com/intune/app-configuration-policies-use-android).
Intune не интерпретирует эти пары. Они передаются в приложение. Приложения, которым нужно получить такую конфигурацию, могут использовать для этого классы `MAMAppConfigManager` и `MAMAppConfig`. Если на одно приложение нацелены несколько политик, возможно, для одного ключа доступно несколько конфликтующих значений.

> [!NOTE] 
> Настройку конфигурации для передачи с помощью MAM-WE невозможно доставить в `offline` (если Корпоративный портал не установлен).  Только Android Enterprise AppRestrictions будут доставляться через `MAMUserNotification` при пустом удостоверении в этом случае.

### <a name="get-the-app-config-for-a-user"></a>Получение конфигурации приложения для пользователя
Конфигурацию приложения можно получить следующим образом:
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
```

Если зарегистрированного пользователя MAM нет, но ваше приложение по-прежнему хочет получить конфигурацию Android Enterprise (которая не будет нацелена на конкретного пользователя), можно передать значение NULL или пустую строку.

### <a name="conflicts"></a>Конфликты
Значение, заданное в конфигурации приложения MAM, переопределит значение с тем же набором ключей в конфигурации Android Enterprise. 

Если администратор настраивает конфликтующие значения для того же ключа (например, для разных наборов конфигурации приложения с одним и тем же ключом в нескольких группах, содержащих одного и того же пользователя), Intune не имеет возможности автоматически устранить этот конфликт и сделает все значения доступными для вашего приложения. 

Приложение может запросить все значения для заданного ключа из объекта `MAMAppConfig`:
```java
List<Boolean> getAllBooleansForKey(String key)
List<Long> getAllIntegersForKey(final String key)
List<Double> getAllDoublesForKey(final String key)
List<String> getAllStringsForKey(final String key)
```

или запросить значение, которое необходимо выбрать:
```java
Boolean getBooleanForKey(String key, BooleanQueryType queryType)
Long getIntegerForKey(String key, NumberQueryType queryType)
Double getDoubleForKey(String key, NumberQueryType queryType)
String getStringForKey(String key, StringQueryType queryType)

enum BooleanQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns true if any of the values are true.
     */
    Or,
    /**
     * In case of conflict, returns false if any of the values are false.
     */
    And
}

enum NumberQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the minimum Integer.
     */
    Min,
    /**
     * In case of conflict, returns the maximum Integer.
     */
    Max
}

enum StringQueryType {
    /**
     * In case of conflict, arbitrarily picks one. This is not guaranteed to return the same value every time.
     */
    Any,
    /**
     * In case of conflict, returns the first result ordered alphabetically.
     */
    Min,

    /**
     * In case of conflict, returns the last result ordered alphabetically.
     */
    Max
}
```

Приложение также может запрашивать необработанные данные в виде списка наборов пар "ключ-значение".

```java
List<Map<String, String>> getFullData()
```

### <a name="full-example"></a>Полный пример
```java
MAMAppConfigManager configManager = MAMComponents.get(MAMAppConfigManager.class);
String identity = "user@contoso.com"
MAMAppConfig appConfig = configManager.getAppConfig(identity);
String fooValue = null;
if (appConfig.hasConflict("foo")) {
    List<String> values = appConfig.getAllStringsForKey("foo");
    fooValue = chooseBestValue(values);
} else {
    valueToUse = appConfig.getStringForKey("foo", MAMAppConfig.StringQueryType.Any);
}
Long barValue = appConfig.getIntegerForKey("bar", MAMAppConfig.NumberQueryType.Min);
```

### <a name="notification"></a>Уведомление
Конфигурация приложения добавляет новый тип уведомления.
* **REFRESH_APP_CONFIG**. Это уведомление отправляется в `MAMUserNotification` и сообщает приложению о том, что доступны новые данные конфигурации приложения.

### <a name="further-reading"></a>Дополнительные материалы
Дополнительные сведения о создании целевой политики конфигурации приложений MAM в Android см. в статье [Использование политик конфигурации приложений Microsoft Intune для Android](https://docs.microsoft.com/intune/app-configuration-policies-managed-app) в разделе, посвященном целевой конфигурации приложений MAM.

Конфигурацию приложения также можно настроить с помощью API Graph. Дополнительные сведения см. в [документации по API Graph для конфигурации для MAM](https://docs.microsoft.com/graph/api/resources/intune-mam-targetedmanagedappconfiguration).

## <a name="custom-themes-optional"></a>Пользовательские темы (необязательно)
В пакете SDK для MAM можно предоставить пользовательскую тему, которая будет применяться ко всем экранам и окнам MAM. Если тема не указана, будет использоваться тема MAM по умолчанию.

### <a name="how-to-provide-a-theme"></a>Как предоставить тему
Чтобы предоставить тему приложению с помощью пакета SDK для MAM, необходимо добавить следующую строку кода в метод `onCreate` приложения:

```java
MAMThemeManager.setAppTheme(R.style.AppTheme);
```

В приведенном выше примере необходимо заменить `R.style.AppTheme` темой стиля для пакета SDK.

## <a name="style-customization-deprecated"></a>Настройка стиля (не рекомендуется)

Сейчас эта функция не рекомендуется, а пользовательские темы (выше) являются предпочтительным способом настройки представлений.

## <a name="default-enrollment-optional"></a>Регистрация по умолчанию (дополнительно)
Ниже приводятся указания по настройке обязательного запроса учетных данных пользователя при запуске приложения для автоматической регистрации в службе APP-WE (в этом разделе она называется **регистрацией по умолчанию**) и настройке политик защиты приложений Intune таким образом, чтобы они разрешали использовать бизнес-приложение для Android, интегрированное с пакетом SDK, только пользователям, защищенным Intune. В нем также рассматривается включение единого входа для бизнес-приложения Android, интегрированного с пакетом SDK. Этот сценарий **не** поддерживается для приложений магазина, с которыми могут работать пользователи, не зарегистрированные в Intune.

> [!NOTE] 
> Преимущества **регистрации по умолчанию** включают в себя упрощенный способ получения политики из службы APP-WE для приложения на устройстве.

> [!NOTE] 
> **Регистрация по умолчанию** учитывает национальные облака.

Включите регистрацию по умолчанию, выполнив следующие действия:

1. Если приложение интегрируется с ADAL или необходимо включить единый вход, [настройте ADAL](#configure-azure-active-directory-authentication-library-adal), используя следующие [распространенные конфигурации ADAL](#common-adal-configurations) #2. В противном случае этот шаг можно пропустить.
   
2. Включите регистрацию по умолчанию, добавив в манифест следующее значение:
   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.DefaultMAMServiceEnrollment" android:value="true" />
   ```
   > [!NOTE] 
   > Это должна быть единственная интеграция со службой MAM-WE в приложении. При наличии других вызовов интерфейсов API MAMEnrollmentManager будут возникать конфликты.

3. Включите требуемую политику MAM, добавив в манифест следующее значение:
   ```xml 
   <meta-data android:name="com.microsoft.intune.mam.MAMPolicyRequired" android:value="true" />
   ```
   > [!NOTE] 
   > В результате пользователю будет необходимо скачать приложение корпоративного портала на устройстве и пройти процедуру регистрации по умолчанию перед использованием.

## <a name="limitations"></a>Ограничения

### <a name="policy-enforcement-limitations"></a>Ограничения применения политики

* **Использование сопоставителей содержимого**. В Intune политика передачи или получения может полностью или частично блокировать использование сопоставителя содержимого для доступа к поставщику содержимого в другом приложении. Это приводит к тому, что методы `ContentResolver` возвращают значение NULL или выдают значение сбоя (например, при блокировке `openOutputStream` выдаст `FileNotFoundException`). Приложение может определить, вызван ли (и может ли быть вызван) сбой записи данных через сопоставитель политики, выполнив вызов:

    ```java
    MAMPolicyManager.getPolicy(currentActivity).getIsSaveToLocationAllowed(contentURI);
    ```

    или при отсутствии связанных действий:

    ```java
    MAMPolicyManager.getPolicy().getIsSaveToLocationAllowed(contentURI);
    ```

    Во втором случае приложения с несколькими удостоверениями обязательно должны задать нужное удостоверение потока (или передать явное удостоверение в вызов `getPolicy`).

### <a name="exported-services"></a>Экспортированные службы
Файл AndroidManifest.xml, входящий в состав пакета SDK для приложений Intune, содержит объект **MAMNotificationReceiverService**, который должен быть экспортированной службой, чтобы дать корпоративному порталу возможность отправлять уведомления в управляемое приложение. Служба проверяет вызывающий объект, чтобы убедиться, что корпоративный портал может отправлять уведомления.

### <a name="reflection-limitations"></a>Ограничения отражения
Некоторые базовые классы MAM (например, `MAMActivity`, `MAMDocumentsProvider`) содержат методы (на основе исходных базовых классов Android), которые используют параметр или типы возвращаемого значения только для определенных уровней API. Поэтому не всегда можно применять отражение для перечисления всех методов компонентов приложения. Это ограничение касается не только MAM. Оно также будет применяться, если приложение само реализовало эти методы из базовых классов Android.

### <a name="robolectric"></a>Robolectric
Тестирование поведения пакета SDK для MAM в Robolectric не поддерживается. Пакет SDK для MAM в Robolectric работает с некоторыми ошибками, так как процедуры в Robolectric неточно имитируют процедуры реальных устройств или эмуляторов.

Если вам нужно протестировать приложение в Robolectric, рекомендуется переместить логику класса приложения во вспомогательное приложение и создать APK модульного тестирования с классом приложения, который не наследуется от MAMApplication.

## <a name="expectations-of-the-sdk-consumer"></a>Ожидания потребителя пакета SDK
Пакет SDK Intune поддерживает контракт, предоставляемый API Android, хотя состояния сбоя могут возникать чаще в результате применения политики. Эти рекомендации для Android позволяют снизить вероятность сбоя:

* Функции пакета SDK для Android, которые могут возвращать значение NULL, теперь с большей вероятностью равны NULL.  Чтобы свести число возникающих проблем к минимуму, обеспечьте наличие проверок значений NULL в нужных местах.

* Функции, которые могут быть проверены, следует проверять с использованием их API-интерфейсов замены MAM.

* Любые производные функции следует вызвать через их версии суперкласса.

* Избегайте неоднозначного использования любых API. Например, использование `Activity.startActivityForResult` без проверки requestCode вызовет нестандартное поведение.

## <a name="telemetry"></a>Телеметрия

Пакет SDK для приложений Intune для Android не управляет сбором данных из приложения. По умолчанию приложение корпоративного портала записывает системные данные. Эти данные отправляются в Microsoft Intune. Согласно политике конфиденциальности Майкрософт мы не собираем персональные данные.

> [!NOTE]
> Если конечные пользователи отказываются от отправки этих данных, им необходимо отключить телеметрию в разделе "Параметры" приложения корпоративного портала. Дополнительные сведения см. в разделе [Отключение сбора данных об использовании корпорацией Майкрософт](https://docs.microsoft.com/mem/intune/user-help/turn-off-microsoft-usage-data-collection-android). 

## <a name="recommended-android-best-practices"></a>Рекомендации для Android

* Все проекты библиотеки должны по мере возможности совместно использовать один и тот же android:package. Это не приведет к эпизодическим сбоям в среде выполнения, так как проблема возникает исключительно при сборке. Более новые версии пакета SDK приложений Intune устранят некоторую избыточность.

* Используйте самые новые средства сборки пакета SDK для Android.

* Удалите все ненужные и неиспользуемые библиотеки (например, android.support.v4).

## <a name="testing"></a>Тестирование
Ознакомьтесь с [руководством по тестированию](app-sdk-android-testing-guide.md).
