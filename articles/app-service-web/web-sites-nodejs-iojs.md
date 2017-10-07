---
title: "aaaHow toouse io.js z aplikacjami sieci Web usługi aplikacji Azure"
description: "Dowiedz się, jak toouse aplikacji sieci web w usłudze Azure App Service z io.js."
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
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="6f332-103">Jak toouse io.js z aplikacjami sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="6f332-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="6f332-104">Witaj popularnych węzeł rozwidlenia [io.js] funkcje projektu Node.js różnych tooJoyent różnice, w tym więcej Otwórz modelu ładu, szybsze cyklu wersji i szybsze przyjęcia nowych i eksperymentalna funkcji JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6f332-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="6f332-105">Gdy [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web ma wiele wersji środowiska Node.js preinstalowany, umożliwia także dla pliku binarnego Node.js dostarczane przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f332-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="6f332-106">W tym artykule opisano dwie metody umożliwiające użycie hello io.js aplikacji sieci Web usługi aplikacji: hello Użyj skryptu wdrożenia rozszerzonego, który automatycznie konfiguruje hello Azure toouse najnowszej wersji io.js dostępne, a także hello ręcznego przekazywania danych binarnych io.js.</span><span class="sxs-lookup"><span data-stu-id="6f332-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="6f332-107">Za pomocą skryptu wdrażania</span><span class="sxs-lookup"><span data-stu-id="6f332-107">Using a Deployment Script</span></span>
<span data-ttu-id="6f332-108">Po wdrożeniu aplikacji Node.js aplikacji usługi sieci Web aplikacji uruchamia liczbę małych poleceń, które tooensure, który hello środowisko jest skonfigurowane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="6f332-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="6f332-109">Za pomocą skryptu wdrażania, ten proces może być dostosowane tooinclude hello pobierania i konfiguracji io.js.</span><span class="sxs-lookup"><span data-stu-id="6f332-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="6f332-110">Witaj [io.js skrypt wdrożenia](https://github.com/felixrieseberg/iojs-azure) jest dostępna w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="6f332-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="6f332-111">io.js tooenable w aplikacji sieci web, wystarczy skopiować **.deployment**, **pliku deploy.cmd** i **plik IISNode.yml** toohello głównego folderu aplikacji i wdrażanie aplikacji tooWeb.</span><span class="sxs-lookup"><span data-stu-id="6f332-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="6f332-112">pierwszy plik Hello **.deployment**, powoduje, że aplikacje sieci Web toorun **pliku deploy.cmd** po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="6f332-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="6f332-113">Ten skrypt uruchamia wszystkie kroki zwykle hello aplikacji Node.js, ale również pobiera najnowsza wersja io.js hello.</span><span class="sxs-lookup"><span data-stu-id="6f332-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="6f332-114">Na koniec **plik IISNode.yml** konfiguruje binarne zamiast wstępnie zainstalowane binary Node.js io.js tylko hello pobrane toouse aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6f332-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="6f332-115">tooupdate hello używany io.js pliku binarnego, po prostu ponownie wdrożyć aplikację — skryptu hello pobierze nowej wersji io.js wdrożonej aplikacji hello co jeden raz.</span><span class="sxs-lookup"><span data-stu-id="6f332-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="6f332-116">Za pomocą ręcznej instalacji</span><span class="sxs-lookup"><span data-stu-id="6f332-116">Using Manual Installation</span></span>
<span data-ttu-id="6f332-117">Instalacja ręczna Hello wersji io.js niestandardowych obejmuje tylko dwa kroki.</span><span class="sxs-lookup"><span data-stu-id="6f332-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="6f332-118">Najpierw pobierz hello **win-x64** binarne bezpośrednio z hello [io.js dystrybucji].</span><span class="sxs-lookup"><span data-stu-id="6f332-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="6f332-119">Wymagane są dwa pliki - **iojs.exe** i **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="6f332-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="6f332-120">Zapisz zarówno tooa folder plików w aplikacji sieci web, na przykład w **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="6f332-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="6f332-121">toouse aplikacje sieci Web tooconfigure **iojs.exe** zamiast wstępnie zainstalowanej wersji węźle, utworzyć **plik IISNode.yml** hello katalogu głównego aplikacji i Dodaj hello następującego wiersza.</span><span class="sxs-lookup"><span data-stu-id="6f332-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="6f332-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f332-122">Next Steps</span></span>
<span data-ttu-id="6f332-123">W tym artykule przedstawiono sposób toouse io.js z aplikacjami sieci Web usługi aplikacji, używane są oba programy podane skryptów wdrażania, a także instalacji ręcznej.</span><span class="sxs-lookup"><span data-stu-id="6f332-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="6f332-124">IO.js jest mocno programowanie i aktualizowane częściej niż Node.js.</span><span class="sxs-lookup"><span data-stu-id="6f332-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="6f332-125">Liczba modułów Node.js może nie działać na io.js - Sprawdź należy zapoznać się z [io.js w serwisie GitHub] do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="6f332-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="6f332-126">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="6f332-126">What's changed</span></span>
* <span data-ttu-id="6f332-127">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="6f332-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="6f332-128">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="6f332-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6f332-129">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="6f332-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js dystrybucji]: https://iojs.org/dist/
[io.js w serwisie GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
