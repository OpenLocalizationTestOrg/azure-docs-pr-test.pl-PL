---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji funkcji w planie usługi aplikacji | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcji w planie usługi aplikacji"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: c0ffbbbf022e5680e5ae3141e784e7c7bced0bc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="6c12e-103">Tworzenie aplikacji funkcji w planie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c12e-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="6c12e-104">Ten przykładowy skrypt tworzy aplikację funkcji Azure to kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="6c12e-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="6c12e-105">Funkcja aplikacji Hello jest tworzony przy użyciu dedykowanych planu usługi aplikacji, co oznacza, że zasoby serwera są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="6c12e-105">hello Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c12e-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6c12e-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6c12e-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6c12e-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6c12e-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6c12e-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6c12e-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6c12e-109">Sample script</span></span>

<span data-ttu-id="6c12e-110">Ten skrypt tworzy aplikacji funkcji platformy Azure za pomocą dedykowanego [planu usługi aplikacji](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="6c12e-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6c12e-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6c12e-111">Script explanation</span></span>

<span data-ttu-id="6c12e-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6c12e-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="6c12e-113">Ten skrypt używa hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6c12e-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="6c12e-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6c12e-114">Command</span></span> | <span data-ttu-id="6c12e-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6c12e-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c12e-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6c12e-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c12e-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6c12e-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c12e-118">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="6c12e-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="6c12e-119">Tworzy konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c12e-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="6c12e-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="6c12e-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="6c12e-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6c12e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6c12e-122">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="6c12e-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="6c12e-123">Tworzy aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c12e-123">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c12e-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c12e-124">Next steps</span></span>

<span data-ttu-id="6c12e-125">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c12e-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c12e-126">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c12e-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
