---
title: "Azure CLI przykładowym skrypcie - uruchamiania zadania z instancją | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="db77d-103">Uruchomione zadania w partii zadań Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="db77d-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="db77d-104">Ten skrypt tworzy zadanie wsadowe i dodaje sekwencję zadań do zadania.</span><span class="sxs-lookup"><span data-stu-id="db77d-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="db77d-105">On również pokazano, jak monitorować zadania i jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="db77d-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="db77d-106">Na koniec widoczny jest sposób zapytania wydajnie uzyskać informacji o zadaniach zadania usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="db77d-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db77d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="db77d-107">Prerequisites</span></span>

- <span data-ttu-id="db77d-108">Zainstaluj interfejs wiersza polecenia platformy Azure przy użyciu instrukcji w [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="db77d-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="db77d-109">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="db77d-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="db77d-110">Zobacz [Tworzenie konta usługi partia zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="db77d-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="db77d-111">Skonfigurować aplikację do uruchamiania z zadania uruchamiania, jeśli nie zostało to jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="db77d-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="db77d-112">Zobacz [Dodawanie aplikacji do partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) przykładowego skryptu, który tworzy aplikację i przekazuje pakietu aplikacji do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="db77d-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="db77d-113">Skonfiguruj pulę, w którym zadanie zostanie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="db77d-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="db77d-114">Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) przykładowego skryptu, który powoduje utworzenie puli z konfiguracji usługi chmury lub konfiguracji maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="db77d-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="db77d-115">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="db77d-115">Sample script</span></span>

<span data-ttu-id="db77d-116">[!code-azurecli[główne](../../../cli_scripts/batch/run-job/run-job.sh "uruchamiania zadania")]</span><span class="sxs-lookup"><span data-stu-id="db77d-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="db77d-117">Oczyszczanie zadania</span><span class="sxs-lookup"><span data-stu-id="db77d-117">Clean up job</span></span>

<span data-ttu-id="db77d-118">Po uruchomieniu powyższy skrypt przykładowy należy uruchomić następujące polecenie, aby usunąć zadania i wszystkie jego zadań podrzędnych.</span><span class="sxs-lookup"><span data-stu-id="db77d-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="db77d-119">Należy pamiętać, że pula będzie trzeba usunąć oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="db77d-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="db77d-120">Zobacz [pule Zarządzanie partii zadań Azure z wiersza polecenia platformy Azure](./batch-cli-sample-manage-pool.md) Aby uzyskać więcej informacji na temat tworzenia i usuwania pule.</span><span class="sxs-lookup"><span data-stu-id="db77d-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="db77d-121">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="db77d-121">Script explanation</span></span>

<span data-ttu-id="db77d-122">Ten skrypt używa następujących poleceń do utworzenia zadania wsadowego i zadania.</span><span class="sxs-lookup"><span data-stu-id="db77d-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="db77d-123">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="db77d-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="db77d-124">Polecenie</span><span class="sxs-lookup"><span data-stu-id="db77d-124">Command</span></span> | <span data-ttu-id="db77d-125">Uwagi</span><span class="sxs-lookup"><span data-stu-id="db77d-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="db77d-126">AZ logowanie się na koncie usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="db77d-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="db77d-127">Uwierzytelnić konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="db77d-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="db77d-128">Utwórz zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="db77d-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="db77d-129">Tworzy zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="db77d-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="db77d-130">Ustaw zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="db77d-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="db77d-131">Aktualizuje właściwości zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="db77d-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="db77d-132">Pokaż zadania wsadowego az</span><span class="sxs-lookup"><span data-stu-id="db77d-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="db77d-133">Pobiera szczegóły określone zadanie wsadowe.</span><span class="sxs-lookup"><span data-stu-id="db77d-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="db77d-134">Utwórz zadanie wsadowe az</span><span class="sxs-lookup"><span data-stu-id="db77d-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="db77d-135">Dodaje zadanie do określonego zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="db77d-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="db77d-136">Pokaż zadania wsadowego az</span><span class="sxs-lookup"><span data-stu-id="db77d-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="db77d-137">Pobiera szczegóły zadania z określonego zadania wsadowego.</span><span class="sxs-lookup"><span data-stu-id="db77d-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="db77d-138">Lista zadań wsadowych az</span><span class="sxs-lookup"><span data-stu-id="db77d-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="db77d-139">Zawiera listę zadań skojarzonych z określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="db77d-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="db77d-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="db77d-140">Next steps</span></span>

<span data-ttu-id="db77d-141">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="db77d-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="db77d-142">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="db77d-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
