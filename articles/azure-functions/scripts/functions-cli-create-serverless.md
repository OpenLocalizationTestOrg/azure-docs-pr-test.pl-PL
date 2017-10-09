---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji funkcja do wykonania niekorzystającą | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a><span data-ttu-id="7c45f-103">Tworzenie aplikacji funkcja do wykonania bez serwera</span><span class="sxs-lookup"><span data-stu-id="7c45f-103">Create a Function App for serverless execution</span></span>

<span data-ttu-id="7c45f-104">Ten przykładowy skrypt tworzy aplikację funkcji Azure to kontener dla funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c45f-104">This sample script creates an Azure Function App, which is a container for your functions.</span></span> <span data-ttu-id="7c45f-105">Witaj aplikacji funkcji jest tworzony przy użyciu hello [planu zużycia](../functions-scale.md#consumption-plan), który jest odpowiedni dla obciążeń niekorzystającą sterowane zdarzeniami.</span><span class="sxs-lookup"><span data-stu-id="7c45f-105">hello Function App is created using hello [consumption plan](../functions-scale.md#consumption-plan), which is ideal for event-driven serverless workloads.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7c45f-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="7c45f-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="7c45f-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="7c45f-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7c45f-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7c45f-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="7c45f-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="7c45f-109">Sample script</span></span>

<span data-ttu-id="7c45f-110">Ten skrypt tworzy aplikacji funkcji platformy Azure za pomocą hello [planu zużycie](../functions-scale.md#consumption-plan).</span><span class="sxs-lookup"><span data-stu-id="7c45f-110">This script creates an Azure Function app using hello [consumption plan](../functions-scale.md#consumption-plan).</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="7c45f-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="7c45f-111">Script explanation</span></span>

<span data-ttu-id="7c45f-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="7c45f-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="7c45f-113">Ten skrypt używa hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7c45f-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="7c45f-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="7c45f-114">Command</span></span> | <span data-ttu-id="7c45f-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7c45f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c45f-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="7c45f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7c45f-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="7c45f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c45f-118">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="7c45f-118">az storage account create</span></span>](/cli/azure/storage/account#create) | <span data-ttu-id="7c45f-119">Tworzy konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="7c45f-119">Creates an Azure Storage account.</span></span> |
| [<span data-ttu-id="7c45f-120">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="7c45f-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="7c45f-121">Tworzy funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c45f-121">Creates an Azure Function.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c45f-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c45f-122">Next steps</span></span>

<span data-ttu-id="7c45f-123">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c45f-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7c45f-124">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7c45f-124">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
