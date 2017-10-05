---
title: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 50d69ac48438920ce59808ee79809235d8330b14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="f40a8-103">Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="f40a8-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="f40a8-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web w lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="f40a8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f40a8-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f40a8-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f40a8-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="f40a8-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="f40a8-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f40a8-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f40a8-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f40a8-108">Sample script</span></span>

<span data-ttu-id="f40a8-109">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git")]</span><span class="sxs-lookup"><span data-stu-id="f40a8-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f40a8-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f40a8-110">Script explanation</span></span>

<span data-ttu-id="f40a8-111">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="f40a8-111">This script uses the following commands.</span></span> <span data-ttu-id="f40a8-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f40a8-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f40a8-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f40a8-113">Command</span></span> | <span data-ttu-id="f40a8-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f40a8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f40a8-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f40a8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f40a8-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f40a8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f40a8-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="f40a8-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f40a8-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f40a8-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f40a8-119">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="f40a8-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f40a8-120">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f40a8-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f40a8-121">ustawiono użytkownika wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="f40a8-121">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="f40a8-122">Ustawia poświadczenia konta poziomu wdrożenia dla aplikacji usługi.</span><span class="sxs-lookup"><span data-stu-id="f40a8-122">Sets the account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="f40a8-123">Źródło wdrożenia az aplikacji sieci Web — config lokalnej — git</span><span class="sxs-lookup"><span data-stu-id="f40a8-123">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="f40a8-124">Tworzy konfiguracji kontroli źródła dla lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="f40a8-124">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="f40a8-125">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="f40a8-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="f40a8-126">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="f40a8-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f40a8-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f40a8-127">Next steps</span></span>

<span data-ttu-id="f40a8-128">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f40a8-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f40a8-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f40a8-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
