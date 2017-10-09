---
title: "aaaCreate Centrum IoT Azure przy użyciu szablonu (.NET) | Dokumentacja firmy Microsoft"
description: "Jak toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT z programem C#."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Tworzenie Centrum IoT przy użyciu szablonu usługi Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Można użyć usługi Azure Resource Manager toocreate i programowe zarządzanie centra Azure IoT. W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT z programu C#.

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Konta magazynu Azure] [ lnk-storage-account] przechowywania plików szablonu usługi Azure Resource Manager.
* [Azure PowerShell 1.0] [ lnk-powershell-install] lub nowszym.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Przygotowanie projektu programu Visual Studio

1. W programie Visual Studio Utwórz projekt Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Nazwa projektu hello **CreateIoTHub**.

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.

3. Sprawdź w Menedżerze pakietów NuGet **Uwzględnij wersję wstępną**, a na powitania **Przeglądaj** wyszukiwanie strony **Microsoft.Azure.Management.ResourceManager**. Wybierz pakiet hello, kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.

4. Wyszukaj w Menedżerze pakietów NuGet **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.

5. W pliku Program.cs Zastąp istniejące hello **przy użyciu** instrukcji z hello następującego kodu:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. W pliku Program.cs Dodaj następujące zmienne statyczne, zastępując symbole zastępcze hello hello. Należy zanotować **ApplicationId**, **SubscriptionId**, **TenantId**, i **hasło** we wcześniejszej części tego samouczka. **Nazwa konta usługi Azure Storage** nazwę hello hello konta usługi Azure Storage służy do przechowywania plików szablonu usługi Azure Resource Manager. **Nazwa grupy zasobów** jest hello nazwę grupy zasobów hello używane podczas tworzenia Centrum IoT hello. Nazwa Hello może być wstępnie istniejącej lub nowej grupy zasobów. **Nazwa wdrożenia** jest nazwę hello wdrożenia, takich jak **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Przesyłanie szablonu toocreate Centrum IoT

Użyj JSON szablonu i parametr pliku toocreate Centrum IoT w grupie zasobów. Umożliwia także usługi Azure Resource Manager szablonu toomake zmiany tooan istniejących Centrum IoT.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**. Dodaj plik JSON o nazwie **template.json** tooyour projektu.

2. tooadd standardowe toohello Centrum IoT **wschodnie stany USA** regionu, Zastąp zawartość hello **template.json** z powitania po definicji zasobu. Dla hello bieżącą listę regionów, które obsługują Centrum IoT [stan Azure][lnk-status]:

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

3. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**. Dodaj plik JSON o nazwie **parameters.JSON następującym kodem** tooyour projektu.

4. Zamień zawartość hello **parameters.JSON następującym kodem** z następujących informacji parametr, który określa nazwę nowego centrum IoT hello, takich jak hello **{inicjały} mynewiothub**. musi być globalnie unikatowe nazwy Centrum IoT Hello, więc powinien zawierać nazwa lub inicjały:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. W **Eksploratora serwera**, Połącz tooyour subskrypcji platformy Azure i w magazynie Azure konta utworzyć kontener o nazwie **szablony**. W hello **właściwości** panelu, zestaw hello **publiczny dostęp do odczytu** uprawnienia hello **szablony** kontenera zbyt**obiektu Blob**.

6. W **Eksploratora serwera**, kliknij prawym przyciskiem myszy na powitania **szablony** kontenera, a następnie kliknij przycisk **kontenera obiektów Blob widoku**. Kliknij hello **przekazania obiektu Blob** przycisku, wybierz dwa pliki hello **parameters.JSON następującym kodem** i **templates.json**, a następnie kliknij przycisk **Otwórz** Witaj tooupload JSON pliki toohello **szablony** kontenera. adresy URL Hello hello obiektów blob zawierający hello dane JSON są:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Dodaj następujące metody tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Dodaj hello następującego kodu toohello **CreateIoTHub** metody toosubmit hello szablon i parametr pliki toohello usługi Azure Resource Manager:

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. Dodaj hello następującego kodu toohello **CreateIoTHub** metodę, która wyświetla stan hello i klucze hello hello nowego centrum IoT:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Hello pełny i uruchamiania aplikacji

Możesz teraz ukończyć aplikacji hello przez wywołującego hello **CreateIoTHub** metody, aby skompilować i uruchomić go.

1. Dodaj kod zakończenia toohello hello hello **Main** metody:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Kliknij przycisk **kompilacji** , a następnie **zbudować rozwiązanie**. Popraw błędy.

3. Kliknij przycisk **debugowania** , a następnie **Rozpocznij debugowanie** toorun hello aplikacji. Może upłynąć kilka minut dla hello toorun wdrożenia.

4. tooverify dodane aplikacji hello nowego centrum IoT, odwiedź stronę hello [portalu Azure] [ lnk-azure-portal] i wyświetlanie listy zasobów. Można również użyć hello **Get-AzureRmResource** polecenia cmdlet programu PowerShell.

> [!NOTE]
> Ta przykładowa aplikacja dodaje Centrum IoT standardowe S1 dla której są rozliczane. Można usunąć Centrum IoT hello za pośrednictwem hello [portalu Azure] [ lnk-azure-portal] lub za pomocą hello **AzureRmResource Usuń** polecenia cmdlet programu PowerShell po zakończeniu.

## <a name="next-steps"></a>Następne kroki
Po wdrożeniu Centrum IoT przy użyciu szablonu usługi Azure Resource Manager z programem C#, można dodatkowo tooexplore:

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
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
