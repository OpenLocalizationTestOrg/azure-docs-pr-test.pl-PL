---
title: "Tworzenie funkcji platformy Azure, umożliwiająca nawiązanie połączenia usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie funkcji platformy Azure, łączącego się z magazynem Azure"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="542c2-103">Integrowanie aplikacji funkcji kontem magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="542c2-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="542c2-104">Ten przykładowy skrypt tworzy aplikację funkcji oraz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="542c2-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="542c2-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="542c2-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="542c2-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="542c2-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="542c2-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="542c2-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="542c2-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="542c2-108">Sample script</span></span>

<span data-ttu-id="542c2-109">Ten przykład tworzy aplikację funkcji platformy Azure i dodaje parametry połączenia magazynu do ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="542c2-109">This sample creates an Azure Function app and adds the storage connection string to an app setting.</span></span>

<span data-ttu-id="542c2-110">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "integracji aplikacji funkcji do konta magazynu Azure")]</span><span class="sxs-lookup"><span data-stu-id="542c2-110">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="542c2-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="542c2-111">Clean up deployment</span></span>

<span data-ttu-id="542c2-112">Po uruchomieniu przykładowym skrypcie następujące polecenie służy do usunięcia grupy zasobów, aplikacji usługi app Service i wszystkie powiązane zasoby:</span><span class="sxs-lookup"><span data-stu-id="542c2-112">After the script sample has been run, the following command can be used to remove the resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="542c2-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="542c2-113">Script explanation</span></span>

<span data-ttu-id="542c2-114">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="542c2-114">This script uses the following commands.</span></span> <span data-ttu-id="542c2-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="542c2-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="542c2-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="542c2-116">Command</span></span> | <span data-ttu-id="542c2-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="542c2-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="542c2-118">AZ logowania</span><span class="sxs-lookup"><span data-stu-id="542c2-118">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="542c2-119">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="542c2-119">Login to Azure.</span></span> |
| [<span data-ttu-id="542c2-120">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="542c2-120">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="542c2-121">Utwórz grupę zasobów z lokalizacji</span><span class="sxs-lookup"><span data-stu-id="542c2-121">Create a resource group with location</span></span> |
| [<span data-ttu-id="542c2-122">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="542c2-122">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="542c2-123">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="542c2-123">Create a storage account</span></span> |
| [<span data-ttu-id="542c2-124">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="542c2-124">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="542c2-125">Utwórz nową aplikację funkcji</span><span class="sxs-lookup"><span data-stu-id="542c2-125">Create a new function app</span></span> |
| [<span data-ttu-id="542c2-126">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="542c2-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="542c2-127">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="542c2-127">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="542c2-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="542c2-128">Next steps</span></span>

<span data-ttu-id="542c2-129">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="542c2-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="542c2-130">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="542c2-130">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
