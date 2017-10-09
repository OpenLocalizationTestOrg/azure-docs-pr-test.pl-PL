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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="e7a8a-103">Tworzenie Centrum IoT przy użyciu szablonu usługi Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="e7a8a-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="e7a8a-104">Można użyć usługi Azure Resource Manager toocreate i programowe zarządzanie centra Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="e7a8a-105">W tym samouczku przedstawiono sposób toouse toocreate szablonu usługi Azure Resource Manager Centrum IoT z programu C#.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a8a-106">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i Model Klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e7a8a-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="e7a8a-107">W tym artykule omówiono przy użyciu modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="e7a8a-108">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="e7a8a-109">Program Visual Studio 2015 lub Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e7a8a-110">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-110">An active Azure account.</span></span> <br/><span data-ttu-id="e7a8a-111">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="e7a8a-112">[Konta magazynu Azure] [ lnk-storage-account] przechowywania plików szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="e7a8a-113">[Azure PowerShell 1.0] [ lnk-powershell-install] lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="e7a8a-114">Przygotowanie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7a8a-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="e7a8a-115">W programie Visual Studio Utwórz projekt Visual C# pulpitu systemu Windows klasycznego przy użyciu hello **aplikacji konsoli (.NET Framework)** szablonu projektu.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="e7a8a-116">Nazwa projektu hello **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="e7a8a-117">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="e7a8a-118">Sprawdź w Menedżerze pakietów NuGet **Uwzględnij wersję wstępną**, a na powitania **Przeglądaj** wyszukiwanie strony **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="e7a8a-119">Wybierz pakiet hello, kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="e7a8a-120">Wyszukaj w Menedżerze pakietów NuGet **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="e7a8a-121">Kliknij przycisk **zainstalować**w **Przejrzyj zmiany** kliknij **OK**, następnie kliknij przycisk **akceptuję** tooaccept hello licencji.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="e7a8a-122">W pliku Program.cs Zastąp istniejące hello **przy użyciu** instrukcji z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="e7a8a-123">W pliku Program.cs Dodaj następujące zmienne statyczne, zastępując symbole zastępcze hello hello.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="e7a8a-124">Należy zanotować **ApplicationId**, **SubscriptionId**, **TenantId**, i **hasło** we wcześniejszej części tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="e7a8a-125">**Nazwa konta usługi Azure Storage** nazwę hello hello konta usługi Azure Storage służy do przechowywania plików szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="e7a8a-126">**Nazwa grupy zasobów** jest hello nazwę grupy zasobów hello używane podczas tworzenia Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="e7a8a-127">Nazwa Hello może być wstępnie istniejącej lub nowej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="e7a8a-128">**Nazwa wdrożenia** jest nazwę hello wdrożenia, takich jak **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="e7a8a-129">Przesyłanie szablonu toocreate Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="e7a8a-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="e7a8a-130">Użyj JSON szablonu i parametr pliku toocreate Centrum IoT w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="e7a8a-131">Umożliwia także usługi Azure Resource Manager szablonu toomake zmiany tooan istniejących Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="e7a8a-132">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="e7a8a-133">Dodaj plik JSON o nazwie **template.json** tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="e7a8a-134">tooadd standardowe toohello Centrum IoT **wschodnie stany USA** regionu, Zastąp zawartość hello **template.json** z powitania po definicji zasobu.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="e7a8a-135">Dla hello bieżącą listę regionów, które obsługują Centrum IoT [stan Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="e7a8a-136">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="e7a8a-137">Dodaj plik JSON o nazwie **parameters.JSON następującym kodem** tooyour projektu.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="e7a8a-138">Zamień zawartość hello **parameters.JSON następującym kodem** z następujących informacji parametr, który określa nazwę nowego centrum IoT hello, takich jak hello **{inicjały} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="e7a8a-139">musi być globalnie unikatowe nazwy Centrum IoT Hello, więc powinien zawierać nazwa lub inicjały:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="e7a8a-140">W **Eksploratora serwera**, Połącz tooyour subskrypcji platformy Azure i w magazynie Azure konta utworzyć kontener o nazwie **szablony**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="e7a8a-141">W hello **właściwości** panelu, zestaw hello **publiczny dostęp do odczytu** uprawnienia hello **szablony** kontenera zbyt**obiektu Blob**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="e7a8a-142">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy na powitania **szablony** kontenera, a następnie kliknij przycisk **kontenera obiektów Blob widoku**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="e7a8a-143">Kliknij hello **przekazania obiektu Blob** przycisku, wybierz dwa pliki hello **parameters.JSON następującym kodem** i **templates.json**, a następnie kliknij przycisk **Otwórz** Witaj tooupload JSON pliki toohello **szablony** kontenera.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="e7a8a-144">adresy URL Hello hello obiektów blob zawierający hello dane JSON są:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="e7a8a-145">Dodaj następujące metody tooProgram.cs hello:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="e7a8a-146">Dodaj hello następującego kodu toohello **CreateIoTHub** metody toosubmit hello szablon i parametr pliki toohello usługi Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="e7a8a-147">Dodaj hello następującego kodu toohello **CreateIoTHub** metodę, która wyświetla stan hello i klucze hello hello nowego centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="e7a8a-148">Hello pełny i uruchamiania aplikacji</span><span class="sxs-lookup"><span data-stu-id="e7a8a-148">Complete and run hello application</span></span>

<span data-ttu-id="e7a8a-149">Możesz teraz ukończyć aplikacji hello przez wywołującego hello **CreateIoTHub** metody, aby skompilować i uruchomić go.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="e7a8a-150">Dodaj kod zakończenia toohello hello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="e7a8a-151">Kliknij przycisk **kompilacji** , a następnie **zbudować rozwiązanie**.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="e7a8a-152">Popraw błędy.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-152">Correct any errors.</span></span>

3. <span data-ttu-id="e7a8a-153">Kliknij przycisk **debugowania** , a następnie **Rozpocznij debugowanie** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="e7a8a-154">Może upłynąć kilka minut dla hello toorun wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="e7a8a-155">tooverify dodane aplikacji hello nowego centrum IoT, odwiedź stronę hello [portalu Azure] [ lnk-azure-portal] i wyświetlanie listy zasobów.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="e7a8a-156">Można również użyć hello **Get-AzureRmResource** polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a8a-157">Ta przykładowa aplikacja dodaje Centrum IoT standardowe S1 dla której są rozliczane.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="e7a8a-158">Można usunąć Centrum IoT hello za pośrednictwem hello [portalu Azure] [ lnk-azure-portal] lub za pomocą hello **AzureRmResource Usuń** polecenia cmdlet programu PowerShell po zakończeniu.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7a8a-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e7a8a-159">Next steps</span></span>
<span data-ttu-id="e7a8a-160">Po wdrożeniu Centrum IoT przy użyciu szablonu usługi Azure Resource Manager z programem C#, można dodatkowo tooexplore:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="e7a8a-161">Przeczytaj informacje o możliwości hello hello [interfejsu API REST dostawcy zasobów Centrum IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="e7a8a-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="e7a8a-162">Odczyt [Omówienie usługi Azure Resource Manager] [ lnk-azure-rm-overview] toolearn więcej informacji na temat możliwości hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e7a8a-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="e7a8a-163">toolearn więcej informacji na temat tworzenia Centrum IoT, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="e7a8a-164">[Wprowadzenie tooC zestawu SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="e7a8a-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="e7a8a-165">[Zestawy SDK Azure IoT][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="e7a8a-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="e7a8a-166">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e7a8a-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e7a8a-167">[Symuluje urządzenia Azure IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e7a8a-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
