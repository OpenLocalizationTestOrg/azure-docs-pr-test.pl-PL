---
title: "Azure CLI skrypt przykładowy — Tworzenie konta usługi partia zadań | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie konta usługi partia zadań"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a><span data-ttu-id="5bd46-103">Tworzenie konta usługi partia zadań z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5bd46-103">Create a Batch account with the Azure CLI</span></span>

<span data-ttu-id="5bd46-104">Ten skrypt tworzy konto partii zadań Azure i pokazuje, jak różne właściwości konta można zbadać i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="5bd46-104">This script creates an Azure Batch account and shows how various properties of the account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bd46-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5bd46-105">Prerequisites</span></span>

<span data-ttu-id="5bd46-106">Zainstaluj interfejs wiersza polecenia platformy Azure przy użyciu instrukcji w [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="5bd46-106">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="5bd46-107">Skrypt przykładowy konta</span><span class="sxs-lookup"><span data-stu-id="5bd46-107">Batch account sample script</span></span>

<span data-ttu-id="5bd46-108">Podczas tworzenia konta usługi partia zadań domyślnie jego węzły obliczeniowe są przypisywane wewnętrznie przez usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="5bd46-108">When you create a Batch account, by default its compute nodes are assigned internally by the Batch service.</span></span> <span data-ttu-id="5bd46-109">Węzły obliczeniowe przydzielone podlegają przydziału rdzeni oddzielne i konta mogą być uwierzytelniane za pośrednictwem klucza wspólnego poświadczeń lub Azure Active Dirctory token.</span><span class="sxs-lookup"><span data-stu-id="5bd46-109">Allocated compute nodes will be subject to a separate core quota and the account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

<span data-ttu-id="5bd46-110">[!code-azurecli[główne](../../../cli_scripts/batch/create-account/create-account.sh "Tworzenie konta")]</span><span class="sxs-lookup"><span data-stu-id="5bd46-110">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]</span></span>

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="5bd46-111">Przy użyciu skryptu próbki subskrypcji użytkownika konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="5bd46-111">Batch account using user subscription sample script</span></span>

<span data-ttu-id="5bd46-112">Można również zdecydować się na ma partii utworzyć jego węzłów obliczeniowych w ramach własnej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5bd46-112">You can also opt to have Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="5bd46-113">Konta, które przydzielić obliczeniowe węzłów w ramach subskrypcji, musi zostać uwierzytelniony za pośrednictwem tokenu programu Azure Active Directory i węzły obliczeniowe przydzielone są zliczane limitu przydziału subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="5bd46-113">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and the compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="5bd46-114">Aby utworzyć konto w tym trybie, jeden Określ odwołanie magazynu kluczy podczas tworzenia konta.</span><span class="sxs-lookup"><span data-stu-id="5bd46-114">To create an account in this mode, one must specify a Key Vault reference when creating the account.</span></span>

<span data-ttu-id="5bd46-115">[!code-azurecli[główne](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Utwórz konto, przy użyciu subskrypcji użytkownika")]</span><span class="sxs-lookup"><span data-stu-id="5bd46-115">[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5bd46-116">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="5bd46-116">Clean up deployment</span></span>

<span data-ttu-id="5bd46-117">Po uruchomieniu dowolnego z powyższych przykładowe skrypty, uruchom następujące polecenie, aby usunąć grupę zasobów i wszystkie powiązane zasoby (w tym konta wsadowego, konta usługi Azure Storage i Azure magazynów kluczy).</span><span class="sxs-lookup"><span data-stu-id="5bd46-117">After you run either of the above sample scripts, run the following command to remove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5bd46-118">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5bd46-118">Script explanation</span></span>

<span data-ttu-id="5bd46-119">Ten skrypt używa następujących poleceń w celu utworzenia grupy zasobów konta usługi partia zadań i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="5bd46-119">This script uses the following commands to create a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="5bd46-120">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="5bd46-120">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="5bd46-121">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5bd46-121">Command</span></span> | <span data-ttu-id="5bd46-122">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5bd46-122">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5bd46-123">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="5bd46-123">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5bd46-124">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5bd46-124">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5bd46-125">Tworzenie konta usługi partia zadań az</span><span class="sxs-lookup"><span data-stu-id="5bd46-125">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="5bd46-126">Tworzy konto usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="5bd46-126">Creates the Batch account.</span></span>  |
| [<span data-ttu-id="5bd46-127">Ustaw konto wsadowe az</span><span class="sxs-lookup"><span data-stu-id="5bd46-127">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="5bd46-128">Aktualizuje właściwości konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="5bd46-128">Updates properties of the Batch account.</span></span>  |
| [<span data-ttu-id="5bd46-129">Pokaż konto wsadowe az</span><span class="sxs-lookup"><span data-stu-id="5bd46-129">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="5bd46-130">Pobiera szczegóły określonego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="5bd46-130">Retrieves details of the specified Batch account.</span></span>  |
| [<span data-ttu-id="5bd46-131">Lista kluczy konta zadań wsadowych az</span><span class="sxs-lookup"><span data-stu-id="5bd46-131">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="5bd46-132">Pobiera klucze dostępu do określonego konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="5bd46-132">Retrieves the access keys of the specified Batch account.</span></span>  |
| [<span data-ttu-id="5bd46-133">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="5bd46-133">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="5bd46-134">Uwierzytelnia określony konta usługi partia zadań dla dalszego interakcja interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="5bd46-134">Authenticates against the specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="5bd46-135">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="5bd46-135">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="5bd46-136">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="5bd46-136">Creates a storage account.</span></span> |
| [<span data-ttu-id="5bd46-137">Utwórz az keyvault</span><span class="sxs-lookup"><span data-stu-id="5bd46-137">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="5bd46-138">Tworzy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="5bd46-138">Creates a key vault.</span></span> |
| [<span data-ttu-id="5bd46-139">keyvault az set-policy.</span><span class="sxs-lookup"><span data-stu-id="5bd46-139">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="5bd46-140">Aktualizacja zasad zabezpieczeń określonego magazynu kluczy.</span><span class="sxs-lookup"><span data-stu-id="5bd46-140">Update the security policy of the specified key vault.</span></span> |
| [<span data-ttu-id="5bd46-141">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="5bd46-141">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="5bd46-142">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5bd46-142">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5bd46-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5bd46-143">Next steps</span></span>

<span data-ttu-id="5bd46-144">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5bd46-144">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5bd46-145">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5bd46-145">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
