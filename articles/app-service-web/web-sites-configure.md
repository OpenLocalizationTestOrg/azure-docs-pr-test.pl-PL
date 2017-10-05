---
title: "Konfigurowanie aplikacji sieci Web w usłudze Azure App Service"
description: "Jak skonfigurować aplikację sieci web w usłudze Azure App Services"
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
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="b8623-103">Konfigurowanie aplikacji sieci Web w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b8623-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="b8623-104">W tym temacie opisano sposób konfigurowania aplikacji sieci web za pomocą [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="b8623-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="b8623-105">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="b8623-105">Application settings</span></span>
1. <span data-ttu-id="b8623-106">W [Azure Portal], otwórz blok dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8623-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="b8623-107">Kliknij przycisk **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b8623-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="b8623-108">Kliknij przycisk **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b8623-108">Click **Application Settings**.</span></span>

![Ustawienia aplikacji][configure01]

<span data-ttu-id="b8623-110">**Ustawienia aplikacji** bloku ma ustawienia pogrupowane w różne kategorie.</span><span class="sxs-lookup"><span data-stu-id="b8623-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="b8623-111">Ustawienia ogólne</span><span class="sxs-lookup"><span data-stu-id="b8623-111">General settings</span></span>
<span data-ttu-id="b8623-112">**Framework w wersji**.</span><span class="sxs-lookup"><span data-stu-id="b8623-112">**Framework versions**.</span></span> <span data-ttu-id="b8623-113">Ustaw tych opcji, jeśli aplikacja używa tych platform:</span><span class="sxs-lookup"><span data-stu-id="b8623-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="b8623-114">**.NET framework**: Ustaw wersji programu .NET framework.</span><span class="sxs-lookup"><span data-stu-id="b8623-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="b8623-115">**PHP**: Ustaw wersję PHP lub **OFF** wyłączyć PHP.</span><span class="sxs-lookup"><span data-stu-id="b8623-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="b8623-116">**Java**: Wybierz wersję Java lub **OFF** wyłączyć Java.</span><span class="sxs-lookup"><span data-stu-id="b8623-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="b8623-117">Użyj **kontener sieci Web** opcję, aby wybrać Tomcat i Jetty wersji.</span><span class="sxs-lookup"><span data-stu-id="b8623-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="b8623-118">**Python**: Wybierz wersję języka Python lub **OFF** wyłączyć Python.</span><span class="sxs-lookup"><span data-stu-id="b8623-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="b8623-119">Ze względów technicznych włączenie Java aplikacji powoduje wyłączenie opcji .NET, PHP i Python.</span><span class="sxs-lookup"><span data-stu-id="b8623-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="b8623-120"><a name="platform"></a>
**Platforma**.</span><span class="sxs-lookup"><span data-stu-id="b8623-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="b8623-121">Wybiera, czy aplikacja sieci web jest uruchamiana w środowisku 32-bitowy lub 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="b8623-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="b8623-122">64-bitowego środowiska wymaga trybu Basic lub Standard.</span><span class="sxs-lookup"><span data-stu-id="b8623-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="b8623-123">Zwolnij i tryby udostępnione są zawsze uruchamiane w środowisku 32-bitowym.</span><span class="sxs-lookup"><span data-stu-id="b8623-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="b8623-124">**Sieci Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="b8623-124">**Web Sockets**.</span></span> <span data-ttu-id="b8623-125">Ustaw **ON** Aby włączyć protokół WebSocket; na przykład, jeśli aplikacja sieci web używa [ASP.NET SignalR] lub [użyciu biblioteki socket.io].</span><span class="sxs-lookup"><span data-stu-id="b8623-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="b8623-126"><a name="alwayson"></a>
**Zawsze włączone**.</span><span class="sxs-lookup"><span data-stu-id="b8623-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="b8623-127">Domyślnie aplikacje sieci web są usuwane, jeśli są one bezczynności przez niektóre czas.</span><span class="sxs-lookup"><span data-stu-id="b8623-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="b8623-128">Pozwala to zaoszczędzić zasoby systemu.</span><span class="sxs-lookup"><span data-stu-id="b8623-128">This lets the system conserve resources.</span></span> <span data-ttu-id="b8623-129">W trybie Basic lub Standard, aby umożliwić **zawsze na** do zachowania aplikacji załadowana przez cały czas.</span><span class="sxs-lookup"><span data-stu-id="b8623-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="b8623-130">Jeśli aplikacja będzie działać ciągłe zadania Webjob lub uruchamia zadania Webjob wyzwolone przy użyciu wyrażenia CRON, należy włączyć **zawsze na**, lub zadania sieci web mogą nie działać prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="b8623-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="b8623-131">**Zarządzane wersji potoku**.</span><span class="sxs-lookup"><span data-stu-id="b8623-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="b8623-132">Ustawia IIS [tryb potokowy].</span><span class="sxs-lookup"><span data-stu-id="b8623-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="b8623-133">Pozostaw tego zestawu na zintegrowane (ustawienie domyślne), chyba że masz starszej wersji aplikacji, która wymaga starszej wersji programu IIS.</span><span class="sxs-lookup"><span data-stu-id="b8623-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="b8623-134">**Automatycznie wymiany**.</span><span class="sxs-lookup"><span data-stu-id="b8623-134">**Auto Swap**.</span></span> <span data-ttu-id="b8623-135">Po włączeniu automatycznej wymiany dla miejsca wdrożenia usługi aplikacji — automatycznie zamianę aplikacji sieci web w środowisku produkcyjnym po naciśnięciu aktualizacji do tego miejsca.</span><span class="sxs-lookup"><span data-stu-id="b8623-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="b8623-136">Aby uzyskać więcej informacji, zobacz [wdrażanie na tymczasowej miejsc aplikacji sieci web w usłudze Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="b8623-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="b8623-137">Debugowanie</span><span class="sxs-lookup"><span data-stu-id="b8623-137">Debugging</span></span>
<span data-ttu-id="b8623-138">**Debugowanie zdalne**.</span><span class="sxs-lookup"><span data-stu-id="b8623-138">**Remote Debugging**.</span></span> <span data-ttu-id="b8623-139">Umożliwia zdalne debugowanie.</span><span class="sxs-lookup"><span data-stu-id="b8623-139">Enables remote debugging.</span></span> <span data-ttu-id="b8623-140">Po włączeniu można użyć zdalnego debugera w programie Visual Studio, aby połączyć się bezpośrednio z aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8623-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="b8623-141">Debugowanie zdalne pozostanie włączony 48 godzin.</span><span class="sxs-lookup"><span data-stu-id="b8623-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="b8623-142">Ustawienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="b8623-142">App settings</span></span>
<span data-ttu-id="b8623-143">Ta sekcja zawiera pary nazwa/wartość, które sieci web aplikacji zostanie załadowany po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="b8623-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="b8623-144">W przypadku aplikacji .NET, te ustawienia są wstrzykiwane do konfiguracji .NET `AppSettings` w czasie wykonywania, zastępowanie istniejących ustawień.</span><span class="sxs-lookup"><span data-stu-id="b8623-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="b8623-145">Aplikacje PHP, Python, Java i węzła mają dostęp do tych ustawień jako zmienne środowiskowe w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="b8623-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="b8623-146">Dla każdego ustawienia aplikacji są tworzone dwie zmienne środowiskowe; jeden z nazwą określoną przez ustawienie wpis aplikacji, a druga z prefiksem APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="b8623-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="b8623-147">Zawierają tę samą wartość.</span><span class="sxs-lookup"><span data-stu-id="b8623-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="b8623-148">Parametry połączeń</span><span class="sxs-lookup"><span data-stu-id="b8623-148">Connection strings</span></span>
<span data-ttu-id="b8623-149">Parametry połączenia dla połączonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="b8623-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="b8623-150">W przypadku aplikacji .NET, te parametry połączenia są wstrzykiwane do konfiguracji .NET `connectionStrings` ustawienia w czasie wykonywania, zastępowanie istniejących wpisów, gdy klucz jest równe nazwy połączonej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b8623-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="b8623-151">W przypadku aplikacji PHP, Python, Java i węzła te ustawienia będą dostępne jako zmienne środowiskowe w czasie wykonywania, prefiksem typu połączenia.</span><span class="sxs-lookup"><span data-stu-id="b8623-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="b8623-152">Prefiksy zmiennej środowiskowej są następujące:</span><span class="sxs-lookup"><span data-stu-id="b8623-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="b8623-153">Program SQL Server:`SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="b8623-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="b8623-154">MySQL:`MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="b8623-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="b8623-155">Baza danych SQL:`SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="b8623-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="b8623-156">Niestandardowe:`CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="b8623-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="b8623-157">Na przykład, jeśli parametry połączenia MySql nazwany `connectionstring1`, czy dostęp do niej za pomocą zmiennej środowiskowej `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="b8623-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="b8623-158">Dokumenty domyślne</span><span class="sxs-lookup"><span data-stu-id="b8623-158">Default documents</span></span>
<span data-ttu-id="b8623-159">Dokument domyślny jest strony sieci web wyświetlaną w głównego adresu URL witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b8623-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="b8623-160">Pierwszy odpowiedniego pliku na liście jest używany.</span><span class="sxs-lookup"><span data-stu-id="b8623-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="b8623-161">Aplikacje sieci Web może używać modułów, że trasy na podstawie adresu URL, a nie obsługujących zawartość statyczną, w którym to przypadku nie jest dokument domyślny, w związku.</span><span class="sxs-lookup"><span data-stu-id="b8623-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="b8623-162">Mapowania programu obsługi</span><span class="sxs-lookup"><span data-stu-id="b8623-162">Handler mappings</span></span>
<span data-ttu-id="b8623-163">Aby dodać procesorów skryptu niestandardowego do obsługi żądań określonych rozszerzeń plików, użyj tego obszaru.</span><span class="sxs-lookup"><span data-stu-id="b8623-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="b8623-164">**Rozszerzenie**.</span><span class="sxs-lookup"><span data-stu-id="b8623-164">**Extension**.</span></span> <span data-ttu-id="b8623-165">Rozszerzenie pliku, które mają być obsługiwane, takie jak *.php lub handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="b8623-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="b8623-166">**Ścieżka do procesora skryptów**.</span><span class="sxs-lookup"><span data-stu-id="b8623-166">**Script Processor Path**.</span></span> <span data-ttu-id="b8623-167">Ścieżka bezwzględna procesora skryptów.</span><span class="sxs-lookup"><span data-stu-id="b8623-167">The absolute path of the script processor.</span></span> <span data-ttu-id="b8623-168">Żądania dostępu do plików, zgodne z rozszerzeniem pliku zostanie przetworzony przez procesora skryptów.</span><span class="sxs-lookup"><span data-stu-id="b8623-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="b8623-169">Użyj ścieżki `D:\home\site\wwwroot` do odwoływania się do katalogu głównego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8623-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="b8623-170">**Dodatkowe argumenty**.</span><span class="sxs-lookup"><span data-stu-id="b8623-170">**Additional Arguments**.</span></span> <span data-ttu-id="b8623-171">Opcjonalne argumenty wiersza polecenia do procesora skryptów</span><span class="sxs-lookup"><span data-stu-id="b8623-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="b8623-172">Wirtualne aplikacje i katalogi</span><span class="sxs-lookup"><span data-stu-id="b8623-172">Virtual applications and directories</span></span>
<span data-ttu-id="b8623-173">Aby skonfigurować wirtualne aplikacje i katalogi, określ każdy katalog wirtualny i jego odpowiedniego ścieżka fizyczna względem katalogu głównego witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b8623-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="b8623-174">Opcjonalnie można wybrać **aplikacji** pole wyboru, aby oznaczyć katalogu wirtualnego jako aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b8623-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="b8623-175">Włączanie dzienników diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="b8623-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="b8623-176">Aby włączyć dzienniki diagnostyczne:</span><span class="sxs-lookup"><span data-stu-id="b8623-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="b8623-177">W bloku dla aplikacji sieci web, kliknij **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b8623-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="b8623-178">Kliknij przycisk **dzienniki diagnostyczne**.</span><span class="sxs-lookup"><span data-stu-id="b8623-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="b8623-179">Opcje zapisywania dzienników diagnostycznych z aplikacji sieci web, która obsługuje rejestrowanie:</span><span class="sxs-lookup"><span data-stu-id="b8623-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="b8623-180">**Rejestrowanie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b8623-180">**Application Logging**.</span></span> <span data-ttu-id="b8623-181">Zapisuje Dzienniki aplikacji w systemie plików.</span><span class="sxs-lookup"><span data-stu-id="b8623-181">Writes application logs to the file system.</span></span> <span data-ttu-id="b8623-182">Rejestrowanie okresu w okresie 12 godzin.</span><span class="sxs-lookup"><span data-stu-id="b8623-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="b8623-183">**Poziom**.</span><span class="sxs-lookup"><span data-stu-id="b8623-183">**Level**.</span></span> <span data-ttu-id="b8623-184">Po włączeniu rejestrowania aplikacji, ta opcja określa, że ilość informacji, które będą rejestrowane (błąd, ostrzeżenie, informacje lub pełne).</span><span class="sxs-lookup"><span data-stu-id="b8623-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="b8623-185">**Rejestrowanie pracy serwera sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="b8623-185">**Web server logging**.</span></span> <span data-ttu-id="b8623-186">Dzienniki są zapisywane w rozszerzonym formacie W3C dziennika pliku.</span><span class="sxs-lookup"><span data-stu-id="b8623-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="b8623-187">**Szczegółowe komunikaty o błędach**.</span><span class="sxs-lookup"><span data-stu-id="b8623-187">**Detailed error messages**.</span></span> <span data-ttu-id="b8623-188">Zapisuje szczegółowe informacje o błędzie komunikatów pliki htm.</span><span class="sxs-lookup"><span data-stu-id="b8623-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="b8623-189">Pliki są zapisywane w obszarze /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="b8623-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="b8623-190">**Śledzenie nieudanych żądań**.</span><span class="sxs-lookup"><span data-stu-id="b8623-190">**Failed request tracing**.</span></span> <span data-ttu-id="b8623-191">Dzienniki nieudane żądania do plików XML.</span><span class="sxs-lookup"><span data-stu-id="b8623-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="b8623-192">Pliki są zapisywane w obszarze/LogFiles/W3SVC*xxx*, gdzie xxx jest unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="b8623-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="b8623-193">Ten folder zawiera plik XSL i co najmniej jeden plik XML.</span><span class="sxs-lookup"><span data-stu-id="b8623-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="b8623-194">Upewnij się, że Pobierz plik XSL, ponieważ zapewnia funkcje dotyczące formatowania i filtrowanie zawartości plików XML.</span><span class="sxs-lookup"><span data-stu-id="b8623-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="b8623-195">Aby wyświetlić pliki dziennika, należy utworzyć poświadczenia FTP w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b8623-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="b8623-196">W bloku dla aplikacji sieci web, kliknij **wszystkie ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="b8623-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="b8623-197">Kliknij przycisk **poświadczenia wdrażania**.</span><span class="sxs-lookup"><span data-stu-id="b8623-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="b8623-198">Wprowadź nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="b8623-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="b8623-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b8623-199">Click **Save**.</span></span>

![Konfigurowanie poświadczeń wdrożenia][configure03]

<span data-ttu-id="b8623-201">Pełna nazwa użytkownika FTP jest "app\username", gdzie *aplikacji* to nazwa aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8623-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="b8623-202">Nazwa użytkownika jest wymieniony w bloku aplikacja sieci web, w obszarze **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="b8623-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![Poświadczenia wdrożenia FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="b8623-204">Inne zadania konfiguracji</span><span class="sxs-lookup"><span data-stu-id="b8623-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="b8623-205">PROTOKÓŁ SSL</span><span class="sxs-lookup"><span data-stu-id="b8623-205">SSL</span></span>
<span data-ttu-id="b8623-206">W trybie Basic lub Standard możesz przekazać certyfikatów SSL dla domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="b8623-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="b8623-207">Aby uzyskać więcej informacji zobacz [Włącz protokół HTTPS dla aplikacji sieci web].</span><span class="sxs-lookup"><span data-stu-id="b8623-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="b8623-208">Aby wyświetlić przekazane certyfikaty, kliknij przycisk **wszystkie ustawienia** > **domen niestandardowych i SSL**.</span><span class="sxs-lookup"><span data-stu-id="b8623-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="b8623-209">Nazwy domen</span><span class="sxs-lookup"><span data-stu-id="b8623-209">Domain names</span></span>
<span data-ttu-id="b8623-210">Dodawanie niestandardowych nazw domen dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="b8623-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="b8623-211">Aby uzyskać więcej informacji zobacz [Konfigurowanie niestandardowej nazwy domeny dla aplikacji sieci web w usłudze Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="b8623-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="b8623-212">Aby wyświetlić nazwy domeny, kliknij przycisk **wszystkie ustawienia** > **domen niestandardowych i SSL**.</span><span class="sxs-lookup"><span data-stu-id="b8623-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="b8623-213">Wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b8623-213">Deployments</span></span>
* <span data-ttu-id="b8623-214">Konfigurowanie ciągłego wdrażania.</span><span class="sxs-lookup"><span data-stu-id="b8623-214">Set up continuous deployment.</span></span> <span data-ttu-id="b8623-215">Zobacz [przy użyciu narzędzia Git do wdrożenia aplikacji Web Apps w usłudze Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b8623-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="b8623-216">Miejsc wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="b8623-216">Deployment slots.</span></span> <span data-ttu-id="b8623-217">Zobacz [wdrożyć środowisk przejściowych dla aplikacji sieci Web w usłudze aplikacji Azure].</span><span class="sxs-lookup"><span data-stu-id="b8623-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="b8623-218">Aby wyświetlić Twojego miejsca wdrożenia, kliknij przycisk **wszystkie ustawienia** > **miejsc wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="b8623-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="b8623-219">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="b8623-219">Monitoring</span></span>
<span data-ttu-id="b8623-220">W trybie Basic lub Standard można sprawdzić dostępności punktów końcowych HTTP lub HTTPS, z maksymalnie trzech rozproszona geograficznie lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b8623-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="b8623-221">Test monitorowania kończy się niepowodzeniem, jeśli kod odpowiedzi HTTP jest błąd (4xx lub 5xx) lub odpowiedzi trwa dłużej niż 30 sekund.</span><span class="sxs-lookup"><span data-stu-id="b8623-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="b8623-222">Punkt końcowy jest traktowany jako dostępne w przypadku powodzenia testów monitorowania w określonych lokalizacjach.</span><span class="sxs-lookup"><span data-stu-id="b8623-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="b8623-223">Aby uzyskać więcej informacji, zobacz [porady: monitorować stan punktu końcowego sieci web].</span><span class="sxs-lookup"><span data-stu-id="b8623-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="b8623-224">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service] (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="b8623-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b8623-225">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="b8623-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b8623-226">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b8623-226">Next steps</span></span>
* <span data-ttu-id="b8623-227">[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="b8623-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="b8623-228">[Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]</span><span class="sxs-lookup"><span data-stu-id="b8623-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="b8623-229">[Skalowanie aplikacji sieci web w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="b8623-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="b8623-230">[Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="b8623-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="b8623-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="b8623-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="b8623-232">[Azure Portal]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="b8623-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="b8623-233">[Konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="b8623-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="b8623-234">[wdrożyć środowisk przejściowych dla aplikacji sieci Web w usłudze aplikacji Azure]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="b8623-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="b8623-235">[Włącz protokół HTTPS dla aplikacji w usłudze aplikacji Azure]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="b8623-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="b8623-236">[porady: monitorować stan punktu końcowego sieci web]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="b8623-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="b8623-237">[Podstawy monitorowania aplikacji sieci Web w usłudze Azure App Service]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="b8623-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="b8623-238">[tryb potokowy]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="b8623-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="b8623-239">[Skalowanie aplikacji sieci web w usłudze Azure App Service]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="b8623-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="b8623-240">[użyciu biblioteki socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="b8623-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="b8623-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="b8623-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
