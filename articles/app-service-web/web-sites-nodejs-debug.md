---
title: "toodebug aaaHow aplikacji sieci web Node.js w usłudze Azure App Service"
description: "Dowiedz się, jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service."
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
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="b2089-103">Jak toodebug Node.js sieci web aplikacji w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b2089-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="b2089-104">Platforma Azure oferuje wbudowane narzędzia diagnostyczne tooassist z debugowaniem aplikacji programu Node.js w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="b2089-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="b2089-105">W tym artykule przedstawiono sposób rejestrowania tooenable stdout i stderr, informacje o błędzie wyświetlanej w przeglądarce hello i jak toodownload i wyświetlanie plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="b2089-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="b2089-106">Diagnostyka dla aplikacji programu Node.js hostowanej na platformie Azure jest zapewniana przez [IISNode].</span><span class="sxs-lookup"><span data-stu-id="b2089-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="b2089-107">Gdy w tym artykule omówiono hello najczęściej używane do zbierania informacji diagnostycznych, nie dostarcza pełne odwołanie do pracy z programu IISNode.</span><span class="sxs-lookup"><span data-stu-id="b2089-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="b2089-108">Aby uzyskać więcej informacji na temat pracy z programu IISNode, zobacz hello [plik Readme programu IISNode] w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2089-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="b2089-109">Włącz rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="b2089-109">Enable logging</span></span>
<span data-ttu-id="b2089-110">Domyślnie aplikacji sieci web usługi aplikacji — tylko przechwytuje informacje diagnostyczne dotyczące wdrożeń, takich jak podczas wdrażania aplikacji sieci web przy użyciu narzędzia Git.</span><span class="sxs-lookup"><span data-stu-id="b2089-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="b2089-111">Informacje te są przydatne, jeśli masz problemy podczas wdrażania, takiej jak awaria podczas instalowania modułu, do którego odwołuje się **package.json**, lub jeśli używasz skryptu wdrażania niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="b2089-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="b2089-112">Witaj tooenable rejestrowania ze strumienia stdout i stderr, należy utworzyć **plik IISNode.yml** hello katalogu głównego aplikacji Node.js i dodaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b2089-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="b2089-113">Dzięki temu rejestrowanie hello stderr i stdout z poziomu aplikacji Node.js.</span><span class="sxs-lookup"><span data-stu-id="b2089-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="b2089-114">Witaj **plik IISNode.yml** pliku mogą być również używane toocontrol, czy przyjazne komunikaty o błędach lub developer błędy są zwracane toohello przeglądarki, gdy wystąpi błąd.</span><span class="sxs-lookup"><span data-stu-id="b2089-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="b2089-115">błędy developer tooenable, Dodaj powitania po wierszu toohello **plik IISNode.yml** pliku:</span><span class="sxs-lookup"><span data-stu-id="b2089-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="b2089-116">Po włączeniu tej opcji program IISNode zwróci hello ostatniego 64 KB informacje wysyłane toostderr zamiast przyjazną błędu, takie jak "Wystąpił wewnętrzny błąd serwera".</span><span class="sxs-lookup"><span data-stu-id="b2089-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="b2089-117">Gdy devErrorsEnabled jest przydatne, gdy diagnozowanie problemów w czasie projektowania, włączenie jej w środowisku produkcyjnym może powodować błędy programowanie wysyłane tooend użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b2089-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="b2089-118">Jeśli hello **plik IISNode.yml** plik nie istnieje już w aplikacji, należy ponownie uruchomić aplikacji sieci web po opublikowaniu aplikacji hello zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="b2089-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="b2089-119">W przypadku po prostu zmiany ustawień w istniejącym **plik IISNode.yml** pliku, który wcześniej został opublikowany, nie jest ponowne uruchomienie wymagane.</span><span class="sxs-lookup"><span data-stu-id="b2089-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="b2089-120">Jeśli aplikacja sieci web została utworzona za pomocą narzędzia wiersza polecenia Azure hello lub poleceń cmdlet Azure PowerShell, domyślny **plik IISNode.yml** plik jest tworzony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b2089-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="b2089-121">aplikacji sieci web hello toorestart, aplikacji sieci web wybierz hello w hello [Azure Portal](https://portal.azure.com), a następnie kliknij przycisk **ponowne URUCHOMIENIE** przycisk:</span><span class="sxs-lookup"><span data-stu-id="b2089-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![Uruchom ponownie przycisku][restart-button]

<span data-ttu-id="b2089-123">Jeśli narzędzia wiersza polecenia Azure hello są zainstalowane w środowisku projektowania, możesz użyć hello następującej aplikacji sieci web hello toorestart polecenia:</span><span class="sxs-lookup"><span data-stu-id="b2089-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="b2089-124">Gdy loggingEnabled i devErrorsEnabled są opcje konfiguracji plik IISNode.yml hello najczęściej używane do przechwytywania informacje diagnostyczne, plik IISNode.yml może mieć tooconfigure używane różne opcje środowisku macierzystym.</span><span class="sxs-lookup"><span data-stu-id="b2089-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="b2089-125">Aby uzyskać pełną listę opcji konfiguracji hello, zobacz hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) pliku.</span><span class="sxs-lookup"><span data-stu-id="b2089-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="b2089-126">Uzyskiwanie dostępu do dzienników</span><span class="sxs-lookup"><span data-stu-id="b2089-126">Accessing logs</span></span>
<span data-ttu-id="b2089-127">Dzienniki diagnostyczne jest dostępny na trzy sposoby; Przy użyciu hello protokołu FTP (File Transfer), pobieranie archiwum Zip lub jako na żywo zaktualizowane strumienia dziennika hello (fragmentu).</span><span class="sxs-lookup"><span data-stu-id="b2089-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="b2089-128">Pobieranie archiwum Zip hello plików dziennika hello lub wyświetlanie hello strumień na żywo wymaga narzędzia wiersza polecenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b2089-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="b2089-129">Mogą być instalowane za pomocą hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b2089-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="b2089-130">Po zainstalowaniu narzędzi hello jest możliwy za pomocą polecenia "azure" hello.</span><span class="sxs-lookup"><span data-stu-id="b2089-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="b2089-131">Witaj narzędzia wiersza polecenia musi najpierw zostać skonfigurowany toouse subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2089-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="b2089-132">Uzyskać informacji o sposobie tooaccomplish to zadań, zobacz hello **jak toodownload, a następnie zaimportuj ustawienia publikowania** sekcji hello [jak tooUse hello narzędzi wiersza polecenia Azure](../xplat-cli-connect.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="b2089-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="b2089-133">FTP</span><span class="sxs-lookup"><span data-stu-id="b2089-133">FTP</span></span>
<span data-ttu-id="b2089-134">informacje diagnostyczne hello tooaccess za pomocą protokołu FTP, odwiedź stronę hello [Azure Portal](https://portal.azure.com), wybierz aplikację sieci web, a następnie wybierz hello **pulpitu NAWIGACYJNEGO**.</span><span class="sxs-lookup"><span data-stu-id="b2089-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="b2089-135">W hello **szybkie linki** sekcji, hello **DZIENNIKÓW diagnostycznych FTP** i **DZIENNIKÓW diagnostycznych FTPS** łącza umożliwiają dostęp toohello dzienników przy użyciu protokołu hello FTP.</span><span class="sxs-lookup"><span data-stu-id="b2089-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b2089-136">Jeśli użytkownik nie zostały wcześniej skonfigurowane nazwy użytkownika i hasła dla FTP lub wdrożenie, możesz to zrobić z hello **szybkiego startu** strony zarządzania przez wybranie **skonfigurowano poświadczeń wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="b2089-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="b2089-137">Witaj FTP adres URL zwracany na pulpicie nawigacyjnym hello jest hello **LogFiles** katalogu, który będzie zawierać Witaj podkatalogi następujące:</span><span class="sxs-lookup"><span data-stu-id="b2089-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="b2089-138">[Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git katalogu hello takiej nazwie zostanie utworzony i będzie zawierać informacje związane z toodeployments.</span><span class="sxs-lookup"><span data-stu-id="b2089-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="b2089-139">nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="b2089-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="b2089-140">Archiwum zip</span><span class="sxs-lookup"><span data-stu-id="b2089-140">Zip archive</span></span>
<span data-ttu-id="b2089-141">toodownload archiwum Zip hello dzienników diagnostycznych, hello Użyj następującego polecenia z narzędzi wiersza polecenia Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b2089-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="b2089-142">Spowoduje to pobranie **diagnostics.zip** w bieżącym katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="b2089-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="b2089-143">To archiwum zawiera powitania po strukturę katalogów:</span><span class="sxs-lookup"><span data-stu-id="b2089-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="b2089-144">wdrożenia — dziennik informacji o wdrożeniach aplikacji</span><span class="sxs-lookup"><span data-stu-id="b2089-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="b2089-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="b2089-145">LogFiles</span></span>
  
  * <span data-ttu-id="b2089-146">[Metody wdrażania](web-sites-deploy.md) — Jeśli używasz metody wdrażania, takie jak Git katalogu hello takiej nazwie zostanie utworzony i będzie zawierać informacje związane z toodeployments.</span><span class="sxs-lookup"><span data-stu-id="b2089-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="b2089-147">nodejs — informacje Stdout i stderr przechwytywane z wszystkich wystąpień aplikacji (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="b2089-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="b2089-148">Strumień na żywo (tail)</span><span class="sxs-lookup"><span data-stu-id="b2089-148">Live stream (tail)</span></span>
<span data-ttu-id="b2089-149">tooview strumień na żywo danych dzienników diagnostycznych hello Użyj następującego polecenia z narzędzi wiersza polecenia Azure hello:</span><span class="sxs-lookup"><span data-stu-id="b2089-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="b2089-150">Zwraca strumienia dziennika zdarzeń, które są aktualizowane w miarę ich występowania na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="b2089-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="b2089-151">Ten strumień zwraca informacje na temat wdrażania, jak również informacje stdout i stderr (jeśli loggingEnabled ma wartość true.)</span><span class="sxs-lookup"><span data-stu-id="b2089-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b2089-152">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2089-152">Next Steps</span></span>
<span data-ttu-id="b2089-153">W niniejszym artykule możesz przedstawiono sposób dostępu i tooenable informacje diagnostyczne dla platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b2089-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="b2089-154">Gdy informacje te są przydatne w opis problemów, które występują w przypadku aplikacji, może wskazywać problem tooa z modułu, którego używasz lub ta wersja hello Node.js używane przez aplikacje sieci Web usługi aplikacji jest inny niż hello używany we wdrożeniu środowisko.</span><span class="sxs-lookup"><span data-stu-id="b2089-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="b2089-155">Informacje w pracy z modułów na platformie Azure, zobacz [przy użyciu modułów Node.js z aplikacjami Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b2089-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="b2089-156">Informacje dotyczące określania wersji środowiska Node.js dla aplikacji, zobacz [określanie wersji środowiska Node.js w aplikacji Azure].</span><span class="sxs-lookup"><span data-stu-id="b2089-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="b2089-157">Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów środowiska Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b2089-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b2089-158">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="b2089-158">What's changed</span></span>
* <span data-ttu-id="b2089-159">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b2089-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b2089-160">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="b2089-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b2089-161">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="b2089-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[plik Readme programu IISNode]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[określanie wersji środowiska Node.js w aplikacji Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

