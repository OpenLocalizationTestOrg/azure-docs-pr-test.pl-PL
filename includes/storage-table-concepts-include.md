## <a name="what-is-table-storage"></a>Co to jest usługa Table Storage
Usługa Azure Table Storage służy do przechowywania dużych ilości danych strukturalnych. Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz hello chmury Azure. Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych. Najczęstsze zastosowania usługi Table Storage to:

* Przechowywanie tabel danych strukturalnych umożliwiających obsługę aplikacji w skali sieci Web
* Zapisywanie zestawów danych, które nie wymagają złożonych sprzężeń, kluczy obcych lub przechowywanych procedur i mogą być nieznormalizowane w celu zapewniania szybkiego dostępu
* Szybkie wykonywanie zapytań o dane przy użyciu indeksu klastrowanego
* Uzyskiwanie dostępu do danych przy użyciu protokołu OData hello i zapytań LINQ z bibliotekami .NET usługi danych WCF

Korzystając z tabeli magazynu toostore i zapytań dotyczących dużych zestawów strukturalnych danych nierelacyjnych i tabele mogą być skalowane wraz ze wzrostem wymagań.

## <a name="table-storage-concepts"></a>Pojęcia związane z usługą Table Storage
Magazyn tabel zawiera hello następujące składniki:

![Diagram składników usługi Table Storage][Table1]

* **Format adresu URL:** kod odwołuje się do tabel na koncie przy użyciu następującego formatu adresu:   
  http://`<storage account>`.table.core.windows.net/`<table>`  
  
  Można rozwiązać tabelach platformy Azure bezpośrednio przy użyciu tego adresu z hello protokołu OData. Więcej informacji znajduje się w witrynie [OData.org][OData.org].
* **Konto magazynu:** wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Aby uzyskać szczegółowe informacje na temat pojemności konta magazynu, zobacz temat [Cele dotyczące skalowalności i wydajności usługi Azure Storage](../articles/storage/common/storage-scalability-targets.md).
* **Tabela**: tabela jest kolekcją obiektów. Tabele nie wymuszają schematu na obiektach, co oznacza, że jedna tabela może zawierać obiekty o różnych zestawach właściwości. Witaj liczba tabel zawierających konto magazynu jest ograniczona tylko przez limitem pojemności konta magazynu hello.
* **Jednostki**: jednostka jest zbiór właściwości, podobne tooa bazy danych wiersza. Jednostki można się too1MB rozmiar.
* **Właściwości**: właściwość to połączenie nazwy i wartości. Każdy obiekt może zawierać zapasowe too252 właściwości toostore danych. Każdy obiekt ma również trzy właściwości systemowe, które określają klucz partycji, klucz wiersza i znacznik czasu. Jednostki z hello na tym samym kluczem partycji mogą szybciej badane oraz wstawiane/aktualizowane w operacjach niepodzielnych. Klucz wiersza obiektu jest jego unikatowym identyfikatorem w partycji.

Aby uzyskać szczegółowe informacje na temat nazewnictwa tabel i właściwości, zobacz [hello opis modelu danych usługi tabel](/rest/api/storageservices/Understanding-the-Table-Service-Data-Model).

[Table1]: ./media/storage-table-concepts-include/table1.png
[OData.org]: http://www.odata.org/
