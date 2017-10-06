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
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a>Tworzenie za pomocą polecenia cmdlet hello AzureRmIotHub nowego centrum IoT

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a>Wprowadzenie

Można użyć toocreate poleceń cmdlet programu PowerShell systemu Azure i zarządzać nimi centra Azure IoT. W tym samouczku przedstawiono sposób toocreate Centrum IoT przy użyciu programu PowerShell.

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].

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

## <a name="create-resource-group"></a>Tworzenie grupy zasobów

Należy toodeploy grupy zasobów Centrum IoT. Można użyć istniejącej grupy zasobów lub Utwórz nową.

Program hello następujących polecenia toodiscover hello lokalizacji, na którym można wdrożyć Centrum IoT:

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

toocreate grupy zasobów Centrum IoT w jednym z hello obsługiwane lokalizacje dla Centrum IoT, hello Użyj następującego polecenia. To przykładowe polecenie tworzy grupę zasobów o nazwie **MyIoTRG1** w hello **wschodnie stany USA** regionu:

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a>Tworzenie centrum IoT

toocreate Centrum IoT w grupie zasobów hello utworzonego hello poprzedniego kroku, hello Użyj następującego polecenia. Ten przykład tworzy **S1** koncentratora o nazwie **MyTestIoTHub** w hello **wschodnie stany USA** regionu:

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

Nazwa centrum IoT hello Hello musi być unikatowa.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


Możesz wyświetlić listę wszystkich centra IoT hello w ramach subskrypcji, za pomocą następującego polecenia hello:

```powershell
Get-AzureRmIotHub
```

Witaj w poprzednim przykładzie dodaje Centrum IoT standardowe S1 dla której są rozliczane. Można usunąć Centrum IoT hello przy użyciu hello następujące polecenie:

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

Alternatywnie można usunąć grupy zasobów i wszystkie hello zasobów zawiera przy użyciu hello następujące polecenie:

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a>Następne kroki

Po wdrożeniu przy użyciu polecenia cmdlet programu PowerShell Centrum IoT można dodatkowo tooexplore:

* Odnajdywanie innych [poleceń cmdlet programu PowerShell do pracy z Centrum IoT][lnk-iothub-cmdlets].
* Przeczytaj informacje o możliwości hello hello [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].

toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:

* [Wprowadzenie tooC zestawu SDK][lnk-c-sdk]
* [Zestawy SDK Azure IoT][lnk-sdks]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
