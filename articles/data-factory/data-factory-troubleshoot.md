---
title: problemy z aaaTroubleshoot fabryki danych Azure
description: "Dowiedz się, jak tootroubleshoot problemy związane z przy użyciu fabryki danych Azure."
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
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="738b7-103">Rozwiązywanie problemów z usługą Data Factory</span><span class="sxs-lookup"><span data-stu-id="738b7-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="738b7-104">Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów w przypadku problemów przy użyciu fabryki danych Azure.</span><span class="sxs-lookup"><span data-stu-id="738b7-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="738b7-105">W tym artykule nie wyświetlają hello ewentualne problemy w przypadku używania usługi hello, ale obejmuje pewne problemy i ogólne porady dotyczące rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="738b7-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="738b7-106">Wskazówki dotyczące rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="738b7-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="738b7-107">Błąd: hello subskrypcji nie jest zarejestrowany toouse przestrzeni nazw "Microsoft.DataFactory"</span><span class="sxs-lookup"><span data-stu-id="738b7-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="738b7-108">Jeśli ten błąd jest wyświetlany, dostawcy zasobów usługi fabryka danych Azure hello nie zarejestrowano na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="738b7-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="738b7-109">Witaj, po:</span><span class="sxs-lookup"><span data-stu-id="738b7-109">Do hello following:</span></span>

1. <span data-ttu-id="738b7-110">Uruchom program Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="738b7-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="738b7-111">Zaloguj się za tooyour konto platformy Azure przy użyciu następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="738b7-112">Uruchom następujące polecenie tooregister hello fabryki danych Azure dostawcy hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="738b7-113">Problem: Nieautoryzowanego błąd podczas uruchamiania polecenia cmdlet usługi fabryka danych</span><span class="sxs-lookup"><span data-stu-id="738b7-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="738b7-114">Prawdopodobnie nie jest używany prawo hello konto platformy Azure lub subskrypcji z hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="738b7-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="738b7-115">Witaj Użyj następującego polecenia cmdlet tooselect hello prawo Azure toouse konto i Subskrypcja z hello Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="738b7-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="738b7-116">Login-AzureRmAccount - Użyj hello prawo użytkownika Identyfikatora i hasła</span><span class="sxs-lookup"><span data-stu-id="738b7-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="738b7-117">Get-AzureRmSubscription — Witaj wszystkie subskrypcje dla konta hello widoku.</span><span class="sxs-lookup"><span data-stu-id="738b7-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="738b7-118">SELECT-AzureRmSubscription &lt;Nazwa subskrypcji&gt; — Wybierz subskrypcję prawym hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="738b7-119">Użyj hello taki sam Użyj toocreate fabryki danych na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="738b7-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="738b7-120">Problem: Niepowodzenie toolaunch Express ustawienia danych zarządzania bramy z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="738b7-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="738b7-121">Ustawienia ekspresowe Hello hello brama zarządzania danymi wymaga programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="738b7-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="738b7-122">W przypadku niepowodzenia toostart hello Express instalacji wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="738b7-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="738b7-123">Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="738b7-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="738b7-124">Jeśli używasz programu Chrome, przejdź toohello [sklepu Chrome web store](https://chrome.google.com/webstore/), wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="738b7-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="738b7-125">Witaj tego samego dla przeglądarki Firefox (Instalowanie dodatku).</span><span class="sxs-lookup"><span data-stu-id="738b7-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="738b7-126">Kliknij przycisk Otwórz Menu na pasku narzędzi hello (trzy poziome linie w hello prawym górnym rogu), kliknij pozycję Dodatki wyszukiwania ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.</span><span class="sxs-lookup"><span data-stu-id="738b7-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="738b7-127">Użyj hello **Podręcznika instalacji** łącza wyświetlany na powitania tego samego bloku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="738b7-128">Użyj tego podejścia toodownload instalacji pliku i uruchomić go ręcznie.</span><span class="sxs-lookup"><span data-stu-id="738b7-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="738b7-129">Po instalacji hello zakończy się pomyślnie, wyświetlona okno dialogowe hello konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="738b7-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="738b7-130">Kopiuj hello **klucza** z hello ekranu portalu i użycie go w hello configuration manager toomanually rejestrowanie bramy hello za pomocą usługi hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="738b7-131">Problem: Niepowodzenie tooconnect tooon lokalnego programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="738b7-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="738b7-132">Uruchom **Menedżera konfiguracji bramy zarządzania danymi** hello maszyna bramy i użyj hello **Rozwiązywanie problemów** karcie tootest hello tooSQL połączenia serwera z hello bramy maszyny.</span><span class="sxs-lookup"><span data-stu-id="738b7-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="738b7-133">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.</span><span class="sxs-lookup"><span data-stu-id="738b7-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="738b7-134">Problem: Wycinki danych wejściowych znajdują się w Oczekiwanie na kiedykolwiek stanu</span><span class="sxs-lookup"><span data-stu-id="738b7-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="738b7-135">wycinki Hello może być w **oczekiwania** stanu ukończenia toovarious powodów.</span><span class="sxs-lookup"><span data-stu-id="738b7-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="738b7-136">Typowe przyczyny hello jest tym hello **zewnętrznych** nie ustawiono właściwości zbyt**true**.</span><span class="sxs-lookup"><span data-stu-id="738b7-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="738b7-137">Wszelkie zestawu danych, który jest także hello poza zakresem fabryki danych Azure powinien być oznaczony przez **zewnętrznych** właściwości.</span><span class="sxs-lookup"><span data-stu-id="738b7-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="738b7-138">Ta właściwość wskazuje, że hello danych jest zewnętrzne i nie kopii zapasowej przez dowolnego potoki w hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="738b7-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="738b7-139">wycinków danych Hello są oznaczone jako **gotowe** po hello dane są dostępne w magazynie odpowiednich hello.</span><span class="sxs-lookup"><span data-stu-id="738b7-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="738b7-140">Zobacz poniższy przykład użycia hello hello hello **zewnętrznych** właściwości.</span><span class="sxs-lookup"><span data-stu-id="738b7-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="738b7-141">Opcjonalnie można określić **externalData*** podczas ustawiania zewnętrznych tootrue.</span><span class="sxs-lookup"><span data-stu-id="738b7-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="738b7-142">Zobacz [zestawów danych](data-factory-create-datasets.md) artykułu, aby uzyskać więcej informacji o tej właściwości.</span><span class="sxs-lookup"><span data-stu-id="738b7-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

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

<span data-ttu-id="738b7-143">tooresolve hello błąd, należy dodać hello **zewnętrznych** właściwości i opcjonalnie hello **externalData** sekcji toohello JSON definicję tabeli wejściowej hello i Utwórz ponownie hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="738b7-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="738b7-144">Problem: Operacja kopiowania hybrydowego kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="738b7-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="738b7-145">Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) dla kroki problemy tootroubleshoot z kopiowanie do/z lokalnymi danymi magazynu przy użyciu hello brama zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="738b7-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="738b7-146">Problem: HDInsight na żądanie obsługi kończy się niepowodzeniem</span><span class="sxs-lookup"><span data-stu-id="738b7-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="738b7-147">Korzystając z połączonej usługi typu HDInsightOnDemand, należy toospecify linkedServiceName, który wskazuje tooan magazynu obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="738b7-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="738b7-148">Usługi fabryka danych używa tego magazynu toostore dzienników i pliki pomocnicze dla klastra usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="738b7-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="738b7-149">Czasami udostępnianie klastra usługi HDInsight na żądanie kończy się niepowodzeniem z hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="738b7-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="738b7-150">Błąd ten zwykle wskazuje, że nie jest hello hello Lokalizacja konta magazynu hello określone w hello linkedServiceName centrum danych tej samej lokalizacji, w którym wykonywane hello HDInsight inicjowania obsługi administracyjnej.</span><span class="sxs-lookup"><span data-stu-id="738b7-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="738b7-151">Przykład: Jeśli fabrykę danych zachodnie stany USA i hello Azure storage jest wschodnie stany USA, hello niepowodzenia inicjowania obsługi administracyjnej na żądanie w zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="738b7-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="738b7-152">Ponadto występuje druga właściwość JSON o nazwie additionalLinkedServiceNames, w której można określić dodatkowe konta magazynu dla usługi HDInsight na żądanie.</span><span class="sxs-lookup"><span data-stu-id="738b7-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="738b7-153">Te dodatkowe połączone konta magazynu musi należeć do hello tej samej lokalizacji co klaster usługi HDInsight hello, lub zakończy się niepowodzeniem z hello tego samego błędu.</span><span class="sxs-lookup"><span data-stu-id="738b7-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="738b7-154">Problem: Niestandardowe działania .NET nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="738b7-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="738b7-155">Zobacz [debugowania potoku z działań niestandardowych](data-factory-use-custom-activities.md#troubleshoot-failures) szczegółowy opis kroków.</span><span class="sxs-lookup"><span data-stu-id="738b7-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="738b7-156">Użyj tootroubleshoot portalu Azure</span><span class="sxs-lookup"><span data-stu-id="738b7-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="738b7-157">Za pomocą portalu bloków</span><span class="sxs-lookup"><span data-stu-id="738b7-157">Using portal blades</span></span>
<span data-ttu-id="738b7-158">Zobacz [potoku Monitor](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) czynności.</span><span class="sxs-lookup"><span data-stu-id="738b7-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="738b7-159">Korzystanie z aplikacji Monitorowanie i zarządzanie</span><span class="sxs-lookup"><span data-stu-id="738b7-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="738b7-160">Zobacz [monitorowanie i zarządzanie nimi przy użyciu monitora i zarządzanie aplikacjami potoki fabryki danych](data-factory-monitor-manage-app.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="738b7-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="738b7-161">Użyj tootroubleshoot programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="738b7-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="738b7-162">Użyj programu Azure PowerShell tootroubleshoot błąd</span><span class="sxs-lookup"><span data-stu-id="738b7-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="738b7-163">Zobacz [fabryki danych monitora potoków przy użyciu programu Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="738b7-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

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
