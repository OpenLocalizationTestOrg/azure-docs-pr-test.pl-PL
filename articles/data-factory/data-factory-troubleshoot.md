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
# <a name="troubleshoot-data-factory-issues"></a>Rozwiązywanie problemów z usługą Data Factory
Ten artykuł zawiera wskazówki dotyczące rozwiązywania problemów w przypadku problemów przy użyciu fabryki danych Azure. W tym artykule nie wyświetlają hello ewentualne problemy w przypadku używania usługi hello, ale obejmuje pewne problemy i ogólne porady dotyczące rozwiązywania problemów.   

## <a name="troubleshooting-tips"></a>Wskazówki dotyczące rozwiązywania problemów
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Błąd: hello subskrypcji nie jest zarejestrowany toouse przestrzeni nazw "Microsoft.DataFactory"
Jeśli ten błąd jest wyświetlany, dostawcy zasobów usługi fabryka danych Azure hello nie zarejestrowano na tym komputerze. Witaj, po:

1. Uruchom program Azure PowerShell.
2. Zaloguj się za tooyour konto platformy Azure przy użyciu następującego polecenia hello.

    ```powershell
    Login-AzureRmAccount
    ```
3. Uruchom następujące polecenie tooregister hello fabryki danych Azure dostawcy hello.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Problem: Nieautoryzowanego błąd podczas uruchamiania polecenia cmdlet usługi fabryka danych
Prawdopodobnie nie jest używany prawo hello konto platformy Azure lub subskrypcji z hello Azure PowerShell. Witaj Użyj następującego polecenia cmdlet tooselect hello prawo Azure toouse konto i Subskrypcja z hello Azure PowerShell.

1. Login-AzureRmAccount - Użyj hello prawo użytkownika Identyfikatora i hasła
2. Get-AzureRmSubscription — Witaj wszystkie subskrypcje dla konta hello widoku.
3. SELECT-AzureRmSubscription &lt;Nazwa subskrypcji&gt; — Wybierz subskrypcję prawym hello. Użyj hello taki sam Użyj toocreate fabryki danych na powitania portalu Azure.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Problem: Niepowodzenie toolaunch Express ustawienia danych zarządzania bramy z portalu Azure
Ustawienia ekspresowe Hello hello brama zarządzania danymi wymaga programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce. W przypadku niepowodzenia toostart hello Express instalacji wykonaj jedną z następujących hello:

* Użyj programu Internet Explorer lub przeglądarki sieci web zgodne Microsoft ClickOnce.

    Jeśli używasz programu Chrome, przejdź toohello [sklepu Chrome web store](https://chrome.google.com/webstore/), wyszukaj ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.

    Witaj tego samego dla przeglądarki Firefox (Instalowanie dodatku). Kliknij przycisk Otwórz Menu na pasku narzędzi hello (trzy poziome linie w hello prawym górnym rogu), kliknij pozycję Dodatki wyszukiwania ze słowem kluczowym "ClickOnce", wybierz jedno z rozszerzeń ClickOnce hello i zainstaluj go.
* Użyj hello **Podręcznika instalacji** łącza wyświetlany na powitania tego samego bloku w portalu hello. Użyj tego podejścia toodownload instalacji pliku i uruchomić go ręcznie. Po instalacji hello zakończy się pomyślnie, wyświetlona okno dialogowe hello konfiguracji bramy zarządzania danymi. Kopiuj hello **klucza** z hello ekranu portalu i użycie go w hello configuration manager toomanually rejestrowanie bramy hello za pomocą usługi hello.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Problem: Niepowodzenie tooconnect tooon lokalnego programu SQL Server
Uruchom **Menedżera konfiguracji bramy zarządzania danymi** hello maszyna bramy i użyj hello **Rozwiązywanie problemów** karcie tootest hello tooSQL połączenia serwera z hello bramy maszyny. Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) porady dotyczące rozwiązywania problemów z bramy/połączenia problemy związane z.   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Problem: Wycinki danych wejściowych znajdują się w Oczekiwanie na kiedykolwiek stanu
wycinki Hello może być w **oczekiwania** stanu ukończenia toovarious powodów. Typowe przyczyny hello jest tym hello **zewnętrznych** nie ustawiono właściwości zbyt**true**. Wszelkie zestawu danych, który jest także hello poza zakresem fabryki danych Azure powinien być oznaczony przez **zewnętrznych** właściwości. Ta właściwość wskazuje, że hello danych jest zewnętrzne i nie kopii zapasowej przez dowolnego potoki w hello fabryki danych. wycinków danych Hello są oznaczone jako **gotowe** po hello dane są dostępne w magazynie odpowiednich hello.

Zobacz poniższy przykład użycia hello hello hello **zewnętrznych** właściwości. Opcjonalnie można określić **externalData*** podczas ustawiania zewnętrznych tootrue.

Zobacz [zestawów danych](data-factory-create-datasets.md) artykułu, aby uzyskać więcej informacji o tej właściwości.

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

tooresolve hello błąd, należy dodać hello **zewnętrznych** właściwości i opcjonalnie hello **externalData** sekcji toohello JSON definicję tabeli wejściowej hello i Utwórz ponownie hello tabeli.

### <a name="problem-hybrid-copy-operation-fails"></a>Problem: Operacja kopiowania hybrydowego kończy się niepowodzeniem.
Zobacz [rozwiązywania problemów bramy](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) dla kroki problemy tootroubleshoot z kopiowanie do/z lokalnymi danymi magazynu przy użyciu hello brama zarządzania danymi.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Problem: HDInsight na żądanie obsługi kończy się niepowodzeniem
Korzystając z połączonej usługi typu HDInsightOnDemand, należy toospecify linkedServiceName, który wskazuje tooan magazynu obiektów Blob Azure. Usługi fabryka danych używa tego magazynu toostore dzienników i pliki pomocnicze dla klastra usługi HDInsight na żądanie.  Czasami udostępnianie klastra usługi HDInsight na żądanie kończy się niepowodzeniem z hello następujący błąd:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Błąd ten zwykle wskazuje, że nie jest hello hello Lokalizacja konta magazynu hello określone w hello linkedServiceName centrum danych tej samej lokalizacji, w którym wykonywane hello HDInsight inicjowania obsługi administracyjnej. Przykład: Jeśli fabrykę danych zachodnie stany USA i hello Azure storage jest wschodnie stany USA, hello niepowodzenia inicjowania obsługi administracyjnej na żądanie w zachodnie stany USA.

Ponadto występuje druga właściwość JSON o nazwie additionalLinkedServiceNames, w której można określić dodatkowe konta magazynu dla usługi HDInsight na żądanie. Te dodatkowe połączone konta magazynu musi należeć do hello tej samej lokalizacji co klaster usługi HDInsight hello, lub zakończy się niepowodzeniem z hello tego samego błędu.

### <a name="problem-custom-net-activity-fails"></a>Problem: Niestandardowe działania .NET nie powiedzie się.
Zobacz [debugowania potoku z działań niestandardowych](data-factory-use-custom-activities.md#troubleshoot-failures) szczegółowy opis kroków.

## <a name="use-azure-portal-tootroubleshoot"></a>Użyj tootroubleshoot portalu Azure
### <a name="using-portal-blades"></a>Za pomocą portalu bloków
Zobacz [potoku Monitor](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) czynności.

### <a name="using-monitor-and-manage-app"></a>Korzystanie z aplikacji Monitorowanie i zarządzanie
Zobacz [monitorowanie i zarządzanie nimi przy użyciu monitora i zarządzanie aplikacjami potoki fabryki danych](data-factory-monitor-manage-app.md) szczegółowe informacje.

## <a name="use-azure-powershell-tootroubleshoot"></a>Użyj tootroubleshoot programu Azure PowerShell
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Użyj programu Azure PowerShell tootroubleshoot błąd
Zobacz [fabryki danych monitora potoków przy użyciu programu Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) szczegółowe informacje.

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
