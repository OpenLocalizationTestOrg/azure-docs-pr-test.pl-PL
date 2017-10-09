---
title: 'Wyniki analizy strumienia: opcje magazynu, analizy | Dokumentacja firmy Microsoft'
description: "Informacje o przeznaczonych dla opcji dane wyjściowe analiza strumienia danych w tym usługi Power BI dla wyników analizy."
keywords: "przekształcenia danych, wyniki analizy, opcje magazynu danych"
services: stream-analytics,documentdb,sql-database,event-hubs,service-bus,storage
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ba6697ac-e90f-4be3-bafd-5cfcf4bd8f1f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 99f8113f0464960e898293397fbe3de90d669857
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-outputs-options-for-storage-analysis"></a>Wyniki analizy strumienia: opcje magazynu, analizy
Podczas tworzenia zadania usługi analiza strumienia, należy rozważyć, jak będą działały hello uzyskane dane. Jak będzie wyświetlania wyników hello hello zadania usługi analiza strumienia i będzie przechowywania go?

W kolejności tooenable różnych wzorców aplikacji usługi Azure Stream Analytics ma inne opcje do przechowywania danych wyjściowych i wyświetlania wyników analizy. To umożliwia łatwe tooview dane wyjściowe zadania i zapewnia elastyczność w hello konsumenckich i magazynu danych wyjściowych zadania hello magazynowania danych i innych celów. Żadnych danych wyjściowych konfigurowane w zadaniu hello musi istnieć przed uruchomiono zadanie hello i uruchomić zdarzeń przepływu. Na przykład jeśli używasz magazynu obiektów Blob jako dane wyjściowe zadania hello nie utworzy konta magazynu automatycznie. Musi on toobe utworzone przez użytkownika hello, przed rozpoczęciem powitalne ASA zadania.

## <a name="azure-data-lake-store"></a>Azure Data Lake Store
Strumienia Analytics obsługuje [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Ten magazyn umożliwia toostore danych dowolnego rozmiar, typ i wprowadzanie szybkość analiz operacyjnych i poznawczych. Ponadto analiza strumienia musi toobe uprawnień tooaccess hello Data Lake Store. Więcej informacji dotyczących autoryzacji i jak toosign dla hello usługi Data Lake Store (w razie potrzeby), omówiono w hello [usługi Data Lake output artykułu](stream-analytics-data-lake-output.md).

### <a name="authorize-an-azure-data-lake-store"></a>Autoryzowanie usługi Azure Data Lake Store
Po wybraniu usługi Data Lake Storage jako dane wyjściowe w hello portalu Azure będzie tooauthorize zostanie wyświetlony monit o połączenie tooan istniejącej usługi Data Lake Store.  

![Autoryzowanie usługi Data Lake Store](./media/stream-analytics-define-outputs/06-stream-analytics-define-outputs.png)  

Następnie wypełnij hello właściwości hello Data Lake Store danych wyjściowych, jak pokazano poniżej:

![Autoryzowanie usługi Data Lake Store](./media/stream-analytics-define-outputs/07-stream-analytics-define-outputs.png)  

Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opisy niezbędny do utworzenia wyjście usługi Data Lake Store.

<table>
<tbody>
<tr>
<td><B>NAZWA WŁAŚCIWOŚCI</B></td>
<td><B>OPIS ELEMENTU</B></td>
</tr>
<tr>
<td>Alias wyjściowy</td>
<td>Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis usługi Data Lake Store.</td>
</tr>
<tr>
<td>Nazwa konta</td>
<td>Nazwa Hello hello konta usługi Data Lake Storage, gdzie wysyłania danych wyjściowych. Zostaną wyświetlone z rozwijanej listy kont usługi Data Lake Store, do których użytkownik hello toowhich rejestrowane w portalu toohello ma dostęp do.</td>
</tr>
<tr>
<td>Wzorzec prefiksu ścieżki [<I>opcjonalne</I>]</td>
<td>Witaj toowrite użyta ścieżka pliku pliki w obrębie hello określić konta usługi Data Lake magazynu. <BR>{date} {time}<BR>Przykład 1: folder1/dzienniki / {date} / {time}<BR>Przykład 2: folder1/dzienniki / {date}</td>
</tr>
<tr>
<td>Data w formacie [<I>opcjonalne</I>]</td>
<td>Jeśli token daty hello jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane. Przykład: RRRR/MM/dd.</td>
</tr>
<tr>
<td>Format czasu [<I>opcjonalne</I>]</td>
<td>Jeśli token czasu hello jest używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane. Wartość hello tylko obsługiwane jest obecnie HH.</td>
</tr>
<tr>
<td>Format serializacji zdarzeń</td>
<td>Format serializacji w danych wyjściowych. JSON, CSV i Avro są obsługiwane.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Jeśli formatu CSV lub JSON, należy określić kodowania. Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.</td>
</tr>
<tr>
<td>Ogranicznik</td>
<td>Dotyczy tylko serializacji woluminów CSV. Analiza strumienia obsługuje różne ograniczniki dla serializacji danych CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek.</td>
</tr>
<tr>
<td>Format</td>
<td>Dotyczy tylko serializacji JSON. Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza. Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON.</td>
</tr>
</tbody>
</table>

### <a name="renew-data-lake-store-authorization"></a>Odnów autoryzacji usługi Data Lake Store
Konieczne będzie toore-uwierzytelniania konta usługi Data Lake Store, jeśli jego hasło uległ zmianie od czasu utworzenia lub ostatniej uwierzytelniony zadania.

![Autoryzowanie usługi Data Lake Store](./media/stream-analytics-define-outputs/08-stream-analytics-define-outputs.png)  

## <a name="sql-database"></a>SQL Database
[Baza danych SQL Azure](https://azure.microsoft.com/services/sql-database/) może służyć jako dane wyjściowe, w charakterze relacyjnym lub aplikacje zależne od hostowanych w relacyjnej bazie danych. Zadania usługi analiza strumienia zapisze tooan istniejącej tabeli w bazie danych SQL Azure.  Należy pamiętać, że schemat tabeli hello musi dokładnie odpowiadać hello pola i ich typy są dane wyjściowe z zadania. [Magazyn danych SQL Azure](https://azure.microsoft.com/documentation/services/sql-data-warehouse/) można również określić jako dane wyjściowe za pośrednictwem hello bazy danych SQL opcji output również (jest to funkcja w wersji zapoznawczej). Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opis tworzenie wyjścia bazy danych SQL.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w bazie danych zapytania toodirect hello zapytania dane wyjściowe toothis. |
| Database (Baza danych) |Nazwa Hello hello bazy danych, gdzie wysyłania danych wyjściowych |
| Nazwa serwera |Nazwa serwera bazy danych SQL Hello |
| Nazwa użytkownika |Witaj nazwy użytkownika, którego toohello toowrite dostępu do bazy danych |
| Hasło |Witaj hasło tooconnect toohello w bazie danych |
| Tabela |Nazwa tabeli Hello którym zostanie zapisany hello danych wyjściowych. Nazwa tabeli Hello jest uwzględniana wielkość liter i schematu hello tej tabeli powinien być zgodny dokładnie toohello liczba pól i ich typy generowane przez dane wyjściowe zadania. |

> [!NOTE]
> Obecnie oferty usługi Azure SQL Database hello jest obsługiwana dla danych wyjściowych zadania w Stream Analytics. Jednak maszyny wirtualnej platformy Azure, programem SQL Server z bazą danych dołączona nie jest obsługiwane. Jest to toochange podmiotu w przyszłych wersjach.
> 
> 

## <a name="blob-storage"></a>Blob Storage
Magazyn obiektów blob oferuje ekonomiczne i skalowalne rozwiązanie do przechowywania dużych ilości danych bez struktury w chmurze hello.  Aby obejrzeć wprowadzenie magazynu obiektów Blob platformy Azure i jego użycia, zobacz dokumentację hello w [jak obiekty BLOB toouse](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opis tworzenia wyjściowego obiektu blob.

<table>
<tbody>
<tr>
<td>NAZWA WŁAŚCIWOŚCI</td>
<td>OPIS</td>
</tr>
<tr>
<td>Alias wyjściowy</td>
<td>Jest to przyjazna nazwa używana w magazynie obiektów blob toothis zapytania toodirect hello zapytania danych wyjściowych.</td>
</tr>
<tr>
<td>Konto magazynu</td>
<td>Nazwa Hello hello konta magazynu, gdzie wysyłania danych wyjściowych.</td>
</tr>
<tr>
<td>Klucz konta magazynu</td>
<td>klucz tajny Hello skojarzone z kontem magazynu hello.</td>
</tr>
<tr>
<td>Kontener magazynu</td>
<td>Kontenery umożliwiają logiczne grupowanie dla obiektów blob przechowywanych w hello usługi obiektów Blob Microsoft Azure. Podczas przekazywania toohello obiektu blob usługi obiektów Blob, należy określić kontener dla tego obiektu blob.</td>
</tr>
<tr>
<td>Wzorzec prefiksu ścieżki [opcjonalnie]</td>
<td>Ścieżka pliku Hello używana toowrite obiektów blob w określonym kontenerze hello.<BR>W ścieżce hello można wybrać jeden lub więcej wystąpień powitania po 2 zmienne toospecify hello częstotliwość obiekty BLOB są zapisywane toouse:<BR>{date} {time}<BR>Przykład 1: Klaster1/dzienniki / {date} / {time}<BR>Przykład 2: Klaster1/dzienniki / {date}</td>
</tr>
<tr>
<td>Format daty [opcjonalnie]</td>
<td>Jeśli token daty hello jest używany w ścieżce prefiks hello, można wybrać format daty hello, w którym pliki są organizowane. Przykład: RRRR/MM/dd.</td>
</tr>
<tr>
<td>Format czasu [opcjonalnie]</td>
<td>Jeśli token czasu hello jest używany w ścieżce prefiks hello, określ hello format czasu, w którym pliki są organizowane. Wartość hello tylko obsługiwane jest obecnie HH.</td>
</tr>
<tr>
<td>Format serializacji zdarzeń</td>
<td>Format serializacji w danych wyjściowych.  JSON, CSV i Avro są obsługiwane.</td>
</tr>
<tr>
<td>Encoding</td>
<td>Jeśli formatu CSV lub JSON, należy określić kodowania. Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8.</td>
</tr>
<tr>
<td>Ogranicznik</td>
<td>Dotyczy tylko serializacji woluminów CSV. Analiza strumienia obsługuje różne ograniczniki dla serializacji danych CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek.</td>
</tr>
<tr>
<td>Format</td>
<td>Dotyczy tylko serializacji JSON. Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza. Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON. Ta tablica zostaną zamknięte, tylko gdy hello zadanie zostanie zatrzymane lub Stream Analytics została przeniesiona na toohello dalej przedział czasu. Ogólnie rzecz biorąc jest wiersza preferowane toouse rozdzielonych JSON, ponieważ nie wymaga żadnej specjalnej obsługi podczas hello plik wyjściowy jest nadal zapisywana.</td>
</tr>
</tbody>
</table>

## <a name="event-hub"></a>Centrum zdarzeń
[Centra zdarzeń](https://azure.microsoft.com/services/event-hubs/) jest wysoce skalowalna publikowania / subskrypcji systemem zbierania zdarzeń. Może on zbierać miliony zdarzeń na sekundę.  Użycie jednego Centrum zdarzeń jako danych wyjściowych jest w przypadku hello dane wyjściowe zadania Stream Analytics będzie wprowadzania hello innego zadania przesyłania strumieniowego.

Istnieje kilka parametrów, które są potrzebne tooconfigure strumieni danych w Centrum zdarzeń jako dane wyjściowe.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis Centrum zdarzeń. |
| Namespace magistrali usług |Przestrzeń nazw magistrali usług to kontener dla zestawu jednostek do obsługi komunikatów. Podczas tworzenia nowego Centrum zdarzeń, utworzono przestrzeni nazw usługi Service Bus |
| Centrum zdarzeń |Nazwa Hello danych wyjściowych Centrum zdarzeń |
| Nazwa zasad Centrum zdarzeń |Witaj zasad dostępu współdzielonego, które mogą być tworzone na karcie Konfigurowanie Centrum zdarzeń hello. Wszystkie zasady dostępu współdzielonego zostanie mają nazwy, możesz ustawić uprawnienia i klucze dostępu |
| Klucz zasad Centrum zdarzeń |klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług |
| Kolumna klucza partycji [opcjonalnie] |Ta kolumna zawiera hello klucza partycji dla danych wyjściowych Centrum zdarzeń. |
| Format serializacji zdarzeń |Format serializacji w danych wyjściowych.  JSON, CSV i Avro są obsługiwane. |
| Encoding |Dla woluminu CSV i JSON jest hello obsługiwany tylko format kodowania w tej chwili UTF-8 |
| Ogranicznik |Dotyczy tylko serializacji woluminów CSV. Usługa Stream Analytics obsługuje różne ograniczniki dla serializacji danych w formacie CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek. |
| Format |Dotyczy tylko typu JSON. Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza. Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON. |

## <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com/) może służyć jako dane wyjściowe tooprovide zadania Stream Analytics, środowisko sformatowanego wizualizacja wyników analizy. Ta możliwość może służyć do operacyjnej pulpity nawigacyjne, Generowanie raportu i metryki na zgłoszenie.

### <a name="authorize-a-power-bi-account"></a>Autoryzuj konto usługi Power BI
1. Po wybraniu usługi Power BI jako dane wyjściowe w hello portalu Azure będzie można zostanie wyświetlony monit o tooauthorize istniejącego Power BI użytkownika lub toocreate nowe konto usługi Power BI.  
   
   ![Autoryzowanie Power BI użytkownika](./media/stream-analytics-define-outputs/01-stream-analytics-define-outputs.png)  
2. Utwórz nowe konto, jeśli nie zostały jeszcze mieć jeden, kliknij przycisk Autoryzuj teraz.  Ekran, tak jak przedstawiono poniżej hello.  
   
   ![Usługa Power BI konto platformy Azure](./media/stream-analytics-define-outputs/02-stream-analytics-define-outputs.png)  
3. W tym kroku podaj pracy hello konta służbowego autoryzacji hello usługi Power BI w danych wyjściowych. Jeśli użytkownik nie jest już zarejestrowany na usługę Power BI, wybierz logowania teraz. Hello konta firmowego lub szkolnego, którego używasz usługi Power BI może się różnić od hello konta subskrypcji platformy Azure, które są obecnie zalogowani przy użyciu.

### <a name="configure-hello-power-bi-output-properties"></a>Skonfiguruj właściwości wyjście usługi Power BI hello
Po utworzeniu konta usługi Power BI hello uwierzytelniony, można skonfigurować właściwości powitania dla danych wyjściowych usługi Power BI. w poniższej tabeli Hello jest hello listę nazw właściwości i ich tooconfigure opis danych wyjściowych usługi Power BI.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w zapytania toodirect hello zapytania dane wyjściowe toothis wyjście usługi Power BI. |
| Obszaru roboczego grupy |tooenable udostępniania danych innym użytkownikom usługi Power BI możesz wybrać grupy wewnątrz usługi Power BI konta lub wybierz opcję "Mój obszar roboczy", jeśli nie chcesz, aby toowrite tooa grupy.  Aktualizowanie istniejącej grupy wymaga odnawianie hello uwierzytelniania usługi Power BI. |
| Nazwa zestawu danych |Podaj nazwę zestawu danych, że jest wymagane dla usługi Power BI hello output toouse |
| Nazwa tabeli |Podaj nazwę tabeli w obszarze hello zestawu danych powitalne output usługi Power BI. Obecnie usługa Power BI dane wyjściowe zadania usługi analiza strumienia może mieć tylko jedną tabelę w zestawie danych |

Przewodnik konfigurowania usługi Power BI w danych wyjściowych i pulpitu nawigacyjnego, zobacz hello [Azure Stream Analytics & usługi Power BI](stream-analytics-power-bi-dashboard.md) artykułu.

> [!NOTE]
> Nie należy jawnie tworzyć hello zestawu danych i tabeli w pulpit nawigacyjny usługi Power BI hello. Witaj zestawu danych i tabeli zostaną wypełnione automatycznie gdy uruchomiono zadanie hello i hello zadanie uruchamia pompującego dane wyjściowe do usługi Power BI. Należy pamiętać, że jeśli zapytanie dotyczące zadań hello nie generuje żadnych wyników, hello zestawu danych i nie można utworzyć tabeli. Wziąć pod uwagę, że jeśli usługi Power BI już zestaw danych i tabeli z hello samą nazwę jak hello ono określone w tym zadaniu Stream Analytics, hello istniejące dane zostaną zastąpione.
> 
> 

### <a name="schema-creation"></a>Tworzenie schematu
Usługa Azure Stream Analytics tworzy zestaw danych usługi Power BI i tabeli w imieniu użytkownika hello, jeśli już nie istnieje. We wszystkich innych przypadkach Tabela hello jest aktualizowana nowymi wartościami. Obecnie istnieje ograniczenie hello tylko jednej tabeli może istnieć w elemencie dataset.

### <a name="data-type-conversion-from-asa-toopower-bi"></a>Konwersja z ASA tooPower BI typu danych
Usługa Azure Stream Analytics aktualizacji modelu danych hello dynamicznie w czasie wykonywania, jeśli hello produkt wyjściowy zmiany schematu. Zmiany nazwy kolumny, zmian typu kolumny, a hello Dodawanie lub usuwanie kolumn są wszystkie śledzone.

W tej tabeli podano hello konwersje typów danych z [typy danych Stream Analytics](https://msdn.microsoft.com/library/azure/dn835065.aspx) tooPower BIs [typy modelu danych jednostki (EDM)](https://powerbi.microsoft.com/documentation/powerbi-developer-walkthrough-push-data/) do usługi POWER BI zestawu danych i tabeli nie istnieją.


Z usługi Stream Analytics | tooPower analizy Biznesowej
-----|-----|------------
bigint | Int64
nvarchar(max) | Ciąg
Data i godzina | Data i godzina
Float | O podwójnej precyzji
Tablica rekordu | Ciąg typu, wartości stałej "IRecord" lub "IArray"

### <a name="schema-update"></a>Aktualizacja schematu
Analiza strumienia wnioskuje schemat modelu danych hello na podstawie pierwszego zestawu hello zdarzeń w danych wyjściowych hello. Później w razie potrzeby schematu modelu danych hello jest tooaccommodate zaktualizowane zdarzeń przychodzących, które mogą nie pasować do oryginalnego schematu hello.

Witaj `SELECT *` zapytania należy unikać tooprevent aktualizacja dynamiczna schematu w wierszach. Ponadto toopotential wpływ na wydajność, może także powodować indeterminacy hello czas poświęcony na powitania wyników. należy wybrać Hello dokładnie pola wymagające toobe wyświetlane na pulpicie nawigacyjnym usługi Power BI. Ponadto hello wartości danych powinny być zgodne z hello wybrany typ danych.


Poprzednie/bieżącym | Int64 | Ciąg | Data i godzina | O podwójnej precyzji
-----------------|-------|--------|----------|-------
Int64 | Int64 | Ciąg | Ciąg | O podwójnej precyzji
O podwójnej precyzji | O podwójnej precyzji | Ciąg | Ciąg | O podwójnej precyzji
Ciąg | Ciąg | Ciąg | Ciąg |  | Ciąg | 
Data i godzina | Ciąg | Ciąg |  Data i godzina | Ciąg


### <a name="renew-power-bi-authorization"></a>Odnów Power BI autoryzacji
Konieczne będzie toore-uwierzytelniania konta usługi Power BI, jeśli jego hasło uległ zmianie od czasu utworzenia lub ostatniej uwierzytelniony zadania. Jeśli uwierzytelnianie wieloskładnikowe (MFA) jest skonfigurowany w dzierżawie usługi Azure Active Directory (AAD) również należy autoryzacji usługi Power BI toorenew co 2 tygodnie. Objawem tego problemu jest Brak danych wyjściowych zadania i "uwierzytelnić użytkownika błędu" w dzienniki operacji hello:

  ![Błąd tokenu odświeżania Power BI](./media/stream-analytics-define-outputs/03-stream-analytics-define-outputs.png)  

tooresolve ten problem, Zatrzymaj uruchomione zadanie, przejdź tooyour usługi Power BI w danych wyjściowych.  Kliknij łącze "Odnawiania autoryzacji" hello, a następnie uruchom ponownie zadanie z hello utraty danych tooavoid czas ostatniego zatrzymania.

  ![Usługa Power BI odnowić autoryzacji](./media/stream-analytics-define-outputs/04-stream-analytics-define-outputs.png)  

## <a name="table-storage"></a>Table Storage
[Magazyn tabel Azure](../storage/common/storage-introduction.md) oferuje magazynu wysokiej dostępności, skalowalna na ogromną skalę, dzięki czemu aplikacja może automatycznie skalować toomeet żądanie użytkownika. Magazyn tabel jest magazynem kluczy/atrybutów NoSQL firmy Microsoft które z nich mogą korzystać z danych strukturalnych z mniej ograniczeń hello schematu. Magazyn tabel Azure mogą być używane toostore danych potrzeby trwałości i efektywnego odzyskiwania.

Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opis tworzenia tabeli danych wyjściowych.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w magazynie tabel toothis zapytania toodirect hello zapytania danych wyjściowych. |
| Konto magazynu |Nazwa Hello hello konta magazynu, gdzie wysyłania danych wyjściowych. |
| Klucz konta magazynu |klucz dostępu Hello skojarzone z kontem magazynu hello. |
| Nazwa tabeli |Nazwa Hello hello tabeli. Jeśli nie istnieje tabela Hello zostaną utworzone. |
| Klucz partycji |Nazwa Hello hello dane wyjściowe kolumny zawierające hello klucza partycji. Witaj klucz partycji to unikatowy identyfikator dla hello partycji w danej tabeli, który wchodzi w skład pierwszej części klucza podstawowego jednostki hello. Jest wartość ciągu, która może być aktywne rozmiarze too1 KB. |
| Klucz wiersza |Nazwa Hello hello dane wyjściowe kolumny zawierające hello klucz wiersza. Witaj, klucz wiersza to unikatowy identyfikator jednostki w danej partycji. Wchodzi w skład hello drugiej części klucza podstawowego jednostki. klucz wiersza Hello jest wartość ciągu, która może być aktywne rozmiarze too1 KB. |
| Rozmiar partii |Witaj liczbę rekordów dla operacji zbiorczej. Zazwyczaj domyślne hello jest wystarczająca dla większości zadań, zobacz toohello [specyfikacji operacji zbiorczej tabeli](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx) Aby uzyskać więcej informacji na temat modyfikowania to ustawienie. |

## <a name="service-bus-queues"></a>Kolejki usługi Service Bus
[Kolejek usługi Service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) oferują pierwszy na wejściu — tooone dostarczania komunikatów pierwszy na wyjściu (FIFO) lub więcej konkurujących konsumentów. Zazwyczaj wiadomości są oczekiwane toobe odbierane i przetwarzane przez odbiorców hello w kolejności danych czasowych hello, w którym zostały one dodane toohello kolejki, a każdy komunikat jest odbierany i przetwarzany przez tylko jednego odbiorcę komunikatów.

Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opis tworzenia kolejki dane wyjściowe.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w zapytaniach toodirect hello zapytania dane wyjściowe toothis kolejką usługi Service Bus. |
| Namespace magistrali usług |Przestrzeń nazw magistrali usług to kontener dla zestawu jednostek do obsługi komunikatów. |
| Nazwa kolejki |Nazwa Hello hello kolejką usługi Service Bus. |
| Nazwa zasad kolejki |Podczas tworzenia kolejki można też utworzyć zasady dostępu współużytkowanego na karcie Konfigurowanie kolejki hello. Wszystkie zasady dostępu współużytkowanego mają nazwy, uprawnienia, które można ustawić, a klucze dostępu. |
| Klucz zasad kolejki |klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług |
| Format serializacji zdarzeń |Format serializacji w danych wyjściowych.  JSON, CSV i Avro są obsługiwane. |
| Encoding |Dla woluminu CSV i JSON jest hello obsługiwany tylko format kodowania w tej chwili UTF-8 |
| Ogranicznik |Dotyczy tylko serializacji woluminów CSV. Usługa Stream Analytics obsługuje różne ograniczniki dla serializacji danych w formacie CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek. |
| Format |Dotyczy tylko typu JSON. Rozdzielone Określa, że hello dane wyjściowe będą formatowane przez poszczególne obiekty JSON rozdzielone znakiem nowego wiersza. Tablica Określa, że hello dane wyjściowe będą formatowane jako tablica obiektów JSON. |

## <a name="service-bus-topics"></a>Tematy dotyczące usługi Service Bus
Gdy kolejek usługi Service Bus zapewniają jedną metodę komunikacji tooone z tooreceiver nadawcy [tematów usługi Service Bus](https://msdn.microsoft.com/library/azure/hh367516.aspx) Podaj jeden do wielu formę komunikacji.

Witaj w poniższej tabeli wymieniono hello nazw właściwości i ich opis tworzenia tabeli danych wyjściowych.

| Nazwa właściwości | Opis |
| --- | --- |
| Alias wyjściowy |Jest to przyjazna nazwa używana w zapytania toodirect hello zapytania dane wyjściowe toothis tematów magistrali usługi. |
| Namespace magistrali usług |Przestrzeń nazw magistrali usług to kontener dla zestawu jednostek do obsługi komunikatów. Podczas tworzenia nowego Centrum zdarzeń, utworzono przestrzeni nazw usługi Service Bus |
| Nazwa tematu |Tematy to obsługi komunikatów, jednostek, podobne tooevent koncentratorów i kolejek. Są one przeznaczone toocollect strumieni zdarzeń z wielu różnych urządzeń i usług. Podczas tworzenia tematu podano również określonej nazwy. wysłane wiadomości powitania tooa tematu nie będą dostępne, chyba że subskrypcja jest tworzony, upewnij się, więc ma jedną lub więcej subskrypcji w temacie hello |
| Nazwa zasad tematu |Podczas tworzenia tematu można też utworzyć zasady dostępu współużytkowanego na karcie Konfigurowanie tematu hello. Wszystkie zasady dostępu współdzielonego zostanie mają nazwy, możesz ustawić uprawnienia i klucze dostępu |
| Klucz tematu zasad |klucz dostęp współdzielony Hello używany tooauthenticate dostępu toohello — przestrzeń nazw magistrali usług |
| Format serializacji zdarzeń |Format serializacji w danych wyjściowych.  JSON, CSV i Avro są obsługiwane. |
| Encoding |Jeśli formatu CSV lub JSON, należy określić kodowania. Witaj obsługiwany tylko format kodowania w tej chwili jest UTF-8 |
| Ogranicznik |Dotyczy tylko serializacji woluminów CSV. Usługa Stream Analytics obsługuje różne ograniczniki dla serializacji danych w formacie CSV. Obsługiwane wartości to przecinek, średnik, miejsca, karta i pionowy pasek. |

## <a name="azure-cosmos-db"></a>Azure Cosmos DB
[Azure DB rozwiązania Cosmos](https://azure.microsoft.com/services/documentdb/) jest pełni zarządzane NoSQL dokumentów bazy danych usługi, która oferuje zapytania i transakcji za pośrednictwem dane bez schematu i przewidywalnego i niezawodna wydajności oraz szybkie opracowywanie.

Witaj poniżej listy szczegóły hello nazwy i właściwości opisujący tworzenie wyjścia bazy danych Azure rozwiązania Cosmos.

* **Dane wyjściowe Alias** — toorefer alias output to zapytanie ASA  
* **Nazwa konta** — hello nazwę lub identyfikator URI hello konto bazy danych rozwiązania Cosmos punktu końcowego.  
* **Klucz konta** — Witaj udostępniony klucz dostępu dla hello konto bazy danych rozwiązania Cosmos.  
* **Baza danych** — Nazwa bazy danych DB rozwiązania Cosmos hello.  
* **Wzorzec nazwy kolekcji** — Nazwa kolekcji hello lub ich wzorzec toobe kolekcje hello używane. format nazwy Hello kolekcji można skonstruować przy użyciu hello tokenu opcjonalne {partition}, gdzie partycje zaczynają się od 0. Poniżej przedstawiono przykładowe prawidłowe wartości wejściowe:  
  1\) MyCollection — jedną kolekcję o nazwie "MyCollection" musi istnieć.  
  2\) MyCollection {partition} — takie kolekcje muszą istnieć — "MyCollection0", "MyCollection1", "MyCollection2" itd.  
* **Klucz partycji** — jest to opcjonalne. Jest to potrzebne tylko, jeśli używasz tokenu {partycjonowania} we wzorcu nazwy Twojej kolekcji. Nazwa Hello hello pola w danych wyjściowych zdarzenia używane toospecify hello klucza do partycjonowania danych wyjściowych na kolekcje. Dla danych wyjściowych jednej kolekcji, wszystkie kolumny wyjściowej dowolnego mogą być używane np. PartitionId.  
* **Identyfikator dokumentu** — jest to opcjonalne. Nazwa Hello hello pola w zdarzeniach wyjściowych używana hello klucz podstawowy toospecify, na które insert lub update bazują operacje.  


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
Już zostały wprowadzone tooStream Analytics — zarządzaną usługę służącą do analizy danych z Internetu rzeczy hello przesyłanych strumieniowo. toolearn więcej informacji na temat tej usługi, zobacz:

* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Link references-->
[stream.analytics.developer.guide]: ../stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
