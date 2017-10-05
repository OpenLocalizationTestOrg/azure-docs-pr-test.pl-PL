---
title: "Azure CLI przykładowym skrypcie - skalowanie aplikacji sieci web na całym świecie z architekturą availabilty wysokiej | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — aplikacji sieci web na całym świecie z architekturą availabilty dużej skali"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4033a50-0e05-4505-8ce8-c876204b2acc
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c368bdc48f197ff5b491d1796d85abfd339051a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="53932-103">Skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="53932-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="53932-104">W tym scenariuszu utworzysz, grupy zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="53932-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="53932-105">Po zakończeniu wykonywania będą miały o wysokiej dostępności architekturę, dzięki czemu zapewnia globalną dostępność aplikacji sieci web, w oparciu o najniższym opóźnieniu sieci.</span><span class="sxs-lookup"><span data-stu-id="53932-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="53932-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="53932-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="53932-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="53932-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="53932-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53932-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="53932-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="53932-109">Sample script</span></span>

<span data-ttu-id="53932-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "geograficzne skali")]</span><span class="sxs-lookup"><span data-stu-id="53932-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="53932-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="53932-111">Script explanation</span></span>

<span data-ttu-id="53932-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web profilu Menedżera ruchu i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="53932-112">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="53932-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="53932-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="53932-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="53932-114">Command</span></span> | <span data-ttu-id="53932-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="53932-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="53932-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="53932-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="53932-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="53932-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="53932-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="53932-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="53932-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="53932-119">Creates an App Service plan.</span></span> <span data-ttu-id="53932-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53932-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="53932-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="53932-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="53932-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="53932-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="53932-123">Utwórz profil Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="53932-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="53932-124">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="53932-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="53932-125">Tworzenie punktu końcowego Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="53932-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="53932-126">Dodaje punkt końcowy profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="53932-126">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="53932-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="53932-127">Next steps</span></span>

<span data-ttu-id="53932-128">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="53932-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="53932-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="53932-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
