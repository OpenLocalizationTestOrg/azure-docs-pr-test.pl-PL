---
title: "aaaImport danych do usługi Azure Search w portalu hello | Dokumentacja firmy Microsoft"
description: "Użyj hello Kreatora usługi Azure Search importu danych w toocrawl Azure Portal hello Azure dane z bazy danych rozwiązania Cosmos Azure NoSQL, magazynu obiektów Blob, Magazyn tabel, bazy danych SQL i programu SQL Server na maszynach wirtualnych Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importowanie danych tooAzure wyszukiwania za pomocą portalu hello
Witaj Azure portal udostępnia **importowania danych** kreatora na pulpicie nawigacyjnym usługi Azure Search hello ładowania danych do indeksu. 

  ![Importuj dane na pasku poleceń hello][1]

Wewnętrznie hello Kreator konfiguruje i wywołuje *indeksatora*, kilka automatyzacji procesu indeksowania hello: 

* Połącz tooan zewnętrznego źródła danych w hello tej samej subskrypcji platformy Azure
* Generowanie schematu indeksu można modyfikować, na podstawie hello źródła danych struktury
* Ładowanie dokumentów JSON do indeksu przy użyciu zestawu wierszy pobrane ze źródła danych hello

Ten przepływ pracy można wypróbować przy użyciu przykładowych danych w usłudze Azure Cosmos DB. Odwiedź stronę [wprowadzenie do usługi Azure Search w portalu Azure hello](search-get-started-portal.md) instrukcje.

> [!NOTE]
> Możesz uruchomić hello **importowania danych** kreatora z toosimplify pulpitu nawigacyjnego bazy danych Azure rozwiązania Cosmos hello indeksowania dla tego źródła danych. W lewym okienku nawigacji przejdź zbyt**kolekcje** > **Dodaj usługi Azure Search** tooget uruchomiona.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Źródła danych obsługiwane przez hello Kreatora importu danych
Kreator importu danych Hello obsługuje hello następujące źródła danych: 

* Usługa Azure SQL Database
* Dane relacyjne programu SQL Server na maszynie wirtualnej platformy Azure
* Azure Cosmos DB
* Azure Blob Storage
* Azure Table Storage

Wymaganymi danymi wejściowymi jest spłaszczony zestaw danych. Importu można dokonać tylko z pojedynczej tabeli, widoku bazy danych lub równoważnej struktury danych. Ta struktura danych należy utworzyć przed uruchomieniem kreatora hello.

## <a name="connect-tooyour-data"></a>Łączenie danych tooyour
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) i hello Otwórz pulpit nawigacyjny usługi. Możesz kliknąć **więcej usług** w toosearch paska szybkiego dostępu hello istniejących "wyszukiwania usług" w bieżącej subskrypcji hello. 
2. Kliknij przycisk **i zaimportuj dane** na pasku blok importowanie danych otwórz hello tooslide poleceń hello.  
3. Kliknij przycisk **połączenia danych tooyour** toospecify definicji źródła danych używane przez indeksator. Dla źródeł danych wewnątrz subskrypcji Kreator hello zwykle mogą wykrywać i przeczytaj informacje o połączeniu, minimalizując ogólnych wymagań dotyczących konfiguracji.

|  |  |
| --- | --- |
| **Istniejące źródło danych** |Jeśli masz już zdefiniowane indeksatory w usłudze wyszukiwania, możesz użyć istniejącej definicji źródła danych na potrzeby innego importu. |
| **Azure SQL Database** |Nazwa usługi, poświadczenia użytkownika bazy danych z uprawnieniem do odczytu i nazwę bazy danych można określić na stronie powitania lub przez parametry połączenia ADO.NET. Wybierz tooview opcji ciąg połączenia hello lub dostosować właściwości. <br/><br/>na stronie powitania należy określić Hello tabeli lub widoku, który udostępnia hello zestawu wierszy. Ta opcja jest dostępna po hello połączenia zakończy się powodzeniem, podając listy rozwijanej, aby należy wybrać opcję. |
| **Program SQL Server na maszynie wirtualnej platformy Azure** |Jako parametry połączenia określ w pełni kwalifikowaną nazwę usługi, identyfikator użytkownika, hasło oraz bazę danych. toouse tego źródła danych, należy wcześniej zainstalowano certyfikat w magazynie lokalnym hello, który szyfruje hello połączenia. Aby uzyskać instrukcje, zobacz [tooAzure połączenia maszyny Wirtualnej SQL wyszukiwania](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>na stronie powitania należy określić Hello tabeli lub widoku, który udostępnia hello zestawu wierszy. Ta opcja jest dostępna po hello połączenia zakończy się powodzeniem, podając listy rozwijanej, aby należy wybrać opcję. |
| **Azure Cosmos DB** |Wymagania dotyczące obejmują hello konta bazy danych i kolekcji. Wszystkie dokumenty w kolekcji hello zostaną uwzględnione w indeksie hello. Można zdefiniować tooflatten zapytania lub filtrowanie wierszy hello lub toodetect zmienić dokumentów dla danych kolejnych operacji odświeżania. |
| **Azure Blob Storage** |Wymagania dotyczące obejmują hello konto magazynu i kontener. Opcjonalnie nazwy obiektów blob wykonaj wirtualnego konwencji nazewnictwa dla celów grupowania, można określić hello katalog wirtualny część nazwy hello jako folder w kontenerze. Więcej informacji zawiera artykuł [Indexing Blob Storage](search-howto-indexing-azure-blob-storage.md) (Indeksowanie w usłudze Blob Storage). |
| **Azure Table Storage** |Wymagania dotyczące obejmują hello konto magazynu i nazwy tabeli. Opcjonalnie można określić zapytania tooretrieve podzbiór hello tabel. Więcej informacji zawiera artykuł [Indexing Table Storage](search-howto-indexing-azure-tables.md) (Indeksowanie w usłudze Table Storage). |

## <a name="customize-target-index"></a>Dostosowywanie indeksu docelowego
Wstępne indeksu jest zwykle wywnioskować na podstawie hello zestawu danych. Dodać, edytować lub usunąć pola toocomplete hello schematu. Ponadto Ustawianie atrybutów na powitania pola poziomu toodetermine jego zachowania kolejnych wyszukiwania.

1. W **Dostosuj indeks docelowy**, określ nazwę hello i **klucza** toouniquely używane rozpoznawania dokumentów. Witaj klucza musi być ciągiem. Jeśli wartości pól zawierać spacji ani kreski się, że tooset zaawansowane opcje w **zaimportować dane** toosuppress hello sprawdzanie poprawności dla tych znaków.
2. Przejrzyj i popraw hello pozostałych pól. Nazwa i typ pola są zazwyczaj wypełniane automatycznie. Można zmienić typu danych hello, górę, aż zostanie utworzony indeks hello. Zmiana go później będzie wymagać odbudowania indeksu.
3. Ustaw atrybuty indeksu dla każdego pola:
   
   * Atrybut pobieranie umożliwia zwracanie pola hello w wynikach wyszukiwania.
   * Atrybut Filtrowanie umożliwia hello toobe pola w wyrażeniach filtru.
   * Sortowanie pozwala toobe pola hello używana podczas sortowania.
   * Tworzenie aspektów umożliwia używanie pola hello w nawigacji aspektowej.
   * Atrybut Wyszukiwanie umożliwia wyszukiwanie pełnotekstowe pola.
4. Kliknij przycisk hello **analizator** karcie, jeśli chcesz, aby toospecify analizatora języka na poziomie pola hello. Obecnie można określić tylko analizatory języka. Skorzystanie z analizatorów niestandardowych lub innych niż analizatory języka, takich jak analizatory słów kluczowych, wzorców itp., będzie wymagać kodu.
   
   * Kliknij przycisk **wyszukiwanie** toodesignate pełnotekstowego wyszukiwania w polu hello i Włącz listę hello analizatora listy rozwijanej.
   * Wybierz hello analizatora, które mają. Zobacz [Create an index for documents in multiple language](search-language-support.md) (Tworzenie indeksu dla dokumentów w wielu językach).
5. Kliknij przycisk hello **Sugestora** tooenable sugestie zapytań w wybranych pól.

## <a name="import-your-data"></a>Importowanie danych
1. W **zaimportować dane**, podaj nazwę hello indeksatora. Odwoływanie tego produktu hello hello importowanie danych kreatora jest indeksatora. Później tooview lub go edytować, należy także wybrać go z hello portalu, a nie przez ponowne uruchomienie Kreatora hello. 
2. Określ harmonogram hello, opartym na regionalnych strefy czasowej hello, w którym zostanie zainicjowana hello usługi.
3. Ustaw progi toospecify zaawansowane opcje na czy indeksowania można nadal dokumentu jest porzucany. Ponadto można określić czy **klucza** toocontain spacje i ukośniki, dozwolone są pola.  
4. Kliknij przycisk **OK** toocreate hello indeksu i zaimportuj dane hello.

Można monitorować indeksowania w portalu hello. Jako dokumenty są załadowane, liczba dokumentu hello wzrośnie indeksu hello zdefiniowane. Czasami zajmuje kilka minut, aż toopick strony portalu hello zapasowej hello najnowsze aktualizacje.

Indeks Hello jest gotowy tooquery jak wszystkie dokumenty hello są ładowane.

## <a name="query-an-index-using-search-explorer"></a>Tworzenie zapytań względem indeksu za pomocą Eksploratora wyszukiwania

Hello portal zawiera **Eksplorator wyszukiwania** tak, aby tworzenie zapytań względem indeksu bez konieczności toowrite żadnego kodu. [Eksploratora wyszukiwania](search-explorer.md) można używać dla dowolnego indeksu.

Witaj wyników wyszukiwania jest na podstawie domyślnych ustawień, takich jak hello [proste składni](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) i domyślne [searchMode parametru zapytania (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Wyniki są zwracane w formacie JSON, w format trybu informacji pełnej, dzięki czemu możesz sprawdzić hello całego dokumentu.

## <a name="edit-an-existing-indexer"></a>Edytowanie istniejącego indeksatora
Jak wspomniano, Kreator importu danych z hello tworzy **indeksatora**, które można zmodyfikować jako konstrukcję autonomicznego w portalu hello.

Na pulpicie nawigacyjnym usługi hello kliknij dwukrotnie tooslide Kafelek indeksator hello limit listę wszystkich indeksatorów utworzonych dla Twojej subskrypcji. Kliknij dwukrotnie jeden toorun indeksatory hello, edytować lub usunąć. Można zastąpić indeksu hello innym istniejących, hello źródło danych zmiany i ustaw opcje progów błąd podczas indeksowania.

## <a name="edit-an-existing-index"></a>Edytowanie istniejącego indeksu
Kreator Hello również utworzone **indeksu**. W usłudze Azure Search indeksu tooan strukturalnych aktualizacji wymaga odbudowania tego indeksu. Odbudowie pociąga za sobą usunięcie indeksu hello, ponowne tworzenie indeksu hello przy użyciu poprawione schemat, który ma żądane zmiany hello i ponownie załadowanie danych. Aktualizacje strukturalne obejmują zmianę typu danych oraz zmianę nazwy lub usunięcie pola.

Do zmian, które nie wymagają odbudowania indeksu, należą: dodanie nowego pola, zmiana profilów oceniania, zmiana funkcji sugestii i zmiana analizatorów języka. Aby uzyskać więcej informacji, zobacz [Aktualizowanie indeksu](https://msdn.microsoft.com/library/azure/dn800964.aspx).


## <a name="next-steps"></a>Następne kroki
Przejrzyj te toolearn łącza więcej informacji na temat indeksatory:

* [Indeksowanie w usłudze Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Indexing Azure Cosmos DB](search-howto-index-documentdb.md) (Indeksowanie w usłudze Azure Cosmos DB)
* [Indeksowanie w usłudze Blob Storage](search-howto-indexing-azure-blob-storage.md)
* [Indeksowanie w usłudze Table Storage](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

