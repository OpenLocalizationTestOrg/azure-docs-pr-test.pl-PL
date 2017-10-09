---
title: "Centrum Azure IoT przy użyciu aaaCreate hello dostawcy zasobów interfejsu API REST | Dokumentacja firmy Microsoft"
description: "Jak toouse hello toocreate interfejsu API REST dostawcy zasobów Centrum IoT."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Tworzenie Centrum IoT przy użyciu dostawcy zasobów hello interfejsu API REST (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Można użyć hello [interfejsu API REST dostawcy zasobów Centrum IoT] [ lnk-rest-api] toocreate i programowe zarządzanie centra Azure IoT. Ten samouczek pokazuje, jak toouse hello toocreate interfejsu API REST dostawcy zasobów Centrum IoT Centrum IoT z programu C#.

> [!NOTE]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).  W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.

toocomplete tego samouczka należy hello następujące:

* Program Visual Studio 2015 lub Visual Studio 2017.
* Aktywne konto platformy Azure. <br/>Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Azure PowerShell 1.0] [ lnk-powershell-install] lub nowszym.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Przygotowanie projektu programu Visual Studio

1. W programie Visual Studio Utwórz projekt Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu. Nazwa projektu hello **CreateIoTHubREST**.

2. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.

3. Sprawdź w Menedżerze pakietów NuGet **Uwzględnij wersję wstępną**, a na powitania **Przeglądaj** wyszukiwanie strony **Microsoft.Azure.Management.ResourceManager**. Wybierz pakiet hello, kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.

4. Wyszukaj w Menedżerze pakietów NuGet **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.

5. W pliku Program.cs Zastąp istniejące hello **przy użyciu** instrukcji z hello następującego kodu:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. W pliku Program.cs Dodaj następujące zmienne statyczne, zastępując symbole zastępcze hello hello. Należy zanotować **ApplicationId**, **SubscriptionId**, **TenantId**, i **hasło** we wcześniejszej części tego samouczka. **Nazwa grupy zasobów** jest hello nazwę grupy zasobów hello używane podczas tworzenia Centrum IoT hello. Możesz użyć wstępnie istniejącą lub nową grupę zasobów. **Nazwa centrum IoT** jest nazwą hello hello Centrum IoT można utworzyć, takich jak **MyIoTHub**. Hello nazwę Centrum IoT musi być globalnie unikatowa. **Nazwa wdrożenia** jest nazwę hello wdrożenia, takich jak **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Użyj hello zasobów dostawcy interfejsu API REST toocreate Centrum IoT

Użyj hello [interfejsu API REST dostawcy zasobów Centrum IoT] [ lnk-rest-api] toocreate Centrum IoT w grupie zasobów. Umożliwia także hello zasobów dostawcy interfejsu API REST toomake zmiany tooan istniejących Centrum IoT.

1. Dodaj następujące metody tooProgram.cs hello:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Dodaj hello następującego kodu toohello **CreateIoTHub** metody. Ten kod tworzy **HttpClient** obiektu o hello token uwierzytelniania w nagłówkach hello:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Dodaj hello następującego kodu toohello **CreateIoTHub** metody. Ten kod zawiera opis toocreate Centrum IoT hello i generuje reprezentacja JSON. Dla bieżącej listy lokalizacje, które obsługują Centrum IoT hello [stan Azure][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Dodaj hello następującego kodu toohello **CreateIoTHub** metody. Ten kod przesyła hello REST żądania tooAzure. Witaj kodu, a następnie sprawdza odpowiedź hello i pobiera adres URL hello służy toomonitor hello stan zadania wdrażania hello:

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Dodaj kod zakończenia toohello hello hello **CreateIoTHub** metody. Ten kod zawiera hello **asyncStatusUri** pobrać adresu w hello poprzedniego kroku toowait toocomplete wdrożenia hello:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Dodaj kod zakończenia toohello hello hello **CreateIoTHub** metody. Ten kod pobiera klucze hello hello Centrum IoT utworzony i wyświetla je toohello konsoli:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Hello pełny i uruchamiania aplikacji

Możesz teraz ukończyć aplikacji hello przez wywołującego hello **CreateIoTHub** metody, aby skompilować i uruchomić go.

1. Dodaj kod zakończenia toohello hello hello **Main** metody:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Kliknij przycisk **kompilacji** , a następnie **zbudować rozwiązanie**. Popraw błędy.

3. Kliknij przycisk **debugowania** , a następnie **Rozpocznij debugowanie** toorun hello aplikacji. Może upłynąć kilka minut dla hello toorun wdrożenia.

4. tooverify, dodania aplikacji hello nowego centrum IoT, odwiedź stronę hello [portalu Azure] [ lnk-azure-portal] i wyświetlanie listy zasobów. Można również użyć hello **Get-AzureRmResource** polecenia cmdlet programu PowerShell.

> [!NOTE]
> Ta przykładowa aplikacja dodaje Centrum IoT standardowe S1 dla której są rozliczane. Gdy skończysz, można usunąć Centrum IoT hello za pośrednictwem hello [portalu Azure] [ lnk-azure-portal] lub za pomocą hello **AzureRmResource Usuń** polecenia cmdlet programu PowerShell po zakończeniu.

## <a name="next-steps"></a>Następne kroki
Po wdrożeniu przy użyciu dostawcy zasobów hello interfejsu API REST Centrum IoT można dodatkowo tooexplore:

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

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
