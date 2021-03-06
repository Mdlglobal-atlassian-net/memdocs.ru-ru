---
title: Привязки Xamarin из пакета SDK для приложений Microsoft Intune
description: Привязки Xamarin из пакета SDK для приложений Intune позволяют использовать политику защиты приложений Intune в приложениях iOS и Android, созданных с помощью Xamarin.
keywords: sdk, Xamarin, intune
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/28/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 275d574b-3560-4992-877c-c6aa480717f4
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune
ms.collection: M365-identity-device-management
ms.openlocfilehash: b29069d4543d4abb4bc403c446441e181d963bdd
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2020
ms.locfileid: "79345563"
---
# <a name="microsoft-intune-app-sdk-xamarin-bindings"></a>Привязки Xamarin из пакета SDK для приложений Microsoft Intune

> [!NOTE]
> Вы можете сначала прочесть статью [Начало работы с пакетом SDK для приложений Intune](app-sdk-get-started.md), в которой описана подготовка к интеграции на каждой поддерживаемой платформе.

## <a name="overview"></a>Overview
[Привязки Xamarin из пакета SDK для приложений Intune](https://github.com/msintuneappsdk/intune-app-sdk-xamarin) позволяют использовать [политику защиты приложений Intune](../apps/app-protection-policy.md) в приложениях iOS и Android, созданных с помощью Xamarin. Привязки разрешают разработчикам легко встраивать в свои приложения на базе Xamarin функции защиты приложений Intune.

Привязки Xamarin из пакета SDK для приложений Microsoft Intune позволяют встраивать в приложения, разработанные с помощью Xamarin, политики защиты приложений Intune, также известные как политики защиты приложений или политики управления мобильными приложениями. В приложение, которое использует MAM, встроен пакет SDK для приложений Intune. ИТ-администраторы могут развернуть политики защиты приложений в вашем мобильном приложении, когда Intune активно управляет им.

## <a name="whats-supported"></a>Поддерживаемые возможности

### <a name="developer-machines"></a>Компьютеры разработчиков
* Windows (версия Visual Studio 15.7 и более поздние)
* macOS

### <a name="mobile-app-platforms"></a>Платформы мобильных приложений
* Android
* iOS

### <a name="intune-mobile-application-management-scenarios"></a>Ситуации, связанные с управлением мобильными приложениями Intune

* Intune APP-WE (без регистрации устройства)
* Устройства, зарегистрированные в Intune MDM
* Сторонние устройства, зарегистрированные в EMM

Приложения Xamarin, созданные с помощью привязок Xamarin из пакета SDK для приложений Intune, теперь могут получать политики защиты приложений Intune как на устройствах, зарегистрированных в системе управления мобильными устройствами (MDM) Intune, так и на незарегистрированных устройствах.

## <a name="prerequisites"></a>Предварительные условия

Прочтите [условия лицензионного соглашения](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/blob/master/Microsoft%20License%20Terms%20Intune%20App%20SDK%20Xamarin%20Component.pdf). Распечатать и сохранить копию условий лицензии для своих записей. Скачивая и используя привязки Xamarin из пакета SDK для приложений Intune, вы соглашаетесь с этими условиями лицензии. Если вы не согласны, не используйте это программное обеспечение.

Для [аутентификации](https://azure.microsoft.com/documentation/articles/active-directory-authentication-scenarios/) пакет SDK для Intune использует [Библиотеку проверки подлинности Active Directory (ADAL)](https://azure.microsoft.com/documentation/articles/active-directory-authentication-libraries/) и сценарии условного запуска. Для этого в приложении должна быть определенная конфигурация [Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-whatis/). 

Если приложение уже настроено для использования ADAL или MSAL и имеет свой собственный пользовательский идентификатор клиента, используемый для проверки подлинности с помощью Azure Active Directory, убедитесь, что выполнены шаги для предоставления разрешений приложения Xamarin для службы управления мобильными приложениями Intune (MAM). Инструкции см. в разделе [Предоставить вашему приложению доступ к Intune защиты службы приложений](app-sdk-get-started.md#give-your-app-access-to-the-intune-app-protection-service-optional) руководства [Приступая к работе с руководством по пакету SDK для Intune](app-sdk-get-started.md).

## <a name="security-considerations"></a>Вопросы безопасности

Во избежание потенциального спуфинга, раскрытия информации и атак с несанкционированным повышением привилегий:

* Убедитесь, что разработка приложений Xamarin выполняется на защищенной рабочей станции.
* Убедитесь, что привязки получены из действительного источника Майкрософт:
  * [Профиль NuGet пакета SDK для приложений MS Intune](https://www.nuget.org/profiles/msintuneappsdk)
  * [Репозиторий Xamarin на ресурсе GitHub для пакета SDK для приложений Intune](https://github.com/msintuneappsdk/intune-app-sdk-xamarin)
* Настройте конфигурацию NuGet для своего проекта таким образом, чтобы доверять подписанным, неизмененным пакетам NuGet.
Дополнительные сведения см. в разделе [Установка подписанных пакетов](https://docs.microsoft.com/nuget/consume-packages/installing-signed-packages).
* Обеспечьте безопасность выходного каталога, содержащего приложение Xamarin. Рассмотрите возможность использования каталога уровня пользователя в качестве выходного каталога.


## <a name="enabling-intune-app-protection-polices-in-your-ios-mobile-app"></a>Включение политик защиты приложений Intune в мобильном приложении iOS
1. Добавьте [пакет Microsoft.Intune.MAM.Xamarin.iOS NuGet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.iOS) в проект Xamarin.iOS.
2. Выполните общие шаги, необходимые для интеграции пакета SDK для приложений Intune в мобильное приложение iOS. Можно начать с шага 3 инструкций по интеграции из раздела [Интеграция пакета SDK с мобильным приложением](app-sdk-ios.md#build-the-sdk-into-your-mobile-app). Последний шаг в этом разделе IntuneMAMConfigurator можно пропустить, так как это средство включено в пакет Microsoft.Intune.MAM.Xamarin.iOS и будет запущено автоматически во время сборки.
    **Важно.** Включение общего доступа к цепочке ключей для приложения в Visual Studio немного отличается от этой процедуры в среде Xcode. Откройте PLIST-файл прав. Убедитесь, что включен параметр "Включить цепочку ключей" и что в этом разделе добавлены соответствующие группы совместного доступа к цепочке ключей. Убедитесь, что PLIST-файл прав указан в поле "Настраиваемые назначения" параметров пакетной подписи iOS проекта для всех соответствующих сочетаний конфигурации и платформы.
3. После добавления привязок и правильной настройки приложение сможет использовать API пакета SDK для Intune. Для этого необходимо включить следующее пространство имен:

      ```csharp
      using Microsoft.Intune.MAM;
      ```

4. Чтобы ваше приложение получало политики защиты приложения, его необходимо зарегистрировать в службе Intune MAM. Если приложение не использует [библиотеку проверки подлинности Azure Active Directory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) (ADAL) или [библиотеку проверки подлинности Майкрософт](https://www.nuget.org/packages/Microsoft.Identity.Client) (MSAL) для аутентификации пользователей и вы хотите передать обработку проверки подлинности пакету SDK Intune, приложение должно предоставлять имя участника-пользователя в метод LoginAndEnrollAccount класса IntuneMAMEnrollmentManager.

      ```csharp
       IntuneMAMEnrollmentManager.Instance.LoginAndEnrollAccount([NullAllowed] string identity);
      ```

      Приложение может передавать значение null, если имя участника-пользователя неизвестно во время вызова. В этом случае пользователям будет предложено ввести адрес электронной почты и пароль.
      
      Если приложение уже использует библиотеку ADAL или MSAL для проверки подлинности пользователей, можно настроить единый вход между приложением и пакетом SDK Intune. Затем необходимо заменить параметры AAD по умолчанию, используемые пакетом SDK Intune, параметрами вашего приложения. Это можно сделать через словарь IntuneMAMSettings в файле Info.plist приложения (см. [руководство для разработчиков пакета SDK для приложений Intune в iOS](app-sdk-ios.md#configure-settings-for-the-intune-app-sdk)) или можно использовать свойства переопределения AAD класса IntuneMAMSettings. Использование файла Info.plist рекомендуется для приложений, параметры ADAL которых являются статическими. И рекомендуется переопределять свойства приложений, которые определяют эти значения во время выполнения. После настройки всех параметров единого входа приложение должно предоставлять имя участника-пользователя методу RegisterAndEnrollAccount класса IntuneMAMEnrollmentManager после успешной проверки подлинности.

      ```csharp
      IntuneMAMEnrollmentManager.Instance.RegisterAndEnrollAccount(string identity);
      ```

      Приложения могут определять результат попытки регистрации путем реализации метода EnrollmentRequestWithStatus в подклассе IntuneMAMEnrollmentDelegate и задания для свойства Delegate класса IntuneMAMEnrollmentManager экземпляра этого класса. 

      После успешной регистрации приложения могут определять имя участника-пользователя зарегистрированной учетной записи (если ранее оно было неизвестно), запрашивая следующее свойство: 

      ```csharp
       string enrolledAccount = IntuneMAMEnrollmentManager.Instance.EnrolledAccount;
      ```      
### <a name="sample-applications"></a>Примеры приложений
Примеры приложений, в которых подчеркивается функциональность MAM в приложениях Xamarin.iOS, представлены на сайте [GitHub](https://github.com/msintuneappsdk/sample-intune-xamarin-ios).

> [!NOTE] 
> Модуль перераспределения для iOS/iPadOS отсутствует. Интеграция в приложение Xamarin.Forms должна быть такой же, как и для обычного проекта Xamarin.iOS. 

## <a name="enabling-intune-app-protection-policies-in-your-android-mobile-app"></a>Включение политик защиты приложений Intune в мобильном приложении Android
1. Добавьте [пакет Microsoft.Intune.MAM.Xamarin.Android NuGet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Xamarin.Android) в проект Xamarin.Android.
    1. Для приложения Xamarin.Forms также добавьте [пакет Microsoft.Intune.MAM.Remapper.Tasks NuGet](https://www.nuget.org/packages/Microsoft.Intune.MAM.Remapper.Tasks) в свой проект Xamarin.Android. 
2. Выполните общие шаги, необходимые для [интеграции пакета SDK для приложений Intune](app-sdk-android.md) в мобильное приложение Android, сверяясь со сведениями в этом документе.

### <a name="xamarinandroid-integration"></a>Интеграция Xamarin.Android

Полный обзор по интеграции пакета SDK для приложений Intune можно найти в [Руководстве разработчика по Microsoft Intune App SDK для Android](app-sdk-android.md). Читая руководство и интегрируя пакет SDK для приложений Intune с приложением Xamarin, используйте следующие разделы, где выделены различия между реализацией собственного приложения Android, разработанного на Java, и приложения Xamarin, разработанного на C#. Эти разделы стоит рассматривать как дополнительные и не следует использовать в качестве замены; обязательно прочитайте руководство целиком.

#### <a name="remapper"></a>Remapper
Начиная с выпуска 1.4428.1 пакет `Microsoft.Intune.MAM.Remapper` можно добавлять в приложение Xamarin.Android в виде [средства сборки](app-sdk-android.md#build-tooling) для выполнения замены класса MAM, метода и системных служб. Если включен Remapper, то при построении для переименованных методов и разделов приложения MAM будут автоматически выполняться эквивалентные замещающие части MAM.

Чтобы исключить класс из MAM с помощью Remapper, в файл `.csproj` проекта можно добавить следующее свойство.

```xml
  <PropertyGroup>
    <ExcludeClasses>Semicolon separated list of relative class paths to exclude from MAM-ification</ExcludeClasses>
  </PropertyGroup>
```

> [!NOTE]
> В настоящее время Remapper не позволяет выполнять отладку в приложениях Xamarin.Android. Для отладки приложения рекомендуется выполнить интеграцию вручную.

#### <a name="renamed-methods"></a>[Переименованные методы](app-sdk-android.md#renamed-methods)
Часто метод, доступный в классе Android, отмечается как окончательный в замещающем классе MAM. В этом случае замещающий класс MAM предоставляет метод с таким же именем (с суффиксом `MAM`), который должен быть переопределен вместо исходного. Например, при наследовании от `MAMActivity` вместо переопределения `OnCreate()` и вызова `base.OnCreate()` объекту `Activity` необходимо переопределить `OnMAMCreate()` и вызвать `base.OnMAMCreate()`.

#### <a name="mam-application"></a>[Приложение MAM](app-sdk-android.md#mamapplication)
Необходимо определить класс `Android.App.Application`. При интеграции MAM вручную он должен наследоваться от `MAMApplication`. Убедитесь, что подкласс правильно декорирован атрибутом `[Application]` и переопределяет конструктор `(IntPtr, JniHandleOwnership)`.

```csharp
    [Application]
    class TaskrApp : MAMApplication
    {
    public TaskrApp(IntPtr handle, JniHandleOwnership transfer)
        : base(handle, transfer) { }
```

> [!NOTE]
> Проблема с привязками MAM Xamarin может привести к сбою при развертывании в режиме отладки. Чтобы избежать этого, необходимо добавить атрибут `Debuggable=false` в класс `Application`, а флаг `android:debuggable="true"` необходимо удалить из манифеста, если он был задан вручную.

#### <a name="enable-features-that-require-app-participation"></a>[Включение функций, требующих содействия со стороны приложения](app-sdk-android.md#enable-features-that-require-app-participation)
Пример. Определение необходимости использования ПИН-кода в приложении

```csharp
MAMPolicyManager.GetPolicy(currentActivity).IsPinRequired;
```

Пример. Определение основного пользователя Intune

```csharp
IMAMUserInfo info = MAMComponents.Get<IMAMUserInfo>();
return info?.PrimaryUser;
```

Пример. Определение разрешения на сохранение данных на устройстве или в облачном хранилище

```csharp
MAMPolicyManager.GetPolicy(currentActivity).GetIsSaveToLocationAllowed(SaveLocation service, String username);
```

#### <a name="register-for-notifications-from-the-sdk"></a>[Регистрация для получения уведомлений из пакета SDK](app-sdk-android.md#register-for-notifications-from-the-sdk)
Ваше приложение следует зарегистрировать для получения уведомлений из пакета SDK. Для этого нужно создать класс `MAMNotificationReceiver` и зарегистрировать его с помощью `MAMNotificationReceiverRegistry`. Для этого укажите получателя, а также тип необходимых уведомлений в `App.OnMAMCreate`, как показано в следующем примере:

```csharp
public override void OnMAMCreate()
{
    // Register the notification receivers
    IMAMNotificationReceiverRegistry registry = MAMComponents.Get<IMAMNotificationReceiverRegistry>();
    foreach (MAMNotificationType notification in MAMNotificationType.Values())
    {
        registry.RegisterReceiver(new ToastNotificationReceiver(this), notification);
    }
    ...
```

#### <a name="mam-enrollment-manager"></a>[Диспетчер регистрации MAM](app-sdk-android.md#mamenrollmentmanager)

```csharp
IMAMEnrollmentManager mgr = MAMComponents.Get<IMAMEnrollmentManager>();
```

### <a name="xamarinforms-integration"></a>Интеграция Xamarin.Forms

Для приложений `Xamarin.Forms` пакет `Microsoft.Intune.MAM.Remapper` автоматически выполняет замену класса MAM, внедряя классы `MAM` в иерархию часто используемых классов `Xamarin.Forms`. 

> [!NOTE]
> Интеграция Xamarin.Forms должна осуществляться помимо интеграции Xamarin.Android, описанной выше. Remapper ведет себя по-другому для приложений Xamarin.Forms, поэтому замены MAM необходимо выполнить вручную.

После добавления Remapper в проект необходимо будет выполнить эквивалентную замену MAM. Например, `FormsAppCompatActivity` и `FormsApplicationActivity` можно продолжать использовать в приложении, если переопределения для `OnCreate` и `OnResume` заменяются эквивалентами MAM `OnMAMCreate` и `OnMAMResume` соответственно.

```csharp
    public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsAppCompatActivity
    {
        protected override void OnMAMCreate(Bundle savedInstanceState)
        {
            base.OnMAMCreate(savedInstanceState);
            global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
            LoadApplication(new App());
        }
```

Если не сделать замену, могут возникнуть следующие ошибки компиляции:
* [Ошибка компилятора CS0239](https://docs.microsoft.com/dotnet/csharp/misc/cs0239). Эта ошибка обычно возникает в этой форме ``'MainActivity.OnCreate(Bundle)': cannot override inherited member 'MAMAppCompatActivityBase.OnCreate(Bundle)' because it is sealed``.
Это ожидаемо; когда remapper изменяет наследование классов Xamarin, некоторые функции станут `sealed` и для переопределения вместо этого добавляется новый вариант MAM.
* [Ошибка компилятора CS0507](https://docs.microsoft.com/dotnet/csharp/language-reference/compiler-messages/cs0507): данная ошибка обычно возникает в этой форме ``'MyActivity.OnRequestPermissionsResult()' cannot change access modifiers when overriding 'public' inherited member ...``. По мере изменения порядка наследования некоторых классов Xamarin средством remapper некоторые функции-члены будут изменены на `public`. Если переопределить какую-либо из этих функций, может также потребоваться изменить модификаторы доступа переопределений на `public`.

> [!NOTE]
> Remapper перезаписывает зависимость, которая используется Visual Studio для автоматического завершения IntelliSense. Таким образом, может потребоваться перезагрузить и перестроить проект в том случае, если был добавлен Remapper, чтобы технология IntelliSense могла правильно распознать изменения.

#### <a name="troubleshooting"></a>Диагностика
* Если после запуска приложения появляется пустой белый экран, то может потребоваться принудительно выполнить вызовы навигации в основном потоке.
* Привязки Xamarin в пакете SDK для Intune не поддерживают приложения, использующие кроссплатформенную среду, такую как MvvmCross, ввиду наличия конфликтов между MvvmCross и классами MAM Intune. Несмотря на то, что некоторым клиентам, возможно, удалось успешно выполнить интеграцию после перемещения приложений в обычные Xamarin.Forms, мы не предоставляем разработчикам приложений, использующим MvvmCross, явные указания или подключаемые модули.

### <a name="company-portal-app"></a>Приложение корпоративного портала
Для включения политик защиты приложений привязкам Xamarin в пакете SDK для Intune требуется наличие на устройстве приложения [Корпоративный портал](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) для Android. Корпоративный портал извлекает политики защиты приложения из службы Intune. При инициализации приложения политики и код загружаются для реализации этой политики на корпоративном портале. Пользователю не нужно выполнять вход.

> [!NOTE]
> Если приложение "Корпоративный портал" отсутствует на устройстве **Android**, управляемое приложение Intune будет работать так же, как обычное приложение, не поддерживающее политики защиты приложений Intune.

Чтобы включить защиту приложений без регистрации устройства, пользователю _**не**_ нужно регистрировать устройство с помощью приложения корпоративного портала.

### <a name="sample-applications"></a>Примеры приложений
Примеры приложений, в которых подчеркивается функциональность MAM в приложениях Xamarin.Android и Xamarin.Forms, представлены на сайте [GitHub](https://github.com/msintuneappsdk/Taskr-Sample-Intune-Xamarin-Android-Apps).

## <a name="support"></a>Поддержка
Если ваша организация является клиентом Intune, обратитесь к представителю Службы технической поддержки Майкрософт, чтобы отправить запрос в службу поддержки, и разместите сведения о проблеме на [соответствующей странице GitHub](https://github.com/msintuneappsdk/intune-app-sdk-xamarin/issues). Мы окажем помощь, как только появится такая возможность. 
