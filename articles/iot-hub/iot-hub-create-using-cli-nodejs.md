---
title: "aaaCreate Centrum IoT przy użyciu wiersza polecenia platformy Azure (azure.js) | Dokumentacja firmy Microsoft"
description: "Jak toocreate Centrum Azure IoT przy użyciu hello wiersza polecenia platformy Azure i platform (azure.js)."
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
ms.openlocfilehash: c2a7ea98500b0a0e55a39f4cdfea4605c92add94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-cli"></a><span data-ttu-id="cc507-103">Tworzenie Centrum IoT przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc507-103">Create an IoT hub using hello Azure CLI</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="cc507-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="cc507-104">Introduction</span></span>

<span data-ttu-id="cc507-105">Można użyć wiersza polecenia platformy Azure (azure.js) toocreate i programowe zarządzanie centra Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="cc507-105">You can use Azure CLI (azure.js) toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="cc507-106">W tym artykule opisano, jak toouse hello Azure CLI (azure.js) toocreate Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="cc507-106">This article shows you how toouse hello Azure CLI (azure.js) toocreate an IoT hub.</span></span>

<span data-ttu-id="cc507-107">Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="cc507-107">You can complete hello task using one of hello following CLI versions:</span></span>

* <span data-ttu-id="cc507-108">Azure CLI (azure.js) — Witaj interfejsu wiersza polecenia dla hello klasycznego i modeli wdrażania, zarządzania zasobów zgodnie z opisem w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="cc507-108">Azure CLI (azure.js) – hello CLI for hello classic and resource management deployment models as described in this article.</span></span>
* <span data-ttu-id="cc507-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) — Witaj generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="cc507-109">[Azure CLI 2.0 (az.py)](iot-hub-create-using-cli.md) - hello next generation CLI for hello resource management deployment model.</span></span>

<span data-ttu-id="cc507-110">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="cc507-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="cc507-111">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc507-111">An active Azure account.</span></span> <span data-ttu-id="cc507-112">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cc507-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="cc507-113">[Azure CLI 0.10.4] [ lnk-CLI-install] lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="cc507-113">[Azure CLI 0.10.4][lnk-CLI-install] or later.</span></span> <span data-ttu-id="cc507-114">Jeśli masz już hello Azure CLI zainstalowana, można sprawdzić poprawność hello bieżącej wersji w wierszu polecenia hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cc507-114">If you already have hello Azure CLI installed, you can validate hello current version at hello command prompt with hello following command:</span></span>

```azurecli
azure --version
```

> [!NOTE]
> <span data-ttu-id="cc507-115">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cc507-115">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="cc507-116">Hello Azure CLI musi być w trybie Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="cc507-116">hello Azure CLI must be in Azure Resource Manager mode:</span></span>
>
> ```azurecli
> azure config mode arm
> ```

## <a name="set-your-azure-account-and-subscription"></a><span data-ttu-id="cc507-117">Ustawianie konta i subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc507-117">Set your Azure account and subscription</span></span>

1. <span data-ttu-id="cc507-118">W wierszu polecenia hello hello logowania, wpisując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cc507-118">At hello command prompt, login by typing hello following command:</span></span>

   ```azurecli
    azure login
   ```

   <span data-ttu-id="cc507-119">Za pomocą przeglądarki sieci web sugerowane hello i tooauthenticate kodu.</span><span class="sxs-lookup"><span data-stu-id="cc507-119">Use hello suggested web browser and code tooauthenticate.</span></span>
1. <span data-ttu-id="cc507-120">Jeśli masz wiele subskrypcji Azure, łączenie tooAzure udziela dostępu tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="cc507-120">If you have multiple Azure subscriptions, connecting tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="cc507-121">Możesz wyświetlić hello subskrypcji platformy Azure i określenie, który jest domyślnym hello, za pomocą polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="cc507-121">You can view hello Azure subscriptions, and identify which one is hello default, using hello command:</span></span>

   ```azurecli
    azure account list
   ```

   <span data-ttu-id="cc507-122">kontekst subskrypcji hello tooset pod którym ma zostać toorun hello reszty hello, użyj polecenia:</span><span class="sxs-lookup"><span data-stu-id="cc507-122">tooset hello subscription context under which you want toorun hello rest of hello commands use:</span></span>

   ```azurecli
    azure account set <subscription name>
   ```

1. <span data-ttu-id="cc507-123">Jeśli nie masz grupy zasobów, można utworzyć jedną o nazwie **exampleResourceGroup**:</span><span class="sxs-lookup"><span data-stu-id="cc507-123">If you do not have a resource group, you can create one named **exampleResourceGroup**:</span></span>

   ```azurecli
    azure group create -n exampleResourceGroup -l westus
   ```

> [!TIP]
> <span data-ttu-id="cc507-124">Artykuł Hello [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów] [ lnk-CLI-arm] zawiera więcej informacji na temat sposobu toouse hello Azure CLI toomanage Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="cc507-124">hello article [Use hello Azure CLI toomanage Azure resources and resource groups][lnk-CLI-arm] provides more information about how toouse hello Azure CLI toomanage Azure resources.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="cc507-125">Tworzenie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="cc507-125">Create an IoT Hub</span></span>

<span data-ttu-id="cc507-126">Wymagane parametry:</span><span class="sxs-lookup"><span data-stu-id="cc507-126">Required parameters:</span></span>

```azurecli
azure iothub create -g <resource-group> -n <name> -l <location> -s <sku-name> -u <units>
```

* <span data-ttu-id="cc507-127">**Grupa zasobów**.</span><span class="sxs-lookup"><span data-stu-id="cc507-127">**resource-group**.</span></span> <span data-ttu-id="cc507-128">Nazwa grupy zasobów Hello.</span><span class="sxs-lookup"><span data-stu-id="cc507-128">hello resource group name.</span></span> <span data-ttu-id="cc507-129">Hello format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, długość 1-64.</span><span class="sxs-lookup"><span data-stu-id="cc507-129">hello format is case insensitive alphanumeric, underscore, and hyphen, 1-64 length.</span></span>
* <span data-ttu-id="cc507-130">**name**.</span><span class="sxs-lookup"><span data-stu-id="cc507-130">**name**.</span></span> <span data-ttu-id="cc507-131">Nazwa Hello toobe Centrum IoT hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="cc507-131">hello name of hello IoT hub toobe created.</span></span> <span data-ttu-id="cc507-132">Hello format jest bez uwzględniania wielkości liter alfanumeryczne, podkreślenia i łączniki, 3 – 50 długości.</span><span class="sxs-lookup"><span data-stu-id="cc507-132">hello format is case insensitive alphanumeric, underscore, and hyphen, 3-50 length.</span></span>
* <span data-ttu-id="cc507-133">**Lokalizacja**.</span><span class="sxs-lookup"><span data-stu-id="cc507-133">**location**.</span></span> <span data-ttu-id="cc507-134">Witaj lokalizacji (region/centrum danych azure) tooprovision hello Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="cc507-134">hello location (azure region/datacenter) tooprovision hello IoT hub.</span></span>
* <span data-ttu-id="cc507-135">**Nazwa jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="cc507-135">**sku-name**.</span></span> <span data-ttu-id="cc507-136">Nazwa Hello sku hello, jeden z: [F1, S1, S2, S3].</span><span class="sxs-lookup"><span data-stu-id="cc507-136">hello name of hello sku, one of: [F1, S1, S2, S3].</span></span> <span data-ttu-id="cc507-137">Hello najnowsze pełną listę można znaleźć toohello stronie dotyczącej cen Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="cc507-137">For hello latest full list, refer toohello pricing page for IoT Hub.</span></span>
* <span data-ttu-id="cc507-138">**jednostki**.</span><span class="sxs-lookup"><span data-stu-id="cc507-138">**units**.</span></span> <span data-ttu-id="cc507-139">Liczba Hello elastycznie jednostki.</span><span class="sxs-lookup"><span data-stu-id="cc507-139">hello number of provisioned units.</span></span> <span data-ttu-id="cc507-140">Zakres: F1 [1-1]: S1, S2 [1 – 200]: [1 – 10] S3.</span><span class="sxs-lookup"><span data-stu-id="cc507-140">Range: F1 [1-1] : S1, S2 [1-200] : S3 [1-10].</span></span> <span data-ttu-id="cc507-141">Jednostki Centrum IoT bazują na całkowita wiadomość hello i liczba liczby urządzeń ma tooconnect.</span><span class="sxs-lookup"><span data-stu-id="cc507-141">IoT Hub units are based on your total message count and hello number of devices you want tooconnect.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

<span data-ttu-id="cc507-142">toosee hello wszystkie dostępne na potrzeby tworzenia parametrów, możesz użyć polecenia pomocy hello w wierszu polecenia:</span><span class="sxs-lookup"><span data-stu-id="cc507-142">toosee all hello parameters available for creation, you can use hello help command in command prompt:</span></span>

```azurecli
azure iothub create -h
```

<span data-ttu-id="cc507-143">Prosty przykład: toocreate Centrum IoT o nazwie **exampleIoTHubName** w grupie zasobów hello **exampleResourceGroup**Uruchom hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="cc507-143">Quick example: toocreate an IoT Hub called **exampleIoTHubName** in hello resource group **exampleResourceGroup**, run hello following command:</span></span>

```azurecli
azure iothub create -g exampleResourceGroup -n exampleIoTHubName -l westus -k s1 -u 1
```

> [!NOTE]
> <span data-ttu-id="cc507-144">To polecenie interfejsu wiersza polecenia Azure umożliwia utworzenie Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="cc507-144">This Azure CLI command creates an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="cc507-145">Można usunąć Centrum IoT hello **exampleIoTHubName** za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="cc507-145">You can delete hello IoT hub **exampleIoTHubName** using following command:</span></span>
>
> ```azurecli
> azure iothub delete -g exampleResourceGroup -n exampleIoTHubName
> ```

## <a name="next-steps"></a><span data-ttu-id="cc507-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc507-146">Next steps</span></span>

<span data-ttu-id="cc507-147">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz hello poniższego artykułu:</span><span class="sxs-lookup"><span data-stu-id="cc507-147">toolearn more about developing for IoT Hub, see hello following article:</span></span>

* <span data-ttu-id="cc507-148">[Zestawy SDK IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="cc507-148">[IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="cc507-149">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="cc507-149">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="cc507-150">[Przy użyciu hello toomanage portalu Azure IoT Hub][lnk-portal]</span><span class="sxs-lookup"><span data-stu-id="cc507-150">[Using hello Azure portal toomanage IoT Hub][lnk-portal]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-CLI-install]:../cli-install-nodejs.md
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-CLI-arm]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md

[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-portal]: iot-hub-create-through-portal.md 
