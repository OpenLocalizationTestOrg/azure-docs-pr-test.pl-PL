---
title: "aaaTroubleshoot usługi Application Insights w projekcie sieci web Java"
description: "Przewodnik rozwiązywania problemów — monitorowania na żywo aplikacji Java za pomocą usługi Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="2af89-103">Rozwiązywanie problemów oraz pytania i odpowiedzi dotyczące usługi Application Insights dla języka Java</span><span class="sxs-lookup"><span data-stu-id="2af89-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="2af89-104">Pytania lub problemy z [Azure Application Insights w języku Java][java]?</span><span class="sxs-lookup"><span data-stu-id="2af89-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="2af89-105">Poniżej przedstawiono kilka wskazówek.</span><span class="sxs-lookup"><span data-stu-id="2af89-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="2af89-106">Błędy kompilacji</span><span class="sxs-lookup"><span data-stu-id="2af89-106">Build errors</span></span>
<span data-ttu-id="2af89-107">**W środowisku Eclipse podczas dodawania hello zestaw SDK usługi Application Insights za pośrednictwem Maven i Gradle, pojawia się błędy sprawdzania poprawności kompilacji lub sumy kontrolnej.**</span><span class="sxs-lookup"><span data-stu-id="2af89-107">**In Eclipse, when adding hello Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="2af89-108">Jeśli hello zależności <version> element jest używanie wzorca z symboli wieloznacznych (np. (Maven) `<version>[1.0,)</version>` lub (Gradle) `version:'1.0.+'`), spróbuj zamiast tego określić określonej wersji, takich jak `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="2af89-108">If hello dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="2af89-109">Zobacz hello [informacje o wersji](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) hello najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="2af89-109">See hello [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for hello latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="2af89-110">Brak danych</span><span class="sxs-lookup"><span data-stu-id="2af89-110">No data</span></span>
<span data-ttu-id="2af89-111">**I dodać usługi Application Insights i uruchomiono mojej aplikacji, ale nigdy nie przejrzane danych w portalu hello.**</span><span class="sxs-lookup"><span data-stu-id="2af89-111">**I added Application Insights successfully and ran my app, but I've never seen data in hello portal.**</span></span>

* <span data-ttu-id="2af89-112">Poczekaj kilka minut i kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="2af89-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="2af89-113">Wykresy Hello odświeżania się okresowo, ale można również odświeżyć ręcznie.</span><span class="sxs-lookup"><span data-stu-id="2af89-113">hello charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="2af89-114">Interwał odświeżania Hello zależy od zakresu czasu hello hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="2af89-114">hello refresh interval depends on hello time range of hello chart.</span></span>
* <span data-ttu-id="2af89-115">Sprawdź, czy klucz Instrumentacji zdefiniowane w pliku ApplicationInsights.xml hello (w folderze zasobów hello w projekcie)</span><span class="sxs-lookup"><span data-stu-id="2af89-115">Check that you have an instrumentation key defined in hello ApplicationInsights.xml file (in hello resources folder in your project)</span></span>
* <span data-ttu-id="2af89-116">Sprawdź, czy jest nie `<DisableTelemetry>true</DisableTelemetry>` węzła w pliku xml hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in hello xml file.</span></span>
* <span data-ttu-id="2af89-117">W zaporze konieczne może być tooopen porty TCP 80 i 443 dla toodc.services.visualstudio.com ruchu wychodzącego. Zobacz hello [pełnej listy wyjątków zapory](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="2af89-117">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com. See hello [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="2af89-118">Uruchom tablicy w hello Microsoft Azure, zobacz Mapowanie stanu usługi hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-118">In hello Microsoft Azure start board, look at hello service status map.</span></span> <span data-ttu-id="2af89-119">W przypadku niektórych alertów oznaczeń, poczekaj, aż one zwrócono tooOK, a następnie zamknij i otwórz ponownie z bloku aplikacji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2af89-119">If there are some alert indications, wait until they have returned tooOK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="2af89-120">Włącz rejestrowanie toohello okna konsoli IDE, dodając `<SDKLogger />` elementu w węźle głównym hello hello ApplicationInsights.xml pliku (w hello folder zasobów w projekcie) i sprawdź, czy wpisy poprzedzone znakiem [Błąd].</span><span class="sxs-lookup"><span data-stu-id="2af89-120">Turn on logging toohello IDE console window, by adding an `<SDKLogger />` element under hello root node in hello ApplicationInsights.xml file (in hello resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="2af89-121">Upewnij się, że poprawny plik ApplicationInsights.xml został pomyślnie załadowany przez hello zestawu Java SDK, analizując komunikaty wyjściowe hello konsoli dla instrukcji "pliku konfiguracyjnego pomyślnie znaleziono" hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-121">Make sure that hello correct ApplicationInsights.xml file has been successfully loaded by hello Java SDK, by looking at hello console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="2af89-122">Jeśli nie znaleziono pliku konfiguracji hello, sprawdź hello dane wyjściowe komunikaty toosee, gdzie hello pliku konfiguracji są wyszukiwane i upewnij się, że powitalne ApplicationInsights.xml znajduje się w jednej z tych lokalizacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="2af89-122">If hello config file is not found, check hello output messages toosee where hello config file is being searched for, and make sure that hello ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="2af89-123">Jako zasadą można umieścić plik konfiguracji hello niemal JARs hello Application Insights zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="2af89-123">As a rule of thumb, you can place hello config file near hello Application Insights SDK JARs.</span></span> <span data-ttu-id="2af89-124">Na przykład: w Tomcat, może oznaczać to hello folderu sieci WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="2af89-124">For example: in Tomcat, this would mean hello WEB-INF/lib folder.</span></span>

#### <a name="i-used-toosee-data-but-it-has-stopped"></a><span data-ttu-id="2af89-125">Użycie danych toosee, ale została zatrzymana</span><span class="sxs-lookup"><span data-stu-id="2af89-125">I used toosee data, but it has stopped</span></span>
* <span data-ttu-id="2af89-126">Sprawdź hello [blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="2af89-126">Check hello [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="2af89-127">Czy osiągnięto limitu przydziału miesięcznego punktów danych?</span><span class="sxs-lookup"><span data-stu-id="2af89-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="2af89-128">Otwórz ustawienia/przydziału i toofind cennik wychodzących. Jeśli tak, możesz uaktualnić swój plan lub zapłacić za dodatkowe pojemności.</span><span class="sxs-lookup"><span data-stu-id="2af89-128">Open Settings/Quota and Pricing toofind out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="2af89-129">Zobacz hello [cennik schemat](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="2af89-129">See hello [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-hello-data-im-expecting"></a><span data-ttu-id="2af89-130">Nie jest wyświetlane wszystkie dane hello używam I oczekiwana</span><span class="sxs-lookup"><span data-stu-id="2af89-130">I don't see all hello data I'm expecting</span></span>
* <span data-ttu-id="2af89-131">Otwórz hello przydziałów i cenach bloku i sprawdź, czy [próbkowania](app-insights-sampling.md) jest używany w operacji.</span><span class="sxs-lookup"><span data-stu-id="2af89-131">Open hello Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="2af89-132">(transmisji 100% oznacza, że próbkowania nie jest w operacji). Witaj usługa Application Insights może być zestaw tooaccept tylko część telemetrii hello, przychodzący z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2af89-132">(100% transmission means that sampling isn't in operation.) hello Application Insights service can be set tooaccept only a fraction of hello telemetry that arrives from your app.</span></span> <span data-ttu-id="2af89-133">Dzięki temu można przechowywać w wykorzystaniu całego przydziału miesięcznego dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="2af89-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="2af89-134">Dane użycia</span><span class="sxs-lookup"><span data-stu-id="2af89-134">No usage data</span></span>
<span data-ttu-id="2af89-135">**Dane dotyczące żądań i czasy odpowiedzi, ale nie widoku strony, przeglądarki lub dane użytkownika są widoczne.**</span><span class="sxs-lookup"><span data-stu-id="2af89-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="2af89-136">Pomyślnie ustawiono telemetrii toosend aplikacji z powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="2af89-136">You successfully set up your app toosend telemetry from hello server.</span></span> <span data-ttu-id="2af89-137">Po następnym krokiem jest zbyt[ustawione telemetrii toosend stron sieci web za pomocą przeglądarki sieci web hello][usage].</span><span class="sxs-lookup"><span data-stu-id="2af89-137">Now your next step is too[set up your web pages toosend telemetry from hello web browser][usage].</span></span>

<span data-ttu-id="2af89-138">Alternatywnie Jeśli klient jest aplikacją w [telefonu lub innego urządzenia][platforms], może wysłać dane telemetryczne z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="2af89-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="2af89-139">Użyj hello sam tooset klucza Instrumentacji w górę telemetrii klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="2af89-139">Use hello same instrumentation key tooset up both your client and server telemetry.</span></span> <span data-ttu-id="2af89-140">Witaj danych będą wyświetlane w hello tego samego zasobu usługi Application Insights i będziesz w stanie toocorrelate zdarzenia z klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="2af89-140">hello data will appear in hello same Application Insights resource, and you'll be able toocorrelate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="2af89-141">Wyłączanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="2af89-141">Disabling telemetry</span></span>
<span data-ttu-id="2af89-142">**Jak wyłączyć telemetrię kolekcji?**</span><span class="sxs-lookup"><span data-stu-id="2af89-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="2af89-143">W kodzie:</span><span class="sxs-lookup"><span data-stu-id="2af89-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="2af89-144">**Lub**</span><span class="sxs-lookup"><span data-stu-id="2af89-144">**Or**</span></span> 

<span data-ttu-id="2af89-145">Zaktualizuj ApplicationInsights.xml (w folderze zasobów hello w projekcie).</span><span class="sxs-lookup"><span data-stu-id="2af89-145">Update ApplicationInsights.xml (in hello resources folder in your project).</span></span> <span data-ttu-id="2af89-146">Dodaj następujące hello w węźle głównym hello:</span><span class="sxs-lookup"><span data-stu-id="2af89-146">Add hello following under hello root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="2af89-147">Aplikacja hello toorestart metodą XML hello mają po zmianie wartości hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-147">Using hello XML method, you have toorestart hello application when you change hello value.</span></span>

## <a name="changing-hello-target"></a><span data-ttu-id="2af89-148">Zmiana hello docelowego</span><span class="sxs-lookup"><span data-stu-id="2af89-148">Changing hello target</span></span>
<span data-ttu-id="2af89-149">**Jak zmienić projektu wysyła dane do zasobów platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="2af89-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="2af89-150">[Pobierz klucz Instrumentacji hello hello nowy zasób.][java]</span><span class="sxs-lookup"><span data-stu-id="2af89-150">[Get hello instrumentation key of hello new resource.][java]</span></span>
* <span data-ttu-id="2af89-151">Jeśli dodano usługę Application Insights tooyour projektu przy użyciu hello Azure zestawu narzędzi dla programu Eclipse kliknij prawym przyciskiem myszy projektu sieci web, wybierz **Azure**, **Konfiguruj usługę Application Insights**i zmienić wartość klucza hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-151">If you added Application Insights tooyour project using hello Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change hello key.</span></span>
* <span data-ttu-id="2af89-152">W przeciwnym razie zaktualizować klucza hello w ApplicationInsights.xml hello folderu zasobów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="2af89-152">Otherwise, update hello key in ApplicationInsights.xml in hello resources folder in your project.</span></span>

## <a name="debug-data-from-hello-sdk"></a><span data-ttu-id="2af89-153">Debugowanie danych z hello zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="2af89-153">Debug data from hello SDK</span></span>

<span data-ttu-id="2af89-154">**Jak można sprawdzić jakie hello wykonywanie operacji zestawu SDK?**</span><span class="sxs-lookup"><span data-stu-id="2af89-154">**How can I find out what hello SDK is doing?**</span></span>

<span data-ttu-id="2af89-155">Dodaj więcej informacji o tym, co się dzieje w hello interfejsu API, tooget `<SDKLogger/>` w węźle głównym hello pliku konfiguracyjnego ApplicationInsights.xml hello.</span><span class="sxs-lookup"><span data-stu-id="2af89-155">tooget more information about what's happening in hello API, add `<SDKLogger/>` under hello root node of hello ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="2af89-156">Można także skonfigurować hello rejestratora toooutput tooa pliku:</span><span class="sxs-lookup"><span data-stu-id="2af89-156">You can also instruct hello logger toooutput tooa file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="2af89-157">Witaj pliki znajdują się w obszarze `%temp%\javasdklogs` lub `java.io.tmpdir` w przypadku serwera Tomcat.</span><span class="sxs-lookup"><span data-stu-id="2af89-157">hello files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="hello-azure-start-screen"></a><span data-ttu-id="2af89-158">Witaj ekranu startowego Azure</span><span class="sxs-lookup"><span data-stu-id="2af89-158">hello Azure start screen</span></span>
<span data-ttu-id="2af89-159">**Wyświetlane [hello portalu Azure](https://portal.azure.com). Mapy hello Powiedz mi coś o mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="2af89-159">**I'm looking at [hello Azure portal](https://portal.azure.com). Does hello map tell me something about my app?**</span></span>

<span data-ttu-id="2af89-160">Nie, pokazuje kondycję hello Azure serwerów wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="2af89-160">No, it shows hello health of Azure servers around hello world.</span></span>

<span data-ttu-id="2af89-161">*Z tablicy hello Azure start (ekranu głównego) jak znaleźć dane o mojej aplikacji?*</span><span class="sxs-lookup"><span data-stu-id="2af89-161">*From hello Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="2af89-162">Wykonując [Konfigurowanie aplikacji dla usługi Application Insights][java], kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie wybierz zasób aplikacji hello utworzony dla twojej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2af89-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select hello app resource you created for your app.</span></span> <span data-ttu-id="2af89-163">tooget szybciej w przyszłości, można przypiąć tablicy start toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2af89-163">tooget there faster in future, you can pin your app toohello start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="2af89-164">Intranetowych serwerów</span><span class="sxs-lookup"><span data-stu-id="2af89-164">Intranet servers</span></span>
<span data-ttu-id="2af89-165">**W moim intranecie można monitorować serwer?**</span><span class="sxs-lookup"><span data-stu-id="2af89-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="2af89-166">Tak, pod warunkiem, serwer może wysyłać dane telemetryczne portalu Application Insights toohello za pośrednictwem hello publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="2af89-166">Yes, provided your server can send telemetry toohello Application Insights portal through hello public internet.</span></span> 

<span data-ttu-id="2af89-167">W zaporze konieczne może być tooopen porty TCP 80 i 443 dla toodc.services.visualstudio.com ruchu wychodzącego i f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="2af89-167">In your firewall, you might have tooopen TCP ports 80 and 443 for outgoing traffic toodc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="2af89-168">Przechowywanie danych</span><span class="sxs-lookup"><span data-stu-id="2af89-168">Data retention</span></span>
<span data-ttu-id="2af89-169">**Jak długo dane są przechowywane w portalu hello? Czy jest bezpieczna?**</span><span class="sxs-lookup"><span data-stu-id="2af89-169">**How long is data retained in hello portal? Is it secure?**</span></span>

<span data-ttu-id="2af89-170">Zobacz [przechowywanie danych i ochrona prywatności][data].</span><span class="sxs-lookup"><span data-stu-id="2af89-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="2af89-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2af89-171">Next steps</span></span>
<span data-ttu-id="2af89-172">**Skonfigurować usługi Application Insights dla aplikacja Mój serwer Java. Co można zrobić?**</span><span class="sxs-lookup"><span data-stu-id="2af89-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="2af89-173">[Monitorowanie dostępności stron sieci web][availability]</span><span class="sxs-lookup"><span data-stu-id="2af89-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="2af89-174">[Monitorowanie użycia strony sieci web][usage]</span><span class="sxs-lookup"><span data-stu-id="2af89-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="2af89-175">[Śledzenie użycia i diagnozowanie problemów w aplikacji dla urządzeń][platforms]</span><span class="sxs-lookup"><span data-stu-id="2af89-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="2af89-176">[Pisanie kodu tootrack użycia aplikacji][track]</span><span class="sxs-lookup"><span data-stu-id="2af89-176">[Write code tootrack usage of your app][track]</span></span>
* <span data-ttu-id="2af89-177">[Przechwyć dzienników diagnostycznych][javalogs]</span><span class="sxs-lookup"><span data-stu-id="2af89-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="2af89-178">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="2af89-178">Get help</span></span>
* [<span data-ttu-id="2af89-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="2af89-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

