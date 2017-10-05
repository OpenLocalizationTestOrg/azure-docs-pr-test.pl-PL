---
title: "Tworzenie Centrum IoT Azure przy użyciu polecenia cmdlet programu PowerShell | Dokumentacja firmy Microsoft"
description: "Jak używać polecenia cmdlet programu PowerShell do tworzenia Centrum IoT."
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
ms.openlocfilehash: 02227adeb8a9a7463506efa44ddc2977f8aae65a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-new-azurermiothub-cmdlet"></a><span data-ttu-id="25758-103">Tworzenie Centrum IoT przy użyciu polecenia cmdlet New-AzureRmIotHub</span><span class="sxs-lookup"><span data-stu-id="25758-103">Create an IoT hub using the New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="25758-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="25758-104">Introduction</span></span>

<span data-ttu-id="25758-105">Tworzenie i zarządzanie nimi centra Azure IoT, można użyć poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25758-105">You can use Azure PowerShell cmdlets to create and manage Azure IoT hubs.</span></span> <span data-ttu-id="25758-106">W tym samouczku przedstawiono sposób tworzenia Centrum IoT przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25758-106">This tutorial shows you how to create an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="25758-107">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="25758-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="25758-108">W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="25758-108">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="25758-109">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="25758-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="25758-110">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25758-110">An active Azure account.</span></span> <br/><span data-ttu-id="25758-111">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="25758-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="25758-112">[Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="25758-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="25758-113">Nawiązywanie połączenia z subskrypcją platformy Azure</span><span class="sxs-lookup"><span data-stu-id="25758-113">Connect to your Azure subscription</span></span>
<span data-ttu-id="25758-114">W wierszu polecenia programu PowerShell wpisz następujące polecenie, aby zalogować się do subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="25758-114">In a PowerShell command prompt, enter the following command to sign in to your Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="25758-115">Jeśli masz wiele subskrypcji Azure, logowanie do platformy Azure udziela dostępu do subskrypcji platformy Azure skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="25758-115">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="25758-116">Aby wyświetlić listę dostępnych przy użyciu subskrypcji platformy Azure, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="25758-116">Use the following command to list the Azure subscriptions available for you to use:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="25758-117">Użyj następującego polecenia, aby wybrać subskrypcję, która ma być używany do uruchamiania poleceń, aby utworzyć Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="25758-117">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="25758-118">Przy użyciu subskrypcji nazwa lub identyfikator z danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="25758-118">You can use either the subscription name or ID from the output of the previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="25758-119">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="25758-119">Create resource group</span></span>

<span data-ttu-id="25758-120">Należy grupę zasobów do wdrożenia Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="25758-120">You need a resource group to deploy an IoT hub.</span></span> <span data-ttu-id="25758-121">Można użyć istniejącej grupy zasobów lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="25758-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="25758-122">Następujące polecenie służy do odnajdywania lokalizacji, w którym można wdrożyć Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="25758-122">You can use the following command to discover the locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="25758-123">Aby utworzyć grupę zasobów Centrum IoT w jednym z obsługiwanych lokalizacji dla Centrum IoT, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="25758-123">To create a resource group for your IoT hub in one of the supported locations for IoT Hub, use the following command.</span></span> <span data-ttu-id="25758-124">To przykładowe polecenie tworzy grupę zasobów o nazwie **MyIoTRG1** w **wschodnie stany USA** regionu:</span><span class="sxs-lookup"><span data-stu-id="25758-124">This example creates a resource group called **MyIoTRG1** in the **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="25758-125">Tworzenie centrum IoT</span><span class="sxs-lookup"><span data-stu-id="25758-125">Create an IoT hub</span></span>

<span data-ttu-id="25758-126">Aby utworzyć Centrum IoT w grupie zasobów utworzonej w poprzednim kroku, użyj następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="25758-126">To create an IoT hub in the resource group you created in the previous step, use the following command.</span></span> <span data-ttu-id="25758-127">Ten przykład tworzy **S1** koncentratora o nazwie **MyTestIoTHub** w **wschodnie stany USA** regionu:</span><span class="sxs-lookup"><span data-stu-id="25758-127">This example creates an **S1** hub called **MyTestIoTHub** in the **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="25758-128">Nazwa centrum IoT musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="25758-128">The name of the IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="25758-129">Możesz wyświetlić listę wszystkich centra IoT w ramach subskrypcji, za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="25758-129">You can list all the IoT hubs in your subscription using the following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="25758-130">Poprzedni przykład dodaje Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="25758-130">The previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="25758-131">Można usunąć Centrum IoT przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="25758-131">You can delete the IoT hub using the following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="25758-132">Alternatywnie można usunąć grupy zasobów i wszystkie zasoby, które zawiera przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="25758-132">Alternatively, you can remove a resource group and all the resources it contains using the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="25758-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25758-133">Next steps</span></span>

<span data-ttu-id="25758-134">Po wdrożeniu przy użyciu polecenia cmdlet programu PowerShell Centrum IoT, może zajść potrzeba dalszego zbadania:</span><span class="sxs-lookup"><span data-stu-id="25758-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want to explore further:</span></span>

* <span data-ttu-id="25758-135">Odnajdywanie innych [poleceń cmdlet programu PowerShell do pracy z Centrum IoT][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="25758-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="25758-136">Przeczytaj informacje o możliwości [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="25758-136">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="25758-137">Aby dowiedzieć się więcej o tworzeniu aplikacji Centrum IoT, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="25758-137">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="25758-138">[Wprowadzenie do zestawu SDK C][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="25758-138">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="25758-139">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="25758-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="25758-140">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="25758-140">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="25758-141">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="25758-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
