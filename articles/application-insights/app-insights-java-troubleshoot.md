---
title: "Rozwiązywanie problemów z usługi Application Insights w projekcie sieci web Java"
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
ms.openlocfilehash: ce46a4f561a273dc340b090a5bf0c8932a308722
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a><span data-ttu-id="b4685-103">Rozwiązywanie problemów oraz pytania i odpowiedzi dotyczące usługi Application Insights dla języka Java</span><span class="sxs-lookup"><span data-stu-id="b4685-103">Troubleshooting and Q and A for Application Insights for Java</span></span>
<span data-ttu-id="b4685-104">Pytania lub problemy z [Azure Application Insights w języku Java][java]?</span><span class="sxs-lookup"><span data-stu-id="b4685-104">Questions or problems with [Azure Application Insights in Java][java]?</span></span> <span data-ttu-id="b4685-105">Poniżej przedstawiono kilka wskazówek.</span><span class="sxs-lookup"><span data-stu-id="b4685-105">Here are some tips.</span></span>

## <a name="build-errors"></a><span data-ttu-id="b4685-106">Błędy kompilacji</span><span class="sxs-lookup"><span data-stu-id="b4685-106">Build errors</span></span>
<span data-ttu-id="b4685-107">**W środowisku Eclipse, dodając zestaw SDK usługi Application Insights za pośrednictwem Maven i Gradle pojawiają się błędy weryfikacji kompilacji lub sumy kontrolnej.**</span><span class="sxs-lookup"><span data-stu-id="b4685-107">**In Eclipse, when adding the Application Insights SDK via Maven or Gradle, I get build or checksum validation errors.**</span></span>

* <span data-ttu-id="b4685-108">Jeśli zależność <version> element jest używanie wzorca z symboli wieloznacznych (np. (Maven) `<version>[1.0,)</version>` lub (Gradle) `version:'1.0.+'`), spróbuj zamiast tego określić określonej wersji, takich jak `1.0.2`.</span><span class="sxs-lookup"><span data-stu-id="b4685-108">If the dependency <version> element is using a pattern with wildcard characters (e.g. (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), try specifying a specific version instead like `1.0.2`.</span></span> <span data-ttu-id="b4685-109">Zobacz [informacje o wersji](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="b4685-109">See the [release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) for the latest version.</span></span>

## <a name="no-data"></a><span data-ttu-id="b4685-110">Brak danych</span><span class="sxs-lookup"><span data-stu-id="b4685-110">No data</span></span>
<span data-ttu-id="b4685-111">**I dodać usługi Application Insights i uruchomiono mojej aplikacji, ale nigdy nie przejrzane danych w portalu.**</span><span class="sxs-lookup"><span data-stu-id="b4685-111">**I added Application Insights successfully and ran my app, but I've never seen data in the portal.**</span></span>

* <span data-ttu-id="b4685-112">Poczekaj kilka minut i kliknij przycisk Odśwież.</span><span class="sxs-lookup"><span data-stu-id="b4685-112">Wait a minute and click Refresh.</span></span> <span data-ttu-id="b4685-113">Wykresy odświeżania się okresowo, ale można również odświeżyć ręcznie.</span><span class="sxs-lookup"><span data-stu-id="b4685-113">The charts refresh themselves periodically, but you can also refresh manually.</span></span> <span data-ttu-id="b4685-114">Interwał odświeżania zależy od zakresu czasu wykresu.</span><span class="sxs-lookup"><span data-stu-id="b4685-114">The refresh interval depends on the time range of the chart.</span></span>
* <span data-ttu-id="b4685-115">Sprawdź, czy klucz Instrumentacji zdefiniowane w pliku ApplicationInsights.xml (w folderze zasobów w projekcie)</span><span class="sxs-lookup"><span data-stu-id="b4685-115">Check that you have an instrumentation key defined in the ApplicationInsights.xml file (in the resources folder in your project)</span></span>
* <span data-ttu-id="b4685-116">Sprawdź, czy jest nie `<DisableTelemetry>true</DisableTelemetry>` węzła w pliku xml.</span><span class="sxs-lookup"><span data-stu-id="b4685-116">Verify that there is no `<DisableTelemetry>true</DisableTelemetry>` node in the xml file.</span></span>
* <span data-ttu-id="b4685-117">W zaporze może być konieczne otwarcie portów TCP 80 i 443 dla ruchu wychodzącego dc.services.visualstudio.com. Zobacz [pełnej listy wyjątków zapory](app-insights-ip-addresses.md)</span><span class="sxs-lookup"><span data-stu-id="b4685-117">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com. See the [full list of firewall exceptions](app-insights-ip-addresses.md)</span></span>
* <span data-ttu-id="b4685-118">Uruchom tablicy w Microsoft Azure, zobacz Mapowanie stanu usługi.</span><span class="sxs-lookup"><span data-stu-id="b4685-118">In the Microsoft Azure start board, look at the service status map.</span></span> <span data-ttu-id="b4685-119">W przypadku niektórych alertów oznaczeń, poczekaj, aż one zwrócono do OK, a następnie zamknij i otwórz ponownie z bloku aplikacji usługi Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b4685-119">If there are some alert indications, wait until they have returned to OK and then close and re-open your Application Insights application blade.</span></span>
* <span data-ttu-id="b4685-120">Włącz rejestrowanie w oknie konsoli IDE, dodając `<SDKLogger />` elementu w obszarze węzła głównego w pliku ApplicationInsights.xml (w folderze zasobów w projekcie) i sprawdź, czy wpisy poprzedzone znakiem [Błąd].</span><span class="sxs-lookup"><span data-stu-id="b4685-120">Turn on logging to the IDE console window, by adding an `<SDKLogger />` element under the root node in the ApplicationInsights.xml file (in the resources folder in your project), and check for entries prefaced with [Error].</span></span>
* <span data-ttu-id="b4685-121">Upewnij się, że właściwy plik ApplicationInsights.xml został pomyślnie załadowany przez zestawu Java SDK analizując komunikaty wyjściowe konsoli dla instrukcji "pliku konfiguracyjnego pomyślnie znaleziono".</span><span class="sxs-lookup"><span data-stu-id="b4685-121">Make sure that the correct ApplicationInsights.xml file has been successfully loaded by the Java SDK, by looking at the console's output messages for a "Configuration file has been successfully found" statement.</span></span>
* <span data-ttu-id="b4685-122">Jeśli nie znaleziono pliku konfiguracji, sprawdź komunikaty, aby zobaczyć, których pliku konfiguracji są wyszukiwane i upewnij się, że ApplicationInsights.xml znajduje się w jednej z tych lokalizacji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="b4685-122">If the config file is not found, check the output messages to see where the config file is being searched for, and make sure that the ApplicationInsights.xml is located in one of those search locations.</span></span> <span data-ttu-id="b4685-123">Jako zasadą można umieścić w pliku config niemal Application Insights SDK JARs.</span><span class="sxs-lookup"><span data-stu-id="b4685-123">As a rule of thumb, you can place the config file near the Application Insights SDK JARs.</span></span> <span data-ttu-id="b4685-124">Na przykład: w Tomcat, oznacza to, czy folder w sieci WEB-INF/lib.</span><span class="sxs-lookup"><span data-stu-id="b4685-124">For example: in Tomcat, this would mean the WEB-INF/lib folder.</span></span>

#### <a name="i-used-to-see-data-but-it-has-stopped"></a><span data-ttu-id="b4685-125">Używany do wyświetlania danych, ale została zatrzymana</span><span class="sxs-lookup"><span data-stu-id="b4685-125">I used to see data, but it has stopped</span></span>
* <span data-ttu-id="b4685-126">Sprawdź [blogu stan](http://blogs.msdn.com/b/applicationinsights-status/).</span><span class="sxs-lookup"><span data-stu-id="b4685-126">Check the [status blog](http://blogs.msdn.com/b/applicationinsights-status/).</span></span>
* <span data-ttu-id="b4685-127">Czy osiągnięto limitu przydziału miesięcznego punktów danych?</span><span class="sxs-lookup"><span data-stu-id="b4685-127">Have you hit your monthly quota of data points?</span></span> <span data-ttu-id="b4685-128">Otwórz ustawienia/przydziału i cennik, aby dowiedzieć się. Jeśli tak, możesz uaktualnić swój plan lub zapłacić za dodatkowe pojemności.</span><span class="sxs-lookup"><span data-stu-id="b4685-128">Open Settings/Quota and Pricing to find out. If so, you can upgrade your plan, or pay for additional capacity.</span></span> <span data-ttu-id="b4685-129">Zobacz [cennik schemat](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="b4685-129">See the [pricing scheme](https://azure.microsoft.com/pricing/details/application-insights/).</span></span>

#### <a name="i-dont-see-all-the-data-im-expecting"></a><span data-ttu-id="b4685-130">Nie widzę wszystkich danych I czy oczekiwana</span><span class="sxs-lookup"><span data-stu-id="b4685-130">I don't see all the data I'm expecting</span></span>
* <span data-ttu-id="b4685-131">Otwórz przydziały i cenach bloku i sprawdź, czy [próbkowania](app-insights-sampling.md) jest używany w operacji.</span><span class="sxs-lookup"><span data-stu-id="b4685-131">Open the Quotas and Pricing blade and check whether [sampling](app-insights-sampling.md) is in operation.</span></span> <span data-ttu-id="b4685-132">(transmisji 100% oznacza, że próbkowania nie jest w operacji). Usługa Application Insights można ustawić do akceptowania tylko część danych telemetrii, przychodzący z aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4685-132">(100% transmission means that sampling isn't in operation.) The Application Insights service can be set to accept only a fraction of the telemetry that arrives from your app.</span></span> <span data-ttu-id="b4685-133">Dzięki temu można przechowywać w wykorzystaniu całego przydziału miesięcznego dane telemetryczne.</span><span class="sxs-lookup"><span data-stu-id="b4685-133">This helps you keep within your monthly quota of telemetry.</span></span> 

## <a name="no-usage-data"></a><span data-ttu-id="b4685-134">Dane użycia</span><span class="sxs-lookup"><span data-stu-id="b4685-134">No usage data</span></span>
<span data-ttu-id="b4685-135">**Dane dotyczące żądań i czasy odpowiedzi, ale nie widoku strony, przeglądarki lub dane użytkownika są widoczne.**</span><span class="sxs-lookup"><span data-stu-id="b4685-135">**I see data about requests and response times, but no page view, browser, or user data.**</span></span>

<span data-ttu-id="b4685-136">Pomyślnie tak skonfigurować aplikację, aby wysłać dane telemetryczne z serwera.</span><span class="sxs-lookup"><span data-stu-id="b4685-136">You successfully set up your app to send telemetry from the server.</span></span> <span data-ttu-id="b4685-137">Teraz z następnym krokiem jest [ustawić stron sieci web, aby wysłać dane telemetryczne z przeglądarki sieci web][usage].</span><span class="sxs-lookup"><span data-stu-id="b4685-137">Now your next step is to [set up your web pages to send telemetry from the web browser][usage].</span></span>

<span data-ttu-id="b4685-138">Alternatywnie Jeśli klient jest aplikacją w [telefonu lub innego urządzenia][platforms], może wysłać dane telemetryczne z tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="b4685-138">Alternatively, if your client is an app in a [phone or other device][platforms], you can send telemetry from there.</span></span> 

<span data-ttu-id="b4685-139">Aby skonfigurować dane telemetryczne klienta i serwera, należy używać tego samego klucza instrumentacji.</span><span class="sxs-lookup"><span data-stu-id="b4685-139">Use the same instrumentation key to set up both your client and server telemetry.</span></span> <span data-ttu-id="b4685-140">Dane będą wyświetlane w tym samym zasobu usługi Application Insights i będzie możliwe do korelowanie zdarzeń z klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="b4685-140">The data will appear in the same Application Insights resource, and you'll be able to correlate events from client and server.</span></span>


## <a name="disabling-telemetry"></a><span data-ttu-id="b4685-141">Wyłączanie telemetrii</span><span class="sxs-lookup"><span data-stu-id="b4685-141">Disabling telemetry</span></span>
<span data-ttu-id="b4685-142">**Jak wyłączyć telemetrię kolekcji?**</span><span class="sxs-lookup"><span data-stu-id="b4685-142">**How can I disable telemetry collection?**</span></span>

<span data-ttu-id="b4685-143">W kodzie:</span><span class="sxs-lookup"><span data-stu-id="b4685-143">In code:</span></span>

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

<span data-ttu-id="b4685-144">**Lub**</span><span class="sxs-lookup"><span data-stu-id="b4685-144">**Or**</span></span> 

<span data-ttu-id="b4685-145">Zaktualizuj ApplicationInsights.xml (w folderze zasobów w projekcie).</span><span class="sxs-lookup"><span data-stu-id="b4685-145">Update ApplicationInsights.xml (in the resources folder in your project).</span></span> <span data-ttu-id="b4685-146">Dodaj następujący kod w węźle głównym:</span><span class="sxs-lookup"><span data-stu-id="b4685-146">Add the following under the root node:</span></span>

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

<span data-ttu-id="b4685-147">Przy użyciu metody XML, należy ponownie uruchomić aplikację po zmianie wartości.</span><span class="sxs-lookup"><span data-stu-id="b4685-147">Using the XML method, you have to restart the application when you change the value.</span></span>

## <a name="changing-the-target"></a><span data-ttu-id="b4685-148">Zmiana obiektu docelowego</span><span class="sxs-lookup"><span data-stu-id="b4685-148">Changing the target</span></span>
<span data-ttu-id="b4685-149">**Jak zmienić projektu wysyła dane do zasobów platformy Azure?**</span><span class="sxs-lookup"><span data-stu-id="b4685-149">**How can I change which Azure resource my project sends data to?**</span></span>

* <span data-ttu-id="b4685-150">[Pobierz klucz Instrumentacji nowego zasobu.][java]</span><span class="sxs-lookup"><span data-stu-id="b4685-150">[Get the instrumentation key of the new resource.][java]</span></span>
* <span data-ttu-id="b4685-151">Jeśli dodano usługę Application Insights do projektu przy użyciu zestawu narzędzi platformy Azure dla programu Eclipse, kliknij prawym przyciskiem myszy projektu sieci web, wybierz **Azure**, **Konfiguruj usługę Application Insights**i zmienić wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="b4685-151">If you added Application Insights to your project using the Azure Toolkit for Eclipse, right click your web project, select **Azure**, **Configure Application Insights**, and change the key.</span></span>
* <span data-ttu-id="b4685-152">W przeciwnym razie zaktualizować klucza w ApplicationInsights.xml w folderze zasobów w projekcie.</span><span class="sxs-lookup"><span data-stu-id="b4685-152">Otherwise, update the key in ApplicationInsights.xml in the resources folder in your project.</span></span>

## <a name="debug-data-from-the-sdk"></a><span data-ttu-id="b4685-153">Debugowanie danych z zestawu SDK</span><span class="sxs-lookup"><span data-stu-id="b4685-153">Debug data from the SDK</span></span>

<span data-ttu-id="b4685-154">**Jak można sprawdzić czynności zestawu SDK?**</span><span class="sxs-lookup"><span data-stu-id="b4685-154">**How can I find out what the SDK is doing?**</span></span>

<span data-ttu-id="b4685-155">Aby uzyskać więcej informacji o tym, co się dzieje w interfejsie API, Dodaj `<SDKLogger/>` w węźle głównym ApplicationInsights.xml pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b4685-155">To get more information about what's happening in the API, add `<SDKLogger/>` under the root node of the ApplicationInsights.xml configuration file.</span></span>

<span data-ttu-id="b4685-156">Można także skonfigurować rejestratora do wypełniania wyjściowego pliku:</span><span class="sxs-lookup"><span data-stu-id="b4685-156">You can also instruct the logger to output to a file:</span></span>

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

<span data-ttu-id="b4685-157">Pliki można znaleźć w `%temp%\javasdklogs` lub `java.io.tmpdir` w przypadku serwera Tomcat.</span><span class="sxs-lookup"><span data-stu-id="b4685-157">The files can be found under `%temp%\javasdklogs` or `java.io.tmpdir` in case of Tomcat server.</span></span>


## <a name="the-azure-start-screen"></a><span data-ttu-id="b4685-158">Ekranu startowego Azure</span><span class="sxs-lookup"><span data-stu-id="b4685-158">The Azure start screen</span></span>
<span data-ttu-id="b4685-159">**Wyświetlane [portalu Azure](https://portal.azure.com). Mapy Powiedz mi coś o mojej aplikacji?**</span><span class="sxs-lookup"><span data-stu-id="b4685-159">**I'm looking at [the Azure portal](https://portal.azure.com). Does the map tell me something about my app?**</span></span>

<span data-ttu-id="b4685-160">Nie, przedstawia prawidłowość serwerów platformy Azure na świecie.</span><span class="sxs-lookup"><span data-stu-id="b4685-160">No, it shows the health of Azure servers around the world.</span></span>

<span data-ttu-id="b4685-161">*Z tablicy Azure start (ekranu głównego) jak znaleźć dane o mojej aplikacji?*</span><span class="sxs-lookup"><span data-stu-id="b4685-161">*From the Azure start board (home screen), how do I find data about my app?*</span></span>

<span data-ttu-id="b4685-162">Wykonując [Konfigurowanie aplikacji dla usługi Application Insights][java], kliknij przycisk Przeglądaj, wybierz usługę Application Insights, a następnie wybierz zasób aplikacji utworzone dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4685-162">Assuming you [set up your app for Application Insights][java], click Browse, select Application Insights, and select the app resource you created for your app.</span></span> <span data-ttu-id="b4685-163">Aby uzyskać szybciej w przyszłości, można przypiąć swoją aplikację w celu rozpoczęcia tablicy.</span><span class="sxs-lookup"><span data-stu-id="b4685-163">To get there faster in future, you can pin your app to the start board.</span></span>

## <a name="intranet-servers"></a><span data-ttu-id="b4685-164">Intranetowych serwerów</span><span class="sxs-lookup"><span data-stu-id="b4685-164">Intranet servers</span></span>
<span data-ttu-id="b4685-165">**W moim intranecie można monitorować serwer?**</span><span class="sxs-lookup"><span data-stu-id="b4685-165">**Can I monitor a server on my intranet?**</span></span>

<span data-ttu-id="b4685-166">Tak, pod warunkiem, że serwer może wysłać dane telemetryczne do portalu usługi Application Insights za pośrednictwem publicznej sieci internet.</span><span class="sxs-lookup"><span data-stu-id="b4685-166">Yes, provided your server can send telemetry to the Application Insights portal through the public internet.</span></span> 

<span data-ttu-id="b4685-167">W zaporze może być konieczne otwarcie portów TCP 80 i 443 dla ruchu wychodzącego dc.services.visualstudio.com i f5.services.visualstudio.com.</span><span class="sxs-lookup"><span data-stu-id="b4685-167">In your firewall, you might have to open TCP ports 80 and 443 for outgoing traffic to dc.services.visualstudio.com and f5.services.visualstudio.com.</span></span>

## <a name="data-retention"></a><span data-ttu-id="b4685-168">Przechowywanie danych</span><span class="sxs-lookup"><span data-stu-id="b4685-168">Data retention</span></span>
<span data-ttu-id="b4685-169">**Jak długo dane są przechowywane w portalu Czy jest bezpieczna?**</span><span class="sxs-lookup"><span data-stu-id="b4685-169">**How long is data retained in the portal? Is it secure?**</span></span>

<span data-ttu-id="b4685-170">Zobacz [przechowywanie danych i ochrona prywatności][data].</span><span class="sxs-lookup"><span data-stu-id="b4685-170">See [Data retention and privacy][data].</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4685-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4685-171">Next steps</span></span>
<span data-ttu-id="b4685-172">**Skonfigurować usługi Application Insights dla aplikacja Mój serwer Java. Co można zrobić?**</span><span class="sxs-lookup"><span data-stu-id="b4685-172">**I set up Application Insights for my Java server app. What else can I do?**</span></span>

* <span data-ttu-id="b4685-173">[Monitorowanie dostępności stron sieci web][availability]</span><span class="sxs-lookup"><span data-stu-id="b4685-173">[Monitor availability of your web pages][availability]</span></span>
* <span data-ttu-id="b4685-174">[Monitorowanie użycia strony sieci web][usage]</span><span class="sxs-lookup"><span data-stu-id="b4685-174">[Monitor web page usage][usage]</span></span>
* <span data-ttu-id="b4685-175">[Śledzenie użycia i diagnozowanie problemów w aplikacji dla urządzeń][platforms]</span><span class="sxs-lookup"><span data-stu-id="b4685-175">[Track usage and diagnose issues in your device apps][platforms]</span></span>
* <span data-ttu-id="b4685-176">[Napisz kod umożliwiający śledzenie użycia aplikacji][track]</span><span class="sxs-lookup"><span data-stu-id="b4685-176">[Write code to track usage of your app][track]</span></span>
* <span data-ttu-id="b4685-177">[Przechwyć dzienników diagnostycznych][javalogs]</span><span class="sxs-lookup"><span data-stu-id="b4685-177">[Capture diagnostic logs][javalogs]</span></span>

## <a name="get-help"></a><span data-ttu-id="b4685-178">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="b4685-178">Get help</span></span>
* [<span data-ttu-id="b4685-179">Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="b4685-179">Stack Overflow</span></span>](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

