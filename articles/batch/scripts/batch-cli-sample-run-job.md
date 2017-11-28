---
title: "Przykładowy skrypt interfejsu wiersza polecenia - uruchamiania zadania z instancją aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - uruchamiania zadania z partii"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="ed222-103">Uruchomione zadania w partii zadań Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ed222-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="ed222-104">Ten skrypt tworzy zadanie wsadowe i dodaje szereg zadań toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="ed222-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="ed222-105">Ponadto przedstawiono sposób toomonitor zadania i jego zadań.</span><span class="sxs-lookup"><span data-stu-id="ed222-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="ed222-106">Na koniec pokazuje, jak tooquery hello usługa partia zadań wydajnie uzyskać informacji o zadaniach hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ed222-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed222-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ed222-107">Prerequisites</span></span>

- <span data-ttu-id="ed222-108">Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="ed222-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="ed222-109">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ed222-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="ed222-110">Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="ed222-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="ed222-111">Jeśli nie zostało to jeszcze zrobione, należy skonfigurować toorun aplikacji z zadania uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="ed222-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="ed222-112">Zobacz [Dodawanie tooAzure aplikacji partii zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje tooAzure pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ed222-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="ed222-113">Skonfiguruj pulę, na które hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ed222-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="ed222-114">Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) przykładowego skryptu, który powoduje utworzenie puli z konfiguracji usługi chmury lub konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ed222-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ed222-115">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ed222-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="ed222-116">Oczyszczanie zadania</span><span class="sxs-lookup"><span data-stu-id="ed222-116">Clean up job</span></span>

<span data-ttu-id="ed222-117">Po uruchomieniu hello powyżej przykładowy skrypt uruchom następujące polecenie tooremove hello zadania i wszystkie jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="ed222-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="ed222-118">Należy zauważyć, że pula hello będzie toobe usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="ed222-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="ed222-119">Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](./batch-cli-sample-manage-pool.md) Aby uzyskać więcej informacji na temat tworzenia i usuwania pule.</span><span class="sxs-lookup"><span data-stu-id="ed222-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="ed222-120">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ed222-120">Script explanation</span></span>

<span data-ttu-id="ed222-121">Ten skrypt używa powitania po toocreate poleceń w trybie wsadowym i zadania.</span><span class="sxs-lookup"><span data-stu-id="ed222-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="ed222-122">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ed222-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ed222-123">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ed222-123">Command</span></span> | <span data-ttu-id="ed222-124">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ed222-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ed222-125">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="ed222-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="ed222-126">Uwierzytelnić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="ed222-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="ed222-127">Utwórz zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="ed222-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="ed222-128">Tworzy zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="ed222-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="ed222-129">Ustaw zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="ed222-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="ed222-130">Aktualizuje właściwości zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="ed222-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="ed222-131">Pokaż zadania wsadowego az</span><span class="sxs-lookup"><span data-stu-id="ed222-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="ed222-132">Pobiera szczegóły określone zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="ed222-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="ed222-133">Utwórz zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="ed222-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="ed222-134">Dodaje toohello zadań określony zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="ed222-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="ed222-135">Pokaż zadania wsadowego az</span><span class="sxs-lookup"><span data-stu-id="ed222-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="ed222-136">Pobiera hello szczegółów zadania z hello określone zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="ed222-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="ed222-137">Lista zadań wsadowych az</span><span class="sxs-lookup"><span data-stu-id="ed222-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="ed222-138">Zawiera listę zadań hello skojarzone z hello określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="ed222-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ed222-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ed222-139">Next steps</span></span>

<span data-ttu-id="ed222-140">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed222-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ed222-141">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ed222-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
