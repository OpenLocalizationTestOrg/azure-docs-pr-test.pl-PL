---
title: "aaaConfigure aplikacji sieci web w usłudze aplikacji Azure"
description: "Jak tooconfigure aplikacji sieci web w usłudze Azure App Services"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="4aa0d-103">Konfigurowanie aplikacji sieci Web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4aa0d-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="4aa0d-104">W tym temacie wyjaśniono, jak hello tooconfigure aplikacji sieci web przy użyciu [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="4aa0d-105">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="4aa0d-105">Application settings</span></span>
1. <span data-ttu-id="4aa0d-106">W hello [Azure Portal], otwórz blok powitania dla aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="4aa0d-107">Kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="4aa0d-108">Kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-108">Click **Application Settings**.</span></span>

![Ustawienia aplikacji][configure01]

<span data-ttu-id="4aa0d-110">Witaj **ustawienia aplikacji** bloku ma ustawienia pogrupowane w różne kategorie.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="4aa0d-111">Ustawienia ogólne</span><span class="sxs-lookup"><span data-stu-id="4aa0d-111">General settings</span></span>
<span data-ttu-id="4aa0d-112">**Framework w wersji**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-112">**Framework versions**.</span></span> <span data-ttu-id="4aa0d-113">Ustaw tych opcji, jeśli aplikacja używa tych platform:</span><span class="sxs-lookup"><span data-stu-id="4aa0d-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="4aa0d-114">**.NET framework**: hello zestawu .NET framework w wersji.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="4aa0d-115">**PHP**: Ustaw wersję PHP hello, lub **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="4aa0d-116">**Java**: hello wybierz wersję Java lub **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="4aa0d-117">Hello użyj **kontener sieci Web** toochoose opcji między Tomcat i Jetty wersji.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="4aa0d-118">**Python**: Wybierz hello wersji języka Python, lub **OFF** toodisable języka Python.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="4aa0d-119">Przyczyn technicznych Java, włączanie aplikacji wyłącza hello opcje .NET, PHP i Python.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="4aa0d-120"><a name="platform"></a>
**Platforma**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="4aa0d-121">Wybiera, czy aplikacja sieci web jest uruchamiana w środowisku 32-bitowy lub 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="4aa0d-122">Witaj 64-bitowego środowiska wymaga trybu Basic lub Standard.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="4aa0d-123">Zwolnij i tryby udostępnione są zawsze uruchamiane w środowisku 32-bitowym.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="4aa0d-124">**Sieci Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-124">**Web Sockets**.</span></span> <span data-ttu-id="4aa0d-125">Ustaw **ON** tooenable hello protokół WebSocket; na przykład, jeśli aplikacja sieci web używa [ASP.NET SignalR] lub [użyciu biblioteki socket.io].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="4aa0d-126"><a name="alwayson"></a>
**Zawsze włączone**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="4aa0d-127">Domyślnie aplikacje sieci web są usuwane, jeśli są one bezczynności przez niektóre czas.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="4aa0d-128">Dzięki temu system hello zaoszczędzenia zasobów.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="4aa0d-129">W trybie Basic lub Standard, aby umożliwić **zawsze na** aplikacji hello tookeep załadować cały czas hello.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="4aa0d-130">Jeśli aplikacja będzie działać ciągłe zadania Webjob lub uruchamia zadania Webjob wyzwolone przy użyciu wyrażenia CRON, należy włączyć **zawsze na**, lub hello zadania sieci web mogą nie działać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="4aa0d-131">**Zarządzane wersji potoku**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="4aa0d-132">Ustawia hello IIS [tryb potokowy].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="4aa0d-133">Pozostaw ustawić tooIntegrated (domyślnie: hello), chyba że masz starszej wersji aplikacji, która wymaga starszej wersji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="4aa0d-134">**Automatycznie wymiany**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-134">**Auto Swap**.</span></span> <span data-ttu-id="4aa0d-135">Po włączeniu automatycznej wymiany dla miejsca wdrożenia usługi App Service automatycznie wymiany hello aplikacji sieci web w środowisku produkcyjnym po naciśnięciu gnieździe toothat aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="4aa0d-136">Aby uzyskać więcej informacji, zobacz [wdrażanie toostaging miejsc aplikacji sieci web w usłudze Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4aa0d-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="4aa0d-137">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="4aa0d-137">Debugging</span></span>
<span data-ttu-id="4aa0d-138">**Debugowanie zdalne**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-138">**Remote Debugging**.</span></span> <span data-ttu-id="4aa0d-139">Umożliwia zdalne debugowanie.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-139">Enables remote debugging.</span></span> <span data-ttu-id="4aa0d-140">Po włączeniu umożliwia hello zdalnego debugera w Visual Studio tooconnect bezpośrednio aplikacji sieci web tooyour.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="4aa0d-141">Debugowanie zdalne pozostanie włączony 48 godzin.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="4aa0d-142">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="4aa0d-142">App settings</span></span>
<span data-ttu-id="4aa0d-143">Ta sekcja zawiera pary nazwa/wartość, które sieci web aplikacji zostanie załadowany po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="4aa0d-144">W przypadku aplikacji .NET, te ustawienia są wstrzykiwane do konfiguracji .NET `AppSettings` w czasie wykonywania, zastępowanie istniejących ustawień.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="4aa0d-145">Aplikacje PHP, Python, Java i węzła mają dostęp do tych ustawień jako zmienne środowiskowe w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="4aa0d-146">Dla każdego ustawienia aplikacji są tworzone dwie zmienne środowiskowe; jeden z nazwą hello określoną przez wpis ustawienie aplikacji hello, a druga z prefiksem APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="4aa0d-147">Zawierają hello tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="4aa0d-148">Parametry połączeń</span><span class="sxs-lookup"><span data-stu-id="4aa0d-148">Connection strings</span></span>
<span data-ttu-id="4aa0d-149">Parametry połączenia dla połączonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="4aa0d-150">W przypadku aplikacji .NET, te parametry połączenia są wstrzykiwane do konfiguracji .NET `connectionStrings` ustawienia w czasie wykonywania, zastępowanie istniejących wpisów, gdzie jest klucz hello hello nazwy połączonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="4aa0d-151">W przypadku aplikacji PHP, Python, Java i węzła te ustawienia będą dostępne jako zmienne środowiskowe w czasie wykonywania, prefiksem hello typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="4aa0d-152">prefiksy zmiennej środowiskowej Hello są następujące:</span><span class="sxs-lookup"><span data-stu-id="4aa0d-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="4aa0d-153">Program SQL Server:`SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4aa0d-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="4aa0d-154">MySQL:`MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4aa0d-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="4aa0d-155">Baza danych SQL:`SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4aa0d-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="4aa0d-156">Niestandardowe:`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4aa0d-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="4aa0d-157">Na przykład, jeśli parametry połączenia MySql nazwany `connectionstring1`, czy dostęp do niej za pomocą zmiennej środowiskowej hello `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="4aa0d-158">Dokumenty domyślne</span><span class="sxs-lookup"><span data-stu-id="4aa0d-158">Default documents</span></span>
<span data-ttu-id="4aa0d-159">dokument domyślny Hello to strona sieci web hello jest wyświetlany na powitania głównego adresu URL witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="4aa0d-160">Witaj pierwszy zgodnego pliku na liście hello jest używany.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="4aa0d-161">Aplikacje sieci Web może używać modułów, że trasy na podstawie adresu URL, a nie obsługujących zawartość statyczną, w którym to przypadku nie jest dokument domyślny, w związku.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="4aa0d-162">Mapowania programu obsługi</span><span class="sxs-lookup"><span data-stu-id="4aa0d-162">Handler mappings</span></span>
<span data-ttu-id="4aa0d-163">Użyj tego obszaru tooadd skryptu niestandardowego procesory toohandle żądania dla określonych rozszerzeń plików.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="4aa0d-164">**Rozszerzenie**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-164">**Extension**.</span></span> <span data-ttu-id="4aa0d-165">toobe rozszerzenie pliku Hello obsłużone, takich jak *.php lub handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="4aa0d-166">**Ścieżka do procesora skryptów**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-166">**Script Processor Path**.</span></span> <span data-ttu-id="4aa0d-167">Ścieżka bezwzględna Hello hello procesora skryptów.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="4aa0d-168">Toofiles żądania, odpowiadających hello rozszerzenie zostanie przetworzony przez hello procesora skryptów.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="4aa0d-169">Użyj ścieżki hello `D:\home\site\wwwroot` katalog główny aplikacji tooyour toorefer.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="4aa0d-170">**Dodatkowe argumenty**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-170">**Additional Arguments**.</span></span> <span data-ttu-id="4aa0d-171">Opcjonalne argumenty wiersza polecenia do procesora skryptów hello</span><span class="sxs-lookup"><span data-stu-id="4aa0d-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="4aa0d-172">Wirtualne aplikacje i katalogi</span><span class="sxs-lookup"><span data-stu-id="4aa0d-172">Virtual applications and directories</span></span>
<span data-ttu-id="4aa0d-173">aplikacje wirtualne tooconfigure i katalogi, określ poszczególne katalogi wirtualne i odpowiednie głównym witryny sieci Web toohello względną ścieżkę fizyczną.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="4aa0d-174">Opcjonalnie można wybrać hello **aplikacji** toomark wyboru katalogu wirtualnego jako aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="4aa0d-175">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="4aa0d-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="4aa0d-176">dzienniki diagnostyczne tooenable:</span><span class="sxs-lookup"><span data-stu-id="4aa0d-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="4aa0d-177">W bloku hello aplikacji sieci web, kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="4aa0d-178">Kliknij przycisk **dzienniki diagnostyczne**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="4aa0d-179">Opcje zapisywania dzienników diagnostycznych z aplikacji sieci web, która obsługuje rejestrowanie:</span><span class="sxs-lookup"><span data-stu-id="4aa0d-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="4aa0d-180">**Rejestrowanie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-180">**Application Logging**.</span></span> <span data-ttu-id="4aa0d-181">Zapisuje Dzienniki aplikacji toohello systemu plików.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="4aa0d-182">Rejestrowanie okresu w okresie 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="4aa0d-183">**Poziom**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-183">**Level**.</span></span> <span data-ttu-id="4aa0d-184">Po włączeniu rejestrowania aplikacji, ta opcja określa hello ilość informacji, która zostanie zarejestrowane (błąd, ostrzeżenie, informacje lub pełne).</span><span class="sxs-lookup"><span data-stu-id="4aa0d-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="4aa0d-185">**Rejestrowanie pracy serwera sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-185">**Web server logging**.</span></span> <span data-ttu-id="4aa0d-186">Dzienniki są zapisywane w hello rozszerzonym formacie W3C dziennika pliku.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="4aa0d-187">**Szczegółowe komunikaty o błędach**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-187">**Detailed error messages**.</span></span> <span data-ttu-id="4aa0d-188">Zapisuje szczegółowe informacje o błędzie komunikatów pliki htm.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="4aa0d-189">Witaj pliki są zapisywane w obszarze /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="4aa0d-190">**Śledzenie nieudanych żądań**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-190">**Failed request tracing**.</span></span> <span data-ttu-id="4aa0d-191">Żądania tooXML pliki dzienników, nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="4aa0d-192">Witaj pliki są zapisywane w obszarze/LogFiles/W3SVC*xxx*, gdzie xxx jest unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="4aa0d-193">Ten folder zawiera plik XSL i co najmniej jeden plik XML.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="4aa0d-194">Czy toodownload hello pliku XSL, należy wprowadzić, ponieważ zawiera funkcję, formatowanie i filtrowania hello zawartość plików XML hello.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="4aa0d-195">pliki dziennika hello tooview, należy utworzyć poświadczenia FTP w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4aa0d-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="4aa0d-196">W bloku hello aplikacji sieci web, kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="4aa0d-197">Kliknij przycisk **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="4aa0d-198">Wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="4aa0d-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-199">Click **Save**.</span></span>

![Konfigurowanie poświadczeń wdrożenia][configure03]

<span data-ttu-id="4aa0d-201">Pełna nazwa użytkownika FTP Hello jest "app\username" gdzie *aplikacji* jest nazwą hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="4aa0d-202">Witaj nazwy użytkownika znajduje się w bloku aplikacja sieci web hello, w obszarze **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Poświadczenia wdrożenia FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="4aa0d-204">Inne zadania konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4aa0d-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="4aa0d-205">PROTOKÓŁ SSL</span><span class="sxs-lookup"><span data-stu-id="4aa0d-205">SSL</span></span>
<span data-ttu-id="4aa0d-206">W trybie Basic lub Standard możesz przekazać certyfikatów SSL dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="4aa0d-207">Aby uzyskać więcej informacji zobacz [Włącz protokół HTTPS dla aplikacji sieci web].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="4aa0d-208">tooview przekazane certyfikaty, kliknij przycisk **wszystkie ustawienia** > **domen niestandardowych i SSL**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="4aa0d-209">Nazwy domen</span><span class="sxs-lookup"><span data-stu-id="4aa0d-209">Domain names</span></span>
<span data-ttu-id="4aa0d-210">Dodawanie niestandardowych nazw domen dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="4aa0d-211">Aby uzyskać więcej informacji zobacz [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="4aa0d-212">kliknij nazwy domeny tooview **wszystkie ustawienia** > **domen niestandardowych i SSL**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="4aa0d-213">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="4aa0d-213">Deployments</span></span>
* <span data-ttu-id="4aa0d-214">Konfigurowanie ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-214">Set up continuous deployment.</span></span> <span data-ttu-id="4aa0d-215">Zobacz [toodeploy przy użyciu narzędzia Git aplikacji sieci Web w usłudze Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4aa0d-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="4aa0d-216">Miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-216">Deployment slots.</span></span> <span data-ttu-id="4aa0d-217">Zobacz [wdrażania środowisk tooStaging dla aplikacji sieci Web w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="4aa0d-218">tooview Twojego miejsca wdrożenia, kliknij przycisk **wszystkie ustawienia** > **miejsc wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="4aa0d-219">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="4aa0d-219">Monitoring</span></span>
<span data-ttu-id="4aa0d-220">W trybie Basic lub Standard można sprawdzić dostępności hello punktów końcowych HTTP lub HTTPS, z zapasowej toothree rozproszona geograficznie lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="4aa0d-221">Test monitorowania kończy się niepowodzeniem, jeśli hello kod odpowiedzi HTTP jest błąd (4xx lub 5xx) lub odpowiedź hello trwa dłużej niż 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="4aa0d-222">Punkt końcowy jest traktowane jako dostępne w przypadku powodzenia testów monitorowania hello ze wszystkich hello określonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="4aa0d-223">Aby uzyskać więcej informacji, zobacz [porady: monitorować stan punktu końcowego sieci web].</span><span class="sxs-lookup"><span data-stu-id="4aa0d-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="4aa0d-224">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service], gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4aa0d-225">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="4aa0d-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4aa0d-226">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4aa0d-226">Next steps</span></span>
* <span data-ttu-id="4aa0d-227">[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="4aa0d-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="4aa0d-228">[Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="4aa0d-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="4aa0d-229">[Skalowanie aplikacji sieci web w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="4aa0d-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="4aa0d-230">[Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="4aa0d-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[wdrażania środowisk tooStaging dla aplikacji sieci Web w usłudze Azure App Service]: ./web-sites-staged-publishing.md
[Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]: ./app-service-web-tutorial-custom-ssl.md
[porady: monitorować stan punktu końcowego sieci web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]: ./web-sites-monitor.md
[tryb potokowy]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Skalowanie aplikacji sieci web w usłudze Azure App Service]: ./web-sites-scale.md
[użyciu biblioteki socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[Wypróbuj usługę App Service]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
