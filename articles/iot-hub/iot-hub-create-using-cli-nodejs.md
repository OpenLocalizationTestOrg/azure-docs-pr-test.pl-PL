---
title: "Tworzenie Centrum IoT przy użyciu wiersza polecenia platformy Azure (azure.js) | Dokumentacja firmy Microsoft"
description: "Jak utworzyć Centrum Azure IoT przy użyciu wiersza polecenia platformy Azure i platform (azure.js)."
services: iot-hub
documentationcenter: .net
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: 46a17831-650c-41d9-b228-445c5bb423d3
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/04/2017
ms.author: boltean
ms.openlocfilehash: 5e37c6c5e8625ce446ab203f19f9a8b2f1cd5a46
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-cli"></a><span data-ttu-id="04410-103">Tworzenie Centrum IoT przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="04410-103">Create an IoT hub using the Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="04410-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="04410-104">Introduction</span></span>

<span data-ttu-id="04410-105">Tworzenie i zarządzanie nimi centra Azure IoT programowo, można użyć wiersza polecenia platformy Azure (azure.js).</span><span class="sxs-lookup"><span data-stu-id="04410-105">You can use Azure CLI (azure.js) to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="04410-106">W tym artykule przedstawiono sposób użycia interfejsu wiersza polecenia Azure (azure.js) do tworzenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="04410-106">This article shows you how to use the Azure CLI (azure.js) to create an IoT hub.</span></span>

<span data-ttu-id="04410-107">Zadanie można wykonać przy użyciu jednej z następujących wersji interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="04410-107">You can complete the task using one of the following CLI versions:</span></span>

* <span data-ttu-id="04410-108">Azure CLI (azure.js) — interfejsu wiersza polecenia dla klasycznego i zasobów zarządzania modeli wdrażania zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="04410-108">Azure CLI (azure.js) – the CLI for the classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="04410-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) — generacji interfejsu wiersza polecenia do zarządzania model wdrażania zasobów.</span><span class="sxs-lookup"><span data-stu-id="04410-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - the next generation CLI for the resource management deployment model.</span></span>

<span data-ttu-id="04410-110">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="04410-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="04410-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04410-111">An active Azure account.</span></span> <span data-ttu-id="04410-112">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="04410-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="04410-113">[Azure CLI 0.10.4] [ lnk-CLI-install] lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="04410-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="04410-114">Jeśli masz już zainstalowany interfejsu wiersza polecenia Azure, możesz sprawdzić bieżącą wersję za pomocą następującego polecenia w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="04410-114">If you already have the Azure CLI installed, you can validate the current version at the command prompt with the following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="04410-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="04410-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="04410-116">Azure CLI musi być w trybie Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="04410-116">The Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="04410-117">Ustawianie konta i subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="04410-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="04410-118">W wierszu polecenia, logowania, wpisując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04410-118">At the command prompt, login by typing the following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="04410-119">Użyj przeglądarki sieci web sugerowane i kod do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="04410-119">Use the suggested web browser and code to authenticate.</span></span>
1. <span data-ttu-id="04410-120">Jeśli masz wiele subskrypcji Azure, nawiązywania Azure udziela dostępu do subskrypcji platformy Azure skojarzone z poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="04410-120">If you have multiple Azure subscriptions, connecting to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="04410-121">Wyświetlanie subskrypcji platformy Azure i określenie, co jest ustawieniem domyślnym, za pomocą polecenia:</span><span class="sxs-lookup"><span data-stu-id="04410-121">You can view the Azure subscriptions, and identify which one is the default, using the command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="04410-122">Aby ustawić kontekst subskrypcji, w którym chcesz uruchomić rest, użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="04410-122">To set the subscription context under which you want to run the rest of the commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="04410-123">Jeśli nie masz grupy zasobów, można utworzyć jedną o nazwie **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="04410-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="04410-124">Artykuł [użyć wiersza polecenia platformy Azure do zarządzania zasobami Azure i grup zasobów] [ lnk-CLI-arm] zawiera więcej informacji o sposobie używania interfejsu wiersza polecenia Azure do zarządzania zasobami Azure.</span><span class="sxs-lookup"><span data-stu-id="04410-124">The article [Use the Azure CLI to manage Azure resources and resource groups][lnk-CLI-arm] provides more information about how to use the Azure CLI to manage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="04410-125">Tworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="04410-125">Create an IoT Hub</span></span>

<span data-ttu-id="04410-126">Wymagane parametry:</span><span class="sxs-lookup"><span data-stu-id="04410-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="04410-127">**Grupa zasobów**.</span><span class="sxs-lookup"><span data-stu-id="04410-127">**resource-group**.</span></span> <span data-ttu-id="04410-128">Nazwa grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="04410-128">The resource group name.</span></span> <span data-ttu-id="04410-129">Format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, długość 1-64.</span><span class="sxs-lookup"><span data-stu-id="04410-129">The format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="04410-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="04410-130">**name**.</span></span> <span data-ttu-id="04410-131">Nazwa centrum IoT, który ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="04410-131">The name of the IoT hub to be created.</span></span> <span data-ttu-id="04410-132">Format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, 3 – 50 długości.</span><span class="sxs-lookup"><span data-stu-id="04410-132">The format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="04410-133">**Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="04410-133">**location**.</span></span> <span data-ttu-id="04410-134">Lokalizacja (region/centrum danych azure) do obsługi administracyjnej Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="04410-134">The location (azure region/datacenter) to provision the IoT hub.</span></span>
* <span data-ttu-id="04410-135">**Nazwa jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="04410-135">**sku-name**.</span></span> <span data-ttu-id="04410-136">Nazwa jednostki sku, jeden z: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="04410-136">The name of the sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="04410-137">Aby uzyskać pełną listę najnowszych można znaleźć na stronie cenowa Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="04410-137">For the latest full list, refer to the pricing page for IoT Hub.</span></span>
* <span data-ttu-id="04410-138">**jednostki**.</span><span class="sxs-lookup"><span data-stu-id="04410-138">**units**.</span></span> <span data-ttu-id="04410-139">Liczba jednostek elastycznie.</span><span class="sxs-lookup"><span data-stu-id="04410-139">The number of provisioned units.</span></span> <span data-ttu-id="04410-140">Zakres: F1 [1-1]: S1, S2 [1 – 200]: [1 – 10] S3.</span><span class="sxs-lookup"><span data-stu-id="04410-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="04410-141">Jednostki Centrum IoT bazują na łącznej liczbie komunikatów i liczbę urządzeń, którymi chcesz się połączyć.</span><span class="sxs-lookup"><span data-stu-id="04410-141">IoT Hub units are based on your total message count and the number of devices you want to connect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="04410-142">Aby wyświetlić wszystkie dostępne na potrzeby tworzenia parametry, można użyć polecenia Pomoc w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="04410-142">To see all the parameters available for creation, you can use the help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="04410-143">Prosty przykład: do tworzenia Centrum IoT o nazwie **exampleIoTHubName** w grupie zasobów **exampleResourceGroup**, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="04410-143">Quick example: To create an IoT Hub called **exampleIoTHubName** in the resource group **exampleResourceGroup**, run the following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="04410-144">To polecenie interfejsu wiersza polecenia Azure umożliwia utworzenie Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="04410-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="04410-145">Centrum IoT można usunąć **exampleIoTHubName** za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="04410-145">You can delete the IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="04410-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04410-146">Next steps</span></span>

<span data-ttu-id="04410-147">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz następujący artykuł:</span><span class="sxs-lookup"><span data-stu-id="04410-147">To learn more about developing for IoT Hub, see the following article:</span></span>

* <span data-ttu-id="04410-148">[Zestawy SDK IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="04410-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="04410-149">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="04410-149">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04410-150">[Przy użyciu portalu Azure do zarządzania Centrum IoT][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="04410-150">[Using the Azure portal to manage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
