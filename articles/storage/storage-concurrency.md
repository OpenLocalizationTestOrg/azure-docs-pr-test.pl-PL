---
title: "aaaManaging współbieżność w magazynie platformy Microsoft Azure"
description: "Jak toomanage concurrency hello usług obiektów Blob, kolejki, tabel i plików"
services: storage
documentationcenter: 
author: jasontang501
manager: tadb
editor: tysonn
ms.assetid: cc6429c4-23ee-46e3-b22d-50dd68bd4680
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: jasontang501
ms.openlocfilehash: 277fbbb880906da6be67b2267ed5c8e457455bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-concurrency-in-microsoft-azure-storage"></a>Zarządzanie współbieżnością w usłudze Microsoft Azure Storage
## <a name="overview"></a>Omówienie
Nowoczesne aplikacje internetowe, na podstawie zwykle mają wielu użytkowników, wyświetlanie i aktualizowanie danych jednocześnie. Wymaga to toothink deweloperzy aplikacji dokładnie o jak tooprovide a przewidywalną wystąpić tootheir użytkowników końcowych, szczególnie w przypadku scenariuszy, w którym można aktualizować wielu użytkowników hello same dane. Istnieją trzy Strategie współbieżności danych głównych, którą deweloperzy będą zwykle należy wziąć pod uwagę:  

1. Optymistycznej współbieżności — aplikacji wykonywanie aktualizacji w ramach jego aktualizacji sprawdzi, czy hello danych zmienił się od aplikacji hello ostatniego odczytu danych. Na przykład jeśli dwóch użytkowników wyświetlania strony typu wiki toohello aktualizacji same strony, a następnie platformy wiki hello należy zapewnić, że aktualizacja drugi hello nie zastępuje pierwszą aktualizacją hello — i zarówno użytkownikom zrozumienie, czy ich aktualizacja zakończyła się powodzeniem. Ta strategia jest najczęściej używana w aplikacji sieci web.
2. Pesymistyczne współbieżności — wyszukiwanie tooperform aktualizacji aplikacji potrwa blokady obiektu uniemożliwia aktualizowanie hello danych do czasu zwolnienia blokady hello przez innych użytkowników. Na przykład w przypadku replikacji danych główny/podległy gdzie tylko wzorca hello wykona aktualizacje wzorca hello zwykle wstrzymuje wyłącznej blokady na dłuższy czas na powitania tooensure danych, nie inny użytkownik może ją aktualizować.
3. Ostatni składnik zapisywania usługi wins — metody, która umożliwia żadnych tooproceed operacje aktualizacji bez sprawdzenia, jeśli inna aplikacja ma zaktualizowane dane powitania od aplikacji hello najpierw odczytu hello danych. Tej strategii (lub brak posiadanie strategii) jest zwykle używany gdzie danych jest podzielona na partycje w taki sposób, że nie istnieje prawdopodobieństwo czy użytkownicy będą uzyskiwać dostęp do hello tych samych danych. Może również być przydatne przetransferowane przetwarzania strumieni danych w krótkim okresie.  

Ten artykuł zawiera omówienie sposobu hello Azure Storage platformy upraszcza tworzenie, zapewniając obsługę pierwszej klasie wszystkie trzy Strategie współbieżności.  

## <a name="azure-storage--simplifies-cloud-development"></a>Usługa Azure Storage — upraszcza tworzenie chmury
Witaj usługą magazynu platformy Azure obsługuje wszystkie trzy strategie, chociaż jest charakterystyczny w jego możliwości tooprovide pełną obsługę optymistycznej i pesymistyczne współbieżności, ponieważ została zaprojektowana tooembrace wysoki poziom spójności modelu, który gwarantuje, że w przypadku Witaj zatwierdzeń usługi Magazyn danych wstawić lub zaktualizować operacji wszystkie dalsze dane toothat uzyskuje dostęp do zobaczą hello najnowszych aktualizacji. Platformy magazynu, które używają modelu spójność ostateczna mają opóźnienie między podczas zapisu jest wykonywane przez jednego użytkownika i po zaktualizowaniu hello dane są widoczne dla innych użytkowników, w związku z tym komplikując rozwoju aplikacji klienckich w kolejności tooprevent niespójności z wpływu na użytkowników końcowych.  

Ponadto tooselecting deweloperzy strategii współbieżności odpowiednie należy wziąć pod uwagę sposób platforma magazynu izoluje zmian — szczególnie toohello zmiany sam obiekt w transakcji. Witaj usługą magazynu platformy Azure używa tooallow izolacji migawki operacje toohappen równocześnie z operacji zapisu w obrębie jednej partycji do odczytu. W przeciwieństwie do innych poziomach izolacji izolacji migawki gwarantuje, że wszystkie operacje odczytu Zobacz migawki spójne hello danych nawet wtedy, gdy aktualizacje są wykonywane — zasadniczo zwracając hello ostatnie wartości przekazane podczas przetwarzania transakcji aktualizacji.  

## <a name="managing-concurrency-in-blob-storage"></a>Zarządzanie współbieżność w magazynie obiektów Blob
Można włączyć toouse współbieżności optymistycznej lub pesymistyczne modele toomanage tooblobs dostępu, a usługa blob hello kontenerów w. Jeśli nie zostanie jawnie strategii ostatnio zapisuje usługi wins jest domyślnym hello.  

### <a name="optimistic-concurrency-for-blobs-and-containers"></a>Optymistycznej współbieżności dla obiektów blob i kontenerów
Witaj usługi magazynu przypisuje identyfikator obiektu tooevery przechowywane. Ten identyfikator jest aktualizowana każdorazowo operacji aktualizacji jest wykonywana na obiekt. Identyfikator Hello jest zwracana toohello klienta jako część przy użyciu hello nagłówka ETag (tag jednostki), który jest zdefiniowany w ramach protokołu hello HTTP odpowiedzi HTTP GET. Wykonywanie użytkownika wysyłania aktualizacji na takiego obiektu w hello oryginalnego elementu ETag oraz tooensure nagłówek warunkowy, który aktualizacji tylko wówczas, gdy spełnione pewne warunki — w takim przypadku warunek hello jest nagłówek "If-Match", co wymaga hello magazynu Usługa wartość hello tooensure hello element ETag określony w żądaniu aktualizacji hello jest hello taki sam jak przechowywany w hello usługi magazynu.  

zarys Hello tego procesu jest następujący:  

1. Pobieranie obiektu blob z usługi magazynowania hello, odpowiedź hello zawiera wartość nagłówka ETag HTTP, która identyfikuje hello bieżąca wersja obiektu hello w usłudze magazynowania hello.
2. Podczas aktualizacji obiektu blob hello zawierają wartość ETag hello otrzymane w kroku 1 w hello **If-Match** nagłówek warunkowy hello żądania, Wyślij toohello usługi.
3. Witaj porównuje hello wartość ETag w żądaniu hello z bieżącej wartości ETag hello hello obiektu blob.
4. Jeśli hello bieżącej wartości ETag obiektu blob hello jest w innej wersji niż hello ETag w hello **If-Match** warunkowego nagłówka w żądaniu hello, usługa hello zwraca błąd 412 toohello klienta. To ustawienie określa klienta toohello inny proces zaktualizował obiektu blob hello ponieważ pobrany powitania klienta.
5. Jeśli bieżąca hello hello ETag wartość obiektu hello blob jest tej samej wersji co hello ETag w hello **If-Match** wykonuje warunkowego nagłówka w żądaniu hello, usługa hello hello żądanej operacji, a aktualizacje hello bieżącej wartości ETag obiektu hello blob tooshow jego utworzeniu nowej wersji.  

Witaj poniższy fragment C#, (za pomocą biblioteki klienta magazynu 4.2.0 hello) zawiera prosty przykład tego, jak tooconstruct **AccessCondition If-Match** oparte na powitania wartość ETag, który jest dostępny z właściwości obiektu blob, który był hello poprzednio pobrane albo wstawiony. Następnie używa hello **AccessCondition** obiektu podczas jej aktualizowania obiektów blob hello: hello **AccessCondition** obiekt dodaje hello **If-Match** nagłówka toohello żądania. Jeśli inny proces został zaktualizowany hello obiektów blob, usługa blob hello zwraca komunikat stanu HTTP 412 (warunek wstępny nie powiodła się.). Witaj pełny przykład można pobrać tutaj: [współbieżności zarządzania przy użyciu usługi Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).  

```csharp
// Retrieve hello ETag from hello newly created blob
// Etag is already populated as UploadText should cause a PUT Blob call
// toostorage blob service which returns hello etag in response.
string orignalETag = blockBlob.Properties.ETag;

// This code simulates an update by a third party.
string helloText = "Blob updated by a third party.";

// No etag, provided so orignal blob is overwritten (thus generating a new etag)
blockBlob.UploadText(helloText);
Console.WriteLine("Blob updated. Updated ETag = {0}",
blockBlob.Properties.ETag);

// Now try tooupdate hello blob using hello orignal ETag provided when hello blob was created
try
{
    Console.WriteLine("Trying tooupdate blob using orignal etag toogenerate if-match access condition");
    blockBlob.UploadText(helloText,accessCondition:
    AccessCondition.GenerateIfMatchCondition(orignalETag));
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
    {
        Console.WriteLine("Precondition failure as expected. Blob's orignal etag no longer matches");
        // TODO: client can decide on how it wants toohandle hello 3rd party updated content.
    }
    else
        throw;
}  
```

Hello usługi magazynu obejmuje również obsługę dodatkowych nagłówków warunkowego takich jak **If-Modified-Since**, **If-Unmodified-Since** i **If-None-Match** oraz ich kombinacji. Aby uzyskać więcej informacji, zobacz [określenie warunkowego nagłówki dla operacji usługi Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx) w witrynie MSDN.  

Witaj Poniższa tabela zawiera podsumowanie hello kontenera operacje warunkowe nagłówków accept takich jak **If-Match** w hello żądania, które zwracają wartość ETag w hello odpowiedzi.  

| Operacja | Zwraca wartość ETag kontenera | Akceptuje warunkowego nagłówki |
|:--- |:--- |:--- |
| Tworzenie kontenera |Tak |Nie |
| Pobierz właściwości kontenera |Tak |Nie |
| Pobranie metadanych kontenera |Tak |Nie |
| Ustaw metadanych kontenera |Tak |Tak |
| Pobierz ACL kontenera |Tak |Nie |
| Ustaw ACL kontenera |Tak |Tak (*) |
| Usunąć kontenera |Nie |Tak |
| Kontener dzierżawy |Tak |Tak |
| Lista obiektów blob |Nie |Nie |

(*) uprawnienia hello zdefiniowane przez SetContainerACL znajdują się w pamięci podręcznej i uprawnienia toothese aktualizacje potrwać 30 sekund, które toopropagate w tym okresie aktualizacje nie są gwarantowane toobe spójne.  

Witaj Poniższa tabela zawiera podsumowanie hello operacji obiektu blob, które warunkowego nagłówków accept takich jak **If-Match** w hello żądania, które zwracają wartość ETag w hello odpowiedzi.

| Operacja | Zwraca wartość ETag | Akceptuje warunkowego nagłówki |
|:--- |:--- |:--- |
| Umieszczanie obiektu Blob |Tak |Tak |
| Pobierz obiekt Blob |Tak |Tak |
| Pobierz właściwości obiektu Blob |Tak |Tak |
| Ustaw właściwości obiektów Blob |Tak |Tak |
| Pobierz metadane obiektu Blob |Tak |Tak |
| Ustaw metadane obiektu Blob |Tak |Tak |
| Obiekt Blob dzierżawy (*) |Tak |Tak |
| Migawki obiektu Blob |Tak |Tak |
| Kopiowanie obiektu Blob |Tak |Tak (w przypadku obiektów blob źródłowego i docelowego) |
| Przerwij kopiowania obiektów Blob |Nie |Nie |
| Usuwanie obiektów Blob |Nie |Tak |
| Umieść bloku |Nie |Nie |
| Umieść zablokowanych |Tak |Tak |
| Pobierz listę zablokowanych |Tak |Nie |
| Umieść stronę |Tak |Tak |
| Get zakresów stron |Tak |Tak |

(*) Obiekt Blob dzierżawy nie zmienia się hello ETag na obiektu blob.  

### <a name="pessimistic-concurrency-for-blobs"></a>Pesymistyczne współbieżności dla obiektów blob
toolock obiektu blob do wyłącznego użytku w przypadku uzyskania [dzierżawy](http://msdn.microsoft.com/library/azure/ee691972.aspx) na nim. Podczas uzyskania dzierżawy, należy określić jak długo muszą hello dzierżawy: może to być dla między 15 sekund too60 lub nieskończone które kwoty tooan w trybie wyłączności. Możesz odnowić tooextend skończoną dzierżawy, go, a można zwolnić wszystkie dzierżawy, po zakończeniu pracy z nim. Usługa blob Hello automatycznie zwalnia skończoną dzierżawy, gdy wygasną.  

Dzierżawy włączenia synchronizacji różne strategie toobe obsługiwane, tym zapisu na wyłączność / udostępnione zapisu odczytu, wyłącznego / wyłącznie do odczytu i zapisu udostępnionego / odczytu na wyłączność. W przypadku, gdy istnieje dzierżawę usługi magazynu hello wymusza na wyłączność zapisów (put, ustaw i operacji usunięcia) jednak zapewnienie wyłączności dla operacji odczytu wymaga hello tooensure developer, że wszystkie aplikacje klienckie używać Identyfikatora dzierżawy i że tylko jeden klient naraz ma identyfikator dzierżawy prawidłowe. Operacje odczytu nie zawierające wynik identyfikator dzierżawy w udostępnionym odczytów.  

Witaj poniższy fragment C# przedstawiono przykład pobierania wyłącznego dzierżawy przez 30 sekund na obiektu blob, aktualizowania zawartości hello hello obiektu blob, a następnie zwolnienie hello dzierżawy. Jeśli istnieje już prawidłowa dzierżawa na powitania blob podczas próby tooacquire nową dzierżawę, usługa blob hello zwraca wynik stanu "Konflikt HTTP (409)". fragment Hello poniżej używa **AccessCondition** obiektu informacji o dzierżawie powitalnych tooencapsulate podczas wykonywania żądania tooupdate hello blob w usłudze magazynowania hello.  Witaj pełny przykład można pobrać tutaj: [współbieżności zarządzania przy użyciu usługi Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
// Acquire lease for 15 seconds
string lease = blockBlob.AcquireLease(TimeSpan.FromSeconds(15), null);
Console.WriteLine("Blob lease acquired. Lease = {0}", lease);

// Update blob using lease. This operation will succeed
const string helloText = "Blob updated";
var accessCondition = AccessCondition.GenerateLeaseCondition(lease);
blockBlob.UploadText(helloText, accessCondition: accessCondition);
Console.WriteLine("Blob updated using an exclusive lease");

//Simulate third party update tooblob without lease
try
{
    // Below operation will fail as no valid lease provided
    Console.WriteLine("Trying tooupdate blob without valid lease");
    blockBlob.UploadText("Update without lease, will fail");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == (int)HttpStatusCode.PreconditionFailed)
        Console.WriteLine("Precondition failure as expected. Blob's lease does not match");
    else
        throw;
}  
```

Przy próbie operacji zapisu dla dzierżawionych obiektu blob bez przekazywania identyfikator dzierżawy hello hello żądanie kończy się niepowodzeniem z powodu błędu 412. Należy pamiętać, że jeśli hello dzierżawy jest wygasa przed wywołaniem hello **UploadText** metoda, ale nadal przekazać hello identyfikator dzierżawy, Żądanie hello nie powiedzie się także z **412** błędu. Aby uzyskać więcej informacji o zarządzaniu identyfikatory dzierżawy i czas wygaśnięcia dzierżawy, zobacz hello [Blob dzierżawy](http://msdn.microsoft.com/library/azure/ee691972.aspx) dokumentacji REST.  

Witaj następujące operacje obiektu blob można użyć współbieżności pesymistyczne toomanage dzierżawy:  

* Umieszczanie obiektu Blob
* Pobierz obiekt Blob
* Pobierz właściwości obiektu Blob
* Ustaw właściwości obiektów Blob
* Pobierz metadane obiektu Blob
* Ustaw metadane obiektu Blob
* Usuwanie obiektów Blob
* Umieść bloku
* Umieść zablokowanych
* Pobierz listę zablokowanych
* Umieść stronę
* Get zakresów stron
* Migawki obiektu Blob — identyfikator dzierżawy jest opcjonalne, jeśli istnieje dzierżawy
* Jeśli dzierżawa istnieje na powitania docelowego obiektu blob wymagany identyfikator dzierżawy kopiowania obiektu Blob-
* Przerwania kopiowania obiektu Blob — identyfikator dzierżawy wymagane, jeśli dzierżawę nieskończone istnieje na powitania docelowego obiektu blob
* Obiekt Blob dzierżawy  

### <a name="pessimistic-concurrency-for-containers"></a>Pesymistyczne współbieżności dla kontenerów
Dzierżawy kontenerów włączyć hello tego samego toobe strategii synchronizacji obsługiwany na obiekty BLOB (wyłącznie zapisu / udostępnione zapisu odczytu, wyłącznego / wyłącznie do odczytu i zapisu udostępnionego / odczytu na wyłączność) jednak w przeciwieństwie do obiektów blob usługi magazynu hello tylko wymusza wyłączności w operacji usuwania. toodelete kontener z aktywną dzierżawę, klient musi zawierać identyfikator aktywną dzierżawę hello hello żądanie usunięcia. Wszystkie operacje kontenera powiedzie się w kontenerze dzierżawionych bez uwzględniania identyfikator dzierżawy hello w takim przypadku są one udostępniane operacji. Jeśli wymagana jest wyłączności aktualizacji (put lub zestawu) lub operacji odczytu następnie deweloperzy powinien zapewnić, że wszyscy klienci używają Identyfikatora dzierżawy, a tylko jednego klienta w czasie ma identyfikator dzierżawy prawidłowe.  

Witaj następujące operacje kontenera, można użyć współbieżności pesymistyczne toomanage dzierżawy:  

* Usunąć kontenera
* Pobierz właściwości kontenera
* Pobranie metadanych kontenera
* Ustaw metadanych kontenera
* Pobierz ACL kontenera
* Ustaw ACL kontenera
* Kontener dzierżawy  

Aby uzyskać więcej informacji, zobacz:  

* [Określanie warunkowego nagłówki dla operacji usługi Blob](http://msdn.microsoft.com/library/azure/dd179371.aspx)
* [Kontener dzierżawy](http://msdn.microsoft.com/library/azure/jj159103.aspx)
* [Obiekt Blob dzierżawy](http://msdn.microsoft.com/library/azure/ee691972.aspx)

## <a name="managing-concurrency-in-hello-table-service"></a>Zarządzanie współbieżność w hello usługi tabel
Usługa tabel Hello używa optymistycznej współbieżności kontroli jako hello domyślne zachowanie podczas pracy z obiektami, w przeciwieństwie do usługi blob hello gdzie należy jawnie wybrać tooperform sprawdzenie optymistycznej współbieżności. Hello innych różnica między usługami hello tabeli i obiektów blob jest umożliwi tylko Zarządzanie hello współbieżności zachowania jednostek podczas, gdy usługa blob hello można zarządzać współbieżności hello kontenerów i obiektów blob.  

toouse optymistycznej współbieżności i toocheck, jeśli inny proces zmodyfikowane jednostki, ponieważ został pobrany z usługi Magazyn tabel hello służy wartość ETag hello otrzymany zwrócona usługa tabel hello jednostki. zarys Hello tego procesu jest następujący:  

1. Pobrać jednostki z usługi Magazyn tabel hello, odpowiedź hello zawiera wartość ETag, która określa identyfikator bieżącego hello skojarzony z tego obiektu w usłudze magazynowania hello.
2. Podczas aktualizacji jednostki hello zawierają wartość ETag hello otrzymane w kroku 1 w hello obowiązkowe **If-Match** nagłówka żądania hello wysyłania toohello usługi.
3. Witaj porównuje hello wartość ETag w żądaniu hello z bieżącej wartości ETag hello hello jednostki.
4. Jeśli hello bieżącej wartości ETag hello jednostki jest inny niż hello ETag w hello obowiązkowe **If-Match** nagłówka w żądaniu hello, usługa hello zwraca błąd 412 toohello klienta. To ustawienie określa klienta toohello inny proces zaktualizował jednostki hello ponieważ pobrany powitania klienta.
5. Jeśli hello bieżącej wartości ETag obiektu hello jest taki sam, jak hello ETag w hello obowiązkowe hello **If-Match** nagłówka w żądaniu hello lub hello **If-Match** nagłówek zawiera hello symbol wieloznaczny (*), usługa hello wykonuje hello żądanej operacji i aktualizacje hello bieżącej wartości ETag tooshow jednostki hello została zaktualizowana.  

Należy pamiętać, że w przeciwieństwie do usługi blob hello, usługi tabel hello wymaga powitania klienta tooinclude **If-Match** nagłówek żądania aktualizacji. Jest jednak możliwe tooforce bezwarunkowe aktualizacji (ostatni składnik zapisywania usługi wins strategii) i obejście kontrolach współbieżności, jeśli klient hello ustawia hello **If-Match** nagłówka w toohello znaki wieloznaczne (*) w żądaniu hello.  

powitania po fragment kodu C# zawiera jednostki klienta, która wcześniej została utworzona lub pobrać o zaktualizować adres e-mail użytkownika. Hello początkowego wstawieniu pobrać wartość ETag hello magazynów operacji w obiekcie klienta hello lub ponieważ próbki hello hello tego samego wystąpienia obiektu podczas wykonywania hello Zakończono operację zamiany, automatycznie wysyła hello ETag wartość tylnej toohello tabeli usługi Włączanie toocheck usługi hello za naruszenia współbieżności. Jeśli inny proces został zaktualizowany hello jednostki w magazynie tabel, usługa hello zwraca komunikat stanu HTTP 412 (warunek wstępny nie powiodła się.).  Witaj pełny przykład można pobrać tutaj: [współbieżności zarządzania przy użyciu usługi Azure Storage](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114).

```csharp
try
{
    customer.Email = "updatedEmail@contoso.org";
    TableOperation replaceCustomer = TableOperation.Replace(customer);
    customerTable.Execute(replaceCustomer);
    Console.WriteLine("Replace operation succeeded.");
}
catch (StorageException ex)
{
    if (ex.RequestInformation.HttpStatusCode == 412)
        Console.WriteLine("Optimistic concurrency violation – entity has changed since it was retrieved.");
    else
        throw;
}  
```

tooexplicitly wyłączenie sprawdzania współbieżności hello, należy ustawić hello **ETag** właściwości hello **pracownika** obiekt zbyt "*" przed wykonaniem operacji Zastąp hello.  

```csharp
customer.ETag = "*";  
```

Witaj poniższej tabeli przedstawiono sposób operacje jednostki tabeli hello Użyj wartości ETag:

| Operacja | Zwraca wartość ETag | Wymaga nagłówek If-Match żądania |
|:--- |:--- |:--- |
| Zapytanie jednostek |Tak |Nie |
| Wstaw jednostkę |Tak |Nie |
| Aktualizowanie jednostek |Tak |Tak |
| Scal jednostki |Tak |Tak |
| Usuwanie jednostki |Nie |Tak |
| Wstawianie lub zastępowanie jednostki |Tak |Nie |
| Wstawianie lub scalania jednostki |Tak |Nie |

Należy pamiętać, że hello **wstawienia lub Zastąp jednostki** i **wstawienia lub scalania jednostki** wykonaj operacje *nie* wykonać wszelkie kontrolach współbieżności, ponieważ nie wysyłaj toohello wartość ETag Usługa tabel.  

Ogólnie rzecz biorąc deweloperzy przy użyciu tabel polegać na optymistycznej współbieżności podczas tworzenia skalowalnych aplikacji. W razie potrzeby pesymistyczne blokowanie deweloperzy jeden z nich można podjąć w przypadku uzyskiwania dostępu do tabel tooassign wyznaczonych obiektu blob dla każdej tabeli i spróbuj tootake dzierżawy na powitania blob przed wykonywaniem operacji na powitania tabeli. Ta metoda wymaga tooensure aplikacji hello dostęp do wszystkich danych ścieżki uzyskać hello toooperating wcześniejsze dzierżawy na powitania tabeli. Należy również zauważyć, że czas dzierżawy minimalna hello jest 15 sekund, co wymaga dokładne brany pod uwagę w przypadku skalowalności.  

Aby uzyskać więcej informacji, zobacz:  

* [Operacje na jednostkach](http://msdn.microsoft.com/library/azure/dd179375.aspx)  

## <a name="managing-concurrency-in-hello-queue-service"></a>Zarządzanie współbieżność w hello usługi kolejki
Scenariusz jest istotny w usłudze kolejkowania hello, w których współbieżności jest, gdy wielu klientów są pobieranie wiadomości z kolejki. Po pobraniu wiadomości z kolejki hello hello odpowiedź zawiera wiadomość hello i wartości otrzymania pop, która jest wymagana toodelete wiadomość hello. wiadomości powitania nie zostanie automatycznie usunięta z kolejki hello, ale po jej pobraniu, nie jest widoczne tooother klientów hello interwału określonego przez parametr visibilitytimeout hello. powitania klienta, który pobiera wiadomość hello jest wiadomość hello toodelete oczekiwany po przetworzeniu i przed hello w czasie określonym przez hello TimeNextVisible elementu hello odpowiedzi, która jest obliczana na podstawie wartości hello hello visibilitytimeout parametr. wartość Hello visibilitytimeout są dodawane toohello czasu, w których hello jest komunikat pobrać wartość hello toodetermine TimeNextVisible.  

Hello Kolejka usługi nie jest obsługiwane pesymistyczne albo optymistycznej współbieżności i dla tego powodu klientów, przetwarzanie wiadomości pobierane z kolejki powinien zapewnić, że komunikaty są przetwarzane w sposób idempotentności. Ostatni strategii wins moduł zapisujący jest używana do operacji aktualizacji, takich jak SetQueueServiceProperties, SetQueueMetaData, SetQueueACL i UpdateMessage.  

Aby uzyskać więcej informacji, zobacz:  

* [Interfejs API REST usługi kolejki](http://msdn.microsoft.com/library/azure/dd179363.aspx)
* [Pobieranie wiadomości](http://msdn.microsoft.com/library/azure/dd179474.aspx)  

## <a name="managing-concurrency-in-hello-file-service"></a>Zarządzanie współbieżność w hello usługi plików
usługi plików Hello jest możliwy za pomocą dwóch różnych punktów końcowych protokołu — protokołu SMB i REST. Hello usługi REST nie jest obsługiwane optymistyczne blokowanie albo pesymistyczne blokowanie i wszystkie aktualizacje zostaną wykonaj ostatniego strategii wins składnika zapisywania. Plik blokowania mechanizmów toomanage dostępu tooshared pliki systemowe — tym hello możliwości tooperform pesymistyczne blokowanie mogą korzystać z klientów SMB, które zainstalować udziały plików. Po otwarciu pliku klienta SMB określa zarówno hello dostęp do plików i udziału tryb. Ustawienie opcji dostępu do pliku "Write" lub "odczytu/zapisu, wraz z trybem udziału plików"None"spowoduje hello plik jest zablokowany przez klienta protokołu SMB do czasu zamknięcia hello pliku. Jeśli nastąpi próba wykonania operacji REST w pliku, gdzie klient protokołu SMB ma zablokowane pliku hello hello usługi REST zwróci kod stanu 409 (konflikt) z kodem błędu SharingViolation.  

Jeśli klient protokołu SMB otwarty plik do usunięcia, oznacza hello pliku jako oczekujące usunięcie do wszystkich klientów SMB są zamknięte otwartymi dojściami w tym pliku. Gdy plik jest oznaczone jako oczekujące na usunięcie, wszelkie operacje REST dla tego pliku i zwróci kod stanu 409 (konflikt) z kodem błędu SMBDeletePending. Kod stanu 404 (nie znaleziono) nie są zwracane, ponieważ istnieje możliwość powitania tooremove klienta SMB hello Oczekujące usunięcie flagi tooclosing wcześniejsze hello pliku. Innymi słowy kod stanu 404 (nie znaleziono) jest oczekiwane tylko w przypadku hello plik został usunięty. Należy pamiętać, że plik w trakcie SMB do czasu usunięcia stanu, jego nie będą uwzględniane w hello listę plików w wynikach. Operacje REST usuwanie plików i katalogów usunąć REST hello są automatycznie zatwierdzone i nie powodują Oczekujące usunięcie stanu.  

Aby uzyskać więcej informacji, zobacz:  

* [Zarządzanie plikiem blokuje](http://msdn.microsoft.com/library/azure/dn194265.aspx)  

## <a name="summary-and-next-steps"></a>Podsumowanie i następne kroki
Hello magazyn Microsoft Azure, usługa została zaprojektowana toomeet potrzeb hello hello najbardziej złożonych aplikacji online bez wymuszania deweloperzy toocompromise lub przemyślenia kluczy założenia takich jak spójności współbieżności i dane mogą pochodzić tootake Aby udzielić.  

Dla hello wykonaj przykładowej aplikacji, do którego odwołuje się ten blog:  

* [Zarządzanie za pomocą usługi Azure Storage — Przykładowa aplikacja współbieżności](http://code.msdn.microsoft.com/Managing-Concurrency-using-56018114)  

Aby uzyskać więcej informacji o usłudze Azure Storage, zobacz:  

* [Strona główna magazynu usługi Microsoft Azure](https://azure.microsoft.com/services/storage/)
* [Wprowadzenie tooAzure magazynu](storage-introduction.md)
* Wprowadzenie do magazynu [obiektu Blob](storage-dotnet-how-to-use-blobs.md), [tabeli](storage-dotnet-how-to-use-tables.md), [kolejek](storage-dotnet-how-to-use-queues.md), i [plików](storage-dotnet-how-to-use-files.md)
* Architektura magazynu — [magazynu Azure: Usługa magazynu w chmurze wysokiej dostępności z wysoki poziom spójności](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

