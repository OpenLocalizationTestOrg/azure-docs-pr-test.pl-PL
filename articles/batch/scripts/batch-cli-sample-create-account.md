---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz konto wsadowe | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a><span data-ttu-id="fd208-103">Tworzenie konta usługi partia zadań z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd208-103">Create a Batch account with hello Azure CLI</span></span>

<span data-ttu-id="fd208-104">Ten skrypt tworzy konto partii zadań Azure i przedstawia różne właściwości konta hello można zbadać i aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="fd208-104">This script creates an Azure Batch account and shows how various properties of hello account can be queried and updated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd208-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd208-105">Prerequisites</span></span>

<span data-ttu-id="fd208-106">Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="fd208-106">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>

## <a name="batch-account-sample-script"></a><span data-ttu-id="fd208-107">Skrypt przykładowy konta</span><span class="sxs-lookup"><span data-stu-id="fd208-107">Batch account sample script</span></span>

<span data-ttu-id="fd208-108">Podczas tworzenia konta usługi partia zadań domyślnie jego węzły obliczeniowe są przypisywane wewnętrznie przez hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="fd208-108">When you create a Batch account, by default its compute nodes are assigned internally by hello Batch service.</span></span> <span data-ttu-id="fd208-109">Węzły obliczeniowe przydzielone będzie limit przydziału rdzeni oddzielnych tooa podmiotu i hello konta mogą być uwierzytelniane za pośrednictwem klucza wspólnego poświadczeń lub Azure Active Dirctory token.</span><span class="sxs-lookup"><span data-stu-id="fd208-109">Allocated compute nodes will be subject tooa separate core quota and hello account can be authenticated either via Shared Key credentials or an Azure Active Dirctory token.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a><span data-ttu-id="fd208-110">Przy użyciu skryptu próbki subskrypcji użytkownika konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="fd208-110">Batch account using user subscription sample script</span></span>

<span data-ttu-id="fd208-111">Można również włączyć toohave partii utworzyć jego węzłów obliczeniowych w ramach własnej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd208-111">You can also opt toohave Batch create its compute nodes in your own Azure subscription.</span></span>
<span data-ttu-id="fd208-112">Konta, które przydzielić obliczeniowe węzłów w ramach subskrypcji, musi zostać uwierzytelniony za pośrednictwem tokenu programu Azure Active Directory i węzły obliczeniowe hello przydzielone są zliczane limitu przydziału subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="fd208-112">Accounts that allocate compute nodes into your subscription must be authenticated via an Azure Active Directory token and hello compute nodes allocated will count towards your subscription quota.</span></span> <span data-ttu-id="fd208-113">toocreate konto w tym trybie, co należy określić odwołanie Key Vault podczas tworzenia konta hello.</span><span class="sxs-lookup"><span data-stu-id="fd208-113">toocreate an account in this mode, one must specify a Key Vault reference when creating hello account.</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fd208-114">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="fd208-114">Clean up deployment</span></span>

<span data-ttu-id="fd208-115">Po uruchomieniu albo hello powyżej przykładowe skrypty, uruchom następujące polecenie tooremove hello grupy zasobów i wszystkie powiązane zasoby (w tym konta wsadowego, konta usługi Azure Storage i Azure magazynów kluczy).</span><span class="sxs-lookup"><span data-stu-id="fd208-115">After you run either of hello above sample scripts, run hello following command tooremove the resource group and all related resources (including Batch accounts, Azure Storage accounts and Azure key vaults).</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fd208-116">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="fd208-116">Script explanation</span></span>

<span data-ttu-id="fd208-117">Ten skrypt używa hello następujące polecenia toocreate grupy zasobów konta usługi partia zadań i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="fd208-117">This script uses hello following commands toocreate a resource group, Batch account, and all related resources.</span></span> <span data-ttu-id="fd208-118">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="fd208-118">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="fd208-119">Polecenie</span><span class="sxs-lookup"><span data-stu-id="fd208-119">Command</span></span> | <span data-ttu-id="fd208-120">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fd208-120">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd208-121">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="fd208-121">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fd208-122">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="fd208-122">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd208-123">Tworzenie konta usługi partia zadań az</span><span class="sxs-lookup"><span data-stu-id="fd208-123">az batch account create</span></span>](https://docs.microsoft.com/cli/azure/batch/account#create) | <span data-ttu-id="fd208-124">Tworzy hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="fd208-124">Creates hello Batch account.</span></span>  |
| [<span data-ttu-id="fd208-125">Ustaw konto wsadowe az</span><span class="sxs-lookup"><span data-stu-id="fd208-125">az batch account set</span></span>](https://docs.microsoft.com/cli/azure/batch/account#set) | <span data-ttu-id="fd208-126">Aktualizuje właściwości hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="fd208-126">Updates properties of hello Batch account.</span></span>  |
| [<span data-ttu-id="fd208-127">Pokaż konto wsadowe az</span><span class="sxs-lookup"><span data-stu-id="fd208-127">az batch account show</span></span>](https://docs.microsoft.com/cli/azure/batch/account#show) | <span data-ttu-id="fd208-128">Pobiera szczegóły hello określić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="fd208-128">Retrieves details of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="fd208-129">Lista kluczy konta zadań wsadowych az</span><span class="sxs-lookup"><span data-stu-id="fd208-129">az batch account keys list</span></span>](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | <span data-ttu-id="fd208-130">Pobiera klucze dostępu hello hello określić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="fd208-130">Retrieves hello access keys of hello specified Batch account.</span></span>  |
| [<span data-ttu-id="fd208-131">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="fd208-131">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="fd208-132">Uwierzytelnia określony hello partii konta dla dalszego interakcja interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fd208-132">Authenticates against hello specified Batch account for further CLI interaction.</span></span>  |
| [<span data-ttu-id="fd208-133">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="fd208-133">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account#create) | <span data-ttu-id="fd208-134">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd208-134">Creates a storage account.</span></span> |
| [<span data-ttu-id="fd208-135">Utwórz az keyvault</span><span class="sxs-lookup"><span data-stu-id="fd208-135">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="fd208-136">Tworzy magazyn kluczy.</span><span class="sxs-lookup"><span data-stu-id="fd208-136">Creates a key vault.</span></span> |
| [<span data-ttu-id="fd208-137">keyvault az set-policy.</span><span class="sxs-lookup"><span data-stu-id="fd208-137">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="fd208-138">Zaktualizuj zasady zabezpieczeń hello hello określonego klucza magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd208-138">Update hello security policy of hello specified key vault.</span></span> |
| [<span data-ttu-id="fd208-139">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="fd208-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="fd208-140">Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="fd208-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd208-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd208-141">Next steps</span></span>

<span data-ttu-id="fd208-142">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fd208-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fd208-143">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fd208-143">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
