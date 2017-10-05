---
title: "Azure CLI skrypt przykładowy — Dodawanie aplikacji w partii | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Dodawanie aplikacji w partii"
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
ms.openlocfilehash: 5d057eaf32867aedc95d58c5185e2be1f9385ec0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="adding-applications-to-azure-batch-with-azure-cli"></a><span data-ttu-id="d84d2-103">Dodawanie aplikacji do partii zadań Azure z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d84d2-103">Adding applications to Azure Batch with Azure CLI</span></span>

<span data-ttu-id="d84d2-104">Ten skrypt pokazuje, jak skonfigurować aplikację do użycia z puli partii zadań Azure lub zadania.</span><span class="sxs-lookup"><span data-stu-id="d84d2-104">This script demonstrates how to set up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="d84d2-105">Aby skonfigurować aplikację, pakiet pliku wykonywalnego, oraz wszelkie zależności, do pliku zip.</span><span class="sxs-lookup"><span data-stu-id="d84d2-105">To set up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="d84d2-106">W tym przykładzie nosi nazwę pliku wykonywalnego zip "Mój-aplikacji-exe.zip".</span><span class="sxs-lookup"><span data-stu-id="d84d2-106">In this example the executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d84d2-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d84d2-107">Prerequisites</span></span>

- <span data-ttu-id="d84d2-108">Zainstaluj interfejs wiersza polecenia platformy Azure przy użyciu instrukcji w [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="d84d2-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="d84d2-109">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d84d2-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="d84d2-110">Zobacz [Tworzenie konta usługi partia zadań z wiersza polecenia platformy Azure](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="d84d2-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d84d2-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d84d2-111">Sample script</span></span>

<span data-ttu-id="d84d2-112">[!code-azurecli[główne](../../../cli_scripts/batch/add-application/add-application.sh "Dodawanie aplikacji")]</span><span class="sxs-lookup"><span data-stu-id="d84d2-112">[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]</span></span>

## <a name="clean-up-application"></a><span data-ttu-id="d84d2-113">Oczyszczanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="d84d2-113">Clean up application</span></span>

<span data-ttu-id="d84d2-114">Po uruchomieniu powyższy skrypt przykładowy należy uruchomić następujące polecenia, aby usunąć aplikację i wszystkie jego pakietów przekazano aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d84d2-114">After you run the above sample script, run the following commands to remove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d84d2-115">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d84d2-115">Script explanation</span></span>

<span data-ttu-id="d84d2-116">Ten skrypt używa następujących poleceń do tworzenia aplikacji i przekaż pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d84d2-116">This script uses the following commands to create an application and upload an application package.</span></span>
<span data-ttu-id="d84d2-117">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="d84d2-117">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d84d2-118">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d84d2-118">Command</span></span> | <span data-ttu-id="d84d2-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d84d2-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d84d2-120">Tworzenie aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="d84d2-120">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="d84d2-121">Tworzy aplikację.</span><span class="sxs-lookup"><span data-stu-id="d84d2-121">Creates an application.</span></span>  |
| [<span data-ttu-id="d84d2-122">zestaw aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="d84d2-122">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="d84d2-123">Aktualizuje właściwości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d84d2-123">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="d84d2-124">Utwórz pakiet aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="d84d2-124">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="d84d2-125">Dodaje pakiet aplikacji dla określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d84d2-125">Adds an application package to the specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="d84d2-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d84d2-126">Next steps</span></span>

<span data-ttu-id="d84d2-127">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d84d2-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d84d2-128">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d84d2-128">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
