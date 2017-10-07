---
title: "aaaAzure fabryki danych — przykłady"
description: "Szczegółowe informacje na temat przykłady, które są dostarczane z hello usługi fabryka danych Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: c0538b90-2695-4c4c-a6c8-82f59111f4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: aa1c15eca21b34b7bcc64358b685d7606baaf691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---samples"></a>Fabryki danych Azure — przykłady
## <a name="samples-on-github"></a>Przykłady z witryny GitHub
Witaj [repozytorium GitHub Azure-DataFactory](https://github.com/azure/azure-datafactory) zawiera kilka przykłady, które ułatwiają szybkie zwiększać usłudze fabryka danych Azure (lub) Zmodyfikuj skrypty hello i używać jej w własnych aplikacji. Hello Samples\JSON folder zawiera fragmenty kodu JSON dla typowych scenariuszy.

| Przykład | Opis |
|:--- |:--- |
| [Wskazówki ADF](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFWalkthrough) |W tym przykładzie przedstawiono wskazówki na trasie do przetwarzania plików dziennika przy użyciu fabryki danych Azure tooturn danych z plików dziennika w tooinsights. <br/><br/>W tym przewodniku hello potoku fabryki danych zbiera dzienniki próbki, procesów i wzbogaca hello dane z dzienników z danych referencyjnych i przekształca hello danych tooevaluate hello skuteczności kampanii marketingowych, która została ostatnio uruchomiona. |
| [Przykłady JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSON) |W tym przykładzie przedstawiono przykłady JSON dla typowych scenariuszy. |
| [Przykładowe narzędzie do pobierania danych http](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample) |Ten przykładowy pokazy pobieranie danych z tooAzure punktu końcowego HTTP magazynu obiektów Blob przy użyciu działań niestandardowych .NET. |
| [Krzyżowe próbki Net działanie elementu AppDomain kropka](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |W tym przykładzie umożliwia tooauthor działania niestandardowego .NET, który nie jest ograniczone wersji tooassembly używanych przez hello ADF uruchamiania (na przykład WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x itp.). |
| [Uruchom skrypt języka R](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample) |Ten przykład zawiera hello fabryki danych niestandardowe działanie, które mogą być używane tooinvoke RScript.exe. Ten przykład współdziała tylko z własnego klastra usługi HDInsight (nie. na żądanie), który jest już zainstalowany R na nim. |
| [Wywołanie zadań Spark dla klastra usługi HDInsight Hadoop](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/Spark) |W tym przykładzie pokazano sposób tooinvoke działania MapReduce toouse programu Spark. Hello spark program tylko kopiuje dane z jednego tooanother kontenera obiektów Blob platformy Azure. |
| [Za pomocą usługi Azure Machine Learning oceniania działania dotyczącego partii usługi analizy w usłudze Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-AzureMLBatchScoringActivity) |W tym przykładzie pokazano, jak toouse AzureMLBatchScoringActivity tooinvoke usługi Azure Machine Learning model, który przeprowadza analizę wskaźniki nastrojów klientów twitter, oceniania prognozowania itp. |
| [Analizy przy użyciu działań niestandardowych w usłudze Twitter](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |W tym przykładzie pokazano, jak toouse niestandardowych tooinvoke działania .NET modelu uczenia maszynowego Azure, który wykonuje twitter analizy wskaźniki nastrojów klientów, oceniania prognozowania itp. |
| [Sparametryzowane potoków dla usługi Azure Machine Learning](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ParameterizedPipelinesForAzureML/) |przykład Witaj zawiera end-to-end C# kodu toodeploy N potoki oceniania i ponownego trenowania, z którym hello listę regionów pochodzi z pliku parameters.txt, który znajduje się w tym przykładzie parametr inny region. |
| [Odwołanie do zadania usługi analiza strumienia Azure odświeżania danych](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ReferenceDataRefreshForASAJobs) |W tym przykładzie pokazano, jak toouse fabryki danych Azure i usługi Azure Stream Analytics razem toorun hello zapytania z odwołania hello dane i ustawienia odświeżania danych referencyjnych zgodnie z harmonogramem. |
| [Hybrydowe potok wraz z lokalną Hortonworks Hadoop](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HybridPipelineWithOnPremisesHortonworksHadoop) |Przykładowe Hello korzysta z lokalnego klastra usługi Hadoop jako docelowy obliczeń uruchomionych zadań w fabryce danych tak samo, jak należy dodać inne obiekty docelowe obliczeń jak HDInsight podstawie klastra usługi Hadoop w chmurze. |
| [Narzędzie konwersji JSON](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/JSONConversionTool) |To narzędzie umożliwia tooconvert JSONs toolatest too2015-07-01-preview z wcześniejszych wersji lub 2015-07-01-preview (ustawienie domyślne). |
| [Plik wejściowy próbki U-SQL](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/U-SQL%20Sample%20Input%20File) |Ten plik jest przykładowy plik używany przez działanie U-SQL. |
| [Usuń plik obiektu blob](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity) | W tym przykładzie ilustrację pliku C#, który może służyć jako część ADF niestandardowe .net działania toodelete pliki ze źródła hello lokalizacji obiektów Blob platformy Azure, po skopiowaniu plików hello.|

## <a name="azure-resource-manager-templates"></a>Szablony usługi Azure Resource Manager
Można znaleźć hello następujące szablony usługi Azure Resource Manager dla fabryki danych w witrynie GitHub.

| Szablon | Opis |
| --- | --- |
| [Kopiowanie z magazynu obiektów Blob Azure tooAzure bazy danych SQL](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-blob-to-sql-copy) |Wdrażanie ten szablon tworzy fabryki danych Azure z potokiem określenia kopie danych z hello Azure blob magazynu toohello — bazy danych Azure SQL |
| [Kopiowanie z tooAzure Salesforce magazynu obiektów Blob](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-salesforce-to-blob-copy) |Wdrażanie ten szablon tworzy fabryki danych Azure z potokiem kopie danych z hello określenia magazynu obiektów blob Azure toohello konta usług Salesforce. |
| [Przekształcanie danych za pomocą skryptu Hive w klastrze usługi HDInsight Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-data-factory-hive-transformation) |Wdrażanie ten szablon tworzy fabryki danych Azure z potokiem przekształcenia danych przez uruchomienie skryptu Hive próbki hello w klastrze usługi Azure HDInsight Hadoop. |

## <a name="samples-in-azure-portal"></a>Przykłady w portalu Azure
Można użyć hello **przykładowe potoki** kafelka na stronie głównej hello Twojej potokach próbki toodeploy fabryki danych i ich skojarzonych elementów (zestawy danych i połączone usługi) w fabryce danych tooyour.

1. Tworzenie fabryki danych lub Otwórz istniejącą fabrykę danych. Zobacz [kopiowanie danych z magazynu obiektów Blob tooSQL bazy danych przy użyciu fabryki danych](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) dla czynności toocreate fabryki danych.
2. W hello **FABRYKI danych** bloku dla fabryki danych hello, kliknij przycisk hello **przykładowe potoki** kafelka.

    ![Przykładowe potoki kafelka](./media/data-factory-samples/SamplePipelinesTile.png)
3. W hello **przykładowe potoki** bloku, kliknij przycisk hello **próbki** , które mają toodeploy.

    ![Przykład potoki bloku](./media/data-factory-samples/SampleTile.png)
4. Określ ustawienia konfiguracji dla przykładu hello. Na przykład z usługi Azure storage konta nazwy i klucza konta, nazwy serwera Azure SQL, bazy danych, identyfikator użytkownika i hasło itp.

    ![Przykładowe bloku](./media/data-factory-samples/SampleBlade.png)
5. Po wykonaniu Określanie ustawień konfiguracji hello, kliknij przycisk **Utwórz** toocreate/wdrażanie hello potoki próbki i usług/tabel połączonych używane przez hello potoków.
6. Zobacz hello stan wdrożenia na kafelku próbki hello kliknięty wcześniej hello **przykładowe potoki** bloku.

    ![Stan wdrożenia](./media/data-factory-samples/DeploymentStatus.png)
7. Po wyświetleniu hello **wdrożenie zakończyło się pomyślnie** wiadomość hello Kafelek dla przykładu hello, zamknij hello **przykładowe potoki** bloku.  
8. Na **FABRYKI danych** bloku, należy upewnić się, że połączone usługi, zestawy danych i potoki są dodany tooyour fabryki danych.  

    ![Blok Fabryka danych](./media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="samples-in-visual-studio"></a>Przykłady programu Visual Studio
### <a name="prerequisites"></a>Wymagania wstępne
Musi mieć zainstalowane na komputerze następujące hello:

* Visual Studio 2013 lub Visual Studio 2015
* Pobierz zestaw Azure SDK dla programu Visual Studio 2013 lub Visual Studio 2015. Przejdź za[strony pobierania Azure](https://azure.microsoft.com/downloads/) i kliknij przycisk **VS 2013** lub **VS 2015** w hello **.NET** sekcji.
* Pobierz najnowszy dodatek fabryki danych Azure hello for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) lub [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005). Jeśli używasz programu Visual Studio 2013, można także zaktualizować hello wtyczki, wykonując następujące kroki hello: polecenie hello menu **narzędzia** -> **rozszerzenia i aktualizacje**  ->  **Online** -> **galerii programu Visual Studio** -> **narzędzia fabryki danych Microsoft Azure dla programu Visual Studio**  ->  **Aktualizacji**.

### <a name="use-data-factory-templates"></a>Za pomocą szablonów fabryki danych
1. Kliknij przycisk **pliku** menu hello polecenie zbyt**nowy**i kliknij przycisk **projektu**.
2. W hello **nowy projekt** okna dialogowego pozycję hello następujące kroki:

   1. Wybierz **DataFactory** w obszarze **szablony**.
   2. Wybierz **szablony fabryki danych** w okienku po prawej stronie powitania.
   3. Wprowadź **nazwa** hello projektu.
   4. Wybierz **lokalizacji** hello projektu.
   5. Kliknij przycisk **OK**.

      ![Okno dialogowe Nowy projekt](./media/data-factory-samples/vs-new-project-adf-templates.png)
3. W hello **szablony fabryki danych** okno dialogowe, wybierz opcję hello przykładowy szablon z hello **przypadek użycia szablonów** sekcji, a następnie kliknij polecenie **dalej**. Witaj następujących krokach objaśniono sposób za pomocą hello **profilowania klienta** szablonu. Kroki są podobne do hello inne przykłady.

    ![Okno dialogowe Szablony fabryki danych](./media/data-factory-samples/vs-data-factory-templates-dialog.png)
4. W hello **konfiguracji fabryki danych** okna dialogowego, kliknij przycisk **dalej** na powitania **podstawy fabryki danych** strony.
5. Na powitania **fabryki danych skonfiguruj** pozycję hello następujące kroki:
   1. Wybierz **tworzenie nowych fabryki danych**. Możesz też wybrać **Użyj istniejącą fabrykę danych**.
   2. Wprowadź **nazwa** hello fabryki danych.
   3. Wybierz hello **subskrypcji platformy Azure** , w której chcesz toobe fabryki danych hello utworzony.
   4. Wybierz hello **grupy zasobów** hello fabryki danych.
   5. Wybierz hello **zachodnie stany USA**, **wschodnie stany USA**, lub **Europa Północna, Europa** dla hello **region**.
   6. Kliknij przycisk **Dalej**.
6. W hello **Konfigurowanie magazynów danych** Określ istniejącą **bazy danych Azure SQL** i **konto magazynu Azure** (lub) Utwórz bazę danych i magazynowania i kliknij przycisk Dalej.
7. W hello **Konfigurowanie obliczeń** , wybierz ustawienia domyślne i kliknij przycisk **dalej**.
8. W hello **Podsumowanie** strony, przejrzyj wszystkie ustawienia, a następnie kliknij przycisk **dalej**.
9. W hello **stan wdrożenia** strony, poczekaj na zakończenie hello wdrożenia, a następnie kliknij przycisk **Zakończ**.
10. Kliknij prawym przyciskiem myszy projekt w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **publikowania**.
11. Jeśli widzisz **Zaloguj tooyour konta Microsoft** okno dialogowe, wprowadź swoje poświadczenia dla konta hello subskrypcji platformy Azure, a następnie kliknij przycisk **Zaloguj**.
12. Powinny zostać wyświetlone następujące okno dialogowe hello:

    ![Okno dialogowe publikowania](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
13. W hello **fabryki danych skonfiguruj** pozycję hello następujące kroki:

    1. Upewnij się, że **Użyj istniejącą fabrykę danych** opcji.
    2. Wybierz hello **fabryki danych** miał wybierz podczas przy użyciu szablonu hello.
    3. Kliknij przycisk **dalej** tooswitch toohello **publikowania elementów** strony. (Naciśnij przycisk **kartę** toomove poza hello nazwę pola tooif hello **dalej** przycisk jest niedostępny.)
14. W hello **publikowania elementów** upewnij się, że wszystkie hello fabryki danych jednostek są zaznaczone, a następnie kliknij przycisk **dalej** tooswitch toohello **Podsumowanie** strony.     
15. Przejrzyj podsumowanie hello i kliknij przycisk **dalej** toostart hello wdrożenie procesu i sprawdź hello **stan wdrożenia**.
16. W hello **stan wdrożenia** strony, powinien zostać wyświetlony stan hello hello procesu wdrażania. Po ukończeniu wdrażania hello, kliknij przycisk Zakończ.

Zobacz [kompilacji pierwszy fabryki danych (Visual Studio)](data-factory-build-your-first-pipeline-using-vs.md) szczegółowe informacje o użyciu jednostek fabryki danych tooauthor programu Visual Studio i publikowania ich tooAzure.          
