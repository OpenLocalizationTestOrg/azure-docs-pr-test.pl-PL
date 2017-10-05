---
title: "Azure CLI przykładowym skrypcie - mapy niestandardową domenę do aplikacji funkcji | Dokumentacja firmy Microsoft"
description: "Przykład skryptu usługi Azure CLI — mapy niestandardową domenę do aplikacji funkcji na platformie Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a><span data-ttu-id="f72b7-103">Zamapować niestandardową domenę do aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="f72b7-103">Map a custom domain to a function app</span></span>

<span data-ttu-id="f72b7-104">Ten przykładowy skrypt tworzy aplikacji funkcji z powiązanych zasobów, a następnie mapuje `www.<yourdomain>` do niego.</span><span class="sxs-lookup"><span data-stu-id="f72b7-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` to it.</span></span> <span data-ttu-id="f72b7-105">Do mapowania na domenę niestandardową, należy utworzyć aplikacji funkcji w planie usługi aplikacji, a nie w planie zużycia.</span><span class="sxs-lookup"><span data-stu-id="f72b7-105">To map to a custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="f72b7-106">Środowisko Azure Functions obsługuje tylko mapowania domeny niestandardowej przy użyciu rekordu A.</span><span class="sxs-lookup"><span data-stu-id="f72b7-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f72b7-107">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f72b7-107">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f72b7-108">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="f72b7-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="f72b7-109">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f72b7-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="f72b7-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f72b7-110">Sample script</span></span>

<span data-ttu-id="f72b7-111">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "zamapować niestandardową domenę do aplikacji funkcji")]</span><span class="sxs-lookup"><span data-stu-id="f72b7-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a function app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f72b7-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f72b7-112">Script explanation</span></span>

<span data-ttu-id="f72b7-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="f72b7-113">This script uses the following commands.</span></span> <span data-ttu-id="f72b7-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="f72b7-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f72b7-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f72b7-115">Command</span></span> | <span data-ttu-id="f72b7-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f72b7-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f72b7-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f72b7-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f72b7-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f72b7-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f72b7-119">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="f72b7-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="f72b7-120">Tworzy wymagane przez aplikację funkcja konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f72b7-120">Creates a storage account required by the function app.</span></span> |
| [<span data-ttu-id="f72b7-121">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="f72b7-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f72b7-122">Tworzy plan usługi aplikacji potrzebne do mapowania domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="f72b7-122">Creates an App Service plan required to map a custom domain.</span></span> |
| [<span data-ttu-id="f72b7-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="f72b7-123">az functionapp create</span></span>]() | <span data-ttu-id="f72b7-124">Tworzy aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="f72b7-124">Creates a function app.</span></span> |
| [<span data-ttu-id="f72b7-125">Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="f72b7-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="f72b7-126">Mapuje domeny niestandardowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="f72b7-126">Maps a custom domain to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f72b7-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f72b7-127">Next steps</span></span>

<span data-ttu-id="f72b7-128">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f72b7-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f72b7-129">Dodatkowe przykłady skryptów funkcji interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="f72b7-129">Additional Functions CLI script samples can be found in the [Azure Functions documentation]().</span></span>
