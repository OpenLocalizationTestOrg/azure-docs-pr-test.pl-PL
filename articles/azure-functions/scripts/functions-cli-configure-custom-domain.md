---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - mapowania aplikacji funkcji tooa domeny niestandardowej | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie usługi Azure CLI - mapy aplikacji funkcji tooa niestandardową domenę na platformie Azure."
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a><span data-ttu-id="d0758-103">Mapa aplikacji funkcji tooa domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="d0758-103">Map a custom domain tooa function app</span></span>

<span data-ttu-id="d0758-104">Ten przykładowy skrypt tworzy aplikacji funkcji z powiązanych zasobów, a następnie mapuje `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="d0758-104">This sample script creates a function app with related resources, and then maps `www.<yourdomain>` tooit.</span></span> <span data-ttu-id="d0758-105">toomap tooa domeny niestandardowej, w planie usługi aplikacji, a nie w planie zużycia, należy utworzyć aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0758-105">toomap tooa custom domain, your function app must be created in an App Service plan and not in a consumption plan.</span></span> <span data-ttu-id="d0758-106">Środowisko Azure Functions obsługuje tylko mapowania domeny niestandardowej przy użyciu rekordu A.</span><span class="sxs-lookup"><span data-stu-id="d0758-106">Azure Functions only supports mapping a custom domain using an A record.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d0758-107">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d0758-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d0758-108">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="d0758-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d0758-109">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d0758-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="d0758-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d0758-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d0758-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d0758-111">Script explanation</span></span>

<span data-ttu-id="d0758-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="d0758-112">This script uses hello following commands.</span></span> <span data-ttu-id="d0758-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d0758-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d0758-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d0758-114">Command</span></span> | <span data-ttu-id="d0758-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d0758-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d0758-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d0758-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d0758-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d0758-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d0758-118">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="d0758-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d0758-119">Tworzy wymagane przez aplikację funkcji hello konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="d0758-119">Creates a storage account required by hello function app.</span></span> |
| [<span data-ttu-id="d0758-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="d0758-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="d0758-121">Tworzy niestandardową domenę toomap wymagane planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d0758-121">Creates an App Service plan required toomap a custom domain.</span></span> |
| [<span data-ttu-id="d0758-122">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="d0758-122">az functionapp create</span></span>]() | <span data-ttu-id="d0758-123">Tworzy aplikację funkcji.</span><span class="sxs-lookup"><span data-stu-id="d0758-123">Creates a function app.</span></span> |
| [<span data-ttu-id="d0758-124">Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta</span><span class="sxs-lookup"><span data-stu-id="d0758-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="d0758-125">Mapuje aplikacji funkcji tooa domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="d0758-125">Maps a custom domain tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d0758-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0758-126">Next steps</span></span>

<span data-ttu-id="d0758-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d0758-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d0758-128">Dodatkowe przykłady skryptów funkcji interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure Functions]().</span><span class="sxs-lookup"><span data-stu-id="d0758-128">Additional Functions CLI script samples can be found in hello [Azure Functions documentation]().</span></span>
