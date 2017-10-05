---
title: Windows Phone Silverlight Engagement SDK Integration
description: "Integrowanie usługi Azure Mobile Engagement z aplikacji Silverlight Windows Phone"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="23696-103">Windows Phone Silverlight Engagement SDK Integration</span><span class="sxs-lookup"><span data-stu-id="23696-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="23696-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="23696-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="23696-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="23696-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="23696-106">iOS</span><span class="sxs-lookup"><span data-stu-id="23696-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="23696-107">Android</span><span class="sxs-lookup"><span data-stu-id="23696-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="23696-108">W tej procedurze opisano Najprostszym sposobem, aby aktywować analizy usługi Azure Mobile Engagement i funkcji w aplikacji Windows Phone Silverlight monitorowania.</span><span class="sxs-lookup"><span data-stu-id="23696-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="23696-109">Poniższe kroki są wystarczająco aktywować raport dzienniki wymagane do obliczenia wszystkich statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals.</span><span class="sxs-lookup"><span data-stu-id="23696-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="23696-110">Raport dzienniki wymagane do obliczenia innych danych statystycznych, takich jak zdarzenia i błędy zadań musi zostać wykonane ręcznie przy użyciu interfejsu API usługi Engagement (zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) poniżej) ponieważ te statystyki są zależne od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23696-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="23696-111">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="23696-111">Supported versions</span></span>
<span data-ttu-id="23696-112">Mobile Engagement SDK dla platformy Silverlight systemu Windows mogą być tylko zintegrowane aplikacji:</span><span class="sxs-lookup"><span data-stu-id="23696-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="23696-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="23696-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="23696-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="23696-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="23696-115">Jeśli przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), zapoznaj się [uniwersalnych systemu Windows procedura integracji](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="23696-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="23696-116">Zainstaluj dodatek Silverlight SDK usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="23696-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="23696-117">Mobile Engagement SDK dla platformy Silverlight systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="23696-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="23696-118">Można ją zainstalować z Visual Studio Menedżera pakietów Nuget.</span><span class="sxs-lookup"><span data-stu-id="23696-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="23696-119">Dodawanie funkcji</span><span class="sxs-lookup"><span data-stu-id="23696-119">Add the capabilities</span></span>
<span data-ttu-id="23696-120">Engagement SDK wymaga prawidłowego funkcjonowania niektórych możliwości Windows Phone Silverlight SDK.</span><span class="sxs-lookup"><span data-stu-id="23696-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="23696-121">Otwórz z `WMAppManifest.xml` plików i pamiętaj, że następujące funkcje są zadeklarowane w `Capabilities` panelu:</span><span class="sxs-lookup"><span data-stu-id="23696-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="23696-122">Inicjowanie usługi Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="23696-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="23696-123">Konfiguracja usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="23696-123">Engagement configuration</span></span>
<span data-ttu-id="23696-124">Konfiguracja zaangażowania jest scentralizowana w `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="23696-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="23696-125">Edytuj ten plik, aby określić:</span><span class="sxs-lookup"><span data-stu-id="23696-125">Edit this file to specify :</span></span>

* <span data-ttu-id="23696-126">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="23696-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="23696-127">Jeśli chcesz określić je w czasie wykonywania, należy wywołać metodę następujące przed zainicjowaniem agenta usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="23696-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="23696-128">Ciąg połączenia dla aplikacji jest wyświetlany w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="23696-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="23696-129">Inicjowania usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="23696-129">Engagement initialization</span></span>
<span data-ttu-id="23696-130">Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="23696-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="23696-131">Ta klasa dziedziczy `Application` i zawiera wiele metod ważne.</span><span class="sxs-lookup"><span data-stu-id="23696-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="23696-132">Będzie można również używany do inicjowania usługi Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="23696-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="23696-133">Modyfikowanie `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="23696-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="23696-134">Dodaj do Twojej `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="23696-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="23696-135">Wstaw `EngagementAgent.Instance.Init` w `Application_Launching` metody:</span><span class="sxs-lookup"><span data-stu-id="23696-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="23696-136">Wstaw `EngagementAgent.Instance.OnActivated` w `Application_Activated` metody:</span><span class="sxs-lookup"><span data-stu-id="23696-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="23696-137">Firma Microsoft zdecydowanie zniechęcić można dodać inicjowania usługi Engagement w innym miejscu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23696-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="23696-138">Jednak należy pamiętać, że `EngagementAgent.Instance.Init` metoda jest uruchamiana na dedykowanym wątku, a nie w wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="23696-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="23696-139">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="23696-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="23696-140">Zalecana metoda: przeciążenia sieci `PhoneApplicationPage` klas</span><span class="sxs-lookup"><span data-stu-id="23696-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="23696-141">Aby aktywować raportu wszystkie dzienniki wymagane przez zaangażowania można obliczyć użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `PhoneApplicationPage` klasy podrzędne dziedziczą `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="23696-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="23696-142">Oto przykład tego, jak to zrobić w strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23696-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="23696-143">Możesz to zrobić to samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23696-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="23696-144">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="23696-144">C# Source file</span></span>
<span data-ttu-id="23696-145">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="23696-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="23696-146">Dodaj do Twojej `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="23696-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="23696-147">Zastąp `PhoneApplicationPage` z `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="23696-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="23696-148">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="23696-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="23696-149">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="23696-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="23696-150">Jeśli dziedziczy po stronie `OnNavigatedTo` metody, należy zachować ostrożność umożliwić `base.OnNavigatedTo(e)` wywołania.</span><span class="sxs-lookup"><span data-stu-id="23696-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="23696-151">W przeciwnym razie nie będą raportowane działania.</span><span class="sxs-lookup"><span data-stu-id="23696-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="23696-152">W rzeczywistości `EngagementPage` wywołuje `StartActivity` wewnątrz `OnNavigatedTo` metody.</span><span class="sxs-lookup"><span data-stu-id="23696-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="23696-153">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="23696-153">XAML file</span></span>
<span data-ttu-id="23696-154">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="23696-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="23696-155">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="23696-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="23696-156">Zastąp `phone:PhoneApplicationPage` z `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="23696-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="23696-157">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="23696-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="23696-158">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="23696-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="23696-159">Zastąpienie zachowania domyślnego</span><span class="sxs-lookup"><span data-stu-id="23696-159">Override the default behavior</span></span>
<span data-ttu-id="23696-160">Domyślnie nazwa klasy strony został zgłoszony jako nazwę działania, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="23696-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="23696-161">Jeśli klasa korzysta z sufiksem "Page", Engagement spowoduje również usunięcie.</span><span class="sxs-lookup"><span data-stu-id="23696-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="23696-162">Jeśli chcesz zastąpić domyślne zachowanie dla nazwy, po prostu dodaj to w kodzie:</span><span class="sxs-lookup"><span data-stu-id="23696-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="23696-163">Jeśli chcesz zgłosić niektóre dodatkowe informacje o Twoich działaniach, możesz dodać to w kodzie:</span><span class="sxs-lookup"><span data-stu-id="23696-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="23696-164">Te metody są wywoływane z poziomu `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="23696-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="23696-165">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="23696-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="23696-166">Jeśli nie możesz lub nie było przeciążyć Twojej `PhoneApplicationPage` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="23696-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="23696-167">Firma Microsoft zaleca wywołania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody z PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="23696-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="23696-168">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="23696-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="23696-169">Zestaw SDK automatycznie wywołuje `EndActivity` metody, gdy aplikacja zostanie zamknięta.</span><span class="sxs-lookup"><span data-stu-id="23696-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="23696-170">W związku z tym jest **wysokiej** zaleca, aby wywołać `StartActivity` metody zmianie aktywności użytkownika i **nigdy** wywołać `EndActivity` — metoda.</span><span class="sxs-lookup"><span data-stu-id="23696-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="23696-171">Ta metoda wysyła wiadomość do serwera usługi Engagement, czy bieżący użytkownik opuścił aplikacji i ma wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="23696-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="23696-172">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="23696-172">Advanced reporting</span></span>
<span data-ttu-id="23696-173">Opcjonalnie, może zajść potrzeba raport aplikacji określonych zdarzeń, błędów i zadań, w tym celu należy użyć innych metod znalezione w `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="23696-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="23696-174">Interfejsu API usługi Engagement pozwala na korzystanie ze wszystkich zaawansowanych możliwości usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="23696-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="23696-175">Aby uzyskać więcej informacji, zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="23696-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="23696-176">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="23696-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="23696-177">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="23696-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="23696-178">Możesz wyłączyć automatyczne awarii, funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="23696-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="23696-179">Następnie, gdy wystąpi nieobsługiwany wyjątek, Engagement nie będzie wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="23696-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="23696-180">Jeśli chcesz wyłączyć tę funkcję, należy pamiętać, że po awarii nieobsługiwany nastąpi w aplikacji, Engagement nie będą wysyłały awarii **i** nie spowoduje zamknięcia sesji i zadania.</span><span class="sxs-lookup"><span data-stu-id="23696-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="23696-181">Aby wyłączyć automatyczne zgłaszanie awarii, wystarczy dostosować konfigurację, w zależności od sposobu należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="23696-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="23696-182">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="23696-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="23696-183">Ustaw awarii raport `false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="23696-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="23696-184">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="23696-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="23696-185">Ustaw awarii raportu przy użyciu obiektu EngagementConfiguration wartość false.</span><span class="sxs-lookup"><span data-stu-id="23696-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="23696-186">Tryb serii</span><span class="sxs-lookup"><span data-stu-id="23696-186">Burst mode</span></span>
<span data-ttu-id="23696-187">Domyślnie raporty usługi Engagement rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="23696-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="23696-188">Jeśli aplikacja zgłasza dzienniki bardzo często, lepiej jest buforu dzienniki i raportuj je w całości na regularne podstawy czasu (jest to nazywane "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="23696-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="23696-189">Aby to zrobić, należy wywołać metodę:</span><span class="sxs-lookup"><span data-stu-id="23696-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="23696-190">Argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="23696-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="23696-191">W dowolnym momencie Jeśli chcesz ponownie uaktywnić rejestrowania w czasie rzeczywistym, po prostu Wywołaj metodę bez parametrów lub z wartością 0.</span><span class="sxs-lookup"><span data-stu-id="23696-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="23696-192">Tryb serii nieco zwiększyć czas pracy baterii, ale ma wpływ na monitorowanie usługi Engagement: wszystkie czas trwania sesji i zadania zostanie zaokrąglony próg serii (w związku z tym sesji i zadania krótsze niż próg serii może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="23696-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="23696-193">Zaleca się przy użyciu progu w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="23696-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="23696-194">Masz wiedzieć, który zapisano dzienniki są ograniczone do 300 elementów.</span><span class="sxs-lookup"><span data-stu-id="23696-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="23696-195">W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="23696-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="23696-196">Próg serii nie można skonfigurować do okresu mniejszym niż 1 sekunda.</span><span class="sxs-lookup"><span data-stu-id="23696-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="23696-197">Jeśli spróbujesz to zrobić, zestaw SDK wyświetli śledzenia błąd i zostanie automatycznie zresetowana do wartości domyślnej, oznacza to zero sekund.</span><span class="sxs-lookup"><span data-stu-id="23696-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="23696-198">Spowoduje to wyzwolenie zestaw SDK, aby zgłosić dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="23696-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

