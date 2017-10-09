---
title: aaa "samouczek: Tworzenie pierwszego indeksu usługi Azure Search w portalu hello | Opis elementu Microsoft Docs": W hello portalu Azure, użyj wstępnie zdefiniowanych przykładowych danych toogenerate indeksu. Dowiedz się więcej o wyszukiwaniu pełnotekstowym, filtrach, aspektach, wyszukiwaniu rozmytym, wyszukiwaniu geograficznym i innych funkcjach.
usługi: wyszukiwania documentationcenter: "Autor: HeidiSteen Menedżera: Edytor jhubbard:" tagi: azure portal

MS.AssetID: 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service: wyszukiwanie ms.devlang: na ms.workload: wyszukać ms.topic: ms.tgt_pltfrm bohater artykuł: na ms.date: ms.author 2017-06/26: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Samouczek: Tworzenie pierwszego indeksu usługi Azure Search w portalu hello

W portalu Azure hello, rozpoczyna się od tooquickly zestawu danych przykładowych wstępnie zdefiniowanych Generowanie indeks, używając hello **importowania danych** kreatora. Zapoznaj się z wyszukiwaniem pełnotekstowym, filtrami, aspektami, wyszukiwaniem rozmytym i wyszukiwaniem geograficznym, korzystając z **Eksploratora wyszukiwania**.  

To wprowadzenie bez użycia kodu pozwala rozpocząć pracę ze wstępnie zdefiniowanymi danymi i umożliwia szybkie pisanie potrzebnych zapytań. Mimo że narzędzia portalu nie zastępują kodu, są one użyteczne w przypadku następujących zadań:

+ Nabycie praktycznych umiejętności w możliwie najkrótszym czasie
+ Utworzenie prototypu indeksu przed napisaniem kodu w kreatorze **importu danych**
+ Testowanie zapytań i składni analizatora w **Eksploratorze wyszukiwania**
+ Wyświetl istniejący indeksu tooyour opublikowane usługi i wyszukaj jego atrybuty

**Szacowany czas:** około 15 minut lub dłużej, jeśli wymagane jest także utworzenie konta lub zarejestrowanie się w usłudze. 

Alternatywnie zdobycia przy użyciu [tooprogramming opartej na kodzie wprowadzenie usługi Azure Search w środowisku .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Wymagania wstępne

Ten samouczek zakłada, że użytkownik posiada [subskrypcję platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) i [usługę Azure Search](search-create-service-portal.md). 

Jeśli nie chcesz od razu tooprovision usługi, możesz obserwować pokaz 6-minutowy hello kroków w tym samouczku, zaczynając od około 3 minuty do tego [wideo Omówienie usługi Azure Search](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Znajdowanie usługi
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Otwórz pulpit nawigacyjny usługi hello usługi Azure Search. Jeśli nie przypiąć hello usługi kafelka tooyour z pulpitu nawigacyjnego, można znaleźć usługi w ten sposób: 
   
   * W hello pasku dostępu kliknij **więcej usług** u dołu okienka nawigacji po lewej stronie powitania hello.
   * W polu wyszukiwania hello wpisz *wyszukiwania* tooget listę wyszukiwania usług dla Twojej subskrypcji. Usługi powinny być wyświetlane na liście hello. 

## <a name="check-for-space"></a>Sprawdzanie ilości wolnego miejsca
Wielu klientów zaczyna hello bezpłatnej usługi. Ta wersja jest ograniczona toothree indeksów, trzech źródeł danych i trzech indeksatorów. Przed rozpoczęciem upewnij się, że dysponujesz miejscem na dodatkowe elementy. W ramach tego samouczka tworzony jest jeden obiekt każdego typu. 

> [!TIP] 
> Kafelki na pulpicie nawigacyjnym usługi hello pokazują, jak wiele indeksów, indeksatorów i źródeł danych istnieje już. Kafelek indeksator Hello zawiera wskaźniki sukces i niepowodzenie. Kliknij przycisk hello kafelka tooview hello indeksatora count. 
>
> ![Kafelki dla indeksatorów i źródeł danych][1]
>

## <a name="create-index"></a> Tworzenie indeksu i ładowanie danych
Zapytania wyszukiwania przechodzą przez kolejne pozycje *indeksu* zawierającego dane z możliwością wyszukiwania, metadane i konstrukcje używane do optymalizacji niektórych zachowań wyszukiwania.

tookeep to zadanie oparte na portalu, stosujemy wbudowanych przykładowego zestawu danych, które mogą być przeszukiwane przy użyciu indeksatora za pośrednictwem hello **importowania danych** kreatora. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Krok 1: Uruchamianie Kreatora hello importu danych
1. Na pulpicie nawigacyjnym usługi Azure Search, kliknij przycisk **importowania danych** w toostart pasek poleceń hello kreatora, który tworzy i wypełnia indeks.
   
    ![Polecenie importu danych][2]

2. W Kreatorze powitania kliknij **źródła danych** > **przykłady** > **współużytkowania us-sample**. To źródło danych jest wstępnie skonfigurowane przy użyciu nazwy, typu i informacji o połączeniu. Po utworzeniu staje się ono „istniejącym źródłem danych”, które może zostać ponownie użyte w innych operacjach importu.

    ![Wybieranie przykładowego zestawu danych][9]

3. Kliknij przycisk **OK** toouse go.

#### <a name="step-2-define-hello-index"></a>Krok 2: Definiowanie indeksu hello
Tworzenie indeksu jest zwykle ręczne i opartych na kodzie, ale hello kreatora można wygenerować indeksu dla dowolnego źródła danych, które można przeszukiwać jej. Minimalny indeks wymaga nazwy i kolekcji pól, z jednym polem oznaczonym jako hello toouniquely klucza dokumentu rozpoznawania dokumentów.

Pola mają typy danych i atrybuty. pola wyboru Hello górze hello są *atrybutami indeksu* kontrolowanie sposobu pola hello jest używany. 

* **Pobieranie** oznacza, że pole jest wyświetlane na liście wyników wyszukiwania. Możesz oznaczyć poszczególne pola tak, aby nie były uwzględniane w wynikach wyszukiwania. W tym celu wystarczy usunąć zaznaczenie danego pola wyboru, na przykład wtedy, gdy pola są używane tylko w wyrażeniach filtrowania. 
* Atrybuty **Filtrowanie**, **Sortowanie** i **Tworzenie aspektów** określają, czy pole może być używane w strukturze nawigacji tworzenia aspektów, filtrowania lub sortowania. 
* **Wyszukiwanie** oznacza, że pole jest uwzględniane podczas wyszukiwania pełnotekstowego. Ciągi można przeszukiwać. Pól liczbowych i logicznych często nie można wyszukiwać. 

Domyślnie Kreator hello skanuje hello źródła danych dla unikatowych identyfikatorów jako podstawa hello hello pola klucza. Ciągi są określane jako możliwe do pobierania i przeszukiwania. Liczby całkowite są określane jako możliwe do pobierania, filtrowania, sortowania i tworzenia aspektów.

  ![Wygenerowany indeks realestate][3]

Kliknij przycisk **OK** toocreate hello indeksu.

#### <a name="step-3-define-hello-indexer"></a>Krok 3: Definiowanie indeksatora hello
Nadal w hello **importowania danych** kreatora, kliknij przycisk **indeksatora** > **nazwa**i wpisz nazwę indeksatora hello. 

Ten obiekt definiuje proces wykonywalny. Możesz zgodnie z harmonogramem cyklicznym, ale dla teraz Użyj hello domyślne opcji toorun hello indeksatora po natychmiast po kliknięciu **OK**.  

  ![Indeksator realestate][8]

## <a name="check-progress"></a>Sprawdzanie postępu
toomonitor danych zaimportować, przejdź wstecz toohello pulpit nawigacyjny usługi, przewiń w dół i kliknij dwukrotnie hello **indeksatory** listę indeksatorów hello tooopen kafelka. Powinny pojawić się indeksatora hello nowo utworzony w liście hello wskazujący stan "w toku" lub pomyślne jego zakończenie wraz hello liczba dokumentów indeksowanych.

   ![Komunikat o postępie indeksatora][4]

## <a name="query-index"></a>Indeks hello zapytania
Istnieje już indeks, który jest gotowy tooquery. **Eksplorator wyszukiwania** to narzędzie zapytania wbudowane hello portalu. Zawiera on pole wyszukiwania, dzięki czemu można zweryfikować, czy wyniki wyszukiwania są zgodne z oczekiwaniami. 

> [!TIP]
> W hello [wideo Omówienie usługi Azure Search](https://channel9.msdn.com/Events/Connect/2016/138), filmu hello przedstawiono w 6m08s hello następujące kroki.
>

1. Kliknij przycisk **Eksplorator wyszukiwania** na powitania paska poleceń.

   ![Polecenie Eksploratora wyszukiwania][5]

2. Kliknij przycisk **zmiany indeksu** na powitania pasek poleceń tooswitch zbyt*współużytkowania us-sample*.

   ![Polecenia indeksu i interfejsu API][6]

3. Kliknij przycisk **ustawić interfejsu API w wersji** na powitania toosee pasek poleceń, dostępnych interfejsów API REST. Interfejsy API udzielanie dostępu toonew funkcje nie zostały jeszcze zwykle wydawane w wersji Preview. Dla zapytań hello poniżej Użyj wersji ogólnie dostępna hello (2016-09-01), chyba że przekierowanie. 

    > [!NOTE]
    > [Interfejsu API REST usługi Azure Search](https://docs.microsoft.com/rest/api/searchservice/search-documents) i hello [biblioteki .NET](search-howto-dotnet-sdk.md#core-scenarios) są w pełni funkcjonalne, ale **Eksplorator wyszukiwania** jest tylko wywołania REST wyposażone toohandle. Akceptuje składni dla obu [prosta składnia zapytań](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) i [pełne analizator składni zapytań Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), oraz wszystkie hello parametry wyszukiwania są dostępne w [wyszukiwania dokumentu](https://docs.microsoft.com/rest/api/searchservice/search-documents) operacji.
    > 

4. Na pasku wyszukiwania hello, wprowadź ciągi zapytań hello poniżej i kliknij przycisk **wyszukiwania**.

  ![Przykład zapytania wyszukiwania][7]

**`search=seattle`**

+ Witaj `search` parametr jest w tym przypadku tooinput używane wyszukiwanie wyszukiwania pełnotekstowego, zwracając list w stanie Województwo króla, Waszyngton, zawierający *Seattle* dowolne pole wyszukiwania w dokumencie hello. 

+ **Eksplorator wyszukiwania** zwraca wyniki w formacie JSON, który jest tooread pełne i trudne w przypadku dokumenty zawierające gęsto struktury. W zależności od dokumentów może być konieczne czy dojść wyszukiwania wyniki tooextract ważne elementy kodu toowrite. 

+ Dokumenty składają się wszystkie pola oznaczone jako pobieranie hello indeksu. atrybuty indeksu tooview w portalu powitania kliknij *współużytkowania us-sample* w hello **indeksów** kafelka.

**`search=seattle&$count=true&$top=100`**

+ Witaj `&` symbol jest używane tooappend parametry wyszukiwania, które można określić w dowolnej kolejności. 

+  Witaj `$count=true` parametru zwraca wartość o liczbie hello sumę wszystkie dokumenty zwrócone. Możesz zweryfikować zapytania filtru, monitorując zmiany raportowane przez parametr `$count=true`. 

+ Witaj `$top=100` hello zwraca najwyższy uszeregowane 100 dokumenty poza hello całkowitej. Domyślnie usługi Azure Search zwraca hello najpierw 50 najlepsze dopasowanie. Można zwiększyć lub zmniejszyć ilość hello za pośrednictwem `$top`.

**`search=*&facet=city&$top=2`**

+ Parametr `search=*` to puste wyszukiwanie. Puste wyszukiwania umożliwiają znalezienie wszystkiego. Jedną z przyczyn przesyłanie pusty zapytania jest zbyt filtru lub aspekt za pośrednictwem hello pełny zestaw dokumentów. Na przykład chcesz tooconsist struktury nawigacji tworzenie aspektów, wszystkie miast hello indeksu.

+  `facet`Zwraca nawigacji struktury, że można przekazać tooa formantu interfejsu użytkownika. Zwraca ona kategorie i liczbę elementów. W takim przypadku kategorie są oparte na powitania wiele miast. Nie istnieje żadna agregacja w usłudze Azure Search, ale możesz przybliżyć się do agregacji za pomocą parametru `facet`, który podaje liczbę dokumentów w poszczególnych kategoriach.

+ `$top=2`ponownie oferuje dwa dokumenty, pokazujący, że można używać `top` tooboth zmniejszenia lub zwiększenia wyników.

**`search=seattle&facet=beds`**

+ To zapytanie to aspekt liczby sypialni w wyszukiwaniu tekstowym dla kategorii *Seattle*. `"beds"`można określić jako zestaw reguł, ponieważ hello pole jest oznaczone jako pobieranie, filtrowanie, tworzenie aspektów w indeksie hello i hello wartości on zawiera (liczbowe, od 1 do 5), są odpowiednie do klasyfikacji zawartości do grupy (listy z sypialni 3, 4 sypialni). 

+ Aspekty mogą być tworzone tylko na podstawie pól z możliwością filtrowania. Tylko pobieranie pól mogą być zwracane w wynikach hello.

**`search=seattle&$filter=beds gt 3`**

+ Witaj `filter` parametr zwraca wyników spełniających podane kryteria hello. W tym przypadku są to oferty z liczbą sypialni większą niż 3. 

+ Składnia filtru to konstrukcja OData. Aby uzyskać więcej informacji, zobacz [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Składnia filtrowania OData).

**`search=granite countertops&highlight=description`**

+ Wyróżnianie trafień odwołuje się tooformatting w tekście dopasowania hello — słowo kluczowe, podane dopasowań znajdują się w określonym polu. Jeśli wyszukiwany termin jest głęboko ukryty w opisie, możesz dodać trafień toomake wyróżnienia go toospot łatwiejsze. W takim przypadku hello sformatowany frazy `"granite countertops"` jest łatwiejsze toosee w polu Opis hello.

**`search=mice&highlight=description`**

+ Wyszukiwanie pełnotekstowe umożliwia znalezienie wyrazów z podobną semantyką. W takim przypadku wyniki wyszukiwania zawierają wyróżnionego tekstu dla "myszy" dla domach mających porażenia myszy w wyszukiwanie słów kluczowych tooa odpowiedź na "myszy". Różne formy powitalne sam wyraz mogą być wyświetlane w wynikach z powodu językową analiza. 

+ Usługa Azure Search obsługuje 56 analizatorów — zarówno oprogramowania Lucene, jak i firmy Microsoft. Witaj domyślne używane przez usługi Azure Search jest hello standardowe Lucene analizatora. 

**`search=samamish`**

+ Pisowni, takie jak "samamish" dla płaska Samammish hello w hello obszaru Seattle nie tooreturn dopasowań w typowych wyszukiwania. pisowni toohandle umożliwia wyszukiwanie rozmyte opisany w następnym przykładzie hello.

**`search=samamish~&queryType=full`**

+ Wyszukiwanie rozmyte jest włączona po określeniu hello `~` symboli i użyć analizatora pełne zapytanie hello interpretuje i poprawnie analizuje hello `~` składni. 

+ Wyszukiwanie rozmyte jest dostępna po przystąpieniu dla analizatora pełne zapytanie hello, który występuje, gdy ustawisz `queryType=full`. Aby uzyskać więcej informacji o scenariuszach zapytania włączane przez analizator składni zapytań pełne hello, zobacz [składnia zapytań Lucene w usłudze Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Gdy `queryType` jest określony, analizator składni zapytań proste domyślne hello jest używany. Analizator składni zapytań prostego powitania jest szybsze, ale jeśli potrzebujesz Wyszukiwanie rozmyte, wyrażeń regularnych, wyszukiwanie w sąsiedztwie lub innych typów zaawansowaną kwerendę, konieczne będzie hello pełnej składni. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ Dane geograficzne wyszukiwanie jest obsługiwane przez hello [edm. Typ danych GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) dla pola zawierające współrzędnych. Wyszukiwanie geograficzne jest rodzajem filtru określonego w artykule [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Składnia filtrowania OData). 

+ Hello przykładowe zapytanie filtruje wszystkie wyniki dla pozycyjnych danych, których wyniki są mniej niż 5 kilometrów od danego punktu (określony jako współrzędne geograficzne). Dodając `$count`, zostanie wyświetlony, ile są zwracane, gdy zmienisz odległość hello lub współrzędne hello. 

+ Wyszukiwanie geoprzestrzenne jest przydatne, jeśli aplikacja wyszukiwania ma funkcję „znajdź w pobliżu” lub używa nawigacji mapy. Nie jest to jednak wyszukiwanie pełnotekstowe. Jeśli masz wymagania użytkownika wyszukiwania na nazwę miejscowości lub kraju według nazwy, Dodaj pola zawierające nazwy miasta lub kraju, w toocoordinates dodanie.

## <a name="next-steps"></a>Następne kroki

+ Zmodyfikuj te z nich hello obiekty, które właśnie utworzony. Po uruchomieniu kreatora hello raz, możesz wrócić i wyświetlić lub zmodyfikować poszczególne składniki: indeks, indeksator lub źródło danych. Niektóre zmiany, takie jak hello zmiana typu danych pola hello, nie są dozwolone w indeksie hello, ale większość właściwości i ustawienia są można modyfikować.

  tooview pojedynczych składników, kliknij przycisk hello **indeksu**, **indeksatora**, lub **źródeł danych** Kafelki na toodisplay Twojego pulpitu nawigacyjnego listę istniejących obiektów. toolearn więcej informacji na temat zmiany indeksu, które nie wymagają kompilowania, zobacz [aktualizacji indeksu (interfejsu API REST usługi Azure Search)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Spróbuj hello narzędzia i kroki z innych źródeł danych. Witaj przykładowego zestawu danych, `realestate-us-sample`, jest z bazy danych SQL Azure, która usługi Azure Search może przeszukiwać. Oprócz usługi Azure SQL Database usługa Azure Search może przeszukiwać płaskie struktury danych w usługach Azure Table Storage, Blob Storage i Azure Cosmos DB oraz w programie SQL Server na maszynie wirtualnej platformy Azure. Na ich podstawie jest też tworzony indeks. Wszystkie te źródła danych są obsługiwane w Kreatorze hello. W kodzie można w łatwy sposób wypełnić indeks przy użyciu *indeksatora*.

+ Innych źródeł danych indeksatora nie są obsługiwane za pośrednictwem modelu wypychania, gdy kod wypchnięcia nowych i zmienić zestawy wierszy w indeksie tooyour JSON. Aby uzyskać więcej informacji, zobacz [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents) (Dodawanie, aktualizowanie lub usuwanie dokumentów w usłudze Azure Search).

Aby dowiedzieć się więcej o innych funkcjach wymienionych w tym artykule, odwiedź następujące linki:

* [Indexers overview](search-indexer-overview.md) (Omówienie indeksatorów)
* [Tworzenie indeksu (zawiera szczegółowe wyjaśnienie atrybutów indeksu hello)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Eksplorator wyszukiwania](search-explorer.md)
* [Search Documents](https://docs.microsoft.com/rest/api/searchservice/search-documents) (Wyszukiwanie dokumentów) — zawiera przykłady składni zapytania


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png