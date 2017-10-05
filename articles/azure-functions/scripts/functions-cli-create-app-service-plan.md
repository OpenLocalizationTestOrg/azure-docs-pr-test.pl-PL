---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcji w planie usługi aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 40c3fa6fa6c07d59e4bf55531e116ba50aa92b91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-in-an-app-service-plan"></a><span data-ttu-id="d4b2d-103">Tworzenie aplikacji funkcji w planie usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="d4b2d-103">Create a Function App in an App Service plan</span></span>

<span data-ttu-id="d4b2d-104">Ten przykładowy skrypt tworzy aplikację funkcji Azure to kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="d4b2d-105">Funkcja aplikacji jest tworzony przy użyciu dedykowanych planu usługi aplikacji, co oznacza, że zasoby serwera są zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-105">The Function App is created using a dedicated App Service plan, which means your server resources are always on.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d4b2d-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d4b2d-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="d4b2d-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d4b2d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d4b2d-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d4b2d-109">Sample script</span></span>

<span data-ttu-id="d4b2d-110">Ten skrypt tworzy aplikacji funkcji platformy Azure za pomocą dedykowanego [planu usługi aplikacji](../functions-scale.md#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="d4b2d-110">This script creates an Azure Function app using a dedicated [App Service plan](../functions-scale.md#app-service-plan).</span></span>

<span data-ttu-id="d4b2d-111">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Tworzenie funkcji platformy Azure na plan usługi aplikacji")]</span><span class="sxs-lookup"><span data-stu-id="d4b2d-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-app-service-plan/create-function-app-app-service-plan.sh "Create an Azure Function on an App Service plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="d4b2d-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d4b2d-112">Script explanation</span></span>

<span data-ttu-id="d4b2d-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="d4b2d-114">Ten skrypt używa następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="d4b2d-114">This script uses the following commands:</span></span>

| <span data-ttu-id="d4b2d-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d4b2d-115">Command</span></span> | <span data-ttu-id="d4b2d-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d4b2d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4b2d-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="d4b2d-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d4b2d-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4b2d-119">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="d4b2d-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="d4b2d-120">Tworzy konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="d4b2d-121">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="d4b2d-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appserviceplan#create) | <span data-ttu-id="d4b2d-122">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d4b2d-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="d4b2d-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#delete) | <span data-ttu-id="d4b2d-124">Tworzy aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4b2d-124">Creates an Azure Function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4b2d-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4b2d-125">Next steps</span></span>

<span data-ttu-id="d4b2d-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4b2d-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d4b2d-127">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d4b2d-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
