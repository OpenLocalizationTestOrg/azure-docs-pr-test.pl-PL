---
title: "Integracja zestawu SDK zaangażowania uniwersalnych aplikacji systemu Windows"
description: "Integrowanie usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
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
ms.openlocfilehash: 898160814304fa8ec65622056a77ca9d4caf2c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="1e623-103">Integracja zestawu SDK zaangażowania uniwersalnych aplikacji systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1e623-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e623-104">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1e623-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="1e623-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1e623-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="1e623-106">iOS</span><span class="sxs-lookup"><span data-stu-id="1e623-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="1e623-107">Android</span><span class="sxs-lookup"><span data-stu-id="1e623-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="1e623-108">W tej procedurze opisano Najprostszym sposobem, aby aktywować usługi Engagement analizy i monitorowania aplikacji uniwersalnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1e623-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="1e623-109">Poniższe kroki są wystarczająco aktywować raport dzienniki wymagane do obliczenia wszystkich statystyki dotyczące użytkowników, sesji, działania, awarii (Crash) i Technicals.</span><span class="sxs-lookup"><span data-stu-id="1e623-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="1e623-110">Raport dzienniki wymagane do obliczenia innych danych statystycznych, takich jak zdarzenia i błędy zadań musi zostać wykonane ręcznie przy użyciu interfejsu API usługi Engagement (zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-use-engagement-api.md) od tych statystyki są aplikacji zależnej.</span><span class="sxs-lookup"><span data-stu-id="1e623-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="1e623-111">Obsługiwane wersje</span><span class="sxs-lookup"><span data-stu-id="1e623-111">Supported versions</span></span>
<span data-ttu-id="1e623-112">Tylko Mobile Engagement SDK dla uniwersalnych aplikacji systemu Windows mogą być zintegrowane środowisko wykonawcze systemu Windows i aplikacji platformy uniwersalnej systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="1e623-112">The Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="1e623-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="1e623-113">Windows 8</span></span>
* <span data-ttu-id="1e623-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1e623-114">Windows 8.1</span></span>
* <span data-ttu-id="1e623-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="1e623-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="1e623-116">Windows 10 (wersje desktop i mobile rodzin)</span><span class="sxs-lookup"><span data-stu-id="1e623-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="1e623-117">Jeśli przeznaczona dla systemu Windows Phone Silverlight, zapoznaj się [procedura integracji systemu Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="1e623-117">If you are targeting Windows Phone Silverlight then refer to the [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="1e623-118">Zainstaluj zestaw SDK usługi Mobile Engagement uniwersalnych aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e623-118">Install the Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="1e623-119">Wszystkie platformy</span><span class="sxs-lookup"><span data-stu-id="1e623-119">All platforms</span></span>
<span data-ttu-id="1e623-120">Mobile Engagement SDK dla aplikacji uniwersalnej systemu Windows jest dostępna jako pakietu Nuget, nazywany *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="1e623-120">The Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="1e623-121">Można ją zainstalować z Visual Studio Menedżera pakietów Nuget.</span><span class="sxs-lookup"><span data-stu-id="1e623-121">You can install it from the Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="1e623-122">Windows 8.x i Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="1e623-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="1e623-123">NuGet automatycznie wdraża zasobów zestawu SDK w `Resources` folder w katalogu głównym projektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-123">NuGet automatically deploys the SDK resources in the `Resources` folder at the root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="1e623-124">Aplikacji platformy uniwersalnej systemu Windows 10 systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1e623-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="1e623-125">NuGet nie automatycznie wdrażać zasobów zestawu SDK w jeszcze aplikacji platformy uniwersalnej systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1e623-125">NuGet does not automatically deploy the SDK resources in your UWP application yet.</span></span> <span data-ttu-id="1e623-126">Należy to zrobić ręcznie do momentu powraca wdrażania zasobów w NuGet:</span><span class="sxs-lookup"><span data-stu-id="1e623-126">You have to do it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="1e623-127">Otwieranie Eksploratora plików w sieci.</span><span class="sxs-lookup"><span data-stu-id="1e623-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="1e623-128">Przejdź do następującej lokalizacji (**x.x.x** jest wersją w przypadku instalowania usługi Engagement): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="1e623-128">Navigate to the following location (**x.x.x** is the version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="1e623-129">Przeciągnij i upuść **zasobów** folder w Eksploratorze plików w katalogu głównym projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1e623-129">Drag and drop the **Resources** folder from the file explorer to the root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="1e623-130">W programie Visual Studio wybierz projektu i Aktywuj **Pokaż wszystkie pliki** ikonę nad **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="1e623-130">In Visual Studio select your project and activate the **Show All files** icon on top of the **Solution Explorer**.</span></span>
5. <span data-ttu-id="1e623-131">Niektóre pliki nie znajdują się w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1e623-131">Some files are not included in the project.</span></span> <span data-ttu-id="1e623-132">Aby zaimportować je jednocześnie kliknij prawym przyciskiem myszy **zasobów** folderu, **wykluczyć z projektu** innego kliknij prawym przyciskiem myszy, a następnie **zasobów** folderu, **uwzględnione w Projekt** ponownie uwzględnienie całego folderu.</span><span class="sxs-lookup"><span data-stu-id="1e623-132">To import them at once right click on the **Resources** folder, **Exclude from project** then another right click on the **Resources** folder, **Include in project** to re-include the whole folder.</span></span> <span data-ttu-id="1e623-133">Wszystkie pliki z **zasobów** folderze znajdują się teraz w projekcie.</span><span class="sxs-lookup"><span data-stu-id="1e623-133">All files from the **Resources** folder are now included in your project.</span></span>

## <a name="add-the-capabilities"></a><span data-ttu-id="1e623-134">Dodawanie funkcji</span><span class="sxs-lookup"><span data-stu-id="1e623-134">Add the capabilities</span></span>
<span data-ttu-id="1e623-135">Engagement SDK wymaga prawidłowego funkcjonowania niektórych możliwości zestaw Windows SDK.</span><span class="sxs-lookup"><span data-stu-id="1e623-135">The Engagement SDK needs some capabilities of the Windows SDK in order to work properly.</span></span>

<span data-ttu-id="1e623-136">Otwórz z `Package.appxmanifest` plików i pamiętaj, że następujące funkcje są deklarowane jako:</span><span class="sxs-lookup"><span data-stu-id="1e623-136">Open your `Package.appxmanifest` file and be sure that the following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="1e623-137">Inicjowanie usługi Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="1e623-137">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="1e623-138">Konfiguracja usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="1e623-138">Engagement configuration</span></span>
<span data-ttu-id="1e623-139">Konfiguracja zaangażowania jest scentralizowana w `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="1e623-139">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="1e623-140">Edytuj ten plik, aby określić:</span><span class="sxs-lookup"><span data-stu-id="1e623-140">Edit this file to specify:</span></span>

* <span data-ttu-id="1e623-141">Parametry połączenia aplikacji między tagami `<connectionString>` i `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="1e623-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="1e623-142">Jeśli chcesz określić je w czasie wykonywania, należy wywołać metodę następujące przed zainicjowaniem agenta usługi Engagement:</span><span class="sxs-lookup"><span data-stu-id="1e623-142">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="1e623-143">Ciąg połączenia dla aplikacji jest wyświetlany w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e623-143">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="1e623-144">Inicjowania usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="1e623-144">Engagement initialization</span></span>
<span data-ttu-id="1e623-145">Podczas tworzenia nowego projektu `App.xaml.cs` plik został wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="1e623-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="1e623-146">Ta klasa dziedziczy `Application` i zawiera wiele metod ważne.</span><span class="sxs-lookup"><span data-stu-id="1e623-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="1e623-147">Będzie można również używany do inicjowania usługi Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="1e623-147">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="1e623-148">Modyfikowanie `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="1e623-148">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="1e623-149">Dodaj do Twojej `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1e623-149">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="1e623-150">Zdefiniuj metodę udostępniania inicjowania usługi Engagement raz dla wszystkich wywołań:</span><span class="sxs-lookup"><span data-stu-id="1e623-150">Define a method to share the Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="1e623-151">Wywołanie `InitEngagement` w `OnLaunched` metody:</span><span class="sxs-lookup"><span data-stu-id="1e623-151">Call `InitEngagement` in the `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="1e623-152">Gdy aplikacja jest uruchamiana za pomocą schematu niestandardowego, inna aplikacja lub wiersza polecenia, a następnie `OnActivated` metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="1e623-152">When your application is launched using a custom scheme, another application or the command line then the `OnActivated` method is called.</span></span> <span data-ttu-id="1e623-153">Należy również inicjowania usługi Engagement SDK, po aktywowaniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-153">You also need to initiate the Engagement SDK when your app is activated.</span></span> <span data-ttu-id="1e623-154">Aby to zrobić, należy zastąpić `OnActivated` metody:</span><span class="sxs-lookup"><span data-stu-id="1e623-154">To do so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="1e623-155">Firma Microsoft zdecydowanie zniechęcić można dodać inicjowania usługi Engagement w innym miejscu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-155">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="1e623-156">Podstawowym raportowaniem</span><span class="sxs-lookup"><span data-stu-id="1e623-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="1e623-157">Zalecana metoda: przeciążenia sieci `Page` klas</span><span class="sxs-lookup"><span data-stu-id="1e623-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="1e623-158">Aby aktywować raportu wszystkie dzienniki wymagane przez zaangażowania można obliczyć użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, możesz po prostu wprowadzić wszystkie Twoje `Page` klasy podrzędne dziedziczą `EngagementPage` klasy.</span><span class="sxs-lookup"><span data-stu-id="1e623-158">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="1e623-159">Oto przykład tego, jak to zrobić w strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-159">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="1e623-160">Możesz to zrobić to samo dla wszystkich stron w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-160">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="1e623-161">Plik źródłowy języka C#</span><span class="sxs-lookup"><span data-stu-id="1e623-161">C# Source file</span></span>
<span data-ttu-id="1e623-162">Zmodyfikuj stronę `.xaml.cs` pliku:</span><span class="sxs-lookup"><span data-stu-id="1e623-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="1e623-163">Dodaj do Twojej `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1e623-163">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="1e623-164">Zastąp `Page` z `EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="1e623-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="1e623-165">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1e623-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="1e623-166">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1e623-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="1e623-167">Jeśli strona zastępuje metodę `OnNavigatedTo`, nie zapomnij wywołać metody `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="1e623-167">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="1e623-168">W przeciwnym razie działanie nie zostanie zgłoszone (element `EngagementPage` wywołuje metodę `StartActivity` wewnątrz jego metody `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="1e623-168">Otherwise,  the activity will not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="1e623-169">Plik XAML</span><span class="sxs-lookup"><span data-stu-id="1e623-169">XAML file</span></span>
<span data-ttu-id="1e623-170">Zmodyfikuj stronę `.xaml` pliku:</span><span class="sxs-lookup"><span data-stu-id="1e623-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="1e623-171">Dodaj deklaracje przestrzeni nazw:</span><span class="sxs-lookup"><span data-stu-id="1e623-171">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="1e623-172">Zastąp `Page` z `engagement:EngagementPage`:</span><span class="sxs-lookup"><span data-stu-id="1e623-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="1e623-173">**Bez usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1e623-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="1e623-174">**Z usługi Engagement:**</span><span class="sxs-lookup"><span data-stu-id="1e623-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-the-default-behaviour"></a><span data-ttu-id="1e623-175">Zastąpienie zachowania domyślnego</span><span class="sxs-lookup"><span data-stu-id="1e623-175">Override the default behaviour</span></span>
<span data-ttu-id="1e623-176">Domyślnie nazwa klasy strony został zgłoszony jako nazwę działania, bez dodatkowych.</span><span class="sxs-lookup"><span data-stu-id="1e623-176">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="1e623-177">Jeśli klasa korzysta z sufiksem "Page", Engagement spowoduje również usunięcie.</span><span class="sxs-lookup"><span data-stu-id="1e623-177">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="1e623-178">Jeśli chcesz zastąpić domyślne zachowanie dla nazwy, po prostu dodaj to w kodzie:</span><span class="sxs-lookup"><span data-stu-id="1e623-178">If you want to override the default behaviour for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="1e623-179">Jeśli chcesz zgłosić niektóre dodatkowe informacje o Twoich działaniach, możesz dodać to w kodzie:</span><span class="sxs-lookup"><span data-stu-id="1e623-179">If you want to report some extra informations with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="1e623-180">Te metody są wywoływane z poziomu `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="1e623-180">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="1e623-181">Alternatywna metoda: wywołanie `StartActivity()` ręcznie</span><span class="sxs-lookup"><span data-stu-id="1e623-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="1e623-182">Jeśli nie możesz lub nie było przeciążyć Twojej `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1e623-182">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="1e623-183">Firma Microsoft zaleca, aby wywołać `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.</span><span class="sxs-lookup"><span data-stu-id="1e623-183">We recommend to call `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="1e623-184">Upewnij się, że prawidłowo zakończyć sesję.</span><span class="sxs-lookup"><span data-stu-id="1e623-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="1e623-185">Uniwersalny zestaw SDK systemu Windows automatycznie wywołuje `EndActivity` metody, gdy aplikacja zostanie zamknięta.</span><span class="sxs-lookup"><span data-stu-id="1e623-185">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="1e623-186">W związku z tym jest **wysokiej** zaleca, aby wywołać `StartActivity` metody zmianie aktywności użytkownika i **nigdy** wywołać `EndActivity` metody, ta metoda wysyła do serwera usługi Engagement który bieżący użytkownik ma pozostawić aplikacji, to zostanie ma wpływ na wszystkie dzienniki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e623-186">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method, this method sends to Engagement server that current user has leave the application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="1e623-187">Zaawansowane raportowanie</span><span class="sxs-lookup"><span data-stu-id="1e623-187">Advanced reporting</span></span>
<span data-ttu-id="1e623-188">Opcjonalnie, może zajść potrzeba raport aplikacji określonych zdarzeń, błędów i zadań, w tym celu należy użyć innych metod znalezione w `EngagementAgent` klasy.</span><span class="sxs-lookup"><span data-stu-id="1e623-188">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="1e623-189">Interfejsu API usługi Engagement pozwala na korzystanie ze wszystkich zaawansowanych możliwości usługi Engagement.</span><span class="sxs-lookup"><span data-stu-id="1e623-189">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="1e623-190">Aby uzyskać więcej informacji, zobacz [sposobu korzystania z zaawansowanych Mobile Engagement znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="1e623-190">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="1e623-191">Konfiguracja zaawansowana</span><span class="sxs-lookup"><span data-stu-id="1e623-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="1e623-192">Wyłącz automatyczne zgłaszanie awarii</span><span class="sxs-lookup"><span data-stu-id="1e623-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="1e623-193">Możesz wyłączyć automatyczne awarii, funkcję zaangażowania raportowania.</span><span class="sxs-lookup"><span data-stu-id="1e623-193">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="1e623-194">Następnie, gdy wystąpi nieobsługiwany wyjątek, Engagement nie będzie wykonywać żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="1e623-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="1e623-195">Jeśli chcesz wyłączyć tę funkcję, należy pamiętać, że po awarii nieobsługiwany nastąpi w aplikacji, Engagement nie będą wysyłały awarii **i** nie spowoduje zamknięcia sesji i zadania.</span><span class="sxs-lookup"><span data-stu-id="1e623-195">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="1e623-196">Aby wyłączyć automatyczne zgłaszanie awarii, wystarczy dostosować konfigurację, w zależności od sposobu należy zadeklarować jako:</span><span class="sxs-lookup"><span data-stu-id="1e623-196">To disable automatic crash reporting, just customize your configuration depending on the way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="1e623-197">Z `EngagementConfiguration.xml` pliku</span><span class="sxs-lookup"><span data-stu-id="1e623-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="1e623-198">Ustaw awarii raport `false` między `<reportCrash>` i `</reportCrash>` tagów.</span><span class="sxs-lookup"><span data-stu-id="1e623-198">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="1e623-199">Z `EngagementConfiguration` obiektu w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="1e623-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="1e623-200">Ustaw awarii raportu przy użyciu obiektu EngagementConfiguration wartość false.</span><span class="sxs-lookup"><span data-stu-id="1e623-200">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="1e623-201">Tryb serii</span><span class="sxs-lookup"><span data-stu-id="1e623-201">Burst mode</span></span>
<span data-ttu-id="1e623-202">Domyślnie raporty usługi Engagement rejestruje się w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1e623-202">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="1e623-203">Jeśli aplikacja zgłasza dzienniki bardzo często, lepiej jest buforu dzienniki i raportuj je w całości na regularne podstawy czasu (jest to nazywane "tryb serii").</span><span class="sxs-lookup"><span data-stu-id="1e623-203">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="1e623-204">Aby to zrobić, należy wywołać metodę:</span><span class="sxs-lookup"><span data-stu-id="1e623-204">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="1e623-205">Argument jest wartością w **milisekund**.</span><span class="sxs-lookup"><span data-stu-id="1e623-205">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="1e623-206">W dowolnym momencie Jeśli chcesz ponownie uaktywnić rejestrowania w czasie rzeczywistym, po prostu Wywołaj metodę bez parametrów lub z wartością 0.</span><span class="sxs-lookup"><span data-stu-id="1e623-206">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="1e623-207">Tryb serii nieco zwiększyć czas pracy baterii, ale ma wpływ na monitorowanie usługi Engagement: wszystkie czas trwania sesji i zadania zostanie zaokrąglony próg serii (w związku z tym sesji i zadania krótsze niż próg serii może nie być widoczna).</span><span class="sxs-lookup"><span data-stu-id="1e623-207">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="1e623-208">Zaleca się przy użyciu progu w serii się niż 30000 (30s).</span><span class="sxs-lookup"><span data-stu-id="1e623-208">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="1e623-209">Masz wiedzieć, który zapisano dzienniki są ograniczone do 300 elementów.</span><span class="sxs-lookup"><span data-stu-id="1e623-209">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="1e623-210">W przypadku wysyłania jest zbyt długa może spowodować utratę niektórych dzienników.</span><span class="sxs-lookup"><span data-stu-id="1e623-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="1e623-211">Próg serii nie można skonfigurować do okresu mniejsza od wartości 1.</span><span class="sxs-lookup"><span data-stu-id="1e623-211">The burst threshold cannot be configured to a period lesser than 1s.</span></span> <span data-ttu-id="1e623-212">Jeśli użytkownik spróbuje to zrobić, zestaw SDK wyświetli śledzenia z powodu błędu i będzie automatycznie resetować wartość domyślna, czyli 0s.</span><span class="sxs-lookup"><span data-stu-id="1e623-212">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, i.e., 0s.</span></span> <span data-ttu-id="1e623-213">Spowoduje to wyzwolenie zestaw SDK, aby zgłosić dzienniki w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="1e623-213">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

