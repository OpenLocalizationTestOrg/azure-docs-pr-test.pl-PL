---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej availabilty | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b72fbccd7f2aaab58e4b4721e14dca14146c7c72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="33a63-103">Skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="33a63-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="33a63-104">W tym scenariuszu utworzysz, grupy zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="33a63-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="33a63-105">Po zakończeniu wykonywania hello będą miały o wysokiej dostępności architekturę, dzięki czemu zapewnia globalną dostępność aplikacji sieci web oparta na powitania najniższe opóźnienia sieci.</span><span class="sxs-lookup"><span data-stu-id="33a63-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="33a63-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="33a63-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="33a63-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="33a63-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="33a63-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="33a63-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="33a63-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="33a63-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-geographic/scale-geographic.sh "Geographic Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="33a63-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="33a63-110">Script explanation</span></span>

<span data-ttu-id="33a63-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, profilu Menedżera ruchu, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="33a63-111">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="33a63-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="33a63-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="33a63-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="33a63-113">Command</span></span> | <span data-ttu-id="33a63-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="33a63-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="33a63-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="33a63-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="33a63-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="33a63-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="33a63-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="33a63-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="33a63-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="33a63-118">Creates an App Service plan.</span></span> <span data-ttu-id="33a63-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33a63-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="33a63-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="33a63-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="33a63-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33a63-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="33a63-122">Utwórz profil Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="33a63-122">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="33a63-123">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="33a63-123">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="33a63-124">Tworzenie punktu końcowego Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="33a63-124">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="33a63-125">Dodaje tooan punktu końcowego profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="33a63-125">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="33a63-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33a63-126">Next steps</span></span>

<span data-ttu-id="33a63-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="33a63-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="33a63-128">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33a63-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
