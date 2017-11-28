---
title: aaaWindows Phone Silverlight Engagement SDK integracji
description: "Jak tooIntegrate Azure Mobile Engagement przy użyciu systemu Windows Phone Silverlight aplikacji"
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
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="abb2d-103">Windows Phone Silverlight Engagement SDK Integration</span><span class="sxs-lookup"><span data-stu-id="abb2d-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="abb2d-104">Aplikacje uniwersalne systemu Windows</span><span class="sxs-lookup"><span data-stu-id="abb2d-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="abb2d-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="abb2d-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="abb2d-106">iOS</span><span class="sxs-lookup"><span data-stu-id="abb2d-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="abb2d-107">Android</span><span class="sxs-lookup"><span data-stu-id="abb2d-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="abb2d-108">W tej procedurze opisano analizy hello najprostszy sposób tooactivate Azure Mobile Engagement i funkcji w aplikacji Windows Phone Silverlight monitorowania.</span><span class="sxs-lookup"><span data-stu-id="abb2d-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="abb2d-109">wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="abb2d-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="abb2d-110">Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) poniżej), ponieważ te statystyki są zależne od aplikacji.</span><span class="sxs-lookup"><span data-stu-id="abb2d-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="abb2d-111">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="abb2d-111">Supported versions</span></span>
<span data-ttu-id="abb2d-112">aplikacji mogą być tylko zintegrowane Hello Mobile Engagement SDK dla platformy Silverlight systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="abb2d-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="abb2d-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="abb2d-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="abb2d-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="abb2d-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="abb2d-115">Jeśli przeznaczona dla Windows Phone 8.1 (z systemem innym niż platformy Silverlight), można znaleźć toohello [uniwersalnych systemu Windows procedura integracji](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="abb2d-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="abb2d-116">Zainstaluj zestaw SDK usługi Mobile Engagement Silverlight hello</span><span class="sxs-lookup"><span data-stu-id="abb2d-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="abb2d-117">Witaj Mobile Engagement SDK dla platformy Silverlight systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="abb2d-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="abb2d-118">Można go zainstalować z hello Menedżera pakietów Nuget programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="abb2d-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="abb2d-119">Dodawanie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="abb2d-119">Add hello capabilities</span></span>
<span data-ttu-id="abb2d-120">Witaj Engagement SDK musi niektóre możliwości hello Windows Phone Silverlight SDK w kolejności toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="abb2d-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="abb2d-121">Otwórz z `WMAppManifest.xml` plików i pamiętaj, że hello następujące funkcje są zadeklarowane w hello `Capabilities` panelu:</span><span class="sxs-lookup"><span data-stu-id="abb2d-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="abb2d-122">Inicjowanie hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="abb2d-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="abb2d-123">Konfiguracja usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="abb2d-123">Engagement configuration</span></span>
<span data-ttu-id="abb2d-124">konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="abb2d-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="abb2d-125">Edytuj toospecify tego pliku:</span><span class="sxs-lookup"><span data-stu-id="abb2d-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="abb2d-126">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="abb2d-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="abb2d-127">Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="abb2d-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="abb2d-128">Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="abb2d-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="abb2d-129">Inicjowania usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="abb2d-129">Engagement initialization</span></span>
<span data-ttu-id="abb2d-130">Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="abb2d-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="abb2d-131">Ta klasa dziedziczy `Application` i zawiera wiele metod ważne.</span><span class="sxs-lookup"><span data-stu-id="abb2d-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="abb2d-132">Konieczne będzie również używany tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="abb2d-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="abb2d-133">Modyfikowanie hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="abb2d-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="abb2d-134">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="abb2d-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="abb2d-135">Wstaw `EngagementAgent.Instance.Init` w hello `Application_Launching` metody:</span><span class="sxs-lookup"><span data-stu-id="abb2d-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="abb2d-136">Wstaw `EngagementAgent.Instance.OnActivated` w hello `Application_Activated` metody:</span><span class="sxs-lookup"><span data-stu-id="abb2d-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="abb2d-137">Firma Microsoft zdecydowanie zniechęcić możesz tooadd hello zaangażowania inicjowania w innym miejscu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="abb2d-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="abb2d-138">Jednak należy pamiętać, że hello `EngagementAgent.Instance.Init` metoda jest uruchamiana na dedykowanym wątku, a nie na powitania wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="abb2d-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="abb2d-139">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="abb2d-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="abb2d-140">Zalecana metoda: przeciążenia sieci `PhoneApplicationPage` klas</span><span class="sxs-lookup"><span data-stu-id="abb2d-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="abb2d-141">W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `PhoneApplicationPage` klasy podrzędne dziedziczą hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="abb2d-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="abb2d-142">Oto przykład tego, jak toodo to strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="abb2d-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="abb2d-143">Możesz zrobić hello samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="abb2d-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="abb2d-144">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="abb2d-144">C# Source file</span></span>
<span data-ttu-id="abb2d-145">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="abb2d-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="abb2d-146">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="abb2d-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="abb2d-147">Zastąp `PhoneApplicationPage` z `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="abb2d-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="abb2d-148">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="abb2d-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="abb2d-149">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="abb2d-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="abb2d-150">Jeśli strony dziedziczy hello `OnNavigatedTo` metody, należy zachować ostrożność toolet hello `base.OnNavigatedTo(e)` wywołania.</span><span class="sxs-lookup"><span data-stu-id="abb2d-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="abb2d-151">W przeciwnym razie nie będą raportowane działania hello.</span><span class="sxs-lookup"><span data-stu-id="abb2d-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="abb2d-152">W rzeczywistości hello `EngagementPage` wywołuje `StartActivity` wewnątrz hello `OnNavigatedTo` metody.</span><span class="sxs-lookup"><span data-stu-id="abb2d-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="abb2d-153">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="abb2d-153">XAML file</span></span>
<span data-ttu-id="abb2d-154">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="abb2d-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="abb2d-155">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="abb2d-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="abb2d-156">Zastąp `phone:PhoneApplicationPage` z `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="abb2d-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="abb2d-157">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="abb2d-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="abb2d-158">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="abb2d-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="abb2d-159">Zastąpienie zachowania domyślnego hello</span><span class="sxs-lookup"><span data-stu-id="abb2d-159">Override hello default behavior</span></span>
<span data-ttu-id="abb2d-160">Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="abb2d-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="abb2d-161">Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement spowoduje również usunięcie.</span><span class="sxs-lookup"><span data-stu-id="abb2d-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="abb2d-162">Jeśli chcesz toooverride hello domyślne zachowanie dla nazwy hello, po prostu dodaj ten kod tooyour:</span><span class="sxs-lookup"><span data-stu-id="abb2d-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="abb2d-163">Jeśli chcesz tooreport pewne dodatkowe informacje o Twoich działaniach, można dodać ten kod tooyour:</span><span class="sxs-lookup"><span data-stu-id="abb2d-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="abb2d-164">Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="abb2d-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="abb2d-165">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="abb2d-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="abb2d-166">Jeśli nie możesz lub nie ma toooverload Twojego `PhoneApplicationPage` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="abb2d-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="abb2d-167">Firma Microsoft zaleca wywołania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody z PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="abb2d-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="abb2d-168">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="abb2d-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="abb2d-169">Witaj SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="abb2d-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="abb2d-170">W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` — metoda.</span><span class="sxs-lookup"><span data-stu-id="abb2d-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="abb2d-171">Ta metoda wysyła komunikat toohello zaangażowania czy bieżący użytkownik hello opuścił aplikacji hello i serwer ma wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="abb2d-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="abb2d-172">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="abb2d-172">Advanced reporting</span></span>
<span data-ttu-id="abb2d-173">Opcjonalnie możesz tooreport aplikacji określonych zdarzeń, błędów i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="abb2d-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="abb2d-174">Witaj interfejsu API usługi Engagement umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="abb2d-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="abb2d-175">Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane usługi Mobile Engagement znakowanie interfejsu API w aplikacji Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="abb2d-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="abb2d-176">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="abb2d-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="abb2d-177">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="abb2d-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="abb2d-178">Możesz wyłączyć hello awarii automatyczne funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="abb2d-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="abb2d-179">Następnie, gdy wystąpi nieobsługiwany wyjątek, Engagement nie będzie wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="abb2d-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="abb2d-180">Jeśli planujesz toodisable tej funkcji, należy pamiętać, że po awarii nieobsługiwany nastąpi w aplikacji, Engagement nie będą wysyłały awarii hello **i** nie spowoduje zamknięcia sesji hello i zadania.</span><span class="sxs-lookup"><span data-stu-id="abb2d-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="abb2d-181">toodisable awarii automatycznego raportowania, po prostu Dostosuj konfigurację w zależności od sposób hello należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="abb2d-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="abb2d-182">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="abb2d-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="abb2d-183">Raport z ustawiania awaria zbyt`false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="abb2d-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="abb2d-184">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="abb2d-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="abb2d-185">Ustaw przy użyciu obiektu EngagementConfiguration toofalse awarii raportu.</span><span class="sxs-lookup"><span data-stu-id="abb2d-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="abb2d-186">Tryb serii</span><span class="sxs-lookup"><span data-stu-id="abb2d-186">Burst mode</span></span>
<span data-ttu-id="abb2d-187">Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="abb2d-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="abb2d-188">Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="abb2d-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="abb2d-189">toodo należy wywołać metodę hello:</span><span class="sxs-lookup"><span data-stu-id="abb2d-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="abb2d-190">Hello argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="abb2d-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="abb2d-191">W dowolnym momencie rejestrowania w czasie rzeczywistym hello tooreactivate należy po prostu Wywołaj metodę hello bez parametrów lub z wartością hello 0.</span><span class="sxs-lookup"><span data-stu-id="abb2d-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="abb2d-192">Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="abb2d-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="abb2d-193">Jest zalecana toouse próg w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="abb2d-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="abb2d-194">Masz toobe wiedzieć, które zapisane dzienniki są ograniczone too300 elementów.</span><span class="sxs-lookup"><span data-stu-id="abb2d-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="abb2d-195">W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="abb2d-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="abb2d-196">Witaj próg serii nie można skonfigurować okres tooa mniejszym niż 1 sekunda.</span><span class="sxs-lookup"><span data-stu-id="abb2d-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="abb2d-197">Jeśli spróbujesz toodo tak, hello zestawu SDK będą Pokaż śledzenia z powodu błędu hello i automatycznie zresetować toohello wartość domyślna, czyli zero sekund.</span><span class="sxs-lookup"><span data-stu-id="abb2d-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="abb2d-198">To spowoduje wyzwolenie hello SDK tooreport hello dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="abb2d-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

