---
title: "Rozwiązywanie problemów z fabryki danych Azure"
description: "Dowiedz się, jak rozwiązać problemy z przy użyciu fabryki danych Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 953a2703db7c8991f580a7c963d6cbd94265c213
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="52a98-103">Rozwiązywanie problemów z usługą Data Factory</span><span class="sxs-lookup"><span data-stu-id="52a98-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="52a98-104">Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów w przypadku problemów przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="52a98-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="52a98-105">W tym artykule nie są wyświetlane wszystkie możliwe problemy podczas korzystania z usługi, ale obejmuje pewne problemy i ogólne porady dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="52a98-105">This article does not list all the possible issues when using the service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="52a98-106">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="52a98-106">Troubleshooting tips</span></span>
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a><span data-ttu-id="52a98-107">Błąd: subskrypcja nie jest zarejestrowana do korzystania z przestrzeni nazw „Microsoft.DataFactory”</span><span class="sxs-lookup"><span data-stu-id="52a98-107">Error: The subscription is not registered to use namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="52a98-108">Wyświetlenie tego błędu oznacza, że dostawca zasobów usługi Azure Data Factory nie został zarejestrowany na maszynie.</span><span class="sxs-lookup"><span data-stu-id="52a98-108">If you receive this error, the Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="52a98-109">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="52a98-109">Do the following:</span></span>

1. <span data-ttu-id="52a98-110">Uruchom program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52a98-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="52a98-111">Zaloguj się do konta platformy Azure przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="52a98-111">Log in to your Azure account using the following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="52a98-112">Uruchom następujące polecenie, aby zarejestrować dostawcę usługi fabryka danych Azure.</span><span class="sxs-lookup"><span data-stu-id="52a98-112">Run the following command to register the Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="52a98-113">Problem: Nieautoryzowanego błąd podczas uruchamiania polecenia cmdlet usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="52a98-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="52a98-114">Przypuszczalnie nie używasz prawidłowego konta lub subskrypcji platformy Azure w programie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52a98-114">You are probably not using the right Azure account or subscription with the Azure PowerShell.</span></span> <span data-ttu-id="52a98-115">Użyj następujących poleceń cmdlet, aby wybrać odpowiednie konto i subskrypcję platformy Azure do stosowania w programie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="52a98-115">Use the following cmdlets to select the right Azure account and subscription to use with the Azure PowerShell.</span></span>

1. <span data-ttu-id="52a98-116">Login-AzureRmAccount - Użyj Identyfikatora prawo użytkownika i hasła</span><span class="sxs-lookup"><span data-stu-id="52a98-116">Login-AzureRmAccount - Use the right user ID and password</span></span>
2. <span data-ttu-id="52a98-117">Get-AzureRmSubscription - wyświetlić wszystkie subskrypcje dla konta.</span><span class="sxs-lookup"><span data-stu-id="52a98-117">Get-AzureRmSubscription - View all the subscriptions for the account.</span></span>
3. <span data-ttu-id="52a98-118">SELECT-AzureRmSubscription &lt;Nazwa subskrypcji&gt; — Wybierz subskrypcję, do prawej.</span><span class="sxs-lookup"><span data-stu-id="52a98-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select the right subscription.</span></span> <span data-ttu-id="52a98-119">Użyj tego samego umożliwiające tworzenie fabryki danych w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="52a98-119">Use the same one you use to create a data factory on the Azure portal.</span></span>

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="52a98-120">Problem: Nie można uruchomić instalacji Express danych zarządzania bramy z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52a98-120">Problem: Fail to launch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="52a98-121">Instalacja ekspresowa bramy zarządzania danymi wymaga przeglądarki Internet Explorer lub przeglądarki zgodnej z technologią Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="52a98-121">The Express setup for the Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="52a98-122">Jeśli uruchomienie instalacji ekspresowej nie powiedzie się, wykonaj jedną z poniższych czynności:</span><span class="sxs-lookup"><span data-stu-id="52a98-122">If the Express Setup fails to start, do one of the following:</span></span>

* <span data-ttu-id="52a98-123">Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="52a98-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="52a98-124">Jeśli używasz przeglądarki Chrome, przejdź do [sklepu internetowego Chrome](https://chrome.google.com/webstore/), wyszukaj słowo kluczowe „ClickOnce”, wybierz jedno z rozszerzeń ClickOnce i je zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="52a98-124">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="52a98-125">Wykonaj te same czynności dla przeglądarki Firefox (Instalowanie dodatku).</span><span class="sxs-lookup"><span data-stu-id="52a98-125">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="52a98-126">Kliknij przycisk Otwórz menu na pasku narzędzi (trzy poziome linie w prawym górnym rogu), kliknij pozycję Dodatki, wyszukaj słowo kluczowe „ClickOnce”, wybierz jedno z rozszerzeń ClickOnce i je zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="52a98-126">Click Open Menu button on the toolbar (three horizontal lines in the top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="52a98-127">Użyj **Podręcznika instalacji** łącza wyświetlany na tym samym bloku w portalu.</span><span class="sxs-lookup"><span data-stu-id="52a98-127">Use the **Manual Setup** link shown on the same blade in the portal.</span></span> <span data-ttu-id="52a98-128">Takie podejście umożliwia Pobierz plik instalacyjny i uruchomić go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="52a98-128">You use this approach to download installation file and run it manually.</span></span> <span data-ttu-id="52a98-129">Po pomyślnej instalacji, zostanie wyświetlone okno dialogowe konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="52a98-129">After the installation is successful, you see the Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="52a98-130">Skopiuj **klucz** z ekranu portalu i użyj go w menedżerze konfiguracji, aby ręcznie zarejestrować bramę w usłudze.</span><span class="sxs-lookup"><span data-stu-id="52a98-130">Copy the **key** from the portal screen and use it in the configuration manager to manually register the gateway with the service.</span></span>  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a><span data-ttu-id="52a98-131">Problem: Nie można nawiązać połączenia z lokalnego serwera SQL</span><span class="sxs-lookup"><span data-stu-id="52a98-131">Problem: Fail to connect to on-premises SQL Server</span></span>
<span data-ttu-id="52a98-132">Uruchom **Menedżera konfiguracji bramy zarządzania danymi** na komputerze bramy i użyj **Rozwiązywanie problemów** kartę, aby przetestować połączenie z programem SQL Server na maszynie bramy.</span><span class="sxs-lookup"><span data-stu-id="52a98-132">Launch **Data Management Gateway Configuration Manager** on the gateway machine and use the **Troubleshooting** tab to test the connection to SQL Server from the gateway machine.</span></span> <span data-ttu-id="52a98-133">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="52a98-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="52a98-134">Problem: Wycinki danych wejściowych znajdują się w Oczekiwanie na kiedykolwiek stanu</span><span class="sxs-lookup"><span data-stu-id="52a98-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="52a98-135">Wycinki może być w **oczekiwania** stanu z różnych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="52a98-135">The slices could be in **Waiting** state due to various reasons.</span></span> <span data-ttu-id="52a98-136">Typowe przyczyny jest to, że **zewnętrznych** nie ustawiono właściwości **true**.</span><span class="sxs-lookup"><span data-stu-id="52a98-136">One of the common reasons is that the **external** property is not set to **true**.</span></span> <span data-ttu-id="52a98-137">Wszelkie zestawu danych, który jest tworzony poza zakresem fabryki danych Azure powinien być oznaczony przez **zewnętrznych** właściwości.</span><span class="sxs-lookup"><span data-stu-id="52a98-137">Any dataset that is produced outside the scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="52a98-138">Ta właściwość wskazuje, że danych jest zewnętrzne i nie kopii zapasowej przez dowolnego potoki w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="52a98-138">This property indicates that the data is external and not backed by any pipelines within the data factory.</span></span> <span data-ttu-id="52a98-139">Wycinki danych są oznaczane jako **Gotowy**, gdy dane staną się dostępne w odpowiednim magazynie.</span><span class="sxs-lookup"><span data-stu-id="52a98-139">The data slices are marked as **Ready** once the data is available in the respective store.</span></span>

<span data-ttu-id="52a98-140">Zobacz poniższy przykład wykorzystania właściwości **external**.</span><span class="sxs-lookup"><span data-stu-id="52a98-140">See the following example for the usage of the **external** property.</span></span> <span data-ttu-id="52a98-141">Opcjonalnie można określić **externalData*** podczas ustawiania zewnętrznych na wartość true.</span><span class="sxs-lookup"><span data-stu-id="52a98-141">You can optionally specify **externalData*** when you set external to true.</span></span>

<span data-ttu-id="52a98-142">Zobacz [zestawów danych](data-factory-create-datasets.md) artykułu, aby uzyskać więcej informacji o tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="52a98-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="52a98-143">Aby rozwiązać ten problem, dodaj właściwość **external** i opcjonalną sekcję **externalData** do definicji JSON tabeli wejściowej i utwórz tabelę ponownie.</span><span class="sxs-lookup"><span data-stu-id="52a98-143">To resolve the error, add the **external** property and the optional **externalData** section to the JSON definition of the input table and recreate the table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="52a98-144">Problem: Operacja kopiowania hybrydowego kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="52a98-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="52a98-145">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) kroki rozwiązywania problemów z kopiowaniem do/z lokalnymi danymi z magazynu przy użyciu bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="52a98-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps to troubleshoot issues with copying to/from an on-premises data store using the Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="52a98-146">Problem: HDInsight na żądanie obsługi kończy się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="52a98-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="52a98-147">Korzystając z połączonej usługi typu HDInsightOnDemand, należy określić linkedServiceName, wskazujące do magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="52a98-147">When using a linked service of type HDInsightOnDemand, you need to specify a linkedServiceName that points to an Azure Blob Storage.</span></span> <span data-ttu-id="52a98-148">Usługa Data Factory korzysta z tego magazynu do przechowywania dzienników i plików pomocniczych dla klastra HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="52a98-148">Data Factory service uses this storage to store logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="52a98-149">Czasami inicjowanie obsługi klastra HDInsight na żądanie kończy się niepowodzeniem z następującym błędem:</span><span class="sxs-lookup"><span data-stu-id="52a98-149">Sometimes provisioning of an on-demand HDInsight cluster fails with the following error:</span></span>

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="52a98-150">Błąd ten wskazuje zazwyczaj, że lokalizacja konta magazynu określona w parametrze linkedServiceName znajduje się w innej lokalizacji centrum danych niż lokalizacja, w której następuje inicjowanie obsługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="52a98-150">This error usually indicates that the location of the storage account specified in the linkedServiceName is not in the same data center location where the HDInsight provisioning is happening.</span></span> <span data-ttu-id="52a98-151">Przykład: Jeśli fabrykę danych zachodnie stany USA i Magazyn Azure to w wschodnie stany USA, udostępniania na żądanie kończy się niepowodzeniem w zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="52a98-151">Example: if your data factory is in West US and the Azure storage is in East US, the on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="52a98-152">Ponadto występuje druga właściwość JSON o nazwie additionalLinkedServiceNames, w której można określić dodatkowe konta magazynu dla usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="52a98-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="52a98-153">Te dodatkowe połączone konta magazynu musi należeć do tej samej lokalizacji co klaster usługi HDInsight lub jego wykonanie nie powiodło się ten sam błąd.</span><span class="sxs-lookup"><span data-stu-id="52a98-153">Those additional linked storage accounts should be in the same location as the HDInsight cluster, or it fails with the same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="52a98-154">Problem: Niestandardowe działania .NET nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="52a98-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="52a98-155">Zobacz [debugowania potoku z działań niestandardowych](data-factory-use-custom-activities.md#troubleshoot-failures) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="52a98-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-to-troubleshoot"></a><span data-ttu-id="52a98-156">Rozwiązywanie problemów za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="52a98-156">Use Azure portal to troubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="52a98-157">Za pomocą portalu bloków</span><span class="sxs-lookup"><span data-stu-id="52a98-157">Using portal blades</span></span>
<span data-ttu-id="52a98-158">Zobacz [potoku Monitor](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) czynności.</span><span class="sxs-lookup"><span data-stu-id="52a98-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="52a98-159">Korzystanie z aplikacji Monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="52a98-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="52a98-160">Zobacz [monitorowanie i zarządzanie nimi przy użyciu monitora i zarządzanie aplikacjami potoki fabryki danych](data-factory-monitor-manage-app.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="52a98-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-to-troubleshoot"></a><span data-ttu-id="52a98-161">Rozwiązywanie problemów przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52a98-161">Use Azure PowerShell to troubleshoot</span></span>
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a><span data-ttu-id="52a98-162">Rozwiązywanie problemów z błędem przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="52a98-162">Use Azure PowerShell to troubleshoot an error</span></span>
<span data-ttu-id="52a98-163">Zobacz [fabryki danych monitora potoków przy użyciu programu Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="52a98-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
