---
title: "How to debug a Node.js web app in Azure App Service (Jak debugować aplikację sieci Web Node.js w usłudze Azure App Service)"
description: "Dowiedz się, jak debugować aplikację sieci web Node.js w usłudze Azure App Service."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="ed9a1-103">How to debug a Node.js web app in Azure App Service (Jak debugować aplikację sieci Web Node.js w usłudze Azure App Service)</span><span class="sxs-lookup"><span data-stu-id="ed9a1-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="ed9a1-104">Platforma Azure oferuje wbudowane narzędzia diagnostyczne z debugowanie aplikacji Node.js hostowanych w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="ed9a1-105">W tym artykule dowiesz się, jak włączyć rejestrowanie stdout i stderr, wyświetlane informacje o błędzie w przeglądarce i sposobu pobierania i wyświetlania plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="ed9a1-106">Diagnostyka dla aplikacji programu Node.js hostowanej na platformie Azure jest zapewniana przez [IISNode].</span><span class="sxs-lookup"><span data-stu-id="ed9a1-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="ed9a1-107">Gdy w tym artykule omówiono najczęściej używane do zbierania informacji diagnostycznych, nie dostarcza pełne odwołanie do pracy z programu IISNode.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="ed9a1-108">Aby uzyskać więcej informacji na temat pracy z programu IISNode, zobacz [plik Readme programu IISNode] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="ed9a1-109">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="ed9a1-109">Enable logging</span></span>
<span data-ttu-id="ed9a1-110">Domyślnie aplikacji sieci web usługi aplikacji — tylko przechwytuje informacje diagnostyczne dotyczące wdrożeń, takich jak podczas wdrażania aplikacji sieci web przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="ed9a1-111">Informacje te są przydatne, jeśli masz problemy podczas wdrażania, takiej jak awaria podczas instalowania modułu, do którego odwołuje się **package.json**, lub jeśli używasz skryptu wdrażania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="ed9a1-112">Aby włączyć rejestrowanie ze strumienia stdout i stderr, należy utworzyć **plik IISNode.yml** plików w katalogu głównym aplikacji Node.js i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="ed9a1-113">Dzięki temu rejestrowanie stderr i stdout z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="ed9a1-114">**Plik IISNode.yml** pliku może również służyć do kontroli czy przyjazne komunikaty o błędach lub developer błędy są zwracane do przeglądarki, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="ed9a1-115">Aby włączyć błędy developer, Dodaj następujący wiersz do **plik IISNode.yml** pliku:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="ed9a1-116">Po włączeniu tej opcji program IISNode zwróci ostatniego 64 KB informacje wysyłane do strumienia wyjściowego stderr zamiast błędu przyjazną, takie jak "Wystąpił wewnętrzny błąd serwera".</span><span class="sxs-lookup"><span data-stu-id="ed9a1-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="ed9a1-117">Gdy devErrorsEnabled jest przydatne, gdy diagnozowanie problemów w czasie projektowania, włączenie jej w środowisku produkcyjnym może powodować błędy programowanie są wysyłane do użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="ed9a1-118">Jeśli **plik IISNode.yml** plik nie istnieje już w aplikacji, należy ponownie uruchomić aplikacji sieci web po opublikowaniu aplikacji zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="ed9a1-119">W przypadku po prostu zmiany ustawień w istniejącym **plik IISNode.yml** pliku, który wcześniej został opublikowany, nie jest ponowne uruchomienie wymagane.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="ed9a1-120">Jeśli aplikacja sieci web została utworzona za pomocą narzędzia wiersza polecenia platformy Azure lub poleceń cmdlet Azure PowerShell, domyślny **plik IISNode.yml** plik jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="ed9a1-121">Można ponownie uruchomić aplikacji sieci web, wybierz aplikację sieci web w [Azure Portal](https://portal.azure.com), a następnie kliknij przycisk **ponowne URUCHOMIENIE** przycisk:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Uruchom ponownie przycisku][restart-button]

<span data-ttu-id="ed9a1-123">Jeśli narzędzia wiersza polecenia platformy Azure są zainstalowane w środowisku projektowania, służy następujące polecenie, aby ponownie uruchomić aplikacji sieci web:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="ed9a1-124">LoggingEnabled i devErrorsEnabled są najczęściej używane opcje konfiguracji plik IISNode.yml przechwytywania informacje diagnostyczne, plik IISNode.yml może służyć do konfigurowania różnych opcji dla danego środowiska hostingu.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="ed9a1-125">Aby uzyskać pełną listę opcji konfiguracji, zobacz [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) pliku.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="ed9a1-126">Uzyskiwanie dostępu do dzienników</span><span class="sxs-lookup"><span data-stu-id="ed9a1-126">Accessing logs</span></span>
<span data-ttu-id="ed9a1-127">Dzienniki diagnostyczne jest dostępny na trzy sposoby; Za pomocą protokołu FTP (File Transfer), pobieranie archiwum Zip lub jako na żywo zaktualizowane strumienia dziennika (fragmentu).</span><span class="sxs-lookup"><span data-stu-id="ed9a1-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="ed9a1-128">Pobieranie archiwum Zip plików dziennika lub wyświetlanie strumień na żywo wymaga narzędzia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="ed9a1-129">Mogą być instalowane za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="ed9a1-130">Po zainstalowaniu narzędzi jest możliwy za pomocą polecenia "azure".</span><span class="sxs-lookup"><span data-stu-id="ed9a1-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="ed9a1-131">Narzędzia wiersza polecenia, należy najpierw skonfigurować do korzystania z subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="ed9a1-132">Aby uzyskać informacje na temat sposobu wykonania tego zadania, zobacz **sposób pobierania i importowania ustawień publikowania** sekcji [sposobu użycia narzędzi wiersza polecenia Azure](../xplat-cli-connect.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="ed9a1-133">FTP</span><span class="sxs-lookup"><span data-stu-id="ed9a1-133">FTP</span></span>
<span data-ttu-id="ed9a1-134">Aby uzyskać dostęp do informacji diagnostycznych za pośrednictwem FTP, odwiedź stronę [Azure Portal](https://portal.azure.com), wybierz aplikację sieci web, a następnie wybierz **pulpitu NAWIGACYJNEGO**.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="ed9a1-135">W **szybkie linki** sekcji **DZIENNIKÓW diagnostycznych FTP** i **DZIENNIKÓW diagnostycznych FTPS** łącza zapewniają dostęp do dzienników przy użyciu protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="ed9a1-136">Jeśli użytkownik nie zostały wcześniej skonfigurowane nazwy użytkownika i hasła dla FTP lub wdrożenie, możesz to zrobić z **szybkiego startu** strony zarządzania przez wybranie **skonfigurowano poświadczeń wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="ed9a1-137">Adres URL FTP zwrócił na pulpicie nawigacyjnym jest **LogFiles** katalogu, który będzie zawierać następujące katalogi podrzędne:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="ed9a1-138">[Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git, katalog o tej samej nazwie zostanie utworzony i będzie zawierać informacje dotyczące wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="ed9a1-139">nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="ed9a1-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="ed9a1-140">Archiwum zip</span><span class="sxs-lookup"><span data-stu-id="ed9a1-140">Zip archive</span></span>
<span data-ttu-id="ed9a1-141">Aby pobrać archiwum Zip dzienników diagnostycznych, użyj następującego polecenia z narzędzi wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="ed9a1-142">Spowoduje to pobranie **diagnostics.zip** w bieżącym katalogu.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="ed9a1-143">To archiwum zawiera następującą strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="ed9a1-144">wdrożenia — dziennik informacji o wdrożeniach aplikacji</span><span class="sxs-lookup"><span data-stu-id="ed9a1-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="ed9a1-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="ed9a1-145">LogFiles</span></span>
  
  * <span data-ttu-id="ed9a1-146">[Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git, katalog o tej samej nazwie zostanie utworzony i będzie zawierać informacje dotyczące wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="ed9a1-147">nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="ed9a1-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="ed9a1-148">Strumień na żywo (tail)</span><span class="sxs-lookup"><span data-stu-id="ed9a1-148">Live stream (tail)</span></span>
<span data-ttu-id="ed9a1-149">Aby wyświetlić strumień na żywo informacji diagnostycznych dziennika, użyj następującego polecenia z narzędzi wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ed9a1-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="ed9a1-150">Zwraca strumienia dziennika zdarzeń, które są aktualizowane w miarę ich występowania na serwerze.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="ed9a1-151">Ten strumień zwraca informacje na temat wdrażania, jak również informacje stdout i stderr (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="ed9a1-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="ed9a1-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed9a1-152">Next Steps</span></span>
<span data-ttu-id="ed9a1-153">W tym artykule przedstawiono sposób włączenia i dostęp do informacji diagnostycznych dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="ed9a1-154">Gdy informacje te są przydatne w opis problemów, które występują w przypadku aplikacji, może to wskazywać na problem z modułem używasz lub wersja Node.js używane przez aplikacje sieci Web usługi aplikacji jest inne niż używane w danym środowisku wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="ed9a1-155">Informacje w pracy z modułów na platformie Azure, zobacz [przy użyciu modułów Node.js z aplikacjami Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="ed9a1-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="ed9a1-156">Informacje dotyczące określania wersji środowiska Node.js dla aplikacji, zobacz [określanie wersji środowiska Node.js w aplikacji Azure].</span><span class="sxs-lookup"><span data-stu-id="ed9a1-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="ed9a1-157">Aby uzyskać więcej informacji, zobacz też [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="ed9a1-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="ed9a1-158">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="ed9a1-158">What's changed</span></span>
* <span data-ttu-id="ed9a1-159">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="ed9a1-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="ed9a1-160">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ed9a1-161">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="ed9a1-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="ed9a1-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="ed9a1-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="ed9a1-163">[plik Readme programu IISNode]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="ed9a1-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="ed9a1-164">[określanie wersji środowiska Node.js w aplikacji Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="ed9a1-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

