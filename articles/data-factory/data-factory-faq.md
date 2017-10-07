---
title: "aaaAzure fabryki danych — często zadawane pytania"
description: "Często zadawane pytania dotyczące usługi fabryka danych Azure."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 532dec5a-7261-4770-8f54-bfe527918058
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 78289fb4b6e15d74772af6c71ec25c7d2ca1a0bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---frequently-asked-questions"></a>Fabryka danych Azure — często zadawane pytania
## <a name="general-questions"></a>Pytania ogólne
### <a name="what-is-azure-data-factory"></a>Czym jest usługa Azure Data Factory?
Fabryka danych jest oparty na chmurze Usługa integracji danych **automatyzuje hello przepływu i przekształcania danych**. Podobnie jak fabryka, która uruchamia urządzeń tootake materiałów i przekształcania gotowych fabryki danych organizuje istniejących usług, które zbierać dane i przetransformować je w informacji gotowe do użycia.

Fabryka danych umożliwia toocreate przepływy pracy z danymi toomove danych między zarówno lokalnych i magazyny danych w chmurze jak i procesu/Przekształcanie danych za pomocą usług obliczeniowych, takich jak Azure HDInsight i usługą Azure Data Lake Analytics. Po utworzeniu potoku, która wykonuje akcję hello, które są potrzebne, można zaplanować toorun okresowo (co godzinę, codziennie, co tydzień itp.).   

Aby uzyskać więcej informacji, zobacz [Przegląd & kluczowe założenia](data-factory-introduction.md).

### <a name="where-can-i-find-pricing-details-for-azure-data-factory"></a>Gdzie można znaleźć szczegóły cennika dla fabryki danych Azure?
Zobacz [strony Szczegóły cennika fabryki danych] [ adf-pricing-details] dla hello cennik szczegóły hello fabryki danych Azure.  

### <a name="how-do-i-get-started-with-azure-data-factory"></a>Jak rozpocząć pracę z fabryki danych Azure?
* Omówienie usługi fabryka danych Azure, zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md).
* Samouczek na temat zbyt**skopiowania/przeniesienia danych** za pomocą działania kopiowania, zobacz [kopiowanie danych z magazynu obiektów Blob Azure tooAzure bazy danych SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* Samouczek na temat zbyt**przekształcania danych** za pomocą działania Hive HDInsight. Zobacz [przetwarzania danych przez uruchomienie skryptu Hive w klastrze usługi Hadoop](data-factory-build-your-first-pipeline.md)

### <a name="what-is-hello-data-factorys-region-availability"></a>Co to jest dostępność regionu fabryki danych hello?
Fabryka danych jest dostępna w **zachodnie nam** i **Europa Północna, Europa**. Witaj obliczeń i usługi magazynu używany przez fabryki danych może być w różnych regionach. Zobacz [obsługiwane regiony](data-factory-introduction.md#supported-regions).

### <a name="what-are-hello-limits-on-number-of-data-factoriespipelinesactivitiesdatasets"></a>Jakie są limity hello liczby danych fabryki/potoki/działań/zestaw danych?
Zobacz **limity fabryki danych Azure** sekcji hello [subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia](../azure-subscription-service-limits.md#data-factory-limits) artykułu.

### <a name="what-is-hello-authoringdeveloper-experience-with-azure-data-factory-service"></a>Co to jest środowisko tworzenia developer hello usłudze fabryka danych Azure?
Autor/tworzenia fabryki danych przy użyciu jednej z hello następujące narzędzia/zestawów SDK:

* **Azure portal** hello bloków fabryki danych w portalu Azure hello udostępniają interfejs użytkownika sformatowanego dla Ciebie usługi ad połączone fabryki danych toocreate. Witaj **Edytor fabryki danych**, która jest również częścią portalu hello pozwala tooeasily Utwórz połączone usługi, tabele zestawów danych i potoki, określając definicji JSON dla tych artefaktów. Zobacz [kompilacji swój pierwszy potok danych przy użyciu portalu Azure](data-factory-build-your-first-pipeline-using-editor.md) przykład użycia hello toocreate portal/edytora i wdrożyć fabryki danych.
* **Visual Studio** można użyć programu Visual Studio toocreate fabryki danych Azure. Zobacz [kompilacji swój pierwszy potok danych przy użyciu programu Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) szczegółowe informacje.
* **Program Azure PowerShell** zobacz [monitor fabryki danych Azure przy użyciu programu Azure PowerShell i Utwórz](data-factory-build-your-first-pipeline-using-powershell.md) samouczek/Przewodnik tworzenia fabryki danych przy użyciu programu PowerShell. Zobacz [odwołania do polecenia Cmdlet fabryki danych] [ adf-powershell-reference] zawartości w bibliotece MSDN dla pełna dokumentacja poleceń cmdlet fabryki danych.
* **Biblioteka klas programu .NET** programowego można utworzyć fabryki danych przy użyciu zestawu .NET SDK fabryki danych. Zobacz [tworzenie, monitorowanie i zarządzanie nimi przy użyciu zestawu .NET SDK fabryki danych](data-factory-create-data-factories-programmatically.md) Przewodnik tworzenia fabryki danych przy użyciu zestawu .NET SDK. Zobacz [odwołanie do biblioteki klasy fabryki danych] [ msdn-class-library-reference] kompleksowe dokumentacji zestawu SDK .NET fabryki danych.
* **Interfejs API REST** można również używać hello udostępnianych przez toocreate usługi fabryka danych Azure hello interfejsu API REST i wdróż fabryki danych. Zobacz [dokumentacja interfejsu API REST fabryki danych] [ msdn-rest-api-reference] dla pełna dokumentacja interfejsu API REST fabryki danych.
* **Szablonu usługi Azure Resource Manager** zobacz [samouczek: Tworzenie pierwszego fabrykę danych Azure przy użyciu szablonu usługi Azure Resource Manager](data-factory-build-your-first-pipeline-using-arm.md) fo szczegóły.

### <a name="can-i-rename-a-data-factory"></a>Czy można zmienić fabryki danych?
Nie. Podobnie jak inne zasoby platformy Azure nie można zmienić nazwy hello fabryki danych Azure.

### <a name="can-i-move-a-data-factory-from-one-azure-subscription-tooanother"></a>Można przenieść fabryka danych z jednego tooanother subskrypcji platformy Azure?
Tak. Użyj hello **Przenieś** przycisku w bloku fabryki danych, jak pokazano w powitania po diagramu:

![Przenieś fabryki danych](media/data-factory-faq/move-data-factory.png)

### <a name="what-are-hello-compute-environments-supported-by-data-factory"></a>Co to są hello środowiska obliczeniowe obsługiwane przez fabryki danych?
Witaj Poniższa tabela zawiera listę środowiska obliczeniowe obsługiwane przez fabrykę danych oraz hello działania, które można uruchomić na nich.

| Środowisko obliczeniowe | activities |
| --- | --- |
| [Klaster usługi HDInsight na żądanie](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) lub [klastrem usługi HDInsight](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md) |
| [Partia zadań Azure](data-factory-compute-linked-services.md#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure Machine Learning](data-factory-compute-linked-services.md#azure-machine-learning-linked-service) |[Działania usługi Machine Learning: wykonywanie wsadowe i aktualizacja zasobów](data-factory-azure-ml-batch-execution-activity.md) |
| [Usługi Azure Data Lake Analytics](data-factory-compute-linked-services.md#azure-data-lake-analytics-linked-service) |[Język U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md) |
| [Azure SQL](data-factory-compute-linked-services.md#azure-sql-linked-service), [magazyn danych Azure SQL](data-factory-compute-linked-services.md#azure-sql-data-warehouse-linked-service), [programu SQL Server](data-factory-compute-linked-services.md#sql-server-linked-service) |[Procedura składowana](data-factory-stored-proc-activity.md) |

### <a name="how-does-azure-data-factory-compare-with-sql-server-integration-services-ssis"></a>Jak fabryki danych Azure porównania z programu SQL Server Integration Services (SSIS)? 
Zobacz hello [vs fabryki danych Azure. SSIS](http://www.sqlbits.com/Sessions/Event15/Azure_Data_Factory_vs_SSIS) prezentacji z jednego z naszych MVP (najbardziej ważnych specjalistów): Reza Rad. Niektóre hello najnowszych zmian w fabryce danych może nie znajdować hello pokaz slajdów. Firma Microsoft stale dodawane więcej możliwości tooAzure fabryki danych. Firma Microsoft stale dodawane więcej możliwości tooAzure fabryki danych. Firma Microsoft będzie włączyć te aktualizacje do porównania hello danych integrację technologii firmy Microsoft chwilę później w tym roku.   

## <a name="activities---faq"></a>Działania — często zadawane pytania
### <a name="what-are-hello-different-types-of-activities-you-can-use-in-a-data-factory-pipeline"></a>Co to są hello różne rodzaje działań, do których można używać w potoku fabryki danych?
* [Działania przepływu danych](data-factory-data-movement-activities.md) toomove danych.
* [Działania przekształcania danych](data-factory-data-transformation-activities.md) tooprocess/przekształcenia danych.

### <a name="when-does-an-activity-run"></a>Gdy działanie jest uruchamiane?
Witaj **dostępności** ustawienia konfiguracji w hello output tabeli danych określa, po uruchomieniu działania hello. Jeśli podano zestawów danych wejściowych, działanie hello sprawdza, czy spełnione są wszystkie zależności w danych wejściowych hello (to znaczy **gotowe** stanu) przed jej uruchomienie.

## <a name="copy-activity---faq"></a>Kopiuj działania — często zadawane pytania
### <a name="is-it-better-toohave-a-pipeline-with-multiple-activities-or-a-separate-pipeline-for-each-activity"></a>Jest to lepszą toohave potoku z wielu działań lub oddzielnego potoku dla każdego działania?
Potoki powinni działań związanych z toobundle. Jeśli hello zestawów danych, które łączą te elementy nie są używane przez inne działania poza hello potoku, można przechowywać hello działania w jednej potoku. Dzięki temu nie trzeba toochain potoku aktywnych okresów tak aby były one ze sobą. Ponadto hello integralność danych w potoku wewnętrzny toohello tabel hello lepiej są zachowywane podczas aktualizowania potoku hello. Zasadniczo potoku aktualizacji zatrzymuje wszystkie działania hello w potoku hello, usuwa je i tworzy je ponownie. Z perspektywy tworzenia może również być łatwiejsze toosee hello przepływu danych w ramach hello związane z działania w formacie JSON jeden plik hello potoku.

### <a name="what-are-hello-supported-data-stores"></a>Co to są hello obsługiwane magazyny danych?
Działanie kopiowania w fabryce danych kopiuje dane z magazynu danych źródła danych magazynu tooa ujścia. Fabryka danych obsługuje powitania po magazynów danych. Obiekt sink tooany można zapisać danych z dowolnego źródła. Kliknij przycisk toolearn magazynu danych, jak toocopy tooand danych z tego magazynu.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Przechowuje dane z * można lokalnie lub na platformie Azure IaaS i wymaga tooinstall [brama zarządzania danymi](data-factory-data-management-gateway.md) na maszynie IaaS na lokalnym/Azure.

### <a name="what-are-hello-supported-file-formats"></a>Co to są hello obsługiwane formaty plików?
[!INCLUDE [data-factory-file-format](../../includes/data-factory-file-format.md)]

### <a name="where-is-hello-copy-operation-performed"></a>Gdzie jest wykonywane hello operacji kopiowania
Zobacz [przenoszenia danych dostępnego globalnie](data-factory-data-movement-activities.md#global) sekcji, aby uzyskać szczegółowe informacje. Krótko mówiąc gdy uczestniczy z lokalnym magazynem danych, operacji kopiowania hello jest wykonywane przez hello brama zarządzania danymi w środowisku lokalnym. I gdy hello przenoszenia danych między dwa sklepy chmury, operacji kopiowania hello jest wykonywane w hello region najbliższy toohello zbiornika lokalizacji w hello tej samej lokalizacji geograficznej.

## <a name="hdinsight-activity---faq"></a>Działanie usługi HDInsight — często zadawane pytania
### <a name="what-regions-are-supported-by-hdinsight"></a>Jakie regiony są obsługiwane przez HDInsight?
Zobacz sekcję dotyczącą dostępności geograficznej w hello poniższego artykułu hello: lub [szczegóły cennika usługi HDInsight][hdinsight-supported-regions].

### <a name="what-region-is-used-by-an-on-demand-hdinsight-cluster"></a>Jakie region jest używane przez klaster usługi HDInsight na żądanie?
Witaj klastra usługi HDInsight na żądanie jest tworzony w hello sam region, w którym istnieje magazyn hello określony toobe używany z klastrem hello.    

### <a name="how-tooassociate-additional-storage-accounts-tooyour-hdinsight-cluster"></a>Jak tooassociate dodatkowy magazyn kont tooyour klastra usługi HDInsight?
Jeśli korzystasz z własnego klastra usługi HDInsight (BYOC - Przenieś swój własny klastra), zobacz następujące tematy hello:

* [Używanie klastra usługi HDInsight z kont magazynu alternatywny i magazyny][hdinsight-alternate-storage]
* [Użyj dodatkowych kont magazynu przy użyciu HDInsight Hive][hdinsight-alternate-storage-2]

Jeśli korzystasz z klastra na żądanie, który jest tworzony przez hello usługi fabryka danych, określ dodatkowe konta magazynu dla hello HDInsight połączonej usługi, dzięki czemu usługi fabryka danych hello można zarejestrować je w Twoim imieniu. W definicji JSON połączonej usługi na żądanie hello hello, użyj **additionalLinkedServiceNames** kont magazynu alternatywny toospecify właściwości pokazane na powitania po fragment kodu JSON:

```JSON
{
    "name": "MyHDInsightOnDemandLinkedService",
    "properties":
    {
        "type": "HDInsightOnDemandLinkedService",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "LinkedService-SampleData",
            "additionalLinkedServiceNames": [ "otherLinkedServiceName1", "otherLinkedServiceName2" ]
        }
    }
}
```
W powyższym przykładzie hello otherLinkedServiceName1 i otherLinkedServiceName2 reprezentują połączone usługi, których definicje zawiera poświadczenia, które hello HDInsight klastra musi tooaccess magazynu alternatywnego konta.

## <a name="slices---faq"></a>Wycinki — często zadawane pytania
### <a name="why-are-my-input-slices-not-in-ready-state"></a>Dlaczego są moje wycinków wejściowy nie jest w stanie gotowe?
Powszechnym błędem jest to ustawienie nie zostanie **zewnętrznych** właściwości zbyt**true** na powitania wejściowy zestaw danych, gdy dane wejściowe hello jest fabryki danych zewnętrznych toohello (nie produkowane przez hello fabryki danych).

W hello poniższy przykład, wystarczy tooset **zewnętrznych** tootrue na **dataset1**.  

**DataFactory1** potoku 1: dataset1 -> działania activity1 -> dataset2 -> activity2 -> potoku dataset3 2: dataset3 -> activity3 -> dataset4

Jeśli masz inną fabryka danych z potok, który przyjmuje dataset4 (utworzonych w ramach potoku 2 w fabryce danych 1), należy oznaczyć dataset4 jako zewnętrzny zestaw danych, ponieważ zestaw danych hello jest generowany przez fabrykę danych (DataFactory1, nie DataFactory2).  

**DataFactory2**    
Potok 1: działanie activity4 -> dataset4 -> dataset5

Właściwość zewnętrznych hello są ustawione właściwie, sprawdź, czy w lokalizacji hello określone w definicji zestawu danych wejściowych hello istnieje hello danych wejściowych.

### <a name="how-toorun-a-slice-at-another-time-than-midnight-when-hello-slice-is-being-produced-daily"></a>Jak toorun wycinka w innym czasie niż północy po wycinek hello jest tworzonym codziennie?
Użyj hello **przesunięcie** czasu hello toospecify właściwości ma toobe wycinka hello utworzone. Zobacz [dostępności zestawu danych](data-factory-create-datasets.md#dataset-availability) sekcji, aby uzyskać szczegółowe informacje o tej właściwości. Poniżej przedstawiono prosty przykład:

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
Codzienne wycinków rozpoczęli **6: 00** zamiast hello domyślne północy.     

### <a name="how-can-i-rerun-a-slice"></a>Jak można ponownie uruchomić wycinek?
Można uruchomić wycinka w jednym z hello następujące sposoby:

* Użyj monitora i zarządzanie aplikacjami toorerun okno działania lub wycinka. Zobacz [Uruchom ponownie wybrane działanie windows](data-factory-monitor-manage-app.md#perform-batch-actions) instrukcje.   
* Kliknij przycisk **Uruchom** na pasku poleceń hello na powitania **WYCINKA danych** bloku hello wycinek hello portalu Azure.
* Uruchom **AzureRmDataFactorySliceStatus zestaw** polecenia cmdlet, o stanie ustawić także**oczekiwania** dla hello wycinka.   

    ```PowerShell
    Set-AzureRmDataFactorySliceStatus -Status Waiting -ResourceGroupName $ResourceGroup -DataFactoryName $df -TableName $table -StartDateTime "02/26/2015 19:00:00" -EndDateTime "02/26/2015 20:00:00"
    ```
Zobacz [AzureRmDataFactorySliceStatus zestaw] [ set-azure-datafactory-slice-status] szczegółowe informacje na temat polecenia cmdlet hello.

### <a name="how-long-did-it-take-tooprocess-a-slice"></a>Jak długo trwało tooprocess wycinek?
Użyj Eksploratora okna działania w tooknow Monitor & Zarządzanie aplikacji, jak długo trwało tooprocess wycinka danych. Zobacz [działania okna Eksploratora](data-factory-monitor-manage-app.md#activity-window-explorer) szczegółowe informacje.

Możesz również wykonać hello po w hello portalu Azure:  

1. Kliknij przycisk **zestawów danych** Kafelek na powitania **FABRYKI danych** bloku fabryką danych.
2. Kliknij przycisk hello określonego zestawu danych na powitania **zestawów danych** bloku.
3. Wybierz hello wycinek, który chcesz z hello **ostatnich wycinków** listy na powitania **tabeli** bloku.
4. Kliknij przycisk uruchamiania z hello działania hello **uruchomień działania** listy na powitania **WYCINKA danych** bloku.
5. Kliknij przycisk **właściwości** Kafelek na powitania **szczegóły uruchomienia działania** bloku.
6. Powinny pojawić się hello **czas trwania** pole z wartością. Ta wartość jest czas hello tooprocess hello wycinka.   

### <a name="how-toostop-a-running-slice"></a>Jak toostop wycinek uruchomiona?
Jeśli potrzebujesz potoku hello toostop wykonywanie, możesz użyć [Suspend-AzureRmDataFactoryPipeline](/powershell/module/azurerm.datafactories/suspend-azurermdatafactorypipeline) polecenia cmdlet. Obecnie wstrzymywania potoku hello nie zatrzymuje wykonaniami wycinek hello, które są w toku. Po Zakończ hello w trakcie wykonania nie dodatkowych wycinek zostaje pobrana.

Czy na pewno chcesz toostop wszystkie wykonaniami hello natychmiast, hello tylko sposób może być toodelete hello potoku i utwórz go ponownie. Jeśli wybierzesz toodelete hello potoku, nie trzeba toodelete tabele i połączone usługi używane przez potok hello.

[create-factory-using-dotnet-sdk]: data-factory-create-data-factories-programmatically.md
[msdn-class-library-reference]: /dotnet/api/microsoft.azure.management.datafactories.models
[msdn-rest-api-reference]: /rest/api/datafactory/

[adf-powershell-reference]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/azurerm.datafactories
[azure-portal]: http://portal.azure.com
[set-azure-datafactory-slice-status]: /powershell/resourcemanager/azurerm.datafactories/v2.3.0/set-azurermdatafactoryslicestatus

[adf-pricing-details]: http://go.microsoft.com/fwlink/?LinkId=517777
[hdinsight-supported-regions]: http://azure.microsoft.com/pricing/details/hdinsight/
[hdinsight-alternate-storage]: http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx
[hdinsight-alternate-storage-2]: http://blogs.msdn.com/b/cindygross/archive/2014/05/05/use-additional-storage-accounts-with-hdinsight-hive.aspx
