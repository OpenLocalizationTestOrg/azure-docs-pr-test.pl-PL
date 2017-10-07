---
title: Przewodnik projektowania tabeli magazynu aaaAzure | Dokumentacja firmy Microsoft
description: "Projektowania skalowalności i wydajności tabel Azure Table Storage"
services: cosmos-db
documentationcenter: na
author: mimig1
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 059f05a1d20e4d9537034b7ca133c5334bbefa04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Przewodnik projektowania tabeli magazynu systemu Azure: Projektowanie skalowalności i wydajności tabele
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign skalowalności i wydajności tabele należy wziąć pod uwagę wiele czynników, takich jak wydajności, skalowalności i kosztów. Wcześniej zaprojektowany schematy relacyjnych baz danych, tych zagadnień będzie znanych tooyou, ale istnieją podobieństwa relacyjne modele i modelu magazynu usługi tabel Azure hello, jest również wiele ważnych różnice. Różnice te zwykle prowadzić toovery różnych projektów, który może wyglądać toosomeone counter-intuitive lub jest on nieprawidłowy zapoznać się z relacyjnych baz danych, ale które wprowadzaj wiedział, w przypadku projektowania magazynu klucza i wartości NoSQL, takie jak hello usługi tabel Azure. Wiele sieci różnice projekt będzie odzwierciedlać hello fakt, że usługa tabel hello jest zaprojektowana toosupport skali chmury aplikacji, które może zawierać miliardów jednostek (wiersze w terminologii relacyjnej bazy danych), danych lub w przypadku zestawów danych, który musi obsługiwać wysokie woluminy transakcji: w związku z tym należy toothink inaczej, o jaki sposób przechowywania danych i zrozumienie, jak działa hello usługi tabel. Magazyn danych NoSQL przemyślany można włączyć tooscale Twojego rozwiązania, znacznie więcej (i koszt będzie niższy koszt) niż rozwiązania, które korzysta z relacyjnej bazy danych. Ten przewodnik pomaga w tych tematach.  

## <a name="about-hello-azure-table-service"></a>O hello usługi tabel Azure
W tej sekcji opisano niektóre z hello funkcji klucza hello tabeli usługi, które są szczególnie istotne toodesigning wydajności i skalowalności. Jeśli jesteś tooAzure nowego magazynu i hello usługi tabel, najpierw przeczytać artykuł [tooMicrosoft wprowadzenie usługi Azure Storage](../storage/common/storage-introduction.md) i [Rozpoczynanie pracy z magazynem tabel Azure przy użyciu platformy .NET](table-storage-how-to-use-dotnet.md) przed odczytaniem hello pozostałej części tej artykuł. Mimo że hello ten przewodnik koncentruje się na powitania usługi tabel, obejmuje niektóre omówienie hello kolejek platformy Azure i usługi obiektów Blob i sposobu ich wykorzystania wraz z hello usługi tabel w rozwiązaniu.  

Co to jest usługa tabel hello? Jak może spodziewać się od nazwy hello, hello usługi tabel używa danych toostore tabelarycznej. W terminologii hello każdego wiersza tabeli hello reprezentuje jednostkę, a magazynu kolumn hello hello różne właściwości tego obiektu. Każdy podmiot zawiera pary kluczy toouniquely go zidentyfikować, a kolumny znaczników czasu, który hello usługi tabel używa tootrack datę ostatniej aktualizacji jednostki hello (dzieje się to automatycznie i nie można ręcznie zastąpić sygnatury czasowej hello z dowolną wartością). Witaj usługi tabel używa to sygnatura czasowa ostatniej modyfikacji (LMT) toomanage optymistycznej współbieżności.  

> [!NOTE]
> Operacje interfejsu API REST usługi tabeli Hello również zwrócić **ETag** wartość, która dziedziczy hello last-modified timestamp (LMT). W tym dokumencie użyjemy hello warunki ETag i LMT zamiennie ponieważ odnoszą toohello sam podstawowy danych.  
> 
> 

Witaj poniższy przykład przedstawia toostore projektu prostą tabelę pracowników i dział jednostek. Wiele przykładów hello pokazano w dalszej części tego przewodnika są oparte na ten projekt proste.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Znacznik czasu</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>ADAM</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>Cze</td>
<td>CaO</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Dział</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Sprzedaż</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>Krzysztof</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Do tej pory to wygląda bardzo podobnie tabeli tooa relacyjnej bazy danych z podstawowych różnic hello jest hello obowiązkowe kolumn, oraz hello toostore możliwości jednostki wiele typów w hello tej samej tabeli. Ponadto, zdefiniowane przez użytkownika właściwości każdej z hello takich jak **imię** lub **wieku** ma typ danych, takie jak liczba całkowita lub ciąg, tylko kolumny w relacyjnej bazie danych. Mimo że w przeciwieństwie do relacyjnej bazy danych bez schematu hello rodzaj hello tabeli usługi oznacza, że właściwość nie wymagają hello sam typ danych dla każdej jednostki. toostore złożone typy danych w jednej właściwości, musi mieć format serializacji takich jak JSON i XML. Aby uzyskać więcej informacji dotyczących typów danych usługi, takie jak obsługiwane tabeli hello, zakres dat obsługiwanych reguły nazewnictwa i ograniczenia rozmiaru, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Jak pokażemy, wybór **PartitionKey** i **RowKey** jest projektowaniu tabel podstawowych toogood. Każdy podmiot przechowywane w tabeli musi mieć unikatową kombinację **PartitionKey** i **RowKey**. Podobnie jak w przypadku kluczy w tabeli relacyjnej bazy danych, hello **PartitionKey** i **RowKey** wartości są indeksowane toocreate indeks klastrowany, który umożliwia szybkie wyszukania; hello usługi tabel tworzy jednak żadnego indeksów pomocniczych, dzięki czemu są one hello tylko dwóch właściwości indeksowanych (niektóre wzorców hello w dalszej części Pokaż jak obejść to ograniczenie widoczna).  

Tabela składa się z co najmniej jedną partycję, i jak pokażemy, wiele hello projektowanie decyzji będzie wokół wybranie odpowiedniej **PartitionKey** i **RowKey** toooptimize rozwiązania. Rozwiązanie może składać się z tylko pojedynczej tabeli, która zawiera wszystkie obiekty podzielony na partycje, ale zazwyczaj rozwiązanie będzie mieć wielu tabel. Tabele ułatwiają toologically organizowanie jednostek, ułatwiają zarządzanie dostępem do toohello danych za pomocą listy kontroli dostępu i może usunąć całą tabelę przy użyciu operacji pojedynczy magazyn.  

### <a name="table-partitions"></a>Partycje tabel
Nazwa konta Hello, nazwę tabeli i **PartitionKey** wspólnie identyfikują hello partycji w ramach której usługa tabel hello przechowuje hello jednostki usługi magazynu hello. Oraz stanowi część hello schematu dla jednostek adresowania, partycje definiowania zakresu dla transakcji (zobacz [transakcji grupy jednostek](#entity-group-transactions) poniżej) i jak usługa tabel hello skaluje podstawę hello formularza. Aby uzyskać więcej informacji na partycje, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](../storage/common/storage-scalability-targets.md).  

W hello usługi tabel, oddzielnego węzła usług jedną lub więcej Wypełnij partycje i hello skali usługi przez dynamiczne równoważenie obciążenia partycji w węzłach. Jeśli węzeł ma pod obciążeniem, usługa tabel hello można *podzielić* hello zakresu partycji obsługiwanych przez ten węzeł na różnych węzłach; gdy zaspokojenie ruchu, usługa hello może *scalania* partycji hello zakresów z quiet węzły ponownie do jednego węzła.  

Aby uzyskać więcej informacji na temat hello wewnętrzny szczegóły hello usługa tabel, a w szczególności, w jaki sposób usługa hello zarządza partycji, zobacz dokument hello [Microsoft Azure Storage: A wysoce dostępna usługa magazynu w chmurze with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Grupowanie jednostki transakcji
W hello usługi tabel transakcji grupy jednostek (EGTs) są hello tylko wbudowany mechanizm atomic aktualizacje na wiele jednostek. EGTs są również określonego tooas *partii transakcji* w części dokumentacji. EGTs może działać tylko na jednostek przechowywanych w hello tej samej partycji (hello udział w tym samym kluczem partycji w danej tabeli), więc w dowolnym momencie należy atomic zachowanie transakcyjnego przez wiele jednostek należy tooensure tych jednostek, w której znajdują się hello tej samej partycji. Jest to często przyczynę zachowania wiele typów jednostek w hello sama tabela (i partycji) i nie używa wielu tabel dla typów jednostek różnych. Pojedynczy EGT może pracować na maksymalnie 100 jednostek.  Jeśli prześlesz wiele równoczesnych EGTs przetworzenia jest ważne tooensure tych EGTs nie działają na jednostek, które są wspólne w EGTs, ponieważ w przeciwnym razie przetwarzania może być opóźnione.

EGTs również wprowadzać potencjalną zależność dla tooevaluate w projekcie: przy użyciu więcej partycji spowoduje zwiększenie skalowalności hello aplikacji, ponieważ platforma Azure ma więcej możliwości Równoważenie obciążenia żądań w węzłach, ale może to ograniczyć hello możliwość transakcji atomic tooperform aplikacji i obsługa wysoki poziom spójności danych. Ponadto istnieją wartości docelowe skalowalności określonych na poziomie hello partycji, która może ograniczyć przepustowość hello transakcji można oczekiwać, że dla jednego węzła: Aby uzyskać więcej informacji o wartości docelowe skalowalności powitania dla konta magazynu platformy Azure i hello tabeli usługi, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](../storage/common/storage-scalability-targets.md). Kolejnych sekcjach niniejszego przewodnika omówiono w nim różne projektowania strategii, które ułatwiają zarządzanie kompromis, takich jak ta i omówienia najlepszy sposób toochoose klucz partycji na podstawie hello określone wymagania aplikacji klienta.  

### <a name="capacity-considerations"></a>Zagadnienia dotyczące wydajności
Witaj Poniższa tabela zawiera niektóre hello wartości klucza toobe uwagę podczas projektowania rozwiązania usługi tabeli:  

| Łączna pojemność konta magazynu platformy Azure | 500 TB. |
| --- | --- |
| Liczba tabel na koncie magazynu Azure |Ograniczone tylko przez hello pojemności konta magazynu hello |
| Liczba partycji w tabeli |Ograniczone tylko przez hello pojemności konta magazynu hello |
| Liczba jednostek w partycji |Ograniczone tylko przez hello pojemności konta magazynu hello |
| Rozmiar pojedynczą jednostkę |Konfigurowanie MB too1 maksymalnie 255 właściwości (w tym hello **PartitionKey**, **RowKey**, i **sygnatury czasowej**) |
| Rozmiar hello **PartitionKey** |Ciąg się o rozmiarze too1 KB |
| Rozmiar hello **RowKey** |Ciąg się o rozmiarze too1 KB |
| Rozmiar grupy jednostki transakcji |Transakcja może zawierać co najwyżej 100 jednostek i hello ładunek musi być mniejszy niż 4 MB. EGT można aktualizować tylko jednostki jeden raz. |

Aby uzyskać więcej informacji, zobacz [hello opis modelu danych usługi tabel](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Zagadnienia dotyczące kosztu
Magazyn tabel jest względnie niedrogie, ale w ramach próbnego dowolnego rozwiązania, które korzysta z usługi tabeli hello, należy uwzględnić szacowane koszty dla obu zdolności użycia i hello ilości transakcji. Jednak w wielu scenariuszach przechowywanie danych nieznormalizowany lub zduplikowane w kolejności tooimprove hello wydajności i skalowalności rozwiązania jest tootake podejście prawidłowe. Aby uzyskać więcej informacji o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Wskazówki dotyczące projektowania tabeli
Te listy Podsumuj niektóre hello wytycznych klucza, który należy mieć na uwadze podczas projektowania tabel, a w tym przewodniku zajmie się nimi wszystkie szczegółowo w dalszej części. Niniejsze wytyczne bardzo różnią się od hello wskazówki, które zwykle należy wykonać dla projektu relacyjnej bazy danych.  

Projektowanie sieci toobe rozwiązania usługi tabeli *odczytu* wydajne:

* ***Projekt do wykonywania zapytań w aplikacjach ciężki odczytu.*** Podczas projektowania tabel pomyśleć o zapytań hello (szczególnie hello opóźnienia poufnych z nich), które będą wykonywane przed zaplanowaniem będzie aktualizowania jednostki. Powoduje to zwykle rozwiązania wydajne i wydajności.  
* ***Określ zarówno PartitionKey i RowKey zapytania.*** *Polecenie zapytania* takich jak te są hello najbardziej efektywny zapytania usługi tabeli.  
* ***Warto przechowywać kopie jednostek.*** Magazyn tabel jest tanie dlatego należy rozważyć przechowywania hello tej samej jednostki zbyt wiele razy (z różnymi kluczami) tooenable efektywniejsze kwerendy.  
* ***Należy rozważyć denormalizing danych.*** Magazyn tabel jest tanie dlatego należy rozważyć denormalizing danych. Na przykład przechowywanie podsumowania jednostek, tak, aby zapytania dotyczące agregowanie danych wymagane jest tylko tooaccess pojedynczej jednostki.  
* ***Użyj wartości klucza złożonego.*** Witaj tylko masz są klucze **PartitionKey** i **RowKey**. Na przykład użyć tooentities ścieżki kluczem dostępu alternatywnego tooenable wartości klucza złożonego.  
* ***Użyj projekcji zapytań.*** Można zmniejszyć hello ilość danych za pośrednictwem sieci hello przy użyciu kwerend wybierających tylko pola hello potrzebne.  

Projektowanie sieci toobe rozwiązania usługi tabeli *zapisu* wydajne:  

* ***Nie należy tworzyć gorących partycji.*** Wybierz klucze, które pozwalają toospread Twojego żądania między wieloma partycjami w dowolnym momencie czasu.  
* ***Unikaj największego ruchu.*** Wygładzanie hello ruchu w odpowiednim przedziale czasu i uniknąć największego ruchu.
* ***Nie należy tworzyć niekoniecznie osobnej tabeli dla każdego typu jednostki.*** Jeśli wymagane jest atomic transakcji między typami jednostek, te wiele typów jednostek można przechowywać w hello sam partycji w hello tej samej tabeli.
* ***Należy wziąć pod uwagę hello maksymalną przepływność, którą należy osiągnąć.*** Należy znać docelowe skalowalności hello hello usługi tabel i upewnij się, że projektu nie spowoduje tooexceed je.  

Omówione w tym przewodniku, zobaczysz przykłady, których praktycznego wdrożenia wszystkich tych zasad.  

## <a name="design-for-querying"></a>Projekt do wykonywania zapytań
Tabela rozwiązań usług mogą być odczytywane obciążający, intensywnie zapisu lub mieszane hello dwa. W tej sekcji koncentruje się na powitania rzeczy toobear pamiętać podczas projektowania sieci toosupport usługi tabeli operacje odczytu dla wydajnie. Projekt, że obsługuje operacje odczytu wydajnie również jest zazwyczaj wydajne dla operacji zapisu. Istnieją dodatkowe zagadnienia toobear pamiętać podczas projektowania toosupport zapisu, omówiona w następnej sekcji hello [projektu do modyfikacji danych](#design-for-data-modification).

Dobry punkt wyjścia dla projektowania tooenable rozwiązania usługi z tabeli danych tooread wydajnie jest tooask "jakie zapytania zostanie Moje aplikacji muszą tooexecute tooretrieve hello dane z usługi tabel hello?"  

> [!NOTE]
> Z hello usługi tabel, jest ważne, tooget hello na początku projektu jest poprawna, ponieważ jest trudne i drogie toochange go później. Na przykład relacyjnej bazy danych jest często tooaddress możliwe problemy z wydajnością po prostu dodając indeksuje tooan istniejącej bazy danych: nie jest opcją z hello usługi tabel.  
> 
> 

W tej sekcji koncentruje się na powitania kluczowych zagadnień, które muszą spełnić przy projektowaniu tabel do wykonywania zapytań. Tematy Hello opisanych w tej sekcji obejmują:

* [Jak wybór PartitionKey i RowKey ma wpływ na wydajność zapytań](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Wybieranie odpowiedniego PartitionKey](#choosing-an-appropriate-partitionkey)
* [Optymalizacja zapytania dotyczące hello usługi tabel](#optimizing-queries-for-the-table-service)
* [Sortowanie danych w hello usługi tabel](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Jak wybór PartitionKey i RowKey ma wpływ na wydajność zapytań
Witaj następujących przykładach przyjmuje usługi tabel hello jest przechowywanie jednostek pracowników z hello następujące struktury (Większość przykładów hello Pomiń hello **sygnatury czasowej** właściwości dla jasności):  

| *Nazwa kolumny* | *Typ danych* |
| --- | --- |
| **PartitionKey** (nazwa działu) |Ciąg |
| **RowKey** (identyfikator pracownika) |Ciąg |
| **Imię** |Ciąg |
| **Nazwisko** |Ciąg |
| **Okres ważności** |Liczba całkowita |
| **EmailAddress** |Ciąg |

Witaj wcześniejszej sekcji [Omówienie usługi Azure tabeli](#overview) opisano niektóre hello główne funkcje hello usługi tabel Azure, które mają bezpośredni wpływ na projektowanie dla zapytania. Wynikiem tych hello następujące ogólne wskazówki dotyczące projektowania zapytań usługi tabeli. Należy pamiętać, że składnia filtru hello używane w poniższych przykładach hello z hello tabeli usługi interfejsu API REST, aby uzyskać więcej informacji, zobacz [jednostek zapytania](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* A ***zapytania punktu*** jest najbardziej wydajnym toouse wyszukiwania hello i jest zalecany toobe wyszukiwań dużych lub wyszukiwań wymagające najniższym opóźnieniu. Takie zapytanie może używać hello indeksów toolocate pojedynczą jednostkę bardzo wydajnie, określając zarówno hello **PartitionKey** i **RowKey** wartości. Na przykład: $filter = (PartitionKey eq 'Sales') i (RowKey eq "2")  
* Drugi najlepiej jest ***kwerendy zakresu*** używającą hello **PartitionKey** i filtry w zakresie **RowKey** wartości tooreturn więcej niż jednej jednostki. Witaj **PartitionKey** wartość identyfikuje określonej partycji i hello **RowKey** identyfikuje podzbiór hello jednostki w tej partycji. Na przykład: $filter = PartitionKey eq "Sprzedaży i RowKey ge" i RowKey lt 'T "  
* Trzeci najlepiej ***skanowania partycji*** używającą hello **PartitionKey** i filtry w innej właściwości niekluczowe i mogą zwracać więcej niż jednej jednostki. Witaj **PartitionKey** wartość identyfikuje określonej partycji, a właściwość hello wartości wybranych dla podzbioru hello jednostek w tej partycji. Na przykład: $filter = PartitionKey eq "Sprzedaży" i nazwisko eq 'Smith'  
* A ***skanowania tabeli*** nie obejmuje hello **PartitionKey** i jest bardzo mało wydajne, ponieważ wszystkie partycje hello, tworzące tabelę z kolei do żadnych zgodnych jednostek wyszukiwania. Zostanie przeprowadzone skanowanie tabeli niezależnie od tego, czy filtr używa hello **RowKey**. Na przykład: $filter = nazwisko eq 'Nowak'  
* Zapytań zwracających wiele jednostek zwrócić posortowane w **PartitionKey** i **RowKey** kolejności. Wybierz tooavoid ponowne sortowanie hello jednostek w kliencie hello **RowKey** definiuje hello najczęściej kolejności sortowania.  

Należy pamiętać, że za pomocą "**lub**" toospecify na podstawie filtru **RowKey** wartości powoduje skanowania partycji i nie jest traktowana jako kwerendy zakresu. W związku z tym należy unikać zapytań, które używać filtrów, takich jak: $filter = PartitionKey eq 'Sales' i (RowKey eq "121" lub RowKey eq "322")  

Aby uzyskać przykładów kodu po stronie klienta, które używają hello biblioteki klienta usługi Storage tooexecute wydajność zapytań zobacz:  

* [Wykonywanie zapytania punktu, przy użyciu hello biblioteki klienta usługi Storage](#executing-a-point-query-using-the-storage-client-library)
* [Trwa pobieranie wiele jednostek za pomocą LINQ](#retrieving-multiple-entities-using-linq)
* [Projekcja po stronie serwera](#server-side-projection)  

Przykłady kodu po stronie klienta, który może obsługiwać wiele jednostek typy przechowywane w hello sam tabeli, zobacz:  

* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Wybieranie odpowiedniego PartitionKey
Wybór **PartitionKey** zrównoważenia hello potrzeby tooenables hello użycie EGTs (tooensure spójności) przed toodistribute wymaganie hello jednostek wiele partycji (tooensure skalowalna).  

W jednym extreme można przechowywać wszystkie obiekty w jednej partycji, ale to może ograniczać skalowalność hello rozwiązania i może uniemożliwić usługi tabel hello stanie równoważenie tooload żądań. Na powitania y. można przechowywać jednej jednostki dla każdej partycji, będzie wysoce skalowalna i co pozwala żądania tooload saldo usług tabeli hello, ale co może uniemożliwić używanie jednostek grupy transakcji.  

Idealnym **PartitionKey** to taki, który umożliwia wydajne zapytania toouse i ma wystarczające tooensure partycje rozwiązania do skalowania. Zazwyczaj można zauważyć, że obiekty odpowiednie właściwości, która dystrybuuje jednostek na partycji wystarczającą.

> [!NOTE]
> Na przykład w systemie, która przechowuje informacje dotyczące użytkowników lub pracowników, nazwa użytkownika może być dobrym PartitionKey. Może mieć kilka jednostki, które korzystają z danym UserID jako klucza partycji hello. Każda jednostka, która przechowuje dane o użytkowniku są pogrupowane w jednej partycji, a więc te jednostki są dostępne przy użyciu transakcji grupy jednostek, przy zachowaniu wysokiej skalowalności.
> 
> 

Istnieją dodatkowe zagadnienia w wybranym **PartitionKey** dotyczących toohow będzie Wstawianie, aktualizowanie i usuwanie jednostek: zobacz sekcję hello [projektu do modyfikacji danych](#design-for-data-modification) poniżej.  

### <a name="optimizing-queries-for-hello-table-service"></a>Optymalizacja zapytania dotyczące hello usługi tabel
Witaj usługi tabel automatycznie indeksuje jednostek przy użyciu hello **PartitionKey** i **RowKey** wartości w jeden indeks klastrowany, dlatego hello przyczyny, że punkt zapytania są hello toouse najbardziej efektywny . Istnieją jednak nie indeksów inną niż hello indeksu klastrowanego na powitania **PartitionKey** i **RowKey**.

Wiele projektów musi spełniać wymagania wyszukiwanie tooenable jednostek na podstawie wielu kryteriów. Na przykład Lokalizowanie jednostek pracownika opartych na wiadomości e-mail, identyfikator lub nazwisko. Witaj następujących wzorce w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) adresów tego rodzaju wymaganie oraz opisano sposoby obchodzić fakt hello usługi tabel hello nie zapewnia indeksów pomocniczych:  

* [Wzorzec pomocniczy indeks partycji wewnątrz](#intra-partition-secondary-index-pattern) -przechowywać wiele kopii każdej jednostki przy użyciu różnych **RowKey** wartości (w hello tej samej partycji) tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różne **RowKey** wartości.  
* [Wzorzec między partycji pomocniczy indeks](#inter-partition-secondary-index-pattern) — przechowywać wiele kopii każdej jednostki przy użyciu różnych wartości RowKey w osobnych partycji lub w oddzielnych tabelach tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różnych **RowKey** wartości.  
* [Wzorzec jednostek indeksu](#index-entities-pattern) — Obsługa indeksu jednostek tooenable wydajne wyszukiwanie zwracających list jednostek.  

### <a name="sorting-data-in-hello-table-service"></a>Sortowanie danych w hello usługi tabel
Hello usługi tabel zwraca jednostki sortowane w kolejności rosnącej według **PartitionKey** , a następnie według **RowKey**. Klucze te są wartości ciągu i tooensure, który wartości liczbowe sortowanie prawidłowo, należy przekonwertować tooa stałej długości i uzupełniania zer. Na przykład, jeśli hello pracownika wartość identyfikatora można użyć jako hello **RowKey** jest wartość całkowita należy przekonwertować identyfikator **123** za**00000123**.  

Wiele aplikacji ma wymagania dotyczące danych toouse posortowane w różnej kolejności: na przykład sortowanie pracowników według nazwy lub przez przyłączenie daty. Witaj następujących wzorce w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) adresów, jak porządki sortowania tooalternate obiekty:  

* [Wzorzec pomocniczy indeks wewnątrz partycji](#intra-partition-secondary-index-pattern) -przechowywać wiele kopii każdej jednostki przy użyciu różnych wartości RowKey (w hello tej samej partycji) tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu innej wartości RowKey.  
* [Wzorzec między partycji pomocniczy indeks](#inter-partition-secondary-index-pattern) — przechowywać wiele kopii każdej jednostki przy użyciu różnych RowKey wartości w osobnych partycji w oddzielnych tabelach tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różnych RowKey wartości.
* [Wzorzec końcowego fragmentu dziennika](#log-tail-pattern) -hello pobrać  *n*  jednostek ostatnio dodany tooa partycji przy użyciu **RowKey** wartość sortujące odwrotnej daty i czasu kolejności.  

## <a name="design-for-data-modification"></a>Projekt do modyfikacji danych
W tej sekcji koncentruje się na informacjach dotyczących projektowania hello optymalizacji operacji wstawienia, aktualizacje i usuwa. W niektórych przypadkach należy tooevaluate hello kompromis między projekty, które Optymalizuj dla zapytaniach dotyczących projektów, które Optymalizuj dla modyfikacji danych tak samo, jak w projektach relacyjnych baz danych (chociaż techniki hello zarządzania hello projektu możliwości różnią się relacyjnej bazy danych). Witaj sekcji [wzorce projektowe tabeli](#table-design-patterns) opisano niektóre wzorce projektowe szczegółowe dla hello usługi tabel i opisano niektóre te kompromisy. W praktyce znajdziesz, że wiele projektów, zoptymalizowana pod kątem zapytań jednostek również działać efektywne w przypadku modyfikowania jednostek.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Optymalizacja wydajności hello wstawiania, aktualizowania i usuwania operacji
tooupdate lub usuwania jednostki, musi być możliwe tooidentify go za pomocą hello **PartitionKey** i **RowKey** wartości. W tym zakresie wybór **PartitionKey** i **RowKey** dla modyfikowanie jednostek należy stosować podobnych kryteriów tooyour wybór toosupport punktu zapytania, ponieważ ma tooidentify jednostek jako najbardziej wydajny sposób. Nie ma toouse nieefektywne partycji lub tabeli skanowania toolocate jednostki w kolejności toodiscover hello **PartitionKey** i **RowKey** wartości muszą tooupdate lub usuń go.  

Witaj następujących wzorce w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) adresów optymalizacji wydajności hello lub Twoje insert, update i operacji usunięcia:  

* [Dużą usunąć wzorzec](#high-volume-delete-pattern) -usunięcie hello Włącz dużą liczbę jednostek przez zapisanie wszystkich jednostek hello do usunięcia jednoczesnych w ich własnych osobnej tabeli; usuwania jednostek hello przez usunięcie hello tabeli.  
* [Wzorzec serii danych](#data-series-pattern) -magazynu pełnych danych serii w pojedynczej jednostki toominimize hello liczba żądań wprowadzania.  
* [Wzorzec szeroki jednostek](#wide-entities-pattern) -wiele jednostek logicznych toostore jednostek fizycznych za pomocą więcej niż 252 właściwości.  
* [Wzorzec dużych jednostek](#large-entities-pattern) -Użyj obiektu blob magazynu toostore właściwość dużej wartości.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Zapewnienie spójności w jednostki przechowywanej
Witaj innych klucza czynnik, który ma wpływ na wybór kluczy dla optymalizacji modyfikacji danych jest sposób tooensure spójności za pomocą atomic transakcji. Toooperate EGT można używać tylko na jednostek przechowywanych w hello tej samej partycji.  

Witaj następujących wzorce w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) adresu zarządzania spójności:  

* [Wzorzec pomocniczy indeks partycji wewnątrz](#intra-partition-secondary-index-pattern) -przechowywać wiele kopii każdej jednostki przy użyciu różnych **RowKey** wartości (w hello tej samej partycji) tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różne **RowKey** wartości.  
* [Wzorzec między partycji pomocniczy indeks](#inter-partition-secondary-index-pattern) — przechowywać wiele kopii każdej jednostki przy użyciu różnych wartości RowKey w osobnych partycji lub w oddzielnych tabelach tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różnych **RowKey** wartości.  
* [Wzorzec transakcji po pewnym czasie spójne](#eventually-consistent-transactions-pattern) -włączyć spójności po pewnym czasie działania przez granice partycji lub granice systemu magazynu za pomocą kolejek platformy Azure.
* [Wzorzec jednostek indeksu](#index-entities-pattern) — Obsługa indeksu jednostek tooenable wydajne wyszukiwanie zwracających list jednostek.  
* [Wzorzec denormalization](#denormalization-pattern) — łączenie dane dotyczące razem w tooenable pojedynczej jednostki tooretrieve hello wszystkie dane, które należy za pomocą kwerendy pojedynczy punkt.  
* [Wzorzec serii danych](#data-series-pattern) -magazynu pełnych danych serii w pojedynczej jednostki toominimize hello liczba żądań wprowadzania.  

Informacje o transakcjach grupy jednostek, sekcji hello [transakcji grupy jednostek](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Zapewnienie projektu wydajne modyfikacji ułatwia efektywne zapytań
W wielu przypadkach to projekt wydajne podczas badania powoduje efektywne modyfikacje, ale zawsze powinni sprawdzić, czy dotyczy hello konkretnego scenariusza. Niektóre wzorców hello w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) jawnie oceń kompromis między sprawdzanie i modyfikowanie jednostek i zawsze należy uwzględnić hello numeru każdego typu konta działania.  

Witaj następujących wzorce w sekcji hello [wzorce projektowe tabeli](#table-design-patterns) kompromis między projektowania zapytań wydajne i projektowania modyfikacji danych wydajne rozwiązania:  

* [Wzorca klucza złożonego](#compound-key-pattern) -Użyj złożone **RowKey** dane z zapytania pojedynczy punkt dotyczące wartości tooenable toolookup klienta.  
* [Wzorzec końcowego fragmentu dziennika](#log-tail-pattern) -hello pobrać  *n*  jednostek ostatnio dodany tooa partycji przy użyciu **RowKey** wartość sortujące odwrotnej daty i czasu kolejności.  

## <a name="encrypting-table-data"></a>Szyfrowanie danych w tabeli
Witaj biblioteki klienta magazynu Azure .NET obsługuje szyfrowanie właściwości jednostki ciągu wstawiania i zamienianie operacji. ciągi Hello szyfrowane są przechowywane w usłudze hello jako właściwości binarnych, a zostaną one przetworzone toostrings wstecz po odszyfrowywania.    

W przypadku tabel Ponadto toohello zasady szyfrowania, użytkownicy muszą określić toobe właściwości hello szyfrowane. Można to zrobić, określając atrybutu [EncryptProperty] (dla jednostki POCO, które pochodzą z TableEntity) lub szyfrowania, program rozpoznawania nazw w opcjach żądania. Rozwiązywanie problemów z szyfrowania jest delegata, który ma klucz partycji, klucz wiersza i nazwy właściwości i zwraca wartość Boolean wskazującą, czy ma być szyfrowana tej właściwości. Podczas szyfrowania powitania klienta biblioteki użyje tego toodecide informacji czy właściwość powinny być szyfrowane podczas przesyłania toohello zapisu. Delegat Hello udostępnia także możliwość hello logiki wokół jak właściwości są szyfrowane. (Na przykład, jeśli X, następnie szyfrować właściwości A; w przeciwnym razie szyfrowania właściwości A i B.) Należy pamiętać, że jest niekonieczne tooprovide te informacje podczas odczytywania lub zapytanie jednostki.

Należy pamiętać, że scalania nie jest obecnie obsługiwany. Ponieważ podzbiór właściwości może być zaszyfrowany wcześniej za pomocą innego klucza, po prostu scalanie hello nowe właściwości i aktualizowania metadanych hello spowoduje utratę danych. Scalanie albo wymaga wprowadzania dodatkowych usługi wywołuje tooread hello istniejące jednostki z usługi hello lub przy użyciu nowego klucza dla właściwości, które nie są odpowiednie ze względu na wydajność.     

Informacje o szyfrowaniu danych z tabeli, zobacz [szyfrowania po stronie klienta i usługi Azure Key Vault dla magazynu Microsoft Azure](../storage/common/storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Relacje modelowania
Tworzenie modeli domeny jest krokiem klucza w projekcie hello złożonych systemów. Zazwyczaj Użyj hello modelowania jednostek tooidentify procesu, a hello relacji między nimi jako toounderstand sposób hello firm domeny i poinformuj o tym hello projektowania systemu. W tej sekcji koncentruje się na jak niektóre hello popularne typy relacji w toodesigns modeli domeny dla usługi tabel hello tłumaczenia. proces Hello mapowanie tooa model danych logicznych fizycznych NoSQL na podstawie — model danych jest bardzo różnią się od używanego podczas projektowania relacyjnej bazy danych. Projekt relacyjnych baz danych zwykle zakłada proces normalizacji danych zoptymalizowane pod kątem minimalizując nadmiarowość — i deklaratywne możliwość podczas badania, która streszczenia hello sposobu implementacji działania hello bazy danych.  

### <a name="one-to-many-relationships"></a>Relacje jeden do wielu
Relacje jeden do wielu obiektów domeny biznesowych występować bardzo często: na przykład w jednym dziale ma wielu pracowników. Obejmuje kilka relacji jeden do wielu tooimplement sposoby hello usługi tabel każdego z zalet i wad, które mogą być istotne toohello danego scenariusza.  

Rozważmy przykład hello z dużych korporacji międzynarodowej dziesiątki tysięcy działów i jednostki pracownika, gdzie każdy dział ma wielu pracowników i pracowników, poszczególnych, związanych z nimi z jednego określonego działu. Jednym z podejść jest działu oddzielne toostore i jednostek pracownika, takich jak te:  

![][1]

W tym przykładzie pokazano niejawnych relacji jeden do wielu między typami hello oparte na powitania **PartitionKey** wartości. Każdy dział może mieć wielu pracowników.  

W tym przykładzie przedstawiono również jednostki działu, a jej podmioty powiązanego pracownika w hello tej samej partycji. Można wybrać toouse różnych partycji, tabel lub nawet kont magazynu dla typów jednostek różnych hello.  

Informacje o innym podejściu jest toodenormalize danych i magazynu jednostek tylko pracowników z działu nieznormalizowany danych, jak pokazano w hello poniższy przykład. W tego scenariusza, takie podejście nieznormalizowany mogą nie być hello najlepszym przypadku wymaganie toobe toochange stanie hello szczegóły manager działu ponieważ toodo to należy tooupdate każdy pracownik działu hello.  

![][2]

Aby uzyskać więcej informacji, zobacz hello [wzorzec Denormalization](#denormalization-pattern) dalszej części tego przewodnika.  

Witaj Poniższa tabela zawiera podsumowanie hello zalet i wad każdej z metod hello opisanych powyżej do przechowywania pracowników i działu obiektów, które mają relacji jeden do wielu. Należy również rozważyć częstotliwość tooperform różne operacje: może być akceptowane toohave projekt, który zawiera kosztowna operacja, jeśli ta operacja odbywa się tylko rzadko.  

<table>
<tr>
<th>Podejście</th>
<th>Specjaliści</th>
<th>Wady</th>
</tr>
<tr>
<td>Oddzielne typy jednostek, tej samej partycji, tej samej tabeli</td>
<td>
<ul>
<li>Można aktualizować jednostek działu z jednej operacji.</li>
<li>Spójności toomaintain EGT można użyć, jeśli masz toomodify wymaganie jednostki działu zawsze, gdy użytkownik aktualizacji/insert/usuwania jednostki pracownika. Na przykład, jeśli liczba pracowników działów, dla każdego działu.</li>
</ul>
</td>
<td>
<ul>
<li>Mogą być potrzebne tooretrieve zarówno pracownika, jak i jednostki działu niektóre działania klienta.</li>
<li>Operacje magazynu wprowadzenia w hello sam partycji. W transakcji wysokiej woluminów może to spowodować punktu aktywnego.</li>
<li>Nie można przenieść pracownika tooa nowy dział przy użyciu EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Typy oddzielnych jednostek, różnych partycji lub tabel lub kont magazynu</td>
<td>
<ul>
<li>Należy zaktualizować działu jednostki lub jednostek pracowników z jednej operacji.</li>
<li>W transakcji wysokiej woluminów, może to ułatwić rozpowszechniania hello obciążenia między więcej partycji.</li>
</ul>
</td>
<td>
<ul>
<li>Mogą być potrzebne tooretrieve zarówno pracownika, jak i jednostki działu niektóre działania klienta.</li>
<li>Nie można użyć EGTs toomaintain spójności po możesz aktualizacji/insert/usuwania pracownik i aktualizacji działu. Na przykład aktualizowania liczba pracowników w jednostce działu.</li>
<li>Nie można przenieść pracownika tooa nowy dział przy użyciu EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Denormalize do pojedynczej jednostki typu</td>
<td>
<ul>
<li>Można pobrać wszystkich hello informacji z pojedynczym żądaniem.</li>
</ul>
</td>
<td>
<ul>
<li>Jeśli potrzebujesz informacji działu tooupdate (wymagałoby to możesz tooupdate hello wszystkich pracowników działu) może być kosztowne toomaintain spójności.</li>
</ul>
</td>
</tr>
</table>

Jak wybrać te opcje, a które specjaliści hello i wad są najbardziej znaczących zależy od scenariuszy określonej aplikacji. Na przykład jak często należy można modyfikować jednostek działu; wszystkie zapytania pracownika wymaga informacji dodatkowych działów hello; jak blisko czy limity skalowalności toohello na partycji lub Twoje konto magazynu?  

### <a name="one-to-one-relationships"></a>Relacje jeden do jednego
Modele domeny może obejmować jeden do jednego relacje między obiektami. Jeśli potrzebujesz tooimplement relacją w hello usługi tabel, należy wybrać jak toolink Witaj dwie jednostki pokrewne, gdy będziesz potrzebować tooretrieve oba te. To łącze może być niejawna, oparte na Konwencji w wartości klucza hello lub jawne, przechowując łącze w formie hello **PartitionKey** i **RowKey** wartości w każdej jednostki tooits powiązanego obiektu. Aby uzyskać informacje dotyczące tego, czy należy przechowywać hello powiązanych jednostek w tej samej partycji Witaj, zobacz sekcję hello [jeden do wielu relacji](#one-to-many-relationships).  

Należy pamiętać, że są także uwagi dotyczące implementacji, które mogą prowadzić możesz relacje jeden do jednego tooimplement w usłudze tabel hello:  

* Obsługa dużych jednostek (Aby uzyskać więcej informacji, zobacz [dużych jednostek wzorzec](#large-entities-pattern)).  
* Wdrożenie kontroli dostępu (Aby uzyskać więcej informacji, zobacz [kontrolowanie dostępu przy użyciu sygnatury dostępu współdzielonego](#controlling-access-with-shared-access-signatures)).  

### <a name="join-in-hello-client"></a>Sprzężenia w powitania klienta
Mimo że istnieją sposoby toomodel relacje w hello usługi tabel, należy nie zapomnij czy hello dwa główne powody przy użyciu usługi tabel hello skalowalność i wydajność. Jeśli okaże się, że są modelowania wielu relacji naruszających hello wydajności i skalowalności rozwiązania, należy poprosić użytkownika, jeśli jest konieczne toobuild hello wszystkie relacje danych w projekcie tabeli. Mogą być stanie toosimplify hello projektu i zwiększyć hello skalowalność i wydajność rozwiązania, jeśli umożliwisz aplikacja kliencka wykonać wszelkie niezbędne sprzężenia.  

Na przykład jeśli małych tabel, które zawierają dane, które nie zmienia się bardzo często, następnie można pobrać dane raz i pamięci podręcznej go na powitania klienta. To uniknąć wielokrotnego dwukierunkowe przesyłanie danych tooretrieve hello tych samych danych. W przykładach hello, które firma Microsoft sprawdzono, w tym przewodniku hello zestaw działów w organizacji małych jest prawdopodobnie toobe małe i zmień rzadko co odpowiednimi kandydatami dla danych, który aplikacja kliencka można pobrać raz i pamięci podręcznej jako wyszukiwania danych.  

### <a name="inheritance-relationships"></a>Relacje dziedziczenia
Jeśli aplikacja kliencka używa zestaw klas, które stanowią część jednostki biznesowe toorepresent relacji dziedziczenia, można łatwo utrwalić tych jednostek w hello usługi tabel. Na przykład może być hello następującego zestawu klas zdefiniowanych w aplikacji klienta gdzie **osoby** jest klasą abstrakcyjną.

![][3]

Można ją utrwalić wystąpienia Witaj dwie klasy w hello usługi tabel za pomocą pojedynczej tabeli osoby za pomocą jednostek tego wyglądają następująco:  

![][4]

Aby uzyskać więcej informacji na temat pracy z wieloma typami jednostek w hello sama tabela w kodzie klienta, zobacz sekcję hello [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types) dalszej części tego przewodnika. Zapewnia to przykłady sposobu toorecognize hello typu jednostki w kodu klienta.  

## <a name="table-design-patterns"></a>Wzorce projektowe tabeli
W poprzednich sekcjach jak już wspomniano niektóre szczegółowe dyskusjach na temat sposób toooptimize tabeli projektowania dla obu podczas pobierania danych jednostki, za pomocą zapytań i wstawiania, aktualizowania i usuwania danych jednostki. W tej sekcji opisano niektóre wzorców, które są odpowiednie do użytku z rozwiązań usług tabeli. Ponadto zobaczysz, jak praktycznie rozwiązać niektóre problemy hello i kompromisy wywoływane wcześniej w tym przewodniku. Witaj Poniższy diagram przedstawia relacje hello hello różnych wzorców:  

![][5]

mapy wzorzec Hello powyżej omówiono niektóre relacje między wzorce (niebieski) i wzorce przed (kolor pomarańczowy), które są opisane w tym przewodniku. Oczywiście istnieje wielu wzorców, które warto uwzględnieniu. Na przykład jednego ze scenariuszy klucza hello usługi tabeli jest toouse hello [Zmaterializowany wzorzec widoku](https://msdn.microsoft.com/library/azure/dn589782.aspx) z hello [polecenia zapytania odpowiedzialność podział (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) wzorca.  

### <a name="intra-partition-secondary-index-pattern"></a>Wzorzec pomocniczy indeks wewnątrz partycji
Przechowywać wiele kopii każdej jednostki przy użyciu różnych **RowKey** wartości (w hello tej samej partycji) tooenable szybkie i wydajne wyszukiwanie i sortowanie alternatywne porządkuje przy użyciu różnych **RowKey** wartości. Aktualizacje między kopie były spójne przy użyciu EGT firmy.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Witaj usługi tabel automatycznie indeksuje jednostek przy użyciu hello **PartitionKey** i **RowKey** wartości. Dzięki temu tooretrieve aplikacji klienta efektywne wykorzystanie te wartości jednostki. Na przykład przy użyciu hello struktura tabeli pokazano poniżej, aplikacja kliencka można użyć punktu tooretrieve zapytania jednostki pracownika przy użyciu nazwy działu hello i identyfikator pracownika hello (hello **PartitionKey** i  **RowKey** wartości). Klient może również pobierać jednostki sortowane według identyfikatora pracownika każdego działu.

![][6]

Jeśli chcesz toofind stanie toobe jednostki pracowników na podstawie wartości hello innej właściwości, takie jak adres e-mail, należy użyć mniej wydajne toofind skanowania partycji dopasowania. Jest to spowodowane hello tabeli Usługa nie zapewnia indeksów pomocniczych. Ponadto istnieje toorequest nie opcji listy pracowników posortowanych w kolejności innej niż **RowKey** kolejności.  

#### <a name="solution"></a>Rozwiązanie
toowork wokół hello braku indeksów pomocniczych, można przechowywać kopie każdego obiektu z każdej kopii przy użyciu innego **RowKey** wartości. Jeśli przechowujesz jednostki o strukturze hello pokazano poniżej, pozwala na efektywne pobieranie jednostek pracowników na podstawie identyfikatora wiadomości e-mail adres lub pracowników. Witaj wartości prefiksu hello **RowKey**, "empid_" i "email_" pozwalają tooquery dla pojedynczego pracownika lub zakres pracowników przy użyciu zakresu adresów e-mail ani identyfikatorów pracownika.  

![][7]

Hello następujące dwa kryteria filtrowania (jeden wyszukiwanie według identyfikatora pracowników i jedną wyszukiwanie według adresu e-mail) zarówno Określ punkt zapytania:  

* $filter = (PartitionKey eq 'Sales') i (RowKey eq "empid_000223")  
* $filter = (PartitionKey eq 'Sales') i (RowKey eq 'email_jonesj@contoso.com")  

Po wykonaniu zapytania dla zakresu jednostek pracownika, można określić zakres sortowane w kolejności identyfikator pracownika, lub zakresem sortowane w kolejności adresu e-mail przez wysyłanie zapytań dla jednostek o prefiksu hello w hello **RowKey**.  

* Użyj wszystkich pracowników działu sprzedaży hello hello z identyfikator pracownika w hello zakresu 000100 too000199 toofind: $filter = (PartitionKey eq 'Sales') i (RowKey ge "empid_000100") i (RowKey le "empid_000199")  
* "element" należy użyć list toofind wszystkie hello pracownicy działu sprzedaży hello posiadających adres e-mail w programie hello: $filter = (PartitionKey eq 'Sales') i (RowKey ge "email_a") i (lt RowKey "email_b")  
  
  Należy pamiętać, że składnia filtru hello używane w powyższych przykładach hello z hello tabeli usługi interfejsu API REST, aby uzyskać więcej informacji, zobacz [jednostek zapytania](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Magazyn tabel jest stosunkowo tanie toouse, więc koszt koszty przechowywania danych zduplikowane hello nie powinno być głównym problemem. Jednak należy zawsze ocenić hello koszt projektu, w zależności od wymagań przewidywanego magazynu i dodawać tylko zduplikowanych wpisów toosupport hello zapytania, który aplikacja kliencka będzie wykonywać.  
* Jednostek pomocniczy indeks hello są przechowywane w hello sam partycji hello oryginalnej jednostki, dlatego należy upewnić się, nie przekraczają wartości docelowe skalowalności powitania dla poszczególnych partycji.  
* Można zachować zduplikowane obiekty zgodne ze sobą za pomocą EGTs tooupdate Witaj dwie kopie jednostki hello atomowo. Oznacza to, że wszystkie kopie jednostki należy przechowywać w hello tej samej partycji. Aby uzyskać więcej informacji, zobacz sekcję hello [przy użyciu transakcji grupy jednostek](#entity-group-transactions).  
* wartość używana dla hello Hello **RowKey** musi być unikatowa dla każdej jednostki. Rozważ użycie wartości klucza złożonego.  
* Dopełnienie wartości liczbowe w hello **RowKey** (na przykład identyfikator pracownika hello 000223), umożliwia Popraw sortowania i filtrowania na podstawie górną i dolną granicę.  
* Koniecznie niepotrzebne tooduplicate hello wszystkich właściwości jednostki. Na przykład, jeśli hello adres zapytań, które wiadomości e-mail przy użyciu hello jednostek hello wyszukiwania w hello **RowKey** nigdy nie trzeba wiek hello pracownika, te jednostki można mieć hello następujące struktury:

![][8]

* Jest zwykle lepiej toostore zduplikowane dane i zapewnić, że można pobrać wszystkich hello dane z pojedynczego zapytania, niż toolocate jedno zapytanie toouse jednostki i innym hello toolookup wymagane dane.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Za pomocą tego wzorca gdy aplikacja kliencka musi tooretrieve jednostek przy użyciu różnych różne klucze, gdy klient musi tooretrieve jednostek w różnych sortowania, a można zidentyfikować każdej jednostki przy użyciu różnych unikatowe wartości. Jednak należy się upewnić, że nie przekraczają limity skalowalności partycji hello przeprowadzania wyszukiwania jednostki przy użyciu różnych hello **RowKey** wartości.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorzec pomocniczy indeks między partycji](#inter-partition-secondary-index-pattern)
* [Wzorca złożonego klucza](#compound-key-pattern)
* [Grupowanie jednostki transakcji](#entity-group-transactions)
* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Wzorzec pomocniczy indeks między partycji
Przechowywać wiele kopii każdej jednostki przy użyciu różnych **RowKey** wartości w osobnych partycji lub w oddzielnych tabelach tooenable szybkie i wydajne wyszukiwań i alternatywne sortowania przy użyciu różnych **RowKey**wartości.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Witaj usługi tabel automatycznie indeksuje jednostek przy użyciu hello **PartitionKey** i **RowKey** wartości. Dzięki temu tooretrieve aplikacji klienta efektywne wykorzystanie te wartości jednostki. Na przykład przy użyciu hello struktura tabeli pokazano poniżej, aplikacja kliencka można użyć punktu tooretrieve zapytania jednostki pracownika przy użyciu nazwy działu hello i identyfikator pracownika hello (hello **PartitionKey** i  **RowKey** wartości). Klient może również pobierać jednostki sortowane według identyfikatora pracownika każdego działu.  

![][9]

Jeśli chcesz toofind stanie toobe jednostki pracowników na podstawie wartości hello innej właściwości, takie jak adres e-mail, należy użyć mniej wydajne toofind skanowania partycji dopasowania. Jest to spowodowane hello tabeli Usługa nie zapewnia indeksów pomocniczych. Ponadto istnieje toorequest nie opcji listy pracowników posortowanych w kolejności innej niż **RowKey** kolejności.  

Są przewidywanie bardzo dużą liczbę transakcji względem tych obiektów, a ryzyko hello toominimize hello ograniczanie klienta usługi tabeli.  

#### <a name="solution"></a>Rozwiązanie
toowork wokół hello braku indeksów pomocniczych, można przechowywać wiele kopii każdej jednostki z każdym Kopiuj, używając innego **PartitionKey** i **RowKey** wartości. Jeśli przechowujesz jednostki o strukturze hello pokazano poniżej, pozwala na efektywne pobieranie jednostek pracowników na podstawie identyfikatora wiadomości e-mail adres lub pracowników. Witaj wartości prefiksu hello **PartitionKey**, "empid_" i "email_" pozwalają tooidentify, który indeksu, który ma być toouse dla zapytania.  

![][10]

Hello następujące dwa kryteria filtrowania (jeden wyszukiwanie według identyfikatora pracowników i jedną wyszukiwanie według adresu e-mail) zarówno Określ punkt zapytania:  

* $filter = (PartitionKey eq ' empid_Sales") i (RowKey eq"000223")
* $filter = (PartitionKey eq ' email_Sales") i (RowKey eq 'jonesj@contoso.com")  

Po wykonaniu zapytania dla zakresu jednostek pracownika, można określić zakres sortowane w kolejności identyfikator pracownika, lub zakresem sortowane w kolejności adresu e-mail przez wysyłanie zapytań dla jednostek o prefiksu hello w hello **RowKey**.  

* Pracownicy działu sprzedaży z identyfikatorem pracowników w zakresie hello hello toofind hello wszystkich pracowników w **000100** za**000199** posortowane w użyciu kolejności identyfikator pracownika: $filter = (PartitionKey eq ' empid_Sales") i (RowKey ge" 000100') i (RowKey le "000199")  
* toofind wszystkie hello pracowników działu sprzedaży hello adres e-mail, który rozpoczyna się od "" posortowane w wiadomości e-mail adres kolejności użycia: $filter = (PartitionKey eq ' email_Sales") i (RowKey ge"") i (RowKey lt 'b')  

Należy pamiętać, że składnia filtru hello używane w powyższych przykładach hello z hello tabeli usługi interfejsu API REST, aby uzyskać więcej informacji, zobacz [jednostek zapytania](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Możesz zachować zduplikowane obiekty ostatecznie zgodne ze sobą za pomocą hello [wzorzec transakcji po pewnym czasie spójne](#eventually-consistent-transactions-pattern) toomaintain hello indeksu podstawowych i pomocniczych podmiotów.  
* Magazyn tabel jest stosunkowo tanie toouse, więc koszt koszty przechowywania danych zduplikowane hello nie powinno być głównym problemem. Jednak należy zawsze ocenić hello koszt projektu, w zależności od wymagań przewidywanego magazynu i dodawać tylko zduplikowanych wpisów toosupport hello zapytania, który aplikacja kliencka będzie wykonywać.  
* wartość używana dla hello Hello **RowKey** musi być unikatowa dla każdej jednostki. Rozważ użycie wartości klucza złożonego.  
* Dopełnienie wartości liczbowe w hello **RowKey** (na przykład identyfikator pracownika hello 000223), umożliwia Popraw sortowania i filtrowania na podstawie górną i dolną granicę.  
* Koniecznie niepotrzebne tooduplicate hello wszystkich właściwości jednostki. Na przykład, jeśli hello adres zapytań, które wiadomości e-mail przy użyciu hello jednostek hello wyszukiwania w hello **RowKey** nigdy nie trzeba wiek hello pracownika, te jednostki można mieć hello następujące struktury:
  
  ![][11]
* Jest zwykle lepsze toostore zduplikowane dane i upewnij się, że można pobrać wszystkich hello dane z pojedynczego zapytania niż toolocate jedno zapytanie toouse jednostki przy użyciu hello pomocniczy indeks i innym toolookup hello wymagane dane hello podstawowego indeksu.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Za pomocą tego wzorca gdy aplikacja kliencka musi tooretrieve jednostek przy użyciu różnych różne klucze, gdy klient musi tooretrieve jednostek w różnych sortowania, a można zidentyfikować każdej jednostki przy użyciu różnych unikatowe wartości. Ten wzorzec należy użyć tooavoid przekracza limity skalowalności partycji hello przeprowadzania wyszukiwania jednostki przy użyciu różnych hello **RowKey** wartości.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorzec ostatecznie spójne transakcji](#eventually-consistent-transactions-pattern)  
* [Wzorzec pomocniczy indeks wewnątrz partycji](#intra-partition-secondary-index-pattern)  
* [Wzorca złożonego klucza](#compound-key-pattern)  
* [Grupowanie jednostki transakcji](#entity-group-transactions)  
* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Wzorzec ostatecznie spójne transakcji
Włączyć spójności po pewnym czasie działania przez granice partycji lub granice systemu magazynu za pomocą kolejek platformy Azure.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
EGTs umożliwiają atomic transakcji między wiele jednostek, które współużytkują hello tego samego klucza partycji. Względu na wydajność i skalowalność, możesz określić toostore jednostek, które mają wymagań spójności w osobnych partycji lub w systemie magazynu oddzielne: w takiej sytuacji nie można użyć EGTs toomaintain spójności. Na przykład może być wymaganie toomaintain spójność ostateczna między:  

* Jednostek przechowywanych w dwóch różnych partycji w hello takie same, w różnych tabel w tabeli w różnych kont magazynu.  
* Jednostki przechowywane w hello usługi tabel a obiektu blob hello usługi Blob.  
* Jednostka przechowywane w usłudze tabel hello i pliku w systemie plików.  
* Jednostki magazynu w hello usługi tabel jeszcze zaindeksowane przy użyciu usługi Azure Search hello.  

#### <a name="solution"></a>Rozwiązanie
Korzystanie z kolejek platformy Azure, można zaimplementować rozwiązania, które zapewnia spójność ostateczna przez dwa lub więcej partycji ani systemów pamięci masowej.
tooillustrate tego podejścia, założono, że masz starego jednostek pracownika wymaganie toobe tooarchive stanie. Stary jednostki pracownika rzadko będą pytani i powinny być wykluczone z żadnych działań, które zajmują się bieżący pracowników. tooimplement to wymaganie, aktywnych pracowników są przechowywane w hello **bieżącego** tabeli i starego pracowników w hello **archiwum** tabeli. Archiwizowanie pracownika wymaga toodelete hello jednostka z hello **bieżącego** tabeli i Dodaj hello jednostki toohello **archiwum** tabeli, ale nie można użyć tooperform EGT tych dwóch operacji. ryzyko hello tooavoid czy awaria powoduje tooappear jednostki w obu lub ani tabel, operacja archiwizacji hello muszą być zgodne po pewnym czasie. Witaj Poniższy diagram sekwencji przedstawiono kroki hello w tej operacji. Więcej szczegółów podano ścieżek wyjątków w hello następujący tekst.  

![][12]

Klient inicjuje operację archiwum hello umieszczając wiadomości w kolejce systemu Azure, w tym przykładzie tooarchive pracownika #456. Rolę procesu roboczego sonduje kolejkę hello nowe wiadomości; Po znalezieniu jednego odczytuje wiadomość hello i pozostawia ukryte kopiowania na powitania kolejki. obok roli procesu roboczego Hello pobiera kopię hello jednostki z hello **bieżącego** tabeli, wstawia kopię hello **archiwum** tabeli, a następnie usuwa hello oryginalnego z hello **bieżącego**tabeli. Jeśli nie wystąpiły błędy z poprzednich kroków hello, roli procesu roboczego hello usuwa ukryte wiadomość hello z hello kolejki.  

W tym przykładzie krok 4 wstawia hello pracowników do hello **archiwum** tabeli. Go można dodać obiektu blob tooa pracownika hello w hello usługa Blob lub pliku w systemie plików.  

#### <a name="recovering-from-failures"></a>Odzyskiwanie z błędami
Ważne jest, że hello czynności w krokach **4** i **5** musi być *idempotentności* w przypadku roli procesu roboczego hello musi toorestart hello archiwum operacji. Jeśli używasz usługi tabel hello w kroku **4** należy użyć operacji "Wstawianie lub zastępowanie"; kroku **5** należy użyć "usunąć, jeśli istnieje" operacji w bibliotece klienta hello są używane. Jeśli korzystasz z innego systemu magazynu, należy użyć operacji odpowiednie idempotentności.  

Jeśli hello roli proces roboczy nigdy nie wykonuje kroku **6**, następnie po wiadomość hello limitu czasu pojawi się w kolejce hello gotowe do tooreprocess tootry roli procesu roboczego hello go. Rola proces roboczy Hello można sprawdzić, ile razy wiadomość w kolejce hello została przeczytana i w razie potrzeby flagi jest komunikat "skażone" do badania wysyłając tooa oddzielnych kolejki. Aby uzyskać więcej informacji na temat odczytywania wiadomości w kolejce i sprawdzanie hello usuwania z kolejki liczby, zobacz [pobrać wiadomości](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Błędy z usługi tabeli i kolejki hello są błędów przejściowych i aplikacja kliencka powinna zawierać toohandle logiki ponawiania odpowiedniego je.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* To rozwiązanie nie wymaga izolacji transakcji. Na przykład klient może odczytać hello **bieżącego** i **archiwum** tabel, gdy rola proces roboczy hello między krokami **4** i **5**i zobaczyć niespójne widok hello danych. Należy pamiętać, że hello dane będą zgodne po pewnym czasie.  
* Należy upewnić się, że kroki 4 i 5 są idempotentności w spójność ostateczna tooensure kolejności.  
* Można skalować rozwiązania hello przy użyciu wielu kolejek i wystąpień roli procesu roboczego.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Ten wzorzec należy użyć tooguarantee spójność ostateczna między jednostkami, które istnieją w różnych partycji lub tabele. Ten wzorzec tooensure spójność ostateczna dla operacji można rozszerzyć na powitania tabeli usługi i usługa Blob hello i innych źródeł danych magazynu Azure, takich jak system plików bazy danych lub hello.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Grupowanie jednostki transakcji](#entity-group-transactions)  
* [Scalanie lub Zastąp](#merge-or-replace)  

> [!NOTE]
> Jeśli izolacji transakcji jest ważne tooyour rozwiązanie, należy rozważyć zmodyfikowanie tooenable Twojego tabel należy toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Wzorzec jednostek indeksu
Obsługa indeksu jednostek tooenable wydajne wyszukiwanie zwracających list jednostek.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Witaj usługi tabel automatycznie indeksuje jednostek przy użyciu hello **PartitionKey** i **RowKey** wartości. Dzięki temu tooretrieve aplikacji klienckich jednostki efektywne wykorzystanie zapytania punktu. Na przykład za pomocą hello struktura tabeli pokazano poniżej, aplikacja kliencka pozwala na efektywne pobieranie jednostki pracownika przy użyciu nazwy działu hello i identyfikator pracownika hello (hello **PartitionKey** i **RowKey** ).  

![][13]

Jeśli chcesz toobe tooretrieve stanie listę jednostek pracowników na podstawie hello wartości innej właściwości nie jest unikatowa, takie jak nazwisko, należy użyć mniej wydajne partycji skanowania dopasowań toofind zamiast toolook indeksu je bezpośrednio w górę. Jest to spowodowane hello tabeli Usługa nie zapewnia indeksów pomocniczych.  

#### <a name="solution"></a>Rozwiązanie
Wyszukiwanie tooenable przez nazwisko ze strukturą entity hello pokazanym powyżej muszą zachować listę identyfikatorów pracownika. Ma tooretrieve hello pracownika jednostki o określonej nazwie ostatniego, takich jak Nowak, należy w pierwszej kolejności zlokalizować hello listę identyfikatorów pracowników dla pracowników z Nowak jako nazwisk i następnie pobrać tych jednostek pracownika. Istnieją trzy główne opcje przechowywania hello listy identyfikatorów pracowników:  

* Użyj magazynu obiektów blob.  
* Utwórz jednostki indeksu w hello sam partycji hello pracownika jednostki.  
* Utwórz jednostki indeksu w oddzielnej partycji lub tabeli.  

<u>Opcja #1: Magazyn obiektów blob służy</u>  

Witaj pierwszej opcji utworzenie obiektu blob każdy unikatowy nazwisko, a w każdym magazynu obiektów blob listę hello **PartitionKey** (dział) i **RowKey** (identyfikator pracownika) wartości dla pracowników, którzy mają to ostatnia Nazwa. Podczas dodawania lub usuwania pracownika należy się upewnić, że zawartość hello hello odpowiedniego obiektu blob jest ostatecznie zgodne z hello pracownika jednostek.  

<u>Opcja #2:</u> Utwórz indeks jednostek w hello tej samej partycji  

Druga opcja hello można użyć indeksu podmiotom przechowywania hello następujące dane:  

![][14]

Witaj **EmployeeIDs** właściwość zawiera listę identyfikatorów pracowników dla pracowników z nazwisko hello przechowywane w hello **RowKey**.  

Hello poniższe kroki wchodzą w skład procesu hello, jakie należy wykonać podczas dodawania nowych pracowników, jeśli używasz hello drugiej opcji. W tym przykładzie dodajemy pracownika z identyfikatorem 000152 i nazwisko Nowak działu sprzedaży hello:  

1. Pobrać jednostki indeksu hello o **PartitionKey** wartość "Sprzedaż" i hello **RowKey** wartość "Nowak". Zapisz hello ETag toouse tej jednostki w kroku 2.  
2. Utwórz jednostki transakcji grupy (to znaczy operacji zbiorczej), która wstawia nową jednostkę pracownika hello (**PartitionKey** wartość "Sprzedaż" i **RowKey** wartość "000152"), i aktualizacje hello jednostki indeksu ( **PartitionKey** wartość "Sprzedaż" i **RowKey** wartość "Nowak"), dodając hello nowych pracowników identyfikator toohello listy w polu EmployeeIDs hello. Aby uzyskać więcej informacji o transakcji grupy jednostek, zobacz [transakcji grupy jednostek](#entity-group-transactions).  
3. Jeśli transakcji grupy jednostki hello zakończy się niepowodzeniem z powodu błędu optymistycznej współbieżności (ktoś właśnie zmodyfikował jednostki indeksu hello), wymagana będzie toostart za pośrednictwem w kroku 1 ponownie.  

Jeśli używasz hello druga opcja, można użyć podobne toodeleting podejście pracownika. Zmiana jego nazwisko jest nieco bardziej skomplikowane, ponieważ będą potrzebne tooexecute transakcji grupy jednostki, która aktualizuje trzy jednostki: hello jednostki pracownika, hello jednostki indeksu dla starego nazwisko hello i hello jednostki indeksu dla nowej nazwy ostatniego hello. Każda jednostka musi pobrać przed wprowadzeniem jakichkolwiek zmian w kolejności wartości ETag hello tooretrieve można następnie użyć tooperform hello aktualizacji za pomocą optymistycznej współbieżności.  

Witaj poniższe kroki wchodzą w skład procesu hello, które należy wykonać, gdy będziesz potrzebować toolook wszystkich pracowników hello o danej nazwie ostatniego w dziale, jeśli używasz hello druga opcja. W tym przykładzie czekamy wszystkich pracowników hello z nazwisko Nowak działu sprzedaży hello:  

1. Pobrać jednostki indeksu hello o **PartitionKey** wartość "Sprzedaż" i hello **RowKey** wartość "Nowak".  
2. Przeanalizować hello listę identyfikatorów, w polu EmployeeIDs hello pracowników.  
3. Aby uzyskać dodatkowe informacje na temat każdego z tych pracowników (na przykład ich adresów e-mail), należy pobrać poszczególnych jednostek pracownika hello przy użyciu **PartitionKey** wartość "Sprzedaż" i **RowKey** wartości z Lista Hello pracowników, który został uzyskany w kroku 2.  

<u>Opcja #3:</u> Utwórz indeks jednostki w oddzielnej partycji lub tabeli  

Trzecia opcja hello można użyć indeksu podmiotom przechowywania hello następujące dane:  

![][15]

Witaj **EmployeeIDs** właściwość zawiera listę identyfikatorów pracowników dla pracowników z nazwisko hello przechowywane w hello **RowKey**.  

Z hello trzecia opcja nie można użyć EGTs toomaintain spójności, ponieważ jednostki indeksu hello znajdują się w oddzielnej partycji z hello pracownika jednostek. Należy się upewnić, że jednostek indeksu hello są ostatecznie zgodne z hello pracownika jednostek.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* To rozwiązanie wymaga co najmniej dwa zapytania tooretrieve dopasowania jednostek: jedna tooquery hello indeksu jednostek tooobtain hello lista **RowKey** wartości, a następnie wykonuje zapytanie tooretrieve każdej jednostki w liście hello.  
* Biorąc pod uwagę, że maksymalnie rozmiar równy 1 MB, opcja #2 zawiera poszczególne jednostki i opcji #3 w rozwiązaniu hello założono hello listę pracowników identyfikatorów dowolnym danym nazwisko nigdy nie jest większa niż 1 MB. Jeśli hello listę identyfikatorów pracowników jest prawdopodobnie toobe większa niż 1 MB, rozmiar, użyj opcji #1 i przechowywać dane indeksu hello w magazynie obiektów blob.  
* Jeśli używasz opcji #2 (przy użyciu toohandle EGTs Dodawanie i usuwanie pracowników i zmienianie jego nazwisko) możesz należy sprawdzić, czy wolumin hello transakcji będzie podejścia hello limity skalowalności w danej partycji. Jeśli hello tak jest, należy rozważyć rozwiązanie po pewnym czasie spójne (#1 lub opcję #3), które używa kolejek toohandle hello aktualizacji żądań i umożliwia toostore możesz jednostek indeksu w oddzielnej partycji z hello pracownika jednostek.  
* Opcja #2 w tym rozwiązaniu założono, że toolook się według nazwisk działu: na przykład chcesz tooretrieve listę pracownikom nazwisko Nowak hello działu sprzedaży. Jeśli chcesz, aby mogli toolook toobe wszystkich pracowników hello z nazwisko Kowalski w całej organizacji hello, należy użyć opcji #1 lub opcja #3.
* Można implementować rozwiązania na podstawie kolejki, które zapewnia spójność ostateczna (zobacz hello [wzorzec transakcji po pewnym czasie spójne](#eventually-consistent-transactions-pattern) więcej szczegółów).  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Ten wzorzec należy użyć toolookup zestawu jednostek, że wszystkie mają wspólne wartość właściwości, na przykład wszystkich pracowników z hello nazwisko Nowak.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorca złożonego klucza](#compound-key-pattern)  
* [Wzorzec ostatecznie spójne transakcji](#eventually-consistent-transactions-pattern)  
* [Grupowanie jednostki transakcji](#entity-group-transactions)  
* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Wzorzec denormalization
Łączenie danych powiązanych ze sobą w tooenable pojedynczej jednostki tooretrieve hello wszystkie dane, które należy za pomocą kwerendy pojedynczy punkt.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
W relacyjnej bazie danych zwykle normalizacji danych tooremove duplikatów, co w zapytaniach, które pobierają dane z wielu tabel. Jeśli normalizacji danych w tabelach platformy Azure, musisz wprowadzić wiele rund z powitania klienta toohello serwera tooretrieve powiązanych danych. Na przykład z hello struktura tabeli pokazano poniżej możesz potrzebne dwa zaokrąglona rund tooretrieve hello szczegółów dla działu: jeden toofetch hello działu jednostki, która zawiera identyfikator menedżera hello i szczegóły innego żądania toofetch hello menedżera pracownika Jednostka.  

![][16]

#### <a name="solution"></a>Rozwiązanie
Zamiast hello danych są przechowywane w dwóch oddzielnych jednostek, denormalize hello danych i przechowywać kopię szczegóły Menedżera hello w jednostce działu hello. Na przykład:  

![][17]

Z jednostkami działu przechowywane z tymi właściwościami można teraz pobrać wszystkie szczegóły hello potrzebnych o dział przy użyciu zapytania punktu.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Brak niektórych koszt nakładów pracy związanych z przechowywaniem niektóre dane dwa razy. Witaj poprawiać wydajność (wynikające z mniej usługi magazynu toohello żądania) zwykle przeważa nad hello brzegowego wzrost kosztów magazynowania (i częściowo przesunięcia ten koszt przez redukcję hello liczba transakcji, które wymagają toofetch hello szczegóły działu).  
* Trzeba zachować spójność hello Witaj dwie jednostki, których są przechowywane informacje o menedżerach. Można obsługiwać hello spójności problem przy użyciu EGTs tooupdate wiele jednostek w ramach jednej transakcji atomic: w tym przypadku hello działu jednostki i jednostki pracownika hello Menedżer działu hello są przechowywane w hello tej samej partycji.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Gdy potrzebne są często toolook powiązane informacje, należy użyć tego wzorca. Ten wzorzec zmniejsza hello liczba zapytań, klient musi wprowadzać tooretrieve hello danych, które wymaga.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorca złożonego klucza](#compound-key-pattern)  
* [Grupowanie jednostki transakcji](#entity-group-transactions)  
* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Wzorca złożonego klucza
Użyj złożone **RowKey** dane z zapytania pojedynczy punkt dotyczące wartości tooenable toolookup klienta.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
W relacyjnej bazie danych, jest dość fizycznych toouse sprzężenia w zapytaniach tooreturn powiązane elementy danych toohello klienta w jednym zapytaniu. Na przykład można użyć toolook identyfikator pracownika hello listę powiązanych jednostek zawierających wydajności i przeglądanie danych dla określonego pracownika.  

Przyjęto założenie, że pracownik jednostki są przechowywane w usłudze tabeli hello przy użyciu następującej struktury hello:  

![][18]

Należy również toostore danych historycznych dotyczących tooreviews i wydajności dla każdego pracownika hello roku działał dla Twojej organizacji i stanie tooaccess toobe te informacje są niezbędne w roku. Jedną z opcji jest toocreate innej tabeli, która przechowuje jednostek z następującej struktury hello:  

![][19]

Należy zauważyć, że ta podejścia można może zadecydować tooduplicate niektóre informacje (takie jak imię i nazwisko) hello nowe jednostki tooenable tooretrieve możesz danych za pomocą pojedynczego żądania. Nie można jednak obsługa wysoki poziom spójności, ponieważ nie można użyć atomowo EGT tooupdate Witaj dwie jednostki.  

#### <a name="solution"></a>Rozwiązanie
Przechowywanie nowy typ jednostek w oryginalnej tabeli przy użyciu jednostek z następującej struktury hello:  

![][20]

Zwróć uwagę, jak hello **RowKey** teraz klucza złożonego składa się z hello identyfikator i hello rok hello przeglądanie danych, który umożliwia tooretrieve hello pracownika wydajności i przejrzyj dane z pojedynczego żądania dla pojedynczej jednostki.  

Witaj poniższy przykład przedstawia, jak można pobrać wszystkich danych przeglądu powitania dla danego pracownika (na przykład 000123 pracownik działu sprzedaży hello):  

$filter = (PartitionKey eq 'Sales') i (RowKey ge "empid_000123") i (lt RowKey "empid_000124") & $select = RowKey, Menedżer klasyfikacji, Klasyfikacja równorzędnej, komentarze  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Należy użyć odpowiedniego separatora, dzięki którym hello łatwe tooparse **RowKey** wartość: na przykład **000123_2012**.  
* Są także zapisanie tej jednostki w hello sam partycji inne jednostki, które zawierają dane związane z hello samego pracownika, co oznacza, można użyć EGTs toomaintain wysoki poziom spójności.
* Należy rozważyć, jak często będą zapytania hello toodetermine danych czy ten wzorzec jest odpowiednia.  Na przykład jeśli będą uzyskiwać dostęp do rzadko hello przeglądanie danych i hello głównego danych o pracownikach często należy go przechowywać jako osobne jednostki.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Użyj tego wzorca należy toostore jedną lub więcej jednostek powiązanych z tej kwerendy można często.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Grupowanie jednostki transakcji](#entity-group-transactions)  
* [Praca z typami jednostek heterogenicznych](#working-with-heterogeneous-entity-types)  
* [Wzorzec ostatecznie spójne transakcji](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Wzorzec końcowego fragmentu dziennika
Pobrać hello  *n*  jednostek ostatnio dodany tooa partycji przy użyciu **RowKey** wartość sortujące odwrotnej daty i czasu kolejności.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Typowym wymaganiem jest możliwe tooretrieve hello ostatnio utworzony jednostki, na przykład hello dziesięć najnowszych wydatków oświadczenia złożone przez pracownika. Pomocy technicznej wysyła zapytanie do tabeli **$top** najpierw zapytania hello tooreturn operacji  *n*  jednostek z zestawu: Brak Brak kwerendy równoważne operacji tooreturn hello ostatniego n jednostek w zestawie.  

#### <a name="solution"></a>Rozwiązanie
Przy użyciu jednostek hello magazynu **RowKey** czy naturalnie sortuje odwrotnie daty/godziny kolejności przy użyciu, dzięki czemu najnowszy wpis hello jest zawsze hello pierwszej tabeli hello.  

Na przykład tooretrieve stanie toobe hello 10 najnowszych oświadczeń wydatków przesłane przez pracownika, można użyć wartości osi w odwrotnej pochodną hello bieżącej daty/godziny. Witaj poniższy przykład kodu C# pokazuje jednokierunkowej toocreate odpowiednią wartość "odwrócony Takty" dla **RowKey** który sortuje od hello najnowszych toohello najstarsze:  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Możesz odzyskać toohello wartość daty i godziny przy użyciu hello następującego kodu:  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

Zapytanie tabeli Hello wygląda następująco:  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Należy konsoli wartości osi w odwrotnej hello zer wartość ciągu hello tooensure Sortuje zgodnie z oczekiwaniami.  
* Należy pamiętać o wartości docelowe skalowalności hello na poziomie hello partycji. Uważaj, aby nie tworzyć partycji punktu aktywnego.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Użyj wzorca to, gdy będziesz potrzebować tooaccess jednostek w kolejności odwrotnej daty/godziny lub tooaccess hello ostatnio dodane jednostek.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Dołączenie wartości / append przed wzorca](#prepend-append-anti-pattern)  
* [Pobieranie jednostki](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Wzorzec delete dużych obciążeń
Włącz usuwanie hello dużą liczbę jednostek przez zapisanie wszystkich jednostek hello do usunięcia jednoczesnych w ich własnych osobnej tabeli; Możesz usunąć jednostek hello przez usunięcie hello tabeli.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Wiele aplikacji Usuń stare dane, które nie będzie już potrzebował aplikacji klienckiej dostępne tooa toobe lub tej aplikacji hello ma zarchiwizowane tooanother nośniku. Zwykle określenie tych danych w dniu: na przykład masz rekordu toodelete wymaganie wszystkich żądań logowania, które są starsze niż 60 dni.  

Jeden projekt możliwe jest toouse hello Data i godzina żądania logowania hello hello **RowKey**:  

![][21]

Takie podejście pozwala uniknąć hotspotami partycji, ponieważ aplikacja hello można Wstawianie i usuwanie jednostek logowania dla każdego użytkownika w oddzielnej partycji. Jednak takie podejście może być kosztowne i czasochłonne, jeśli masz dużą liczbę jednostek, ponieważ najpierw należy tooperform tabeli skanowanie w kolejności tooidentify wszystkie toodelete jednostek hello oraz musisz usunąć każdej jednostki stary. Należy pamiętać, że można zmniejszyć hello liczby rund toohello serwera wymagane toodelete hello starego jednostek przez przetwarzanie wsadowe wiele żądań delete służących do EGTs.  

#### <a name="solution"></a>Rozwiązanie
Użyj osobnej tabeli dla każdego dnia prób logowania. Hello jednostki projektu powyżej hotspotami tooavoid można używać podczas wstawiania jednostek i usuwania starych jednostek jest teraz po prostu kwestia usuwanie codziennie w jednej tabeli (operację jednego magazynu) zamiast znajdowania i usuwania, a setki tysięcy logowania poszczególnych jednostek każdego dnia.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Projekt obsługuje inne sposoby aplikacja będzie korzystać z hello dane, takie jak wyszukiwanie konkretnych obiektów połączeń przy użyciu innych danych lub generowania agregują informacje?  
* Projektu uniknąć punkty aktywne wstawiając nowych jednostek  
* Oczekiwane opóźnienia, jeśli chcesz, aby tooreuse hello takie same nazwy tabeli po jej usunięciu. Konieczne jest lepsze tooalways Użyj unikatowej tabeli nazw.  
* Oczekiwać, że niektóre ograniczenia przepustowości przy pierwszym użyciu nową tabelę podczas hello usługi tabel uzyskuje informacje o hello wzorce dostępu i rozpowszechnia hello partycji w węzłach. Należy rozważyć, jak często należy toocreate nowe tabele.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Użyj tego wzorca, jeśli masz dużą liczbę jednostek, które należy usunąć na powitania tym samym czasie.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Grupowanie jednostki transakcji](#entity-group-transactions)
* [Modyfikowanie jednostek](#modifying-entities)  

### <a name="data-series-pattern"></a>Wzorzec serii danych
Seria pełnych danych magazynu w pojedynczej jednostki toominimize hello liczbę żądań, które należy wykonać.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Typowy scenariusz dotyczy toostore aplikacji serii danych, że zwykle wymaga ona tooretrieve jednocześnie. Na przykład aplikacji może rejestrować liczbę wiadomości Błyskawiczne każdy pracownik wysyła co godzinę, a następnie użyj tego tooplot informacje, ile wiadomości wysyłane poszczególnych użytkowników za pośrednictwem hello poprzednich 24 godzin. Jeden projekt może być toostore 24 jednostki dla każdej pracowników:  

![][22]

Ten projekt można łatwo zlokalizować i aktualizować hello tooupdate jednostki dla każdego pracownika zawsze, gdy aplikacja hello musi wartości liczby wiadomość hello tooupdate. Jednak tooretrieve hello tooplot informacji wykres aktywności hello hello poprzednie 24 godziny, należy pobrać 24 jednostek.  

#### <a name="solution"></a>Rozwiązanie
Użyj następującego projektu wraz z liczbą wiadomość hello toostore oddzielne właściwości dla każdej godziny hello:  

![][23]

Ten projekt można użyć liczbą wiadomość hello tooupdate operacji scalania dla pracowników na określone godziny. Teraz można pobrać wszystkich informacji hello potrzebne tooplot hello wykresu przy użyciu żądania dla pojedynczej jednostki.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Jeśli pełnych danych serii nie pasuje do pojedynczej jednostki (jednostka może mieć właściwości too252), należy użyć magazynu danych alternatywnych, takich jak obiektu blob.  
* Jeśli wielu klientów jednocześnie aktualizowania jednostki, konieczne będzie toouse hello **ETag** tooimplement optymistycznej współbieżności. Jeśli wielu klientów, może wystąpić wysokiej rywalizacji.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Użyj tego wzorca należy tooupdate i pobrać serii danych skojarzonych z pojedynczą jednostkę.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorzec dużych jednostek](#large-entities-pattern)  
* [Scalanie lub Zastąp](#merge-or-replace)  
* [Wzorzec transakcji po pewnym czasie spójne](#eventually-consistent-transactions-pattern) (jeśli są przechowywane hello serii danych w obiekcie blob)  

### <a name="wide-entities-pattern"></a>Wzorzec szeroki jednostek
Wiele jednostek logicznych toostore jednostek fizycznych za pomocą więcej niż 252 właściwości.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Pojedynczą jednostkę może mieć maksymalnie 252 właściwości (z wyjątkiem właściwości systemu obowiązkowe hello) i nie można przechowywać więcej niż 1 MB danych, w sumie. W relacyjnej bazie danych zwykle jak round żadnych limitów dotyczących hello rozmiar wiersza przez dodanie nowej tabeli i wymuszania między nimi relacji 1-do-1.  

#### <a name="solution"></a>Rozwiązanie
Usługa tabel hello można przechowywać wiele jednostek toorepresent obiekt pojedynczego dużych firm z więcej niż 252 właściwości. Na przykład jeśli chcesz toostore liczbę hello liczbę wiadomości Błyskawicznych wysyłane przez każdy pracownik dla hello ostatnich 365 dni, można użyć powitania po projekt, który używa dwie jednostki z różnych schematów:  

![][24]

Jeśli potrzebujesz toomake zmiany, która wymaga zaktualizowania zarówno tookeep jednostek, ich synchronizowane ze sobą służy EGT. W przeciwnym razie można liczbę operacji wiadomość hello tooupdate pojedynczego scalania dla określonego dnia. wszystkie hello danych dla poszczególnych pracowników, należy pobrać obie te jednostki, co można zrobić za pomocą dwóch wydajne żądania, które używają obu tooretrieve **PartitionKey** i **RowKey** wartości.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Pobieranie całą jednostkę logiczną obejmuje co najmniej dwóch transakcji magazynowych: jeden tooretrieve Jednostka fizyczna.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Usługa tabel którego rozmiaru lub liczby właściwości przekracza limity hello pojedynczą jednostkę w hello jednostek toostore muszą używać tego wzorca.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Grupowanie jednostki transakcji](#entity-group-transactions)
* [Scalanie lub Zastąp](#merge-or-replace)

### <a name="large-entities-pattern"></a>Wzorzec dużych jednostek
Użyj wartości właściwości dużych toostore magazynu obiektów blob.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Poszczególne jednostki nie można przechowywać więcej niż 1 MB danych w całości. Jeśli jeden lub kilka właściwości przechowywane wartości powodujące hello całkowity rozmiar tooexceed Twojego jednostki, ta wartość, nie można przechowywać hello całej jednostki w hello usługi tabel.  

#### <a name="solution"></a>Rozwiązanie
Jeśli jednostki przekracza 1 MB rozmiar, ponieważ co najmniej jednej właściwości zawierają dużą ilość danych, można przechowywać dane w hello usługa Blob i następnie zapisać hello adres obiektu blob hello we właściwości w obiekcie hello. Na przykład można przechowywać hello zdjęcie pracownika w magazynie obiektów blob i przechowywać zdjęcie toohello łącze w hello **fotografii** właściwości jednostki pracowników:  

![][25]

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* spójność ostateczna toomaintain między hello jednostki w hello usługi tabel i danych hello hello usługa Blob, użyj hello [wzorzec transakcji po pewnym czasie spójne](#eventually-consistent-transactions-pattern) toomaintain jednostek.
* Pobieranie całą jednostkę obejmuje co najmniej dwóch transakcji magazynowych: jedną jednostkę hello tooretrieve i hello tooretrieve jednego obiektu blob danych.  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Ten wzorzec należy używać wtedy, gdy konieczne toostore jednostek, którego rozmiar przekracza limity hello pojedynczą jednostkę w usłudze tabel hello.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorzec ostatecznie spójne transakcji](#eventually-consistent-transactions-pattern)  
* [Wzorzec szeroki jednostek](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Dołączenie wartości Dołącz przed wzorca
Zwiększenie skalowalności, jeśli masz dużą liczbę operacji wstawienia przez rozłożenie wstawia hello wiele partycji.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Dołączanie lub dołączanie jednostek tooyour przechowywane jednostek zwykle powoduje dodanie nowych jednostek toohello najpierw aplikacji hello lub ostatni partycji sekwencji partycji. W takim przypadku wszystkie wstawia hello w danym momencie są odbywa się w hello wstawia tej samej partycji, tworzenie punkt aktywny, która uniemożliwia hello tabeli usługi równoważenia obciążenia w wielu węzłach i może doprowadzić do Twojej aplikacji toohit hello skalowalności obiekty docelowe dla partycji. Na przykład jeśli masz aplikację, która dzienniki sieci i zasobów dostępu przez pracowników, może spowodować struktury jednostek, jak pokazano poniżej, a następnie hello staje się punkt aktywny, jeśli wielkość hello transakcji osiągnie hello skalowalność docelową dla partycji bieżącej godziny poszczególnych partycji:  

![][26]

#### <a name="solution"></a>Rozwiązanie
Witaj następującej struktury jednostek alternatywnych pozwala uniknąć punkt aktywny na określonej partycji jako zdarzenia Dzienniki aplikacji hello:  

![][27]

Zwróć uwagę, z tym przykładem sposobu zarówno hello **PartitionKey** i **RowKey** są klucze złożone. Witaj **PartitionKey** używa hello działu, jak i rejestrowania hello toodistribute identyfikator pracownika na wiele partycji.  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o hello jak tooimplement tego wzorca:  

* Wykonuje hello alternatywnych klucza strukturę, która pozwala uniknąć tworzenia dynamicznej partycji w operacji wstawienia wydajnie kwerend hello pomocy technicznej aplikacji klienckiej sprawia, że?  
* Przewidywany woluminu transakcji oznacza są prawdopodobnie tooreach hello wartości docelowe skalowalności dla poszczególnych partycji i jest ograniczany przez usługę magazynu hello?  

#### <a name="when-toouse-this-pattern"></a>Gdy toouse tego wzorca
Unikaj hello dołączy Dołącz wzorzec przed gdy woluminu transakcji jest prawdopodobnie tooresult w ograniczania przez usługę magazynu hello, gdy uzyskujesz dostęp do partycji gorących.  

#### <a name="related-patterns-and-guidance"></a>Wskazówki i wzorce pokrewne
Witaj następujące wskazówki i wzorce mogą także mieć znaczenie w przypadku implementacja tego wzorca:  

* [Wzorca złożonego klucza](#compound-key-pattern)  
* [Wzorzec końcowego fragmentu dziennika](#log-tail-pattern)  
* [Modyfikowanie jednostek](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Wzorzec przed dane dziennika
Zwykle należy używać hello usługa Blob zamiast hello danych dziennika toostore usługi tabeli.  

#### <a name="context-and-problem"></a>Kontekst, jak i problemu
Typowy przypadek użycia dla danych dziennika jest tooretrieve wybrane wpisy dziennika dla zakresu określonej daty/godziny: na przykład chcesz toofind hello wszystkie komunikaty o błędach i krytyczne zarejestrowane przez aplikację między 15:04 i 15:06 w określonym dniu. Nie ma toouse hello Data i godzina hello dziennika komunikatów toodetermine hello partycji zapisywania dziennika jednostki do: czy wyniki w dynamicznej partycji, ponieważ w danym momencie, muszą współdzielić wszystkich jednostek dziennika hello hello sam **PartitionKey** wartość (zobacz sekcja hello [Prepend/dołączanie wzorzec przed](#prepend-append-anti-pattern)). Na przykład hello następującego schematu jednostki dla komunikatu dziennika wyniki gorących partycji, ponieważ aplikacja hello zapisuje komunikaty dziennika toohello partycji dla hello bieżącą datę i godzinę:  

![][28]

W tym przykładzie hello **RowKey** hello Data i godzina tooensure wiadomości dziennika hello komunikaty dziennika są przechowywane, sortowane w kolejności daty/godziny i zawierają identyfikator komunikatu w przypadku, gdy wiele komunikatów dziennika udostępnianie hello same daty i godziny.  

Innym rozwiązaniem jest toouse **PartitionKey** która sprawia, że aplikacja hello zapisuje komunikaty w zakresie partycji. Na przykład jeśli hello źródło komunikatu dziennika hello udostępnia toodistribute sposób wiadomości między wiele partycji, można użyć powitania po schemat podmiotu:  

![][29]

Jednak hello problem z tym schemacie jest tym tooretrieve hello wszystkie komunikaty dziennika dla określonego okresu musi przeszukać każdej partycji w tabeli hello.

#### <a name="solution"></a>Rozwiązanie
Hello poprzedniej sekcji wyróżnione hello problem w trakcie toouse hello wpisów dziennika toostore usługi tabeli i sugerowane dwa niezadowalające, projektów usług. Jedno rozwiązanie, które doprowadziły tooa gorących partycji o hello ryzyko niską wydajnością, zapisywanie wiadomości dziennika. Hello innego rozwiązania dało w wyniku zapytania niską wydajność ze względu na powitania wymaganie tooscan każdej partycji w wiadomości powitania tabeli tooretrieve dziennika dla zakresu określonego czasu. Magazyn obiektów blob oferuje lepszym rozwiązaniem dla tego typu scenariuszy i jak Azure analityka magazynu magazynów hello dziennika dane są zbierane.  

W tej sekcji opisano, jak analityka magazynu przechowuje dane dziennika w magazynie obiektów blob jako ilustracja to danych toostoring podejście, które zwykle zapytania według zakresu.  

Analityka magazynu przechowuje komunikaty dziennika w formacie rozdzielanym w wielu obiektów blob. format rozdzielanej Hello ułatwia dla klienta danych hello tooparse aplikacji hello wiadomości dziennika.  

Analityka magazynu używa konwencji nazewnictwa dla obiektów blob, które umożliwia toolocate hello obiektów blob (lub obiektów blob) zawierające komunikaty dziennika hello, dla których w przypadku wyszukiwania. Na przykład obiektu blob o nazwie "queue/2014/07/31/1800/000001.log" zawiera komunikatów dziennika, które dotyczą usługi kolejek toohello hello godzinę, począwszy od 18:00 w 31 lipca 2014. Witaj "000001" wskazuje, że jest hello pierwszy plik dziennika dla tego okresu. Analityka magazynu najpierw rejestruje także hello znacznikami czasu hello i ostatniego logowania wiadomości przechowywanych w pliku hello jako część metadane hello obiektu blob. Witaj interfejsu API dla obiekt blob magazynu umożliwia Znajdź obiekty BLOB w kontenerze na podstawie prefiksu nazwy: toolocate wszystkie obiekty BLOB hello, które zawierają kolejki rejestrowanie danych przez hello godzinę, począwszy od 18:00, możesz użyć hello prefiksu "kolejki/2014/07/31/1800."  

Analityka magazynu buforuje wiadomości dziennika wewnętrznie i okresowo aktualizuje hello odpowiednich obiektów blob lub tworzy nowy adres w usłudze hello partii najnowsze wpisy dziennika. Pozwala to zmniejszyć liczbę hello zapisów wykonaj toohello usługi blob.  

W przypadku wdrażania rozwiązania podobne w swojej aplikacji, należy rozważyć sposób toomanage hello kompromis między niezawodności (zapisywanie co magazynu tooblob wpisu dziennika zdarza się to) i kosztów i skalowalności (buforowanie aktualizacji aplikacji i zapisywanie ich tooblob magazynu w partiach).  

#### <a name="issues-and-considerations"></a>Problemy i zagadnienia
Należy wziąć pod uwagę następujące punkty podczas podejmowania decyzji o sposobie toostore rejestrowanie danych hello:  

* Jeśli tworzysz projekt tabeli, pozwalający na uniknięcie potencjalnych gorących partycji, może się okazać, że nie masz dostępu do danych dziennika wydajnie.  
* dane dziennika tooprocess, klient często musi tooload wiele rekordów.  
* Mimo że często mają strukturę danych dziennika, magazynu obiektów blob może okazać się lepszym rozwiązaniem.  

### <a name="implementation-considerations"></a>Uwagi dotyczące implementacji
W tej sekcji omówiono niektóre toobear zagadnienia hello na uwadze podczas implementowania wzorce hello opisanych w poprzednich sekcjach hello. Większość ta sekcja używa przykładów napisane w języku C#, które używają hello biblioteki klienta usługi Storage (wersja 4.3.0 w czasie zapisywania hello).  

### <a name="retrieving-entities"></a>Pobieranie jednostki
Zgodnie z opisem w sekcji hello [projektowania zapytań](#design-for-querying), hello najbardziej efektywny zapytanie jest zapytaniem punktu. Jednak w niektórych scenariuszach może być konieczne tooretrieve wiele jednostek. W tej sekcji opisano niektóre typowe jednostki tooretrieving podejścia przy użyciu hello biblioteki klienta usługi Storage.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Wykonywanie zapytania punktu, przy użyciu hello biblioteki klienta usługi Storage
Hello najprostszy sposób tooexecute zapytania punkt jest toouse hello **pobrać** tabeli operacji, jak pokazano w hello następującego fragmentu kodu w języku C#, który pobiera obiekt o **PartitionKey** wartość "sprzedaż" i  **RowKey** wartości "212":  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Zwróć uwagę, jak w tym przykładzie oczekuje hello jednostek pobiera ona toobe typu **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Trwa pobieranie wiele jednostek za pomocą LINQ
Możesz pobrać wiele jednostek za pomocą LINQ z biblioteki klienta usługi Storage i określenie zapytania z **gdzie** klauzuli. tooavoid skanowania tabeli, należy zawsze pamiętać hello **PartitionKey** wartość hello gdzie klauzuli i jeśli jest to możliwe hello **RowKey** wartość tooavoid skanowania tabeli i partycji. Witaj tabeli usługa obsługuje ograniczony zestaw toouse operatory porównania (większe, większa niż lub równy mniej niż mniej niż lub równy takie same i nie równa) w hello gdzie klauzuli. Witaj poniższy fragment kodu C# znajduje wszystkich pracowników hello których ostatnia nazwa rozpoczyna się od znaku "B" (przy założeniu, że hello **RowKey** magazynów hello nazwisko) działu sprzedaży hello (przy założeniu hello **PartitionKey** przechowuje nazwę działu hello):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Zwróć uwagę, jak hello zapytania określa **RowKey** i **PartitionKey** tooensure lepszą wydajność.  

Witaj Poniższy przykładowy kod przedstawia równoważne funkcje przy użyciu interfejsu API fluent hello (Aby uzyskać więcej informacji o interfejsach API fluent ogólnie rzecz biorąc, zobacz [najlepsze rozwiązania dotyczące projektowania Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> Witaj próbki zagnieżdżony wielu **CombineFilters** tooinclude metody hello trzy warunki filtru.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Pobieranie dużą liczbą jednostek w wyniku zapytania
Optymalne zapytanie zwraca pojedynczą jednostkę na podstawie **PartitionKey** wartość i **RowKey** wartości. Jednak w niektórych scenariuszach może być tooreturn wymaganie wiele jednostek z hello tej samej partycji lub nawet z wielu partycji.  

Należy zawsze pełni przetestować wydajność aplikacji hello w takich scenariuszach.  

Zapytanie usługi tabel hello może zwrócić maksymalnie 1000 jednostek w tym samym czasie i mogą realizować maksymalnie pięć sekund. Jeśli hello zestaw wyników zawiera więcej niż 1000 jednostek, jeśli zapytanie hello nie została ukończona w ciągu pięciu sekund lub jeśli zapytanie hello przecina granicę partycji hello, zwraca hello usługi tabel tooenable token kontynuacji hello powitania toorequest aplikacji klienta Następny zestaw jednostek. Aby uzyskać więcej informacji dotyczących sposobu kontynuacji tokeny pracy, zobacz [limit czasu zapytania i podział na strony](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Jeśli używasz hello biblioteki klienta usługi Storage on automatycznie obsługi tokenów kontynuacji dla Ciebie zgodnie z hello usługi tabel zwraca jednostek. Hello następujące C# przykładowy kod automatycznie przy użyciu hello biblioteki klienta usługi Storage obsługuje tokenów kontynuacji Jeśli usługa tabel hello zwraca je w odpowiedzi:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Witaj następującego kodu C# obsługuje tokenów kontynuacji jawnie:  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

Za pomocą tokenów kontynuacji jawnie, można kontrolować, gdy aplikacja pobiera hello następnego segmentu danych. Na przykład jeśli aplikacja kliencka umożliwia toopage użytkowników za pomocą jednostek hello przechowywane w tabeli, użytkownik może zadecydować nie toopage za pośrednictwem wszystkich jednostek hello pobierane przez zapytanie hello, aplikacja będzie używane tylko hello token tooretrieve kontynuacji dalej segment po hello użytkownik miał stronicowania przez wszystkie jednostki hello w bieżącym segmencie hello. Takie podejście ma wiele zalet:  

* Umożliwia toolimit hello ilości danych tooretrieve z hello usługi tabel i przenieść hello sieci.  
* Dzięki temu można tooperform asynchroniczne We/Wy w .NET.  
* Umożliwia magazynu token toopersistent kontynuacji hello tooserialize tak w przypadku awarii aplikacji hello można kontynuować.  

> [!NOTE]
> Token kontynuacji zwykle zwraca segment zawierający 1000 jednostek, chociaż może być mniej. Dotyczy to również hello Ogranicz hello liczbę wpisów zapytanie zwraca przy użyciu **zająć** tooreturn hello pierwsze n jednostek spełniających kryteria wyszukiwania: Usługa tabel hello może zwrócić segment zawierający mniej niż n jednostek wzdłuż z tooenable token kontynuacji możesz tooretrieve hello pozostałych jednostek.  
> 
> 

Witaj następujące C# kod przedstawia sposób toomodify hello liczbę jednostek zwrotu wewnątrz segment:  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Projekcja po stronie serwera
Pojedyncza jednostka ma właściwości too255 i być too1 MB rozmiar. Gdy zapytania tabeli hello i pobrać jednostek, mogą nie być potrzebne wszystkie właściwości hello i uniknąć niepotrzebnego przesyłania danych (toohelp zmniejszenia opóźnienia i kosztów). Można użyć właściwości hello tylko tootransfer projekcji po stronie serwera, które należy. Hello poniższym przykładzie jest po prostu hello pobiera **E-mail** właściwości (wraz z **PartitionKey**, **RowKey**, **sygnatury czasowej**i  **Element ETag**) z wybranych przez zapytanie hello encji hello.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Zwróć uwagę, jak hello **RowKey** wartość jest dostępna, mimo że nie został uwzględniony w hello lista tooretrieve właściwości.  

### <a name="modifying-entities"></a>Modyfikowanie jednostek
Witaj biblioteki klienta usługi Storage umożliwia toomodify jednostek przechowywany w usłudze tabeli hello przez wstawianie, usuwanie i aktualizowanie jednostek. EGTs toobatch można użyć wielu insert, update i operacji usuwania razem tooreduce hello liczby rund wymagane i zwiększyć wydajność hello rozwiązania.  

Zwróć uwagę, że wyjątki zgłaszane, gdy hello biblioteki klienta usługi Storage wykonuje EGT zwykle obejmuje indeksu hello hello jednostki, który spowodował hello toofail partii. Jest to przydatne podczas debugowania kodu korzystającego z EGTs.  

Należy również rozważyć, jak projektu wpływa na sposób obsługi przez aplikację kliencką operacje współbieżności i aktualizacji.  

#### <a name="managing-concurrency"></a>Zarządzanie współbieżności
Domyślnie usługa tabel hello implementuje optymistycznej współbieżności testy na poziomie hello poszczególnych jednostek dla **Wstaw**, **scalania**, i **usunąć** operacje, Chociaż można dla hello tooforce klienta tabeli toobypass usługi kontrole. Aby uzyskać więcej informacji o zarządzaniu współbieżności hello usługi tabel, zobacz [Zarządzanie współbieżność w magazynie platformy Microsoft Azure](../storage/common/storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Scalanie lub Zastąp
Witaj **Zastąp** metody hello **TableOperation** klasy zastąpi całą jednostkę hello w hello usługi tabel. Jeśli nie zostanie uwzględniony właściwości w żądaniu hello, gdy istnieje tej właściwości w obiekcie hello przechowywane, Żądanie hello Usuwa właściwość z hello przechowywanie jednostki. Chyba że chcesz tooremove właściwości jawnie z przechowywanych jednostki musi zawierać dla każdej właściwości w żądaniu hello.  

Można użyć hello **scalania** metody hello **TableOperation** klasy tooreduce hello ilość danych wysłanie usługi tabel toohello należy tooupdate jednostki. Witaj **scalania** metoda zastępuje wszystkie właściwości w obiekcie hello przechowywane wartości właściwości z obiektu hello zawarte w żądaniu hello, ale pozostawia nienaruszone wszystkie właściwości w hello przechowywane jednostki, które nie są uwzględnione w żądaniu hello. Jest to przydatne, jeśli masz dużych jednostek i wymagane jest tylko tooupdate niewielkiej liczby właściwości w żądaniu.  

> [!NOTE]
> Witaj **Zastąp** i **scalania** metody zawiodą, jeśli hello jednostka nie istnieje. Alternatywnie, można użyć hello **InsertOrReplace** i **InsertOrMerge** metod, które Utwórz nową jednostkę, jeśli nie istnieje.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Praca z typami jednostek heterogenicznych
Witaj usługi tabel jest *bez schematu* sklepu tabeli, która oznacza, że pojedynczej tabeli można przechowywać jednostek wiele typów, zapewniając elastyczność w projekcie. Witaj poniższy przykład przedstawia przechowywania zarówno pracowników i działu jednostek tabeli:  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Znacznik czasu</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Należy pamiętać, że każdy obiekt muszą mieć **PartitionKey**, **RowKey**, i **sygnatury czasowej** wartości, którzy mogą mieć dowolny zbiór właściwości. Ponadto nie ma nic tooindicate hello typu jednostki, chyba że zostanie toostore te informacje innym. Dostępne są dwie opcje do identyfikacji typu jednostki hello:  

* Dołączenie wartości hello jednostki typu toohello **RowKey** (lub prawdopodobnie hello **PartitionKey**). Na przykład **EMPLOYEE_000123** lub **DEPARTMENT_SALES** jako **RowKey** wartości.  
* Użyj oddzielnych toorecord hello jednostki typu właściwości zgodnie z poniższą tabelą hello.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Znacznik czasu</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Dla obiektu</th>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>Pracownika</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Dla obiektu</th>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>Pracownika</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Dla obiektu</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Dział</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>Dla obiektu</th>
<th>Imię</th>
<th>Nazwisko</th>
<th>Wiek</th>
<th>Adres e-mail</th>
</tr>
<tr>
<td>Pracownika</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Pierwsza opcja Hello, dołączanie hello jednostki typu toohello **RowKey**, jest przydatne, jeśli istnieje możliwość, że dwie jednostki z różnymi typami może być hello sama wartość klucza. Grup jednostek z tego samego typu razem partycji hello hello.  

Witaj techniki opisane w tej sekcji są szczególnie istotne toohello dyskusji [relacji dziedziczenia](#inheritance-relationships) wcześniej w tym przewodniku w sekcji hello [modelowania relacji](#modelling-relationships).  

> [!NOTE]
> Należy należy rozważyć umieszczenie numeru wersji w hello obiekty typu wartości tooenable klienta aplikacji tooevolve POCO obiektów i pracy z różnymi wersjami.  
> 
> 

Witaj pozostałej części tej sekcji opisano niektóre z funkcji hello w hello biblioteki klienta usługi Storage, które ułatwiają Praca z wieloma typami jednostek w hello takie same tabeli.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Trwa pobieranie typów jednostek heterogenicznych
Jeśli używasz hello biblioteki klienta usługi Storage, masz trzy opcje do pracy z wielu typów jednostek.  

Jeśli znasz hello typ jednostki hello przechowywane z określonym **RowKey** i **PartitionKey** wartości, a następnie można określić typ jednostki hello podczas pobierania jednostki hello, jak pokazano w przykładach hello dwoma poprzednimi który pobrać jednostki typu **EmployeeEntity**: [wykonywania zapytania punktu, przy użyciu hello biblioteki klienta usługi Storage](#executing-a-point-query-using-the-storage-client-library) i [pobierania wiele jednostek za pomocą LINQ](#retrieving-multiple-entities-using-linq).  

Druga opcja Hello jest toouse hello **DynamicTableEntity** typu (zbiór właściwości), zamiast do konkretnego typu jednostki POCO (Ta opcja również może zwiększyć wydajność, ponieważ nie istnieje żadne tooserialize potrzeby i zbyt deserializacji hello jednostki. Typy sieci). Witaj potencjalnie następującego kodu C# pobiera wielu jednostek o różnych typach z hello tabeli, ale zwraca wszystkie jednostki jako **DynamicTableEntity** wystąpień. Następnie używa hello **EntityType** typ hello toodetermine właściwości każdej jednostki:  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Należy pamiętać, że tooretrieve inne właściwości, należy użyć hello **TryGetValue** metody na powitania **właściwości** właściwości hello **DynamicTableEntity** klasy.  

Trzecia opcja to toocombine przy użyciu hello **DynamicTableEntity** typu i **EntityResolver** wystąpienia. Dzięki temu możesz tooresolve toomultiple POCO typów w hello tego samego zapytania. W tym przykładzie hello **EntityResolver** delegata używa hello **EntityType** toodistinguish właściwości między hello dwa typy jednostek, które hello zapytanie zwraca. Hello **rozwiązać** metoda używa hello **rozpoznawania** delegować tooresolve **DynamicTableEntity** wystąpienia zbyt**TableEntity** wystąpień.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modyfikowanie jednostek heterogenicznych typów
Nie trzeba tooknow typu hello toodelete jednostki go i zawsze o jego wstawieniem hello typu jednostki. Można jednak użyć **DynamicTableEntity** wpisz tooupdate jednostki bez uprzedniego uzyskania informacji o jego typ, a także bez korzystania z klasą jednostki POCO. Witaj Poniższy przykładowy kod pobiera pojedynczej jednostki i sprawdza hello **EmployeeCount** istnieje właściwość przed zaktualizowaniem go.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Kontrolowanie dostępu przy użyciu sygnatury dostępu współdzielonego
Można użyć dostępu sygnatury dostępu Współdzielonego tokenów tooenable klienta aplikacji toomodify (i zapytania) jednostek tabeli bezpośrednio, bez tooauthenticate potrzeby hello bezpośrednio z usługi tabel hello. Zazwyczaj są trzy podstawowe zalety toousing SAS w aplikacji:  

* Nie trzeba toodistribute magazynu konta klucza tooan niezabezpieczonych platformy (np. urządzenie przenośne) w kolejności tooallow tooaccess tego urządzenia i zmodyfikować jednostki w hello usługi tabel.  
* Można odciążyć część hello tę sieć web i roli proces roboczy wykonywać w zarządzaniu urządzeniami tooclient jednostek takich jak komputery użytkowników końcowych i urządzeń przenośnych.  
* Można przypisać ograniczone i czas ograniczony zestaw uprawnień tooa klienta (na przykład zezwalania na dostęp tylko do odczytu zasobów toospecific).  

Aby uzyskać więcej informacji o korzystaniu z tokeny sygnatury dostępu Współdzielonego z hello usługi tabel, zobacz [przy użyciu dostępu sygnatur dostępu Współdzielonego](../storage/common/storage-dotnet-shared-access-signature-part-1.md).  

Jednak nadal należy wygenerować tokeny sygnatury dostępu Współdzielonego hello określającymi udzielenie klienta jednostek toohello aplikacji w usłudze tabel hello: należy to zrobić w środowisku, w którym ma bezpieczny dostęp do kluczy konta magazynu tooyour. Zazwyczaj używana w sieci web lub procesu roboczego roli toogenerate hello SAS tokeny i dostarczania ich toohello aplikacji klienckich, które wymagają dostępu tooyour jednostek. Ponieważ jest nadal koszty związane z generowania i dostarczanie tooclients tokeny sygnatury dostępu Współdzielonego, należy rozważyć tooreduce najlepszego ten narzut, szczególnie w sytuacjach dużego.  

Jest możliwe toogenerate tokenu sygnatury dostępu Współdzielonego, że przyznaje dostęp do podzbioru tooa hello jednostek w tabeli. Domyślnie, możesz utworzyć token sygnatury dostępu Współdzielonego dla całej tabeli, ale jest również możliwe toospecify tego hello SAS grant tokenu dostępu tooeither zakres **PartitionKey** wartości lub zakres **PartitionKey** i  **RowKey** wartości. Możesz wybrać toogenerate tokeny sygnatury dostępu Współdzielonego dla poszczególnych użytkowników systemu tak, aby każdy użytkownik tokenu sygnatury dostępu Współdzielonego tylko umożliwia im dostęp do własnych jednostek hello tootheir usługa tabel.  

### <a name="asynchronous-and-parallel-operations"></a>Operacje asynchroniczne i równoległych
Pod warunkiem rozpraszania swoje żądania między wieloma partycjami można zwiększyć elastyczność przepływności i klienta przy użyciu asynchronicznej lub równoległego zapytań.
Na przykład może być wystąpień roli dwóch lub więcej procesów roboczych podczas uzyskiwania dostępu do tabel równolegle. Może istnieć role poszczególnych pracowników odpowiedzialnych za poszczególne zbiory partycji lub po prostu ma wiele wystąpień roli procesu roboczego, w każdym stanie tooaccess hello wszystkie partycje w tabeli.  

W wystąpieniu klienta może zwiększyć przepływność, wykonując operacje magazynu asynchronicznie. Hello biblioteki klienta usługi Storage umożliwia łatwe toowrite asynchronicznych zapytań i zmiany. Na przykład rozpoczynać hello metoda synchroniczna pobiera wszystkie hello jednostek w partycji, jak pokazano w hello następującego kodu C#:  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Można łatwo zmodyfikować ten kod, aby zapytania hello uruchamia asynchronicznie w następujący sposób:  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

W tym przykładzie asynchroniczne można wyświetlić hello poniższe zmiany wersji synchroniczne hello:  

* Podpis metody Hello zawiera teraz hello **async** modyfikator i zwraca **zadań** wystąpienia.  
* Zamiast wywoływania hello **ExecuteSegmented** wyników tooretrieve metod, hello metody teraz wywołania hello **ExecuteSegmentedAsync** — metoda i używa hello **await** modyfikator tooretrieve powoduje asynchronicznie.  

Aplikacja kliencka Hello tę metodę mogą wywoływać wielokrotnie (o różnych wartościach dla hello **działu** parametru), i każda kwerenda zostanie uruchomiona w oddzielnym wątku.  

Należy pamiętać, że nie ma asynchronicznych wersji hello **Execute** metoda hello **TableQuery** klasy, ponieważ hello **IEnumerable** interfejs nie obsługuje asynchroniczne wyliczenie.  

Można również wstawiania, aktualizacji i usuwania jednostek asynchronicznie. Hello poniższy przykład C# pokazuje tooinsert prostą, synchroniczne metodę lub zastępowanie jednostki pracowników:  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Można łatwo zmodyfikować ten kod, dzięki czemu aktualizację hello uruchamia asynchronicznie w następujący sposób:  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

W tym przykładzie asynchroniczne można wyświetlić hello poniższe zmiany wersji synchroniczne hello:  

* Podpis metody Hello zawiera teraz hello **async** modyfikator i zwraca **zadań** wystąpienia.  
* Zamiast wywoływania hello **Execute** metody tooupdate hello jednostki, hello metody teraz wywołania hello **ExecuteAsync** — metoda i używa hello **await** tooretrieve modyfikator powoduje asynchronicznie.  

powitania klienta aplikacji można wywołać wiele metod asynchronicznych, takich jak ta, a każde wywołanie metody zostanie uruchomiony w oddzielnym wątku.  

### <a name="credits"></a>Środki na korzystanie z
Chcielibyśmy hello toothank następujących członków hello Azure zespołu dla ich wkład: Dominic Betts, Jason Hogg, Jean Ghanem, Haridas WSiSW, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah i Serdar Ozler jak również Hollander Tomasz z DX firmy Microsoft. 

Również chcielibyśmy hello toothank czynności Microsoft MVP ich opinie przydatna podczas cykli Przegląd: Igor Papirov i Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

