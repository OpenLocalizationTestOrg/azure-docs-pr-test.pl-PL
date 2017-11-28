---
title: "aaaCreate Centrum IoT Azure przy użyciu szablonu (PowerShell) | Dokumentacja firmy Microsoft"
description: "Jak toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT przy użyciu programu PowerShell."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="e9c50-103">Tworzenie Centrum IoT przy użyciu szablonu usługi Azure Resource Manager (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e9c50-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="e9c50-104">Można użyć usługi Azure Resource Manager toocreate i programowe zarządzanie centra Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e9c50-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="e9c50-105">W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9c50-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="e9c50-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9c50-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9c50-107">W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e9c50-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="e9c50-108">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e9c50-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e9c50-109">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c50-109">An active Azure account.</span></span> <br/><span data-ttu-id="e9c50-110">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e9c50-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="e9c50-111">[Azure PowerShell 1.0] [ lnk-powershell-install] lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="e9c50-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="e9c50-112">Artykuł Hello [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager] [ lnk-powershell-arm] zawiera więcej informacji na temat toouse środowiska PowerShell i usługi Azure Resource Manager toocreate szablonów Azure zasobów.</span><span class="sxs-lookup"><span data-stu-id="e9c50-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="e9c50-113">Połącz tooyour subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="e9c50-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="e9c50-114">W wierszu polecenia programu PowerShell wprowadź hello następujące polecenia toosign w tooyour subskrypcji platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="e9c50-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e9c50-115">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9c50-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="e9c50-116">Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:</span><span class="sxs-lookup"><span data-stu-id="e9c50-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="e9c50-117">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e9c50-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="e9c50-118">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="e9c50-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="e9c50-119">Program hello po toodiscover poleceń, w którym można wdrożyć Centrum IoT i hello aktualnie obsługiwane wersje interfejsu API:</span><span class="sxs-lookup"><span data-stu-id="e9c50-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="e9c50-120">Tworzenie Centrum IoT przy użyciu następującego polecenia w jednym z hello obsługiwane lokalizacje dla Centrum IoT hello toocontain grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e9c50-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="e9c50-121">To przykładowe polecenie tworzy grupę zasobów o nazwie **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="e9c50-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="e9c50-122">Przesyłanie szablonu toocreate Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e9c50-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="e9c50-123">Użyj toocreate szablonu JSON Centrum IoT w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e9c50-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="e9c50-124">Umożliwia także usługi Azure Resource Manager szablonu toomake zmiany tooan istniejących Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e9c50-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="e9c50-125">Użyj toocreate edytora tekstu, nazywany szablonem usługi Azure Resource Manager **template.json** z hello następujących zasobów definicji toocreate nowego centrum IoT standardowa.</span><span class="sxs-lookup"><span data-stu-id="e9c50-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="e9c50-126">W tym przykładzie dodaje hello Centrum IoT w hello **wschodnie stany USA** regionu, tworzy dwie grupy konsumentów (**cg1** i **cg2**) na punkt końcowy hello zgodnego Centrum zdarzeń i używa hello **2016-02-03** wersja interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e9c50-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="e9c50-127">Ten szablon również oczekuje toopass w nazwie Centrum IoT hello jako parametr o nazwie **hubName**.</span><span class="sxs-lookup"><span data-stu-id="e9c50-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="e9c50-128">Dla bieżącej listy lokalizacje, które obsługują Centrum IoT hello [stan Azure][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="e9c50-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

2. <span data-ttu-id="e9c50-129">Zapisz plik szablonu usługi Azure Resource Manager hello na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e9c50-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="e9c50-130">W tym przykładzie przyjęto założenie, zapisz go w folderze o nazwie **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="e9c50-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="e9c50-131">Uruchom następujące polecenie toodeploy hello nowego centrum IoT, przekazując hello nazwę Centrum IoT jako parametr.</span><span class="sxs-lookup"><span data-stu-id="e9c50-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="e9c50-132">W tym przykładzie nazwa hello Centrum IoT hello jest `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="e9c50-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="e9c50-133">musi być globalnie unikatowa nazwa Hello Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="e9c50-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="e9c50-134">dane wyjściowe Hello Wyświetla klucze hello Centrum IoT hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="e9c50-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="e9c50-135">tooverify dodane aplikacji hello nowego centrum IoT, odwiedź stronę hello [portalu Azure] [ lnk-azure-portal] i wyświetlanie listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e9c50-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="e9c50-136">Można również użyć hello **Get-AzureRmResource** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9c50-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e9c50-137">Ta przykładowa aplikacja dodaje Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="e9c50-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="e9c50-138">Można usunąć Centrum IoT hello za pośrednictwem hello [portalu Azure] [ lnk-azure-portal] lub za pomocą hello **AzureRmResource Usuń** polecenia cmdlet programu PowerShell po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="e9c50-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9c50-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e9c50-139">Next steps</span></span>

<span data-ttu-id="e9c50-140">Po wdrożeniu przy użyciu szablonu usługi Azure Resource Manager przy użyciu programu PowerShell Centrum IoT można dodatkowo tooexplore:</span><span class="sxs-lookup"><span data-stu-id="e9c50-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="e9c50-141">Przeczytaj informacje o możliwości hello hello [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="e9c50-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="e9c50-142">Odczyt [Omówienie usługi Azure Resource Manager] [ lnk-azure-rm-overview] toolearn więcej informacji na temat możliwości hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e9c50-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="e9c50-143">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="e9c50-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="e9c50-144">[Wprowadzenie tooC zestawu SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="e9c50-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="e9c50-145">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="e9c50-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="e9c50-146">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e9c50-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e9c50-147">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e9c50-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
