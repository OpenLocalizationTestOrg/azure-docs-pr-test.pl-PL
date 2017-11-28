---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcja do wykonania niekorzystającą | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcja do wykonania bez serwera"
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
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="b3333-103">Tworzenie aplikacji funkcja do wykonania bez serwera</span><span class="sxs-lookup"><span data-stu-id="b3333-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="b3333-104">Ten przykładowy skrypt tworzy aplikację funkcji Azure to kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3333-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="b3333-105">Funkcja aplikacji jest tworzony przy użyciu [planu zużycia](../functions-scale.md#consumption-plan), który jest odpowiedni dla obciążeń niekorzystającą sterowane zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="b3333-105">The Function App is created using the [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b3333-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b3333-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b3333-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="b3333-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="b3333-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b3333-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b3333-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b3333-109">Sample script</span></span>

<span data-ttu-id="b3333-110">Ten skrypt tworzy aplikacji funkcji platformy Azure przy użyciu [planu zużycie](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="b3333-110">This script creates an Azure Function app using the [consumption plan](../functions-scale.md#consumption-plan).</span></span>

<span data-ttu-id="b3333-111">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Tworzenie funkcji platformy Azure w planie zużycie")]</span><span class="sxs-lookup"><span data-stu-id="b3333-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b3333-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b3333-112">Script explanation</span></span>

<span data-ttu-id="b3333-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b3333-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="b3333-114">Ten skrypt używa następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="b3333-114">This script uses the following commands:</span></span>

| <span data-ttu-id="b3333-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b3333-115">Command</span></span> | <span data-ttu-id="b3333-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b3333-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b3333-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="b3333-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b3333-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b3333-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b3333-119">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="b3333-119">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="b3333-120">Tworzy konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="b3333-120">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="b3333-121">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="b3333-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="b3333-122">Tworzy funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b3333-122">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b3333-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3333-123">Next steps</span></span>

<span data-ttu-id="b3333-124">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b3333-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b3333-125">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b3333-125">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
