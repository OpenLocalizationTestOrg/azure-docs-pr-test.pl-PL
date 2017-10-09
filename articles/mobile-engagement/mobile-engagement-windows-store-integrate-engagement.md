---
title: "aaaWindows uniwersalnych integracji zestawu SDK usługi Engagement aplikacji"
description: "Jak tooIntegrate usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="c2f6e-103">Integracja zestawu SDK zaangażowania uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c2f6e-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c2f6e-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c2f6e-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="c2f6e-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="c2f6e-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="c2f6e-106">iOS</span><span class="sxs-lookup"><span data-stu-id="c2f6e-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="c2f6e-107">Android</span><span class="sxs-lookup"><span data-stu-id="c2f6e-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="c2f6e-108">W tej procedurze opisano analizy i monitorowania aplikacji uniwersalnych systemu Windows hello najprostszy sposób tooactivate usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="c2f6e-109">wymaga wystarczającej ilości raportu hello tooactivate dzienników toocompute wszystkie statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals to Hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="c2f6e-110">Raport Hello dzienników potrzebne toocompute innych danych statystycznych jak zadań, błędy i zdarzenia musi zostać wykonane ręcznie przy użyciu hello zaangażowania interfejsu API (zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md) od te statystyki są aplikacji zależnej.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="c2f6e-111">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="c2f6e-111">Supported versions</span></span>
<span data-ttu-id="c2f6e-112">tylko Hello Mobile Engagement SDK dla uniwersalnych aplikacji systemu Windows mogą być zintegrowane środowisko wykonawcze systemu Windows i aplikacji platformy uniwersalnej systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="c2f6e-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="c2f6e-113">Windows 8</span></span>
* <span data-ttu-id="c2f6e-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c2f6e-114">Windows 8.1</span></span>
* <span data-ttu-id="c2f6e-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="c2f6e-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="c2f6e-116">Windows 10 (wersje desktop i mobile rodzin)</span><span class="sxs-lookup"><span data-stu-id="c2f6e-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="c2f6e-117">Jeśli przeznaczona dla systemu Windows Phone Silverlight można znaleźć toohello [procedura integracji systemu Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="c2f6e-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="c2f6e-118">Zainstaluj hello Mobile Engagement uniwersalny zestaw SDK aplikacji</span><span class="sxs-lookup"><span data-stu-id="c2f6e-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="c2f6e-119">Wszystkie platformy</span><span class="sxs-lookup"><span data-stu-id="c2f6e-119">All platforms</span></span>
<span data-ttu-id="c2f6e-120">Witaj Mobile Engagement SDK dla aplikacji uniwersalnej systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="c2f6e-121">Można go zainstalować z hello Menedżera pakietów Nuget programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="c2f6e-122">Windows 8.x i Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="c2f6e-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="c2f6e-123">NuGet automatycznie wdraża hello zasobów zestawu SDK w hello `Resources` folder w katalogu głównym projektu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="c2f6e-124">Aplikacji platformy uniwersalnej systemu Windows 10 systemu Windows</span><span class="sxs-lookup"><span data-stu-id="c2f6e-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="c2f6e-125">NuGet nie automatycznie wdrażać hello zasobów zestawu SDK w jeszcze aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="c2f6e-126">Masz toodo powraca go ręcznie do wdrażania zasobów w NuGet:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="c2f6e-127">Otwieranie Eksploratora plików w sieci.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="c2f6e-128">Przejdź toohello następującej lokalizacji (**x.x.x** jest wersja hello w przypadku instalowania usługi Engagement): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="c2f6e-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="c2f6e-129">Przeciąganie i upuszczanie hello **zasobów** folderu z katalogu głównego toohello Eksploratora plików hello projektu w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="c2f6e-130">W programie Visual Studio wybierz projektu i Aktywuj hello **Pokaż wszystkie pliki** ikony na powitania **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="c2f6e-131">Niektóre pliki nie znajdują się w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-131">Some files are not included in hello project.</span></span> <span data-ttu-id="c2f6e-132">tooimport je jednocześnie kliknij prawym przyciskiem myszy hello **zasobów** folderu, **wykluczyć z projektu** , a następnie innego kliknij prawym przyciskiem myszy hello **zasobów** folderu, **dołączania w projekcie** toore-zawierają hello cały folder.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="c2f6e-133">Wszystkie pliki z hello **zasobów** folderze znajdują się teraz w projekcie.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="c2f6e-134">Dodawanie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="c2f6e-134">Add hello capabilities</span></span>
<span data-ttu-id="c2f6e-135">Witaj Engagement SDK musi niektóre możliwości hello zestaw Windows SDK w kolejności toowork poprawnie.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="c2f6e-136">Otwórz z `Package.appxmanifest` plików i pamiętaj, że hello następujące funkcje są deklarowane jako:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="c2f6e-137">Inicjowanie hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="c2f6e-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="c2f6e-138">Konfiguracja usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="c2f6e-138">Engagement configuration</span></span>
<span data-ttu-id="c2f6e-139">konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="c2f6e-140">Edytuj toospecify tego pliku:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="c2f6e-141">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="c2f6e-142">Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="c2f6e-143">Parametry połączenia Hello aplikacji jest wyświetlany na powitania klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="c2f6e-144">Inicjowania usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="c2f6e-144">Engagement initialization</span></span>
<span data-ttu-id="c2f6e-145">Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="c2f6e-146">Ta klasa dziedziczy `Application` i zawiera wiele metod ważne.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="c2f6e-147">Konieczne będzie również używany tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="c2f6e-148">Modyfikowanie hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="c2f6e-149">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="c2f6e-150">Zdefiniuj inicjowania usługi Engagement — metoda tooshare hello raz dla wszystkich wywołań:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="c2f6e-151">Wywołanie `InitEngagement` w hello `OnLaunched` metody:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="c2f6e-152">Gdy aplikacja jest uruchamiana za pomocą schematu niestandardowego, innego wiersza polecenia aplikacji lub hello następnie hello `OnActivated` metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="c2f6e-153">Należy również hello tooinitiate Engagement SDK po aktywowaniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="c2f6e-154">tak, Zastąp toodo `OnActivated` metody:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="c2f6e-155">Firma Microsoft zdecydowanie zniechęcić możesz tooadd hello zaangażowania inicjowania w innym miejscu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="c2f6e-156">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="c2f6e-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="c2f6e-157">Zalecana metoda: przeciążenia sieci `Page` klas</span><span class="sxs-lookup"><span data-stu-id="c2f6e-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="c2f6e-158">W raporcie hello tooactivate kolejności wszystkich dzienników hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="c2f6e-159">Oto przykład tego, jak toodo to strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="c2f6e-160">Możesz zrobić hello samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="c2f6e-161">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="c2f6e-161">C# Source file</span></span>
<span data-ttu-id="c2f6e-162">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="c2f6e-163">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="c2f6e-164">Zastąp `Page` z `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="c2f6e-165">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c2f6e-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="c2f6e-166">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c2f6e-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="c2f6e-167">Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="c2f6e-168">W przeciwnym razie działanie hello nie będą raportowane (hello `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).</span><span class="sxs-lookup"><span data-stu-id="c2f6e-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="c2f6e-169">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="c2f6e-169">XAML file</span></span>
<span data-ttu-id="c2f6e-170">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="c2f6e-171">Dodaj deklaracje przestrzeni nazw tooyour:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="c2f6e-172">Zastąp `Page` z `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="c2f6e-173">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c2f6e-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="c2f6e-174">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="c2f6e-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="c2f6e-175">Zastąpienie zachowania domyślnego hello</span><span class="sxs-lookup"><span data-stu-id="c2f6e-175">Override hello default behaviour</span></span>
<span data-ttu-id="c2f6e-176">Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="c2f6e-177">Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement spowoduje również usunięcie.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="c2f6e-178">Jeśli chcesz toooverride hello domyślne zachowanie dla nazwy hello, po prostu dodaj ten kod tooyour:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="c2f6e-179">Jeśli chcesz tooreport niektóre dodatkowe informacje o Twoich działaniach, można dodać ten kod tooyour:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="c2f6e-180">Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="c2f6e-181">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="c2f6e-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="c2f6e-182">Jeśli nie możesz lub nie ma toooverload Twojego `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="c2f6e-183">Firma Microsoft zaleca toocall `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="c2f6e-184">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="c2f6e-185">Witaj uniwersalnego zestawu SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="c2f6e-186">W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` metoda, ta metoda wysyła tooEngagement serwer, że bieżący użytkownik aplikacji hello pozostaw, spowoduje to ma wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="c2f6e-187">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="c2f6e-187">Advanced reporting</span></span>
<span data-ttu-id="c2f6e-188">Opcjonalnie możesz tooreport aplikacji określonych zdarzeń, błędów i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="c2f6e-189">Witaj interfejsu API usługi Engagement umożliwia toouse wszystkie funkcje zaawansowane usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="c2f6e-190">Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="c2f6e-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="c2f6e-191">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="c2f6e-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="c2f6e-192">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="c2f6e-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="c2f6e-193">Możesz wyłączyć hello awarii automatyczne funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="c2f6e-194">Następnie, gdy wystąpi nieobsługiwany wyjątek, Engagement nie będzie wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="c2f6e-195">Jeśli planujesz toodisable tej funkcji, należy pamiętać, że po awarii nieobsługiwany nastąpi w aplikacji, Engagement nie będą wysyłały awarii hello **i** nie spowoduje zamknięcia sesji hello i zadania.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="c2f6e-196">toodisable awarii automatycznego raportowania, po prostu Dostosuj konfigurację w zależności od sposób hello należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="c2f6e-197">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="c2f6e-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="c2f6e-198">Raport z ustawiania awaria zbyt`false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="c2f6e-199">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="c2f6e-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="c2f6e-200">Ustaw przy użyciu obiektu EngagementConfiguration toofalse awarii raportu.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="c2f6e-201">Tryb serii</span><span class="sxs-lookup"><span data-stu-id="c2f6e-201">Burst mode</span></span>
<span data-ttu-id="c2f6e-202">Domyślnie raporty usługi Engagement hello rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="c2f6e-203">Jeśli aplikacja zgłasza dzienniki bardzo często, jest lepsze toobuffer hello dzienniki i tooreport ich jednocześnie na regularne podstawy czasu (jest to nazywane hello "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="c2f6e-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="c2f6e-204">toodo należy wywołać metodę hello:</span><span class="sxs-lookup"><span data-stu-id="c2f6e-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="c2f6e-205">Hello argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="c2f6e-206">W dowolnym momencie rejestrowania w czasie rzeczywistym hello tooreactivate należy po prostu Wywołaj metodę hello bez parametrów lub z wartością hello 0.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="c2f6e-207">Witaj tryb serii wydłużyć baterii hello życia ale ma wpływ na powitania Monitor zaangażowania: wszystkie czas trwania zadania i sesje będą zaokrąglone toohello serii próg (w związku z tym sesji i zadania krótsze niż próg serii hello może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="c2f6e-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="c2f6e-208">Jest zalecana toouse próg w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="c2f6e-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="c2f6e-209">Masz toobe wiedzieć, które zapisane dzienniki są ograniczone too300 elementów.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="c2f6e-210">W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="c2f6e-211">Próg serii Hello nie można skonfigurować okres tooa mniejsza od wartości 1.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="c2f6e-212">Jeśli spróbujesz toodo tak, hello zestawu SDK będą Pokaż śledzenia z powodu błędu hello i automatycznie resetować toohello wartość domyślna, czyli 0s.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="c2f6e-213">To spowoduje wyzwolenie hello SDK tooreport hello dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c2f6e-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

