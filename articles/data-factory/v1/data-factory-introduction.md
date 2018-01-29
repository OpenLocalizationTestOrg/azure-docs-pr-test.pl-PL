---
title: "Wprowadzenie do usługi Data Factory — usługi integracji danych | Microsoft Docs"
description: "Dowiedz się, czym jest usługa Azure Data Factory: usługa integracji danych w chmurze, która służy do aranżacji i automatyzacji przenoszenia i przekształcania danych."
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
ms.date: 01/22/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: bcd0535c689bfda02b3c100b4ae3ab8bacb932e3
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="introduction-to-azure-data-factory"></a>Wprowadzenie do usługi Azure Data Factory
 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](data-factory-introduction.md)
> * [Wersja 2 — wersja zapoznawcza](../introduction.md)

> [!NOTE]
> Ten artykuł dotyczy wersji 1 usługi Azure Data Factory, która jest ogólnie dostępna (GA). Jeśli używasz wersji 2 usługi Data Factory, która jest w wersji zapoznawczej, zobacz [Introduction to Data Factory V2 (Wprowadzenie do usługi Data Factory w wersji 2)](../introduction.md).


## <a name="what-is-azure-data-factory"></a>Czym jest usługa Azure Data Factory?
W jaki sposób istniejące dane są wykorzystywane w biznesowej rzeczywistości opartej na danych big data? Czy można wzbogacić informacje wygenerowane w chmurze danymi referencyjnymi, pochodzącymi z lokalnych — lub innych, różnorodnych — źródeł danych? 

Na przykład firma tworząca gry zbiera dzienniki generowane przez gry w chmurze. Chce analizować te dzienniki w celu uzyskania szczegółowych informacji dotyczących preferencji klientów, danych demograficznych, zachowania użytkowników podczas korzystania z gier itp. Firma chce też identyfikować możliwości sprzedaży droższych produktów i sprzedaży wiązanej, opracowywać nowe atrakcyjne funkcje pozytywnie wpływające na rozwój biznesowy oraz oferować klientom udoskonalone środowisko gier. 

Do analizy tych dzienników firma musi użyć danych referencyjnych, np. informacji o kliencie, grze i kampanii marketingowej, które znajdują się w lokalnym magazynie danych. W związku z tym firma chce pozyskać dane dzienników z magazynu danych w chmurze oraz dane referencyjne z lokalnego magazynu danych. 

Następnie firma chce przetwarzać dane, używając usługi Hadoop w chmurze (Azure HDInsight). Dane wynikowe mają zostać opublikowane w magazynie danych w chmurze, takim jak Azure SQL Data Warehouse, lub w lokalnym magazynie danych, np. SQL Server. Firma chce uruchamiać taki przepływ pracy raz w tygodniu. 

Firma potrzebuje platformy, na której może utworzyć przepływ pracy pozyskujący dane z magazynu lokalnego i w chmurze. Firma musi mieć też możliwość przekształcania lub przetwarzania danych za pomocą istniejących usług obliczeniowych, takich jak Hadoop, i publikowania wyników w lokalnym magazynie danych lub magazynie danych w chmurze, aby mogły z nich korzystać aplikacje analizy biznesowej. 

![Omówienie usługi Data Factory](media/data-factory-introduction/what-is-azure-data-factory.png) 

Usługa Azure Data Factory to platforma umożliwiająca realizację takich scenariuszy. Jest to *oparta na chmurze usługa integracji danych, za pomocą której można tworzyć oparte na danych przepływy pracy w chmurze służące do organizowania i automatyzowania przenoszenia i przekształcania danych*. Za pomocą usługi Azure Data Factory można wykonywać następujące zadania: 

- Tworzyć oparte na danych przepływy pracy (nazywane potokami) pozyskujące dane z różnych magazynów danych i ustalać ich harmonogram.

- Przetwarzać i przekształcać dane za pomocą usług obliczeniowych, takich jak Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics i Azure Machine Learning.

-  Publikować dane wyjściowe w magazynach danych, na przykład Azure SQL Data Warehouse, w celu użycia przez aplikacje analizy biznesowej.  

To bardziej platforma, która najpierw wyodrębnia i ładuje, a następnie przekształca i ładuje, niż tradycyjna platforma wyodrębniania, przekształcania i ładowania. Podczas przekształcania dane są przetwarzane przez zastosowanie usług obliczeniowych, a nie przez dodanie kolumn pochodnych, które służą do zliczania liczby wierszy, sortowania danych itp. 

Obecnie dane używane i generowane przez przepływy pracy w usłudze Azure Data Factory to dane z *określonego przedziału czasu* (godzina, dzień, tydzień itd.). Na przykład potok może odczytać dane wejściowe, przetworzyć je i wygenerować dane wyjściowe raz dziennie. Przepływ pracy można także uruchomić tylko jeden raz.  
  

## <a name="how-does-it-work"></a>Jak to działa? 
Potoki (oparte na danych przepływy pracy) w usłudze Azure Data Factory zwykle wykonują następujące trzy kroki:

![Trzy etapy działania usługi Azure Data Factory](media/data-factory-introduction/three-information-production-stages.png)

### <a name="connect-and-collect"></a>Łączenie i zbieranie
Dane używane w przedsiębiorstwach mają różne typy i znajdują się w rozproszonych źródłach. Pierwszym krokiem tworzenia systemu produkcji informacji jest połączenie wszystkich potrzebnych źródeł danych i przetwarzania. Do tych źródeł należą usługi SaaS, udziały plików, serwery FTP i usługi internetowe. Następnym krokiem jest przeniesienie danych w miarę potrzeb do centralnej lokalizacji w celu ich dalszego przetwarzania.

Firmy, które nie korzystają z usługi Data Factory, muszą tworzyć niestandardowe składniki umożliwiające przepływ danych lub projektować własne usługi, aby zintegrować źródła danych i systemy przetwarzania. Takie podejście jest kosztowne, a integracja i utrzymanie systemów stwarza trudności. Takie systemy rzadko zapewniają mechanizmy kontrolne oraz funkcje monitorowania i wysyłania alertów na poziomie korporacyjnym. Możliwości te są natomiast dostępne w przypadku w pełni zarządzanej usługi.

Usługa Data Factory udostępnia działanie kopiowania w potoku danych, które pozwala przenosić dane z lokalnych magazynów danych i źródeł danych w chmurze do centralnego magazynu danych w chmurze w celu przeprowadzenia kolejnych etapów analizy. 

Na przykład można pobrać dane z usługi Azure Data Lake Store i przekształcić je później za pomocą usługi obliczeniowej Azure Data Lake Analytics. Można też pobrać dane z usługi Azure Blob Storage, aby przekształcić je później przy użyciu klastra usługi Azure HDInsight na platformie Hadoop.

### <a name="transform-and-enrich"></a>Przekształcanie i wzbogacanie
Po umieszczeniu danych w centralnym magazynie danych w chmurze zebrane dane należy przetworzyć lub przetransferować za pomocą usług obliczeniowych, takich jak HDInsight Hadoop, Spark, Data Lake Analytics lub Machine Learning. Przekształcone dane powinny być generowane niezawodnie i zgodnie z możliwym do utrzymania i kontrolowania harmonogramem, aby zapewnić środowiskom produkcyjnym zaufane dane. 

### <a name="publish"></a>Publikowanie 
Przekształcone dane należy dostarczyć z chmury do źródeł lokalnych, takich jak program SQL Server. Można też zachować je w magazynach w chmurze do wykorzystania przez narzędzia analityczne, aplikacje analizy biznesowej i inne aplikacje.

## <a name="key-components"></a>Główne składniki
Subskrypcja platformy Azure może zawierać jedno lub więcej wystąpień usługi Azure Data Factory (lub fabryk danych). Usługa Azure Data Factory składa się z czterech głównych składników. Ich współdziałanie pozwala udostępnić platformę umożliwiającą tworzenie opartych na danych przepływów pracy wraz z etapami służącymi do przenoszenia i przekształcania danych. 

### <a name="pipeline"></a>Potok
Fabryka danych może obejmować jeden lub wiele potoków. Potok jest grupą działań, które umożliwiają wykonanie zadania. 

Na przykład potok może zawierać grupę działań, które pozwalają pozyskać dane z obiektu blob platformy Azure, a następnie uruchomić zapytanie programu Hive w klastrze usługi HDInsight w celu podzielenia danych. Zaletą korzystania z potoku jest możliwość zarządzania zestawem działań. Na przykład zamiast planować oddzielne działania można wdrożyć i zaplanować potok. 

### <a name="activity"></a>Działanie
Potok może obejmować jedno lub wiele działań. Działania definiują akcje do wykonania na danych. Można na przykład użyć działania kopiowania w celu skopiowania danych z jednego magazynu danych do drugiego. Analogicznie można użyć działania programu Hive. Uruchamia ono zapytanie programu Hive w klastrze usługi Azure HDInsight, aby przekształcić lub przeanalizować dane. Usługa Data Factory obsługuje dwa typy działań — w zakresie przekształcania oraz przenoszenia danych.

### <a name="data-movement-activities"></a>Działania dotyczące przenoszenia danych
Działanie kopiowania w usłudze Data Factory kopiuje dane z magazynu danych źródła do magazynu danych ujścia. Dane z dowolnego źródła można zapisać do dowolnego ujścia. Wybierz magazyn danych, aby dowiedzieć się, jak kopiować dane do i z tego magazynu. Usługa Data Factory obsługuje następujące magazyny danych:

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

Aby uzyskać więcej informacji, zobacz [Move data by using Copy Activity (Przenoszenie danych za pomocą działania kopiowania)](data-factory-data-movement-activities.md).

### <a name="data-transformation-activities"></a>Działania dotyczące przekształcania danych
[!INCLUDE [data-factory-transformation-activities](../../../includes/data-factory-transformation-activities.md)]

Aby uzyskać więcej informacji, zobacz [Move data by using Copy Activity (Przenoszenie danych za pomocą działania kopiowania)](data-factory-data-transformation-activities.md).

### <a name="custom-net-activities"></a>Niestandardowe działania programu .NET
Jeśli musisz przenieść dane do/z magazynu danych nieobsługiwanego przez działanie kopiowania lub przekształcić dane za pomocą własnej logiki, utwórz niestandardowe działanie programu .NET. Aby uzyskać szczegółowe informacje na temat tworzenia i używania niestandardowego działania, zobacz [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) (Korzystanie z niestandardowych działań w potoku usługi Azure Data Factory).

### <a name="datasets"></a>Zestawy danych
Każde działanie pobiera 0 lub więcej zestawów danych jako dane wejściowe i generuje co najmniej jeden zestaw danych jako dane wyjściowe. Zestawy danych reprezentują struktury danych w magazynach danych. Te struktury wskazują dane, których chcesz użyć w swoich działaniach (takie jak dane wejściowe lub wyjściowe), albo odwołują się do nich. 

Na przykład zestaw danych obiektów blob platformy Azure określa kontener obiektów blob i folder w usłudze Azure Blob Storage, z których potok ma odczytywać dane. Alternatywnie zestaw danych tabeli SQL Azure określa tabelę, w której działanie zapisuje dane wyjściowe. 

### <a name="linked-services"></a>Połączone usługi
Połączone usługi działają podobnie do parametrów połączenia, umożliwiając definiowanie informacji wymaganych przez usługę Data Factory do nawiązywania połączeń z zasobami zewnętrznymi. Mechanizm ten działa następująco: połączona usługa definiuje połączenie ze źródłem danych, a zestaw danych reprezentuje strukturę danych. 

Na przykład połączona usługa Azure Storage określa parametry połączenia, które umożliwiają połączenie z kontem usługi Azure Storage. Natomiast zestaw danych obiektów blob platformy Azure określa kontener obiektów blob oraz folder, który zawiera dane.   

Połączone usługi w usłudze Data Factory służą do dwóch celów:

* Reprezentowanie *magazynu danych*, w tym między innymi bazy danych na lokalnym serwerze SQL Server, bazy danych Oracle, udziału plików lub konta usługi Azure Blob Storage. Listę obsługiwanych magazynów danych można znaleźć w sekcji [Data movement activities](#data-movement-activities) (Działania przenoszenia danych).

* Reprezentowanie *zasobu obliczeniowego*, który może hostować wykonywanie działania. Na przykład działanie HDInsightHive jest wykonywane w klastrze HDInsight na platformie Hadoop. Listę obsługiwanych środowisk obliczeniowych można znaleźć w sekcji [Data transformation activities (Działania przekształcania danych)](#data-transformation-activities).

### <a name="relationship-between-data-factory-entities"></a>Relacje między obiektami usługi Data Factory

![Diagram: Data Factory, usługa integracji danych w chmurze — najważniejsze pojęcia](./media/data-factory-introduction/data-integration-service-key-concepts.png)

## <a name="supported-regions"></a>Obsługiwane regiony
Obecnie można tworzyć fabryki danych w regionach Zachodnie stany USA, Wschodnie stany USA oraz Europa Północna. Jednak fabryka danych może mieć dostęp do magazynów danych i usług obliczeniowych w innych regionach świadczenia usługi Azure, aby przenosić dane między magazynami danych lub przetwarzać dane przy użyciu usług obliczeniowych.

Sama usługa Azure Data Factory nie przechowuje żadnych danych. Pozwala ona tworzyć przepływy pracy oparte na danych służące do organizowania przenoszenia danych między [obsługiwanymi magazynami danych](#data-movement-activities). Pozwala ona także przetwarzać dane przy użyciu [usług obliczeniowych](#data-transformation-activities) w innych regionach lub w środowisku lokalnym. Dodatkowo umożliwia [monitorowanie przepływów pracy i zarządzanie nimi](data-factory-monitor-manage-pipelines.md) przy użyciu zarówno mechanizmów programowych, jaki i interfejsu użytkownika.

Usługa Data Factory jest dostępna tylko w regionach Zachodnie stany USA, Wschodnie stany USA i Europa Północna. Jednak usługa, która obsługuje przenoszenie danych w usłudze Data Factory, jest dostępna [globalnie](data-factory-data-movement-activities.md#global) w wielu regionach. Jeśli magazyn danych znajduje się za zaporą, dane są przenoszone przez [bramę zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) zainstalowaną w środowisku lokalnym.

Załóżmy na przykład, że środowiska obliczeniowe, takie jak klaster usługi Azure HDInsight i usługa Azure Machine Learning, są zlokalizowane w regionie Europa Zachodnia. Można wtedy utworzyć wystąpienie usługi Azure Data Factory w regionie Europa Północna i korzystać z niego. Następnie można go używać do planowania zadań w środowiskach obliczeniowych w regionie Europa Zachodnia. Wyzwolenie zadania w środowisku obliczeniowym zajmuje usłudze Data Factory kilka milisekund, ale czas uruchomienia zadania w środowisku obliczeniowym nie zmienia się.

## <a name="get-started-with-creating-a-pipeline"></a>Rozpoczynanie tworzenia potoku
Potoki danych w usłudze Azure Data Factory można tworzyć za pomocą następujących narzędzi lub interfejsów API: 

- Azure Portal
- Visual Studio
- PowerShell
- Interfejs API .NET
- Interfejs API REST
- Szablon usługi Azure Resource Manager

Wykonaj instrukcje krok po kroku w następujących samouczkach, aby dowiedzieć się, jak tworzyć fabryki danych z potokami danych:

| Samouczek | Opis |
| --- | --- |
| [Przenoszenie danych między dwoma magazynami danych w chmurze](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) |Utwórz fabrykę danych z potokiem, który przenosi dane z magazynu obiektów blob do bazy danych SQL. |
| [Przekształcanie danych przy użyciu klastra Hadoop](data-factory-build-your-first-pipeline.md) |Utwórz pierwszą fabrykę danych platformy Azure z potokiem danych przetwarzającym dane, uruchamiając skrypt programu Hive w klastrze usługi Azure HDInsight (Hadoop). |
| [Przenoszenie danych między lokalnym magazynem danych i magazynem danych w chmurze przy użyciu bramy zarządzania danymi](data-factory-move-data-between-onprem-and-cloud.md) |Utwórz fabrykę danych z potokiem, przenoszącym dane z lokalnej bazy danych programu SQL Server do obiektu blob platformy Azure. W ramach tego przewodnika zainstalujesz i skonfigurujesz bramę zarządzania danymi na tym komputerze. |
