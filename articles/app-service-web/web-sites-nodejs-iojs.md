---
title: "Sposób użycia platformy io.js z aplikacjami Web Apps w usłudze Azure App Service"
description: "Dowiedz się, jak używać aplikacji sieci web w usłudze Azure App Service z io.js."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="41391-103">Sposób użycia platformy io.js z aplikacjami Web Apps w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="41391-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="41391-104">Popularne rozwidlenia węzła [io.js] funkcji różnych różnice do projektu Node.js w Joyent, tym bardziej otwarte modelu ładu, szybsze cyklu wersji i szybsze przyjęcia nowych i eksperymentalna funkcji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="41391-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="41391-105">Gdy [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web ma wiele wersji środowiska Node.js preinstalowany, umożliwia także dla pliku binarnego Node.js dostarczane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="41391-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="41391-106">W tym artykule opisano dwie metody umożliwia używanie io.js aplikacji sieci Web usługi aplikacji: Użyj skryptu wdrożenia rozszerzonego, który automatycznie konfiguruje Azure, aby używać najnowszej wersji io.js dostępne, a także ręcznego przekazywania io.js binarnego.</span><span class="sxs-lookup"><span data-stu-id="41391-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="41391-107">Za pomocą skryptu wdrażania</span><span class="sxs-lookup"><span data-stu-id="41391-107">Using a Deployment Script</span></span>
<span data-ttu-id="41391-108">Po wdrożeniu aplikacji Node.js aplikacji usługi sieci Web aplikacji działa wiele małych poleceń, aby zapewnić poprawne skonfigurowanie środowiska.</span><span class="sxs-lookup"><span data-stu-id="41391-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="41391-109">Za pomocą skryptu wdrażania tego procesu można dostosować do pobierania i konfiguracji io.js.</span><span class="sxs-lookup"><span data-stu-id="41391-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="41391-110">[Io.js skrypt wdrożenia](https://github.com/felixrieseberg/iojs-azure) jest dostępna w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="41391-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="41391-111">Aby włączyć io.js w aplikacji sieci web, wystarczy skopiować **.deployment**, **pliku deploy.cmd** i **plik IISNode.yml** do głównego folderu aplikacji i wdrażania aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="41391-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="41391-112">Pierwszy plik **.deployment**, powoduje, że aplikacje sieci Web do uruchamiania **pliku deploy.cmd** po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="41391-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="41391-113">Ten skrypt uruchamia wszystkie kroki zwykle aplikacji Node.js, ale również pobiera najnowsza wersja io.js.</span><span class="sxs-lookup"><span data-stu-id="41391-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="41391-114">Na koniec **plik IISNode.yml** konfiguruje aplikacje sieci Web do używania właśnie pobrany io.js binarne zamiast wstępnie zainstalowane binarnym środowiska Node.js.</span><span class="sxs-lookup"><span data-stu-id="41391-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="41391-115">Aby zaktualizować plik binarny używany io.js, po prostu ponownie wdrożyć aplikację - skrypt pobierze nowej wersji io.js co jeden raz wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41391-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="41391-116">Za pomocą ręcznej instalacji</span><span class="sxs-lookup"><span data-stu-id="41391-116">Using Manual Installation</span></span>
<span data-ttu-id="41391-117">Instalacja ręczna wersji niestandardowych io.js obejmuje tylko dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="41391-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="41391-118">Najpierw pobierz **win-x64** binarne bezpośrednio z [io.js dystrybucji].</span><span class="sxs-lookup"><span data-stu-id="41391-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="41391-119">Wymagane są dwa pliki - **iojs.exe** i **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="41391-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="41391-120">Zapisz oba pliki do folderu wewnątrz aplikacji sieci web, na przykład w **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="41391-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="41391-121">Aby skonfigurować aplikacje sieci Web do używania **iojs.exe** zamiast wstępnie zainstalowanej wersji węźle, utworzyć **plik IISNode.yml** plików w katalogu głównym aplikacji i Dodaj następujący wiersz.</span><span class="sxs-lookup"><span data-stu-id="41391-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="41391-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41391-122">Next Steps</span></span>
<span data-ttu-id="41391-123">W tym artykule przedstawiono sposób używania io.js z aplikacjami sieci Web usługi aplikacji, używane są oba programy podać skryptów wdrażania oraz jak ręczna instalacja.</span><span class="sxs-lookup"><span data-stu-id="41391-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="41391-124">IO.js jest mocno programowanie i aktualizowane częściej niż Node.js.</span><span class="sxs-lookup"><span data-stu-id="41391-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="41391-125">Liczba modułów Node.js może nie działać na io.js - Sprawdź należy zapoznać się z [io.js w serwisie GitHub] do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="41391-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="41391-126">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="41391-126">What's changed</span></span>
* <span data-ttu-id="41391-127">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="41391-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="41391-128">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="41391-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="41391-129">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="41391-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="41391-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="41391-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="41391-131">[io.js dystrybucji]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="41391-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="41391-132">[io.js w serwisie GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="41391-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
