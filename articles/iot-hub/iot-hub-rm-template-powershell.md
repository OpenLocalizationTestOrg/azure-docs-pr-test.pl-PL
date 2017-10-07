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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a>Tworzenie Centrum IoT przy użyciu szablonu usługi Azure Resource Manager (PowerShell)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Można użyć usługi Azure Resource Manager toocreate i programowe zarządzanie centra Azure IoT. W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT przy użyciu programu PowerShell.

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Azure PowerShell 1.0] [ lnk-powershell-install] lub nowszym.

> [!TIP]
> Artykuł Hello [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager] [ lnk-powershell-arm] zawiera więcej informacji na temat toouse środowiska PowerShell i usługi Azure Resource Manager toocreate szablonów Azure zasobów.

## <a name="connect-tooyour-azure-subscription"></a>Połącz tooyour subskrypcji platformy Azure

W wierszu polecenia programu PowerShell wprowadź hello następujące polecenia toosign w tooyour subskrypcji platformy Azure:

```powershell
Login-AzureRmAccount
```

Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika. Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:

```powershell
Get-AzureRMSubscription
```

Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello. Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

Program hello po toodiscover poleceń, w którym można wdrożyć Centrum IoT i hello aktualnie obsługiwane wersje interfejsu API:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

Tworzenie Centrum IoT przy użyciu następującego polecenia w jednym z hello obsługiwane lokalizacje dla Centrum IoT hello toocontain grupy zasobów. To przykładowe polecenie tworzy grupę zasobów o nazwie **MyIoTRG1**:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Przesyłanie szablonu toocreate Centrum IoT

Użyj toocreate szablonu JSON Centrum IoT w grupie zasobów. Umożliwia także usługi Azure Resource Manager szablonu toomake zmiany tooan istniejących Centrum IoT.

1. Użyj toocreate edytora tekstu, nazywany szablonem usługi Azure Resource Manager **template.json** z hello następujących zasobów definicji toocreate nowego centrum IoT standardowa. W tym przykładzie dodaje hello Centrum IoT w hello **wschodnie stany USA** regionu, tworzy dwie grupy konsumentów (**cg1** i **cg2**) na punkt końcowy hello zgodnego Centrum zdarzeń i używa hello **2016-02-03** wersja interfejsu API. Ten szablon również oczekuje toopass w nazwie Centrum IoT hello jako parametr o nazwie **hubName**. Dla bieżącej listy lokalizacje, które obsługują Centrum IoT hello [stan Azure][lnk-status].

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

2. Zapisz plik szablonu usługi Azure Resource Manager hello na komputerze lokalnym. W tym przykładzie przyjęto założenie, zapisz go w folderze o nazwie **c:\templates**.

3. Uruchom następujące polecenie toodeploy hello nowego centrum IoT, przekazując hello nazwę Centrum IoT jako parametr. W tym przykładzie nazwa hello Centrum IoT hello jest `abcmyiothub`. musi być globalnie unikatowa nazwa Hello Centrum IoT:

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. dane wyjściowe Hello Wyświetla klucze hello Centrum IoT hello utworzony.

5. tooverify dodane aplikacji hello nowego centrum IoT, odwiedź stronę hello [portalu Azure] [ lnk-azure-portal] i wyświetlanie listy zasobów. Można również użyć hello **Get-AzureRmResource** polecenia cmdlet programu PowerShell.

> [!NOTE]
> Ta przykładowa aplikacja dodaje Centrum IoT standardowe S1 dla której są rozliczane. Można usunąć Centrum IoT hello za pośrednictwem hello [portalu Azure] [ lnk-azure-portal] lub za pomocą hello **AzureRmResource Usuń** polecenia cmdlet programu PowerShell po zakończeniu.

## <a name="next-steps"></a>Następne kroki

Po wdrożeniu przy użyciu szablonu usługi Azure Resource Manager przy użyciu programu PowerShell Centrum IoT można dodatkowo tooexplore:

* Przeczytaj informacje o możliwości hello hello [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].
* Odczyt [Omówienie usługi Azure Resource Manager] [ lnk-azure-rm-overview] toolearn więcej informacji na temat możliwości hello Azure Resource Manager.

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:

* [Wprowadzenie tooC zestawu SDK][lnk-c-sdk]
* [Zestawy SDK Azure IoT][lnk-sdks]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]

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
