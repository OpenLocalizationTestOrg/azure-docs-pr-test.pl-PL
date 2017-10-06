---
title: "aaaCreate Centrum IoT Azure przy użyciu polecenia cmdlet programu PowerShell | Dokumentacja firmy Microsoft"
description: Jak toouse toocreate polecenia cmdlet programu PowerShell Centrum IoT.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="ba4b2-103">Tworzenie za pomocą polecenia cmdlet hello AzureRmIotHub nowego centrum IoT</span><span class="sxs-lookup"><span data-stu-id="ba4b2-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="ba4b2-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="ba4b2-104">Introduction</span></span>

<span data-ttu-id="ba4b2-105">Można użyć toocreate poleceń cmdlet programu PowerShell systemu Azure i zarządzać nimi centra Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="ba4b2-106">W tym samouczku przedstawiono sposób toocreate Centrum IoT przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="ba4b2-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ba4b2-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ba4b2-108">W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="ba4b2-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ba4b2-110">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-110">An active Azure account.</span></span> <br/><span data-ttu-id="ba4b2-111">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="ba4b2-112">[Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="ba4b2-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="ba4b2-113">Połącz tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ba4b2-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="ba4b2-114">W wierszu polecenia programu PowerShell wprowadź hello następujące polecenia toosign w tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="ba4b2-115">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="ba4b2-116">Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="ba4b2-117">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="ba4b2-118">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="ba4b2-119">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="ba4b2-119">Create resource group</span></span>

<span data-ttu-id="ba4b2-120">Należy toodeploy grupy zasobów Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="ba4b2-121">Można użyć istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="ba4b2-122">Program hello następujących polecenia toodiscover hello lokalizacji, na którym można wdrożyć Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="ba4b2-123">toocreate grupy zasobów Centrum IoT w jednym z hello obsługiwane lokalizacje dla Centrum IoT, hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="ba4b2-124">To przykładowe polecenie tworzy grupę zasobów o nazwie **MyIoTRG1** w hello **wschodnie stany USA** regionu:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="ba4b2-125">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="ba4b2-125">Create an IoT hub</span></span>

<span data-ttu-id="ba4b2-126">toocreate Centrum IoT w grupie zasobów hello utworzonego hello poprzedniego kroku, hello Użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="ba4b2-127">Ten przykład tworzy **S1** koncentratora o nazwie **MyTestIoTHub** w hello **wschodnie stany USA** regionu:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="ba4b2-128">Nazwa centrum IoT hello Hello musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="ba4b2-129">Możesz wyświetlić listę wszystkich centra IoT hello w ramach subskrypcji, za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="ba4b2-130">Witaj w poprzednim przykładzie dodaje Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="ba4b2-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="ba4b2-131">Można usunąć Centrum IoT hello przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="ba4b2-132">Alternatywnie można usunąć grupy zasobów i wszystkie hello zasobów zawiera przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="ba4b2-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba4b2-133">Next steps</span></span>

<span data-ttu-id="ba4b2-134">Po wdrożeniu przy użyciu polecenia cmdlet programu PowerShell Centrum IoT można dodatkowo tooexplore:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="ba4b2-135">Odnajdywanie innych [poleceń cmdlet programu PowerShell do pracy z Centrum IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="ba4b2-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="ba4b2-136">Przeczytaj informacje o możliwości hello hello [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="ba4b2-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="ba4b2-137">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="ba4b2-138">[Wprowadzenie tooC zestawu SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="ba4b2-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="ba4b2-139">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="ba4b2-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="ba4b2-140">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="ba4b2-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ba4b2-141">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ba4b2-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
