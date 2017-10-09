---
title: "tooData aaaIntroduction fabryki, usługa integracji danych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, czym jest usługa Azure Data Factory: usługa integracji danych w chmurze, która służy do aranżacji i automatyzacji przenoszenia i przekształcania danych."
keywords: "integracja danych, integracja danych w chmurze, czym jest usługa azure data factory"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: cec68cb5-ca0d-473b-8ae8-35de949a009e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 4cc30515315efc938951057743ff8eb3701214ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-data-factory"></a>Wprowadzenie tooAzure fabryki danych 
## <a name="what-is-azure-data-factory"></a>Czym jest usługa Azure Data Factory?
Witaj świecie danych big jak jest istniejących danych wykorzystywana w firmie? Jest to możliwe tooenrich danych wygenerowanych w chmurze hello przy użyciu danych referencyjnych z lokalnych źródeł danych lub innych różnych źródeł danych? Na przykład firma gier zbiera wiele dzienniki generowane przez gry w chmurze hello. Chce tooanalyze te dzienniki insights toogain toocustomer preferencje, demograficznymi, zachowanie użycia możliwości sprzedaży w górę i sprzedaży itd. tooidentify, tworzenie nowych atrakcyjnej rozwoju firmy toodrive funkcje i lepsze środowisko pracy toocustomers. 

tooanalyze te dzienniki hello firmy wymaga danych referencyjnych hello toouse, takie jak informacje o kliencie, informacji gier, marketingu informacje kampanii, które znajduje się w magazynie danych lokalnych. W związku z tym hello firma chce tooingest danych dziennika z magazynu danych w chmurze hello i danych referencyjnych z magazynu danych lokalne powitania. Następnie proces hello danych przy użyciu platformy Hadoop w hello chmury (Azure HDInsight) i opublikować wynik hello magazynu danych do magazynu danych chmury, takich jak magazyn danych SQL Azure lub danych lokalnych, takich jak SQL Server. Chce toorun ten przepływ pracy co tydzień raz. 

Potrzebna jest to platforma, która umożliwia toocreate firmy hello przepływu pracy, który może pozyskiwania dane, zarówno lokalnie, jak i magazynów danych w chmurze i Przekształć lub procesu przy użyciu istniejących usług obliczeniowych, takich jak Hadoop i publikować hello wyniki tooan lokalnej lub w chmurze BI tooconsume aplikacji w magazynie danych. 

![Omówienie usługi Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Fabryka danych Azure to platforma hello tego rodzaju scenariusze. Jest **Usługa integracji danych opartych na chmurze, która pozwala przepływów pracy opartych na danych toocreate w chmurze hello organizowanie i automatyzowanie przenoszenia danych i przekształcania danych**. Przy użyciu fabryki danych Azure, możesz utworzyć i zaplanować opartych na danych przepływów pracy (nazywanym potoki), które można pozyskiwania danych z różnych magazynów, proces/przekształcania danych hello za pomocą usług obliczeniowych, takich jak Azure HDInsight Hadoop, Spark, usługa Azure Data Lake Analizy i usługi Azure Machine Learning i publikowanie danych wyjściowych danych toodata przechowuje takie jak magazyn danych SQL Azure dla tooconsume aplikacje programu business intelligence (BI).  

To bardziej platforma, która najpierw wyodrębnia i ładuje, a następnie przekształca i ładuje, niż tradycyjna platforma wyodrębniania, przekształcania i ładowania. przekształcenia Hello, które są wykonywane są tootransform/przetwarzania danych przy użyciu usług obliczeniowych, zamiast przekształcenia tooperform, takich jak hello te dodawania pochodnych kolumn zliczania wierszy, sortowanie danych itp. 

Obecnie w fabryce danych Azure, dane hello jest używane i produkowane przez przepływy pracy są **podział czasu danych** (co godzinę, codziennie, co tydzień, itp.). Na przykład potok może odczytać dane wejściowe, przetworzyć je i wygenerować dane wyjściowe raz dziennie. Przepływ pracy można także uruchomić tylko jeden raz.  
  

## <a name="how-does-it-work"></a>Jak to działa? 
potoki Hello (przepływów pracy opartych na danych) w fabryce danych Azure na ogół wykonać hello następujące trzy kroki:

![Trzy etapy działania usługi Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Łączenie i zbieranie
Dane używane w przedsiębiorstwach mają różne typy i znajdują się w rozproszonych źródłach. Witaj pierwszym krokiem tworzenia systemu produkcji informacji jest tooconnect tooall hello wymagane źródeł danych i przetwarzania, takich jak usługi SaaS, usługi sieci web udziałów, FTP, plików i przenieść hello danych wymagane tooa scentralizowane lokalizację dla kolejnych przetwarzanie.

Bez fabryki danych przedsiębiorstwa musi kompilacji składniki przepływu danych niestandardowych lub zapisać toointegrate usługi niestandardowe tych źródeł danych i przetwarzania. Jest kosztowne i twardych toointegrate i obsługa takich systemów i często brakuje klasy enterprise hello monitorowania oraz alertów i formantów hello, które może zaoferować w pełni zarządzana usługa.

Przy użyciu fabryki danych można użyć hello działanie kopiowania w potoku danych toomove danych z lokalnie i w chmurze źródło magazynów tooa centralizacji danych magazynu danych w chmurze hello w celu dalszej analizy. Na przykład można zebrać danych usługi Azure Data Lake Store i transformacja hello później za pomocą usługi Azure Data Lake Analytics obliczeń. Można też pobrać dane z usługi Azure Blob Storage, aby przekształcić je przy użyciu klastra usługi Azure HDInsight na platformie Hadoop.

### <a name="transform-and-enrich"></a>Przekształcanie i wzbogacanie
Gdy dane są obecne w magazynie danych scentralizowane w chmurze hello, ma toobe danych hello zbierane, przetwarzane lub przekształcone przy użyciu usług obliczeniowych, takich jak HDInsight Hadoop, Spark, Data Lake Analytics i uczenia maszynowego. Ma tooreliably produktu przekształcone dane danymi w środowiskach produkcyjnych toofeed harmonogram łatwy w obsłudze i kontrolowane zaufanych. 

### <a name="publish"></a>Publikowanie 
Dostarczenia przekształcone dane z chmury hello tooon lokalnych źródeł, takich jak SQL Server, czy też pozostawić go w chmurze źródeł magazynu do użycia przez analizy biznesowej (BI) i narzędzia do analizy i inne aplikacje.

## <a name="key-components"></a>Główne składniki
Subskrypcja platformy Azure może zawierać jedno lub więcej wystąpień usługi Azure Data Factory (lub fabryk danych). Fabryka danych Azure składa się z czterech najważniejsze składniki, które współpracują ze sobą tooprovide hello platformy, na którym można utworzyć, opartych na danych przepływy pracy z danymi toomove i transformacja kroki. 

### <a name="pipeline"></a>Potok
Fabryka danych może obejmować jeden lub wiele potoków. Potok jest grupą działań, Razem hello działań w potoku wykonania zadania. Na przykład potoku może zawierać grupy działań, który wysyła strumień danych z obiektów blob platformy Azure, a następnie uruchom zapytanie Hive na dane hello toopartition klastra usługi HDInsight. korzyści Hello tego jest tego potoku hello pozwala toomanage hello działania zgodnie z ustaleniami zamiast każdego z nich osobno. Można na przykład wdrożyć i zaplanować potoku hello, zamiast działania hello niezależnie. 

### <a name="activity"></a>Działanie
Potok może obejmować jedno lub wiele działań. Działania zdefiniować hello akcje tooperform danych. Na przykład może użyć toocopy działania kopiowania danych z magazynu danych tooanother jednego danych w magazynie. Podobnie możesz użyć działania Hive, uruchamianej zapytań programu Hive w usłudze Azure HDInsight tootransform klastra lub analizowania danych. Usługa Data Factory obsługuje dwa typy działań — w zakresie przekształcania oraz przenoszenia danych.

### <a name="data-movement-activities"></a>Działania dotyczące przenoszenia danych
Działanie kopiowania w fabryce danych kopiuje dane z magazynu danych źródła danych magazynu tooa ujścia. Fabryka danych obsługuje powitania po magazynów danych. Obiekt sink tooany można zapisać danych z dowolnego źródła. Kliknij przycisk toolearn magazynu danych, jak toocopy tooand danych z tego magazynu.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przenoszenia danych](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Działania dotyczące przekształcania danych
[!INCLUDE [data-factory-transformation-activities](../../includes/data-factory-transformation-activities.md)]

Aby uzyskać więcej informacji, zobacz artykuł [Działania dotyczące przekształcania danych](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Niestandardowe działania programu .NET
Jeśli potrzebujesz toomove danych do/z magazynu danych danego działania kopiowania nie obsługuje, lub Przekształcanie danych za pomocą własną logikę, Utwórz **działania niestandardowego .NET**. Aby uzyskać szczegółowe informacje na temat tworzenia i używania niestandardowego działania, zobacz artykuł [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) (Korzystanie z niestandardowych działań w potoku usługi Azure Data Factory).

### <a name="datasets"></a>Zestawy danych
Każde działanie pobiera 0 lub więcej zestawów danych jako dane wejściowe i generuje co najmniej jeden zestaw danych jako dane wyjściowe. Zestawy danych reprezentują struktury danych w ramach hello magazyny danych, które po prostu punktu lub odwołać hello dane, które mają toouse w działaniach jako danych wejściowych lub wyjściowych. Na przykład zestaw danych obiektów Blob platformy Azure określa hello kontenera obiektów blob i folder w magazynie obiektów Blob Azure hello z których hello potoku odczytywane dane hello. Lub zestaw tabel SQL Azure Określa dane wyjściowe hello toowhich tabeli hello są zapisywane przez działanie hello. 

### <a name="linked-services"></a>Połączone usługi
Połączone usługi są podobne do parametrów połączenia, które definiują informacje o połączeniu hello wymagane dla fabryki danych tooconnect tooexternal zasobów. Należy traktować go w ten sposób — źródło danych toohello połączenia hello definiuje połączonej usługi i hello struktury danych hello reprezentuje zestaw danych. Na przykład połączoną usługą magazynu Azure Określa konto Azure Storage toohello tooconnect ciąg połączenia. I zestawu danych obiektów Blob platformy Azure określa hello kontenera obiektów blob i hello folder, który zawiera dane hello.   

Połączone usługi w usłudze Fabryka danych służą do dwóch celów:

* toorepresent **magazynu danych** tym między innymi do lokalnego programu SQL Server, bazy danych Oracle, udziału plików lub konta magazynu obiektów Blob Azure. Zobacz hello [działań przepływu danych](#data-movement-activities) sekcja zawiera listę magazynów obsługiwane dane.
* toorepresent **zasoby obliczeniowe** który może obsługiwać hello wykonywania działania. Na przykład hello HDInsightHive działanie uruchamia w klastrze usługi HDInsight Hadoop. Listę obsługiwanych środowisk obliczeniowych można znaleźć w sekcji [Data transformation activities](#data-transformation-activities) (Działania przekształcania danych).

### <a name="relationship-between-data-factory-entities"></a>Relacje między obiektami usługi Data Factory
![Diagram: Data Factory, usługa integracji danych w chmurze — najważniejsze pojęcia](./media/data-factory-introduction/data-integration-service-key-concepts.png)
**Rysunek 2.** Relacje między elementami Zestaw danych, Działanie, Potok i Połączona usługa

## <a name="supported-regions"></a>Obsługiwane regiony
Obecnie można utworzyć fabryki danych w hello **zachodnie stany USA**, **wschodnie stany USA**, i **Europa Północna, Europa** regionów. Jednak obliczeniowe usług w innych danych toomove regiony platformy Azure między magazynów danych i dostępne magazyny danych fabryki danych lub przetwarzania danych przy użyciu obliczeniowe usług.

Sama usługa Fabryka danych Azure nie przechowuje żadnych danych. Umożliwia tworzenie przepływów pracy z danymi tooorchestrate przepływu danych między [obsługiwane magazyny danych](#data-movement-activities) i przetwarzania danych przy użyciu [obliczeniowe usług](#data-transformation-activities) w innych regionów lub lokalnego środowisko. Umożliwia ona również zbyt[monitorować i zarządzać nimi przepływy pracy](data-factory-monitor-manage-pipelines.md) za pomocą obu programowych i mechanizmów interfejsu użytkownika.

Mimo że fabryki danych jest dostępna tylko w **zachodnie stany USA**, **wschodnie stany USA**, i **Europa Północna, Europa** regionach, jest dostępna usługa hello Włączanie hello przenoszenia danych z fabryki danych [globalnie](data-factory-data-movement-activities.md#global) w wielu regionach. Jeśli magazyn danych znajduje się za zaporą, a następnie [brama zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) zainstalowany w danych hello przenosi środowiska lokalnego.

Załóżmy na przykład, że środowiska obliczeniowe, takie jak klaster usługi Azure HDInsight i usługa Azure Machine Learning, są uruchamiane z regionu Europa Zachodnia. Można tworzyć i użyj wystąpienia fabryki danych Azure w Europa Północna i należy jej używać tooschedule zadania na środowiska obliczeniowego w Europie zachodnie. Zajmuje kilka milisekund dla fabryki danych tootrigger hello zadania w środowisku obliczeń, ale nie zmienia hello czas uruchomienia zadania hello na środowisko przetwarzania danych.

## <a name="get-started-with-creating-a-pipeline"></a>Rozpoczynanie tworzenia potoku
Można użyć jednej z tych narzędzi i potoki danych toocreate interfejsów API w fabryce danych Azure: 

- Azure Portal
- Visual Studio
- PowerShell
- Interfejs API .NET
- Interfejs API REST
- Szablon usługi Azure Resource Manager 

toolearn jak potoków toobuild fabryki danych z danymi, wykonaj instrukcje krok po kroku w hello następujące samouczki:

| Samouczek | Opis |
| --- | --- |
| [Przenoszenie danych między dwoma magazynami danych w chmurze](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |W tym samouczku utworzysz fabryki danych z potoku który **przenosi dane** z bazy danych tooSQL magazynu obiektów Blob. |
| [Przekształcanie danych przy użyciu klastra Hadoop](data-factory-build-your-first-pipeline.md) |W tym samouczku utworzysz pierwszą fabrykę danych platformy Azure przy użyciu potoku danych, który **przetwarza dane**, uruchamiając skrypt Hive w klastrze Azure HDInsight (Hadoop). |
| [Przenoszenie danych między lokalnym magazynem danych i magazynem danych w chmurze przy użyciu bramy zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) |W tym samouczku tworzenia fabryki danych z potokiem który **przenosi dane** z **lokalnymi** tooan bazy danych programu SQL Server obiektów blob platformy Azure. W ramach hello wskazówki zainstalowaniu i skonfigurowaniu hello brama zarządzania danymi na tym komputerze. |
