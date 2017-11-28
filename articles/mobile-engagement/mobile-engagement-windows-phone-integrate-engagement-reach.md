---
title: "aaaWindows osiągnąć integracji zestawu SDK programu Phone Silverlight"
description: "Jak tooIntegrate usługi Azure Mobile Engagement nawiązać połączenia z aplikacjami programu Windows Phone Silverlight"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="d33dc-103">Windows Phone Silverlight dotarcia do integracji zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="d33dc-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="d33dc-104">Musisz wykonać procedurę integracji hello opisanego w hello [integracji zestawu SDK usługi Engagement Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) przed wykonaniem tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="d33dc-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="d33dc-105">Osadź hello Engagement Reach SDK do projektu systemu Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="d33dc-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="d33dc-106">Nie masz żadnych tooadd.</span><span class="sxs-lookup"><span data-stu-id="d33dc-106">You do not have anything tooadd.</span></span> <span data-ttu-id="d33dc-107">`EngagementReach`referencje i zasoby są już w projekcie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="d33dc-108">Można dostosować obrazy znajdujące się w hello `Resources` folderu projektu, szczególnie hello brand ikona (tej domyślnej toohello Engagement).</span><span class="sxs-lookup"><span data-stu-id="d33dc-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="d33dc-109">Dodawanie funkcji hello</span><span class="sxs-lookup"><span data-stu-id="d33dc-109">Add hello capabilities</span></span>
<span data-ttu-id="d33dc-110">zestaw SDK Reach usługi Engagement Hello musi niektóre dodatkowe funkcje.</span><span class="sxs-lookup"><span data-stu-id="d33dc-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="d33dc-111">Otwórz z `WMAppManifest.xml` plików i pamiętaj, że hello następujące funkcje są deklarowane jako:</span><span class="sxs-lookup"><span data-stu-id="d33dc-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="d33dc-112">Hello najpierw jednym jest używana przez hello MPNS usługi tooallow hello wyświetlanie wyskakujących powiadomień.</span><span class="sxs-lookup"><span data-stu-id="d33dc-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="d33dc-113">Witaj drugim jest używane tooembed zadania przeglądarki do hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="d33dc-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="d33dc-114">Edytuj hello `WMAppManifest.xml` plik i dodać wewnątrz hello `<Capabilities />` tagu:</span><span class="sxs-lookup"><span data-stu-id="d33dc-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="d33dc-115">Włącz hello Microsoft Push Notification Service</span><span class="sxs-lookup"><span data-stu-id="d33dc-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="d33dc-116">W kolejności toouse hello **Microsoft Push Notification Service** (określanych jako usługi MPNS) z `WMAppManifest.xml` plik musi mieć `<App />` tagu z `Publisher` ustawiony atrybut toohello nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="d33dc-117">Zainicjuj zestaw SDK Reach usługi Engagement hello</span><span class="sxs-lookup"><span data-stu-id="d33dc-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="d33dc-118">Konfiguracja usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="d33dc-118">Engagement configuration</span></span>
<span data-ttu-id="d33dc-119">konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="d33dc-120">Zmień konfigurację reach toospecify tego pliku:</span><span class="sxs-lookup"><span data-stu-id="d33dc-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="d33dc-121">*Opcjonalne*, wskazuje, czy włączono hello natywnych powiadomień wypychanych (MPNS), czy między `<enableNativePush>` i `</enableNativePush>` tagi (`true` domyślnie).</span><span class="sxs-lookup"><span data-stu-id="d33dc-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="d33dc-122">*Opcjonalne*, nazwa hello kanału wypychanych hello między `<channelName>` i `</channelName>` tagów, podaj hello tej samej aplikacji mogą obecnie korzystać lub pozostaw puste.</span><span class="sxs-lookup"><span data-stu-id="d33dc-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="d33dc-123">Jeśli chcesz, aby toospecify go w czasie wykonywania zamiast tego możesz wywołać program hello następujące metody przed zainicjowaniem agenta zaangażowania hello:</span><span class="sxs-lookup"><span data-stu-id="d33dc-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="d33dc-124">Można określić nazwę hello kanału wypychanych usługi MPNS hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33dc-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="d33dc-125">Domyślnie program zaangażowania tworzy nazwę oparte na powitania appId.</span><span class="sxs-lookup"><span data-stu-id="d33dc-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="d33dc-126">Możesz nie mieć potrzeby toospecify hello nazwy użytkownika, z wyjątkiem przypadków, jeśli planujesz kanału wypychanych hello toouse poza zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="d33dc-127">Inicjowania usługi Engagement</span><span class="sxs-lookup"><span data-stu-id="d33dc-127">Engagement initialization</span></span>
<span data-ttu-id="d33dc-128">Modyfikowanie hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d33dc-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="d33dc-129">Dodaj tooyour `using` instrukcji:</span><span class="sxs-lookup"><span data-stu-id="d33dc-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="d33dc-130">Wstaw `EngagementReach.Instance.Init` tuż po `EngagementAgent.Instance.Init` w `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="d33dc-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="d33dc-131">Wstaw `EngagementReach.Instance.OnActivated` w hello `Application_Activated` metody:</span><span class="sxs-lookup"><span data-stu-id="d33dc-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="d33dc-132">Witaj `EngagementReach.Instance.Init` działa w dedykowanym wątku.</span><span class="sxs-lookup"><span data-stu-id="d33dc-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="d33dc-133">Nie masz toodo ją samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="d33dc-134">Zagadnienia dotyczące przesyłania magazynu aplikacji</span><span class="sxs-lookup"><span data-stu-id="d33dc-134">App store submission considerations</span></span>
<span data-ttu-id="d33dc-135">Microsoft nakłada niektórych reguł przy użyciu powiadomień wypychanych hello:</span><span class="sxs-lookup"><span data-stu-id="d33dc-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="d33dc-136">Z hello Microsoft [zasady aplikacji] dokumentacji, sekcja 2.9:</span><span class="sxs-lookup"><span data-stu-id="d33dc-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="d33dc-137">Musisz poprosić hello wysyłanie powiadomień wypychanych tooreceive tooaccept użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33dc-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="d33dc-138">Następnie w ustawieniach, należy dodać powiadomień wypychanych hello toodisable sposób.</span><span class="sxs-lookup"><span data-stu-id="d33dc-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="d33dc-139">Obiekt EngagementReach Hello oferuje dwie metody toomanage hello w/opt — zrezygnować, `EnableNativePush()` i `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="d33dc-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="d33dc-140">Można na przykład utworzyć opcję w ustawieniach hello z toodisable przełącznika lub włączyć usługi MPNS.</span><span class="sxs-lookup"><span data-stu-id="d33dc-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="d33dc-141">Można również określić, że toodeactivate MPNS za pomocą konfiguracji zaangażowania hello\<konfiguracji systemu windows-phone-sdk-reach —\>.</span><span class="sxs-lookup"><span data-stu-id="d33dc-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="d33dc-142">2.9.1) aplikacji hello najpierw musi opisywać toobe powiadomienia hello podane i **uzyskać wyraźnej zgody użytkownika hello (opt — ruch przychodzący)**, i **podać mechanizm, za pomocą których hello użytkownik może zrezygnować z odbierania powiadomienia wypychane**.</span><span class="sxs-lookup"><span data-stu-id="d33dc-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="d33dc-143">Wszystkie powiadomienia realizowane przy użyciu usługi powiadomień wypychanych firmy Microsoft hello muszą być zgodne z hello dostarczony opis toohello użytkownika i musi spełniać wszystkie odpowiednie [zasady aplikacji] [ Content Policies]i [dodatkowe wymagania dotyczące typów określonej aplikacji].</span><span class="sxs-lookup"><span data-stu-id="d33dc-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="d33dc-144">Nie należy używać zbyt wiele powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="d33dc-144">You should not use too many push notifications.</span></span> <span data-ttu-id="d33dc-145">Zaangażowania obsługi powiadomień dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="d33dc-146">2.9.2) aplikacji hello i jego użycie hello Microsoft Push Notification Service musi nie nadmiernie pojemność sieci lub przepustowości hello usługi powiadomień wypychanych firmy Microsoft lub w przeciwnym razie nadmiernie obciążać Windows Phone lub innych urządzeń firmy Microsoft lub usługi z nadmiernego powiadomień wypychanych, zgodnie z ustaleniami firmy Microsoft uznania i nie musi uszkodzić lub zakłócać żadnych sieci firmy Microsoft lub serwerów lub dowolnych innych firm lub serwerów sieci toohello podłączonej usługi powiadomień wypychanych firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d33dc-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="d33dc-147">Nie należy polegać na MPNS toosend criticals informacji.</span><span class="sxs-lookup"><span data-stu-id="d33dc-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="d33dc-148">Zaangażowania używana jest usługa MPNS, więc ta reguła ma zastosowanie również kampanii hello tworzone wewnątrz hello zaangażowania frontonu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="d33dc-149">2.9.3) hello usługi powiadomień wypychanych firmy Microsoft nie może być używane toosend powiadomień, które są misji krytycznych lub w inny sposób mogą wpłynąć na sprawach życia lub śmierci, w tym bez urządzenia medyczne pokrewne tooa krytyczne powiadomienia ograniczenia lub warunku.</span><span class="sxs-lookup"><span data-stu-id="d33dc-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="d33dc-150">MICROSOFT wyraźnie, że nie ponosi ANY gwarancji czy hello użycia z hello MICROSOFT PUSH POWIADOMIEŃ usługi lub DOSTARCZANIA z MICROSOFT PUSH POWIADOMIEŃ usługi POWIADOMIEŃ będzie można nieprzerwaną, bez błędów, lub w inny sposób gwarantowane tooOCCUR ON A w czasie rzeczywistym podstawy.</span><span class="sxs-lookup"><span data-stu-id="d33dc-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="d33dc-151">**Nie możemy zagwarantować aplikacji przekazuje proces weryfikacji hello Jeśli nie przestrzega te zalecenia.**</span><span class="sxs-lookup"><span data-stu-id="d33dc-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="d33dc-152">Obsługa wypychanie danych (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="d33dc-152">Handle data push (optional)</span></span>
<span data-ttu-id="d33dc-153">Aby wypychania Twojej aplikacji toobe tooreceive stanie Reach danych, masz tooimplement dwa zdarzenia hello EngagementReach klasy:</span><span class="sxs-lookup"><span data-stu-id="d33dc-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

<span data-ttu-id="d33dc-154">Wywołanie zwrotne hello każdego metoda zwraca wartość logiczną jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="d33dc-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="d33dc-155">Zaangażowania wysyła opinii tooits zaplecza po wysłaniu hello wypychanie danych.</span><span class="sxs-lookup"><span data-stu-id="d33dc-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="d33dc-156">Jeśli wywołanie zwrotne hello zwraca wartość false, hello `exit` opinii będzie wysyłania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="d33dc-157">W przeciwnym razie będzie `action`.</span><span class="sxs-lookup"><span data-stu-id="d33dc-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="d33dc-158">Jeśli bez wywołania zwrotnego ustawiono dla zdarzeń hello, hello `drop` Opinia zostanie zwrócony tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="d33dc-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="d33dc-159">Zaangażowania nie jest możliwe tooreceive wielokrotności opinie do wypychania danych.</span><span class="sxs-lookup"><span data-stu-id="d33dc-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="d33dc-160">Jeśli planujesz tooset kilka programów obsługi zdarzeń, należy pamiętać, że opinia hello będzie odpowiadać toohello ostatnią wysłane.</span><span class="sxs-lookup"><span data-stu-id="d33dc-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="d33dc-161">W takim przypadku zalecamy tooalways zwraca hello tego samego tooavoid wartość o mylące opinii na powitania frontonu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="d33dc-162">Dostosowywanie interfejsu użytkownika (opcjonalne)</span><span class="sxs-lookup"><span data-stu-id="d33dc-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="d33dc-163">Pierwszym krokiem</span><span class="sxs-lookup"><span data-stu-id="d33dc-163">First step</span></span>
<span data-ttu-id="d33dc-164">Zezwolimy toocustomize hello reach interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33dc-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="d33dc-165">toodo więc z toocreate podklasą hello `EngagementReachHandler` klasy.</span><span class="sxs-lookup"><span data-stu-id="d33dc-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="d33dc-166">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="d33dc-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="d33dc-167">Następnie ustaw hello zawartość hello `EngagementReach.Instance.Handler` pole z niestandardowego obiektu w Twojej `App.xaml.cs` klasa w hello `Application_Launching` — metoda.</span><span class="sxs-lookup"><span data-stu-id="d33dc-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="d33dc-168">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="d33dc-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="d33dc-169">Domyślnie program zaangażowania używa własną implementację `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="d33dc-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="d33dc-170">Nie masz toocreate własny, a jeśli tak zrobisz, nie masz toooverride każdej metody.</span><span class="sxs-lookup"><span data-stu-id="d33dc-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="d33dc-171">Witaj domyślne zachowanie to obiektu podstawowego tooselect hello zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="d33dc-172">Układy</span><span class="sxs-lookup"><span data-stu-id="d33dc-172">Layouts</span></span>
<span data-ttu-id="d33dc-173">Domyślnie Reach będzie używać zasobów osadzonych hello hello DLL toodisplay hello powiadomień i strony.</span><span class="sxs-lookup"><span data-stu-id="d33dc-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="d33dc-174">Jednak można zdecydować, toouse tooreflect własnych zasobów oznakowanie w tych składników.</span><span class="sxs-lookup"><span data-stu-id="d33dc-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="d33dc-175">Można zastąpić `EngagementReachHandler` metod w Twojej toouse zaangażowania tootell podklasy układów:</span><span class="sxs-lookup"><span data-stu-id="d33dc-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="d33dc-176">**Przykładowy kod:**</span><span class="sxs-lookup"><span data-stu-id="d33dc-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="d33dc-177">Witaj `CreateNotification` metoda może zwracać wartości zerowej.</span><span class="sxs-lookup"><span data-stu-id="d33dc-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="d33dc-178">nie będą wyświetlane powiadomienia Hello, które zostaną usunięte hello reach kampanii.</span><span class="sxs-lookup"><span data-stu-id="d33dc-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="d33dc-179">toosimplify implementacji układu, firma Microsoft udostępnia również własnej xaml, który może służyć jako podstawa dla kodu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="d33dc-180">Znajdują się one w archiwum Engagement SDK hello (/ src/reach /).</span><span class="sxs-lookup"><span data-stu-id="d33dc-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="d33dc-181">Hello źródeł, które firma Microsoft udostępnia są dokładnie takie same jak których używamy hello.</span><span class="sxs-lookup"><span data-stu-id="d33dc-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="d33dc-182">Dlatego toomodify je bezpośrednio, nie zapomnij toochange hello w przestrzeni nazw i hello nazwy.</span><span class="sxs-lookup"><span data-stu-id="d33dc-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="d33dc-183">Pozycja powiadomień</span><span class="sxs-lookup"><span data-stu-id="d33dc-183">Notification position</span></span>
<span data-ttu-id="d33dc-184">Domyślnie na powitania lewym dolnym rogu aplikacji hello zostanie wyświetlone powiadomienie w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d33dc-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="d33dc-185">Możesz zmienić to zachowanie przez zastąpienie hello `GetNotificationPosition` metody hello `EngagementReachHandler` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="d33dc-186">Obecnie można wybrać hello `BOTTOM` (ustawienie domyślne) i `TOP` pozycji.</span><span class="sxs-lookup"><span data-stu-id="d33dc-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="d33dc-187">Uruchamianie wiadomości</span><span class="sxs-lookup"><span data-stu-id="d33dc-187">Launch message</span></span>
<span data-ttu-id="d33dc-188">Gdy użytkownik kliknie powiadomienie systemowe (alert), aplikacji hello powoduje uruchomienie zaangażowania, zawartość hello obciążenia hello push wiadomości i wyświetlić stronę hello hello odpowiadającego kampanii.</span><span class="sxs-lookup"><span data-stu-id="d33dc-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="d33dc-189">Występuje opóźnienie między uruchamiania hello hello aplikacji i hello wyświetlania strony hello (w zależności od szybkości hello sieci).</span><span class="sxs-lookup"><span data-stu-id="d33dc-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="d33dc-190">tooindicate toohello użytkownika, który wystąpił podczas ładowania, należy podać visual informacji, takich jak pasek postępu lub wskaźnik postępu.</span><span class="sxs-lookup"><span data-stu-id="d33dc-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="d33dc-191">Zaangażowania nie może obsłużyć, ale udostępnia kilka programy obsługi dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d33dc-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="d33dc-192">tooimplement hello wywołania zwrotnego, czy:</span><span class="sxs-lookup"><span data-stu-id="d33dc-192">tooimplement hello callback, do:</span></span>

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="d33dc-193">Hello wywołania zwrotnego można ustawić w Twojej `Application_Launching` metody z `App.xaml.cs` plików, najlepiej przed hello `EngagementReach.Instance.Init()` wywołania.</span><span class="sxs-lookup"><span data-stu-id="d33dc-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="d33dc-194">Każdy program obsługi jest wywoływana przez hello wątku interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33dc-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="d33dc-195">Nie masz tooworry, korzystając z MessageBox lub coś związanych z interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d33dc-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[zasady aplikacji]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[dodatkowe wymagania dotyczące typów określonej aplikacji]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

