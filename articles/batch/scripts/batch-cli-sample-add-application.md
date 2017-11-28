---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Dodawanie aplikacji w partii | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a><span data-ttu-id="ee38d-103">Dodawanie aplikacji tooAzure partii zadań z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ee38d-103">Adding applications tooAzure Batch with Azure CLI</span></span>

<span data-ttu-id="ee38d-104">Ten skrypt pokazuje, jak tooset aplikacji do użycia z puli partii zadań Azure lub zadania.</span><span class="sxs-lookup"><span data-stu-id="ee38d-104">This script demonstrates how tooset up an application for use with an Azure Batch pool or task.</span></span> <span data-ttu-id="ee38d-105">tooset aplikacji, pakietu pliku wykonywalnego, oraz wszelkie zależności, do pliku zip.</span><span class="sxs-lookup"><span data-stu-id="ee38d-105">tooset up an application, package your executable, together with any dependencies, into a .zip file.</span></span> <span data-ttu-id="ee38d-106">W zip pliku wykonywalnego hello przykład pliku o nazwie "Mój-aplikacji-exe.zip".</span><span class="sxs-lookup"><span data-stu-id="ee38d-106">In this example hello executable zip file is called 'my-application-exe.zip'.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee38d-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ee38d-107">Prerequisites</span></span>

- <span data-ttu-id="ee38d-108">Zainstaluj hello wiersza polecenia platformy Azure przy użyciu hello instrukcjami hello [Przewodnik instalacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli), jeśli nie ma jeszcze zrobione.</span><span class="sxs-lookup"><span data-stu-id="ee38d-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="ee38d-109">Tworzenie konta usługi partia zadań, jeśli nie został wcześniej.</span><span class="sxs-lookup"><span data-stu-id="ee38d-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="ee38d-110">Zobacz [Tworzenie konta usługi partia zadań z hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) przykładowego skryptu, który tworzy konto.</span><span class="sxs-lookup"><span data-stu-id="ee38d-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ee38d-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ee38d-111">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a><span data-ttu-id="ee38d-112">Oczyszczanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ee38d-112">Clean up application</span></span>

<span data-ttu-id="ee38d-113">Po uruchomieniu hello powyżej przykładowy skrypt, uruchom następujące polecenia tooremove hello aplikacji i wszystkich jego pakietów przekazano aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee38d-113">After you run hello above sample script, run hello following commands tooremove the application and all of its uploaded application packages.</span></span>

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a><span data-ttu-id="ee38d-114">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ee38d-114">Script explanation</span></span>

<span data-ttu-id="ee38d-115">Ten skrypt używa powitania po toocreate polecenia aplikacji i przekazywanie pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee38d-115">This script uses hello following commands toocreate an application and upload an application package.</span></span>
<span data-ttu-id="ee38d-116">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ee38d-116">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ee38d-117">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ee38d-117">Command</span></span> | <span data-ttu-id="ee38d-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ee38d-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ee38d-119">Tworzenie aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="ee38d-119">az batch application create</span></span>](https://docs.microsoft.com/cli/azure/batch/application#create) | <span data-ttu-id="ee38d-120">Tworzy aplikację.</span><span class="sxs-lookup"><span data-stu-id="ee38d-120">Creates an application.</span></span>  |
| [<span data-ttu-id="ee38d-121">zestaw aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="ee38d-121">az batch application set</span></span>](https://docs.microsoft.com/cli/azure/batch/application#set) | <span data-ttu-id="ee38d-122">Aktualizuje właściwości aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee38d-122">Updates properties of an application.</span></span>  |
| [<span data-ttu-id="ee38d-123">Utwórz pakiet aplikacji partii az</span><span class="sxs-lookup"><span data-stu-id="ee38d-123">az batch application package create</span></span>](https://docs.microsoft.com/cli/azure/batch/application/package#create) | <span data-ttu-id="ee38d-124">Dodaje toohello pakietu aplikacji określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ee38d-124">Adds an application package toohello specified application.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ee38d-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ee38d-125">Next steps</span></span>

<span data-ttu-id="ee38d-126">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ee38d-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ee38d-127">Dodatkowe przykłady skryptów partii interfejsu wiersza polecenia można znaleźć w hello [dokumentacji interfejsu wiersza polecenia Azure partii](../batch-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ee38d-127">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
