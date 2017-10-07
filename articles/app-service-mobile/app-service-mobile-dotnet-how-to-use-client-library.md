---
title: "Klient biblioteki zarządzanej aaaWorking z hello App Service Mobile Apps (z systemem Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse klienta .NET dla usługi Azure App Service Mobile Apps w aplikacjach systemu Windows i Xamarin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0280785c-e027-4e0d-aaf2-6f155e5a6197
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 01/04/2017
ms.author: glenga
ms.openlocfilehash: b056e606b19406398f5b6faabb0931ad651125e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a>Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a>Omówienie
W tym przewodniku przedstawiono sposób tooperform typowych scenariuszy przy użyciu hello zarządzania biblioteki klienta dla aplikacji usługi Azure App Service Mobile aplikacji dla systemu Windows i Xamarin. W przypadku nowych aplikacji tooMobile należy rozważyć pierwszy hello Kończenie [szybkiego startu usługi Azure Mobile Apps] [ 1] samouczka. W tym przewodniku, możemy skupić się na powitania klienta zarządzanego zestawu SDK. toolearn więcej na temat hello zestawów SDK po stronie serwera dla Mobile Apps, zobacz dokumentację hello na powitania [.NET SDK serwera] [ 2] lub [Node.js Server SDK] [ 3].

## <a name="reference-documentation"></a>Dokumentacja referencyjna
Witaj dokumentacji powitania klienta SDK znajduje się tutaj: [odwołania klienta usługi Azure Mobile Apps .NET][4].
Możesz również znaleźć kilka przykładów klienta w hello [repozytorium GitHub przykłady Azure][5].

## <a name="supported-platforms"></a>Obsługiwane platformy
Witaj platformy .NET obsługuje hello następujące platformy:

* Dla systemu Xamarin Android wersje interfejsu API 19 do 24 (KitKat za pośrednictwem nugacie)
* Zwalnia systemu Xamarin iOS dla systemu iOS w wersji 8.0 lub nowszej
* Platforma uniwersalna systemu Windows
* Windows Phone 8.1
* Windows Phone 8.0, z wyjątkiem aplikacji Silverlight

Hello "serwer flow" uwierzytelnianie przy użyciu widoku sieci Web dla hello przedstawione interfejsu użytkownika.  Jeśli hello urządzenie nie jest możliwe toopresent UI widoku sieci Web, potrzebne są inne metody uwierzytelniania.  Zestaw SDK w związku z tym nie jest odpowiedni dla typu czujki lub podobnie ograniczeniami urządzeń.

## <a name="setup"></a>Instalacji i wymagania wstępne
Przyjęto założenie, że możesz już utworzono i opublikowano projektu zaplecza aplikacji mobilnej, który zawiera co najmniej jedna tabela.  W kodzie hello używane w tym temacie, nosi nazwę tabeli hello `TodoItem` i ma hello następujące kolumny: `Id`, `Text`, i `Complete`. Ta tabela jest hello tej samej tabeli utworzone po zakończeniu [szybkiego startu usługi Azure Mobile Apps][1].

Witaj odpowiedniego typu po stronie klienta typu w języku C# jest hello następujące klasy:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }
}
```

Witaj [JsonPropertyAttribute] [ 6] jest używane toodefine hello *PropertyName* mapowanie między powitania klienta hello tabeli pola i.

toolearn jak toocreate tabel w zapleczu swojej Mobile Apps, zobacz hello [temacie .NET SDK serwera] [ 7] lub hello [tematu Node.js Server SDK] [ 8] . Jeśli utworzono zaplecza aplikacji mobilnej hello Azure za pomocą portalu hello szybkiego startu, można również użyć hello **łatwe tabel** ustawienie w hello [portalu Azure].

### <a name="how-to-install-hello-managed-client-sdk-package"></a>Porady: hello instalacji zarządzany pakiet SDK klienta
Użyj hello następujące metody tooinstall hello zarządzany pakiet SDK klienta dla aplikacji mobilnych z [NuGet][9]:

* **Visual Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj hello `Microsoft.Azure.Mobile.Client` pakietu, a następnie kliknij przycisk **zainstalować**.
* **Program Xamarin Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj** > **Dodawanie pakietów NuGet**, wyszukaj hello `Microsoft.Azure.Mobile.Client `pakietu, a następnie kliknij przycisk **Dodaj Pakiet**.

W pliku głównym działaniu Pamiętaj następujące hello tooadd **przy użyciu** instrukcji:

```
using Microsoft.WindowsAzure.MobileServices;
```

### <a name="symbolsource"></a>Porady: Praca z symboli debugowania w programie Visual Studio
są dostępne na powitania symbole dla przestrzeni nazw Microsoft.Azure.Mobile hello [SymbolSource][10].  Zobacz toothe [instrukcje SymbolSource] [ 11] toointegrate SymbolSource z programem Visual Studio.

## <a name="create-client"></a>Utwórz powitania klienta Mobile Apps
Witaj poniższy kod tworzy hello [MobileServiceClient] [ 12] obiekt, który jest używany tooaccess zaplecza aplikacji mobilnej.

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

W hello poprzedzających kodu, Zastąp `MOBILE_APP_URL` z adresem URL hello hello zaplecza aplikacji mobilnej, który znajduje się w bloku dla zaplecza aplikacji mobilnej w hello [portalu Azure]. Obiekt MobileServiceClient Hello powinna być klasą pojedynczą.

## <a name="work-with-tables"></a>Praca z tabelami
Witaj, jak poniższe informacje sekcji toosearch i pobieranie rekordów i modyfikowanie danych hello hello tabeli.  obejmuje Hello następujące tematy:

* [Tworzenie odwołania do tabeli](#instantiating)
* [Dane zapytania](#querying)
* [Filtr zwrócił danych](#filtering)
* [Sortowanie zwrócone dane](#sorting)
* [Zwróć dane strony](#paging)
* [Wybrać określone kolumny](#selecting)
* [Wyszukaj według identyfikatora](#lookingup)
* [Dotyczących zapytań bez typu](#untypedqueries)
* [Wstawianie danych](#inserting)
* [Aktualizowanie danych](#updating)
* [Usuwanie danych](#deleting)
* [Rozwiązywanie konfliktów i optymistycznej współbieżności](#optimisticconcurrency)
* [Powiązanie tooa interfejsu użytkownika systemu Windows](#binding)
* [Zmiana rozmiaru strony hello](#pagesize)

### <a name="instantiating"></a>Porady: Tworzenie odwołania do tabeli
Cały kod hello, który uzyskuje dostęp do lub modyfikuje dane w tabeli wewnętrznej bazy danych wymaga funkcji na powitania `MobileServiceTable` obiektu. Uzyskaj odwołanie do tabeli toohello za hello wywoływania [Metoda GetTable] metody, w następujący sposób:

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

Witaj zwrócony obiekt używa hello serializacji typu modelu. Obsługiwane jest również modelem serializacji bez typu. Poniższy przykład [tworzy tabelę bez typu tooan odwołanie]:

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

W zapytaniach bez typu należy określić hello bazowy ciągu zapytania OData.

### <a name="querying"></a>Porady: zapytania na danych z aplikacji mobilnej
W tej sekcji opisano, jak tooissue odpytuje toohello zaplecza aplikacji mobilnej, która obejmuje następujące funkcje hello:

* [Filtr zwrócił danych](#filtering)
* [Sortowanie zwrócone dane](#sorting)
* [Zwróć dane strony](#paging)
* [Wybrać określone kolumny](#selecting)
* [Wyszukiwać dane według Identyfikatora](#lookingup)

> [!NOTE]
> Rozmiar strony oparte na serwerze jest wymuszone tooprevent wszystkich wierszy zwracanych.  Stronicowania zachowuje żądań domyślny dla dużych zestawów danych z niekorzystnego wpływu na powitania usługi.  tooreturn więcej niż 50 wierszy, użyj hello `Skip` i `Take` metody, zgodnie z opisem w [zwrócić dane na stronach](#paging).

### <a name="filtering"></a>Porady: Filtr zwrócił danych
Witaj poniższy kod ilustruje sposób danych toofilter, umieszczając w niej `Where` klauzuli w zapytaniu. Zwraca wszystkie elementy z `todoTable` których `Complete` właściwości jest równa za`false`. Witaj [gdzie] funkcja ma zastosowanie filtrowania predykatu do hello zapytania dotyczącego tabeli hello wiersza.

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

Możesz wyświetlić hello URI hello żądanie wysłane toohello wewnętrznej bazy danych za pomocą komunikatów inspekcji oprogramowania, takich jak narzędzia dla deweloperów w przeglądarce lub [Fiddler]. Jeśli przyjrzymy się identyfikator URI żądania hello, zwróć uwagę zmodyfikowania ciągu kwerendy hello:

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

To żądanie OData jest przekształcana na kwerendę SQL przez powitania serwera SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

Funkcja, która została przekazana toohello Hello `Where` metody może mieć dowolną liczbę warunków.

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

W tym przykładzie będzie można przetłumaczyć kwerendę SQL przez powitania serwera SDK:

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

To zapytanie również może zostać podzielony na wiele klauzul:

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

Witaj dwie metody są równoważne i mogą być używane zamiennie.  Witaj wcześniejsze opcji&mdash;z łączenie wielu predykatów w jednym zapytaniu&mdash;jest bardziej compact i zalecanym.

Witaj `Where` klauzuli obsługuje operacje, które można przetłumaczyć hello podzestawu OData. Dostępne są następujące operacje:

* Operatory relacyjne (==,! =, <, < =, >, > =),
* Operatory arytmetyczne (+, -, /, *, %),
* Liczba precision (Math.Floor —, Math.Ceiling)
* Funkcje ciągów (długość, Substring, Zamień, IndexOf, StartsWith, EndsWith)
* Data właściwości (rok, miesiąc, dzień, godzina, minuty, sekundy),
* Dostęp do właściwości obiektu i
* Każdej z tych operacji łączenia wyrażenia.

Gdy biorąc pod uwagę co hello serwera SDK obsługuje, można rozważyć hello [OData v3 dokumentacji].

### <a name="sorting"></a>Porady: sortowanie zwrócone dane
Witaj poniższy kod ilustruje sposób danych toosort, umieszczając w niej [OrderBy] lub [OrderByDescending] funkcji w zapytaniu hello. Zwraca elementy z `todoTable` sortowane rosnąco przez hello `Text` pola.

```
// Sort items in ascending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderBy(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();

// Sort items in descending order by Text field
MobileServiceTableQuery<TodoItem> query = todoTable
                .OrderByDescending(todoItem => todoItem.Text)
List<TodoItem> items = await query.ToListAsync();
```

### <a name="paging"></a>Porady: zwrócić dane na stronach
Domyślnie program hello wewnętrznej bazy danych zwraca tylko hello 50 pierwszych wierszy. Można zwiększyć hello liczbę wierszy zwróconych przez wywołanie hello [zająć] metody. Użyj `Take` wraz z hello [Pomiń] toorequest metody określonej "strony" hello całkowita zestawu danych zwróconych przez zapytanie hello. Witaj następującej kwerendy, po wykonaniu zwraca hello pierwszych trzech elementów hello tabeli.

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Hello następujące zapytanie poprawione pomija hello pierwsze trzy wyniki i zwraca hello trzech kolejnych wyników. To zapytanie tworzy hello drugi "page" danych, których rozmiar strony hello jest trzy elementy.

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

Witaj [IncludeTotalCount] metoda żąda hello łączną liczbę dla *wszystkie* hello rekordów, które mogłyby być zwracane, ignorowanie klauzuli stronicowania/limit określony:

```
query = query.IncludeTotalCount();
```

W aplikacji rzeczywistych można użyć zapytania toohello podobne poprzedzających przykład z formantem pagera lub porównywalny interfejsu użytkownika do przechodzenia między stronami.

> [!NOTE]
> limit wierszy 50 hello toooverride w zaplecza aplikacji mobilnej, należy także zastosować hello [EnableQueryAttribute] toohello publicznego GET, metoda i Określ zachowanie stronicowania hello. Gdy metoda toohello zastosowane, powitania po ustawia too1000 maksymalna liczba wierszy zwróconych:
>
> `[EnableQuery(MaxTop=1000)]`


### <a name="selecting"></a>Porady: Wybieranie określonych kolumn
Można określić, który zestaw właściwości tooinclude w hello powoduje dodanie [wybierz] klauzuli tooyour zapytania. Na przykład Witaj następującego kodu pokazuje sposób tooselect tylko jednego pola, a także sposób tooselect i formatowanie wielu pól:

```
// Select one field -- just hello Text
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => todoItem.Text);
List<string> items = await query.ToListAsync();

// Select multiple fields -- both Complete and Text info
MobileServiceTableQuery<TodoItem> query = todoTable
                .Select(todoItem => string.Format("{0} -- {1}",
                    todoItem.Text.PadRight(30), todoItem.Complete ?
                    "Now complete!" : "Incomplete!"));
List<string> items = await query.ToListAsync();
```

Witaj wszystkie funkcje do tej pory opisane są addytywne, dlatego firma Microsoft może zapewnić łańcucha je. Każde wywołanie łańcuchowa ma wpływ na więcej hello zapytania. Przykładem więcej:

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <a name="lookingup"></a>Porady: wyszukiwanie danych według Identyfikatora
Witaj [LookupAsync] funkcja może być używane toolook zapasową obiektów z bazy danych hello o określonym identyfikatorze.

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <a name="untypedqueries"></a>Porady: wykonywanie zapytań bez typu
Podczas wykonywania zapytania za pomocą obiektu tabeli bez typu, należy jawnie określić ciąg zapytania OData hello, wywołując [ReadAsync]w hello poniższy przykład:

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

Możesz odzyskać wartości JSON, które można używać jak zbioru właściwości. Aby uzyskać więcej informacji na JToken i Newtonsoft Json.NET, zobacz hello [Json.NET] lokacji.

### <a name="inserting"></a>Porady: wstawianie danych do zaplecza aplikacji mobilnej
Wszystkie typy klientów musi zawierać element członkowski o nazwie **identyfikator**, który jest domyślnie ciąg. To **identyfikator** jest wymagane do przeprowadzenia operacji CRUD i dla synchronizacji w trybie offline. hello następującego kodu ilustruje sposób toouse hello [InsertAsync] metody tooinsert nowych wierszy do tabeli. Parametr Hello zawiera hello toobe dane wstawiane jak dla obiektu .NET.

```
await todoTable.InsertAsync(todoItem);
```

Jeśli wartość Unikatowy identyfikator niestandardowych nie jest objęta hello `todoItem` podczas wstawiania identyfikator GUID jest generowany przez serwer hello.
Możesz pobrać hello generowany identyfikator sprawdzając hello obiektu po wywołaniu hello zwraca.

tooinsert bez typu danych, użytkownik może skorzystać z Json.NET:

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

Oto przykład przy użyciu adresu e-mail jako identyfikator unikatowy ciąg:

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a>Praca z wartościami identyfikatorów
Aplikacje mobilne obsługuje wartości unikatowe niestandardowy ciąg hello tabeli **identyfikator** kolumny. Wartość ciągu umożliwia aplikacjom toouse wartości niestandardowych, takich jak adresy e-mail lub nazwy użytkownika dla identyfikatora hello.  Identyfikatory ciągów dostarczyć hello następujące korzyści:

* Identyfikatory są generowane bez wprowadzania toohello obiegu bazy danych.
* Rekordy są łatwiejsze toomerge z różnych tabel lub baz danych.
* Wartości identyfikatorów można lepiej zintegrować z logiki aplikacji.

Jeśli wartość Identyfikatora ciągu nie jest ustawiony na wstawionego rekordu, zaplecza aplikacji mobilnej hello generuje unikatową wartość dla identyfikatora. Można użyć hello [Guid.NewGuid] toogenerate metody własnego Identyfikatora wartości na powitania klienta lub w hello wewnętrznej bazy danych.

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <a name="modifying"></a>Porady: modyfikowanie danych w zaplecza aplikacji mobilnej
Witaj poniższy kod ilustruje sposób toouse hello [UpdateAsync] tooupdate metody istniejący rekord z hello sam identyfikator nowymi informacjami. Parametr Hello zawiera toobe danych hello zaktualizowane jak dla obiektu .NET.

```
await todoTable.UpdateAsync(todoItem);
```

tooupdate bez typu danych, użytkownik może skorzystać z [Json.NET] w następujący sposób:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

`id` Należy podać wartość pola podczas wprowadzania aktualizacji. Hello wewnętrznej bazy danych używa hello `id` tooidentify pola, które tooupdate wiersz. Witaj `id` pola można uzyskać od wyniku hello hello `InsertAsync` wywołania. `ArgumentException` Jest wywoływane przy próbie tooupdate elementu bez podawania hello `id` wartość.

### <a name="deleting"></a>Porady: usuwanie danych zaplecza aplikacji mobilnej
Witaj poniższy kod ilustruje sposób toouse hello [DeleteAsync] toodelete metody istniejącego wystąpienia. wystąpienie Hello jest identyfikowane przez hello `id` pola zestawu na powitania `todoItem`.

```
await todoTable.DeleteAsync(todoItem);
```

toodelete bez typu danych, użytkownik może skorzystać z struktury Json.NET w następujący sposób:

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

Po wprowadzeniu żądanie usunięcia, należy określić identyfikator. Inne właściwości nie są one przekazywane toohello usługi lub są ignorowane w hello usług. Witaj wynik `DeleteAsync` wywołanie jest zwykle `null`. toopass identyfikator Hello w można uzyskać od wyniku hello hello `InsertAsync` wywołania. A `MobileServiceInvalidOperationException` jest generowany, gdy spróbujesz toodelete elementu bez określania hello `id` pola.

### <a name="optimisticconcurrency"></a>Porady: użycie optymistycznej współbieżności do rozwiązywania konfliktów
Dwa lub więcej klientów może zapisać zmian toohello sam element na powitania sam czas. Bez wykrywania konfliktów hello ostatniego zapisu zastąpiłaby wszelkie poprzednie aktualizacje. **Optymistyczne sterowanie współbieżnością** założono, że każdej transakcji można zatwierdzić i dlatego nie używa żadnych zasobów blokowania.  Przed zatwierdzeniem transakcji, optymistyczne sterowanie współbieżnością sprawdza, czy nie inne transakcje nie zmienione hello danych. W przypadku modyfikacji danych hello hello zatwierdzania transakcji została wycofana.

Aplikacje mobilne obsługuje optymistyczne sterowanie współbieżnością za śledzenia zmian elementu tooeach przy użyciu hello `version` kolumny właściwości systemu, który jest zdefiniowany dla każdej tabeli w zaplecza aplikacji mobilnej. Przy każdym aktualizacji rekordu Mobile Apps ustawia hello `version` właściwości w tym rejestrowania tooa nową wartość. Podczas każdego żądania aktualizacji hello `version` Właściwość rekordu hello dołączone do żądania hello jest porównywany toohello tę samą właściwość dla rekordu hello na powitania serwera. Jeśli wersja przekazaną za pomocą żądania hello jest niezgodna z hello wewnętrznej bazy danych, a następnie wywołuje powitania klienta biblioteki `MobileServicePreconditionFailedException<T>` wyjątku. Typ Hello dołączonego wyjątek hello jest hello rekord na podstawie hello wersja wewnętrznej bazy danych zawierające hello serwerów hello rekordu. Witaj aplikacji można używać tego toodecide informacji czy tooexecute hello aktualizacji żądanie ponownie, podając poprawną hello `version` wartość z zakresu od hello zaplecza toocommit zmiany.

Zdefiniować kolumnę na powitania klasy tabeli dla hello `version` optymistycznej współbieżności tooenable właściwości systemu. Na przykład:

```
public class TodoItem
{
    public string Id { get; set; }

    [JsonProperty(PropertyName = "text")]
    public string Text { get; set; }

    [JsonProperty(PropertyName = "complete")]
    public bool Complete { get; set; }

    // *** Enable Optimistic Concurrency *** //
    [JsonProperty(PropertyName = "version")]
    public string Version { set; get; }
}
```

Aplikacje przy użyciu tabel bez typu włączyć optymistycznej współbieżności przez ustawienie hello `Version` Flaga na `SystemProperties` z hello tabeli w następujący sposób.

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

W dodatku tooenabling optymistycznej współbieżności, musi również catch hello `MobileServicePreconditionFailedException<T>` wyjątek w kodzie podczas wywoływania metody [UpdateAsync].  Rozwiąż konflikt hello stosując hello poprawne `version` toothe zaktualizować rekord i wywołanie [UpdateAsync] z hello rozpoznać rekordu. Witaj następującego kodu pokazano, jak tooresolve zapisu raz wykryty konflikt:

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at hello remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, hello item has changed since hello last query
        // Resolve hello conflict between hello local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user toochoose hello resoltion between versions
    MessageDialog msgDialog = new MessageDialog(
        String.Format("Server Text: \"{0}\" \nLocal Text: \"{1}\"\n",
        serverItem.Text, localItem.Text),
        "CONFLICT DETECTED - Select a resolution:");

    UICommand localBtn = new UICommand("Commit Local Text");
    UICommand ServerBtn = new UICommand("Leave Server Text");
    msgDialog.Commands.Add(localBtn);
    msgDialog.Commands.Add(ServerBtn);

    localBtn.Invoked = async (IUICommand command) =>
    {
        // tooresolve hello conflict, update hello version of hello item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while hello user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

Aby uzyskać więcej informacji, zobacz hello [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps] tematu.

### <a name="binding"></a>Porady: interfejs użytkownika systemu Windows tooa danych Bind Mobile Apps
W tej sekcji przedstawiono, jak toodisplay zwróciło obiektów danych, za pomocą elementów interfejsu użytkownika w aplikacji systemu Windows.  Poniższy przykładowy kod wiąże toohello źródła hello listy przy użyciu zapytania niezakończonych elementów. [MobileServiceCollection] tworzy kolekcję przenośnych aplikacji obsługujących powiązania.

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound tooa UI list control
IEnumerable itemsControl  = items;

// Bind this tooa ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

Niektóre formanty w hello zarządzane Obsługa środowiska uruchomieniowego interfejs o nazwie [ISupportIncrementalLoading]. Ten interfejs umożliwia toorequest formanty dodatkowe dane, gdy hello użytkownik przewija widok. Jest wbudowaną obsługę ten interfejs dla uniwersalnych aplikacji systemu Windows za pośrednictwem [MobileServiceIncrementalLoadingCollection], który automatycznie obsługuje wywołań z hello formantów. Użyj `MobileServiceIncrementalLoadingCollection` w aplikacjach systemu Windows w następujący sposób:

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

toouse hello nowej kolekcji w aplikacji Windows Phone 8 i "Silverlight" hello użyj `ToCollection` metody rozszerzenia na `IMobileServiceTableQuery<T>` i `IMobileServiceTable<T>`. Wywołaj danych tooload `LoadMoreItemsAsync()`.

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

Jeśli używasz kolekcji hello utworzona przez wywołanie metody `ToCollectionAsync` lub `ToCollection`, pobrać kolekcję, która może być powiązane tooUI formantów.  Ta kolekcja jest obsługujący stronicowania.  Ponieważ kolekcji hello ładuje dane z sieci, podczas ładowania czasami kończy się niepowodzeniem. toohandle takie błędy zastąpienie hello `OnException` metoda `MobileServiceIncrementalLoadingCollection` wyjątki toohandle wyniku wywołania zbyt`LoadMoreItemsAsync`.

Należy wziąć pod uwagę, jeśli ta tabela ma wiele pól, ale mają toodisplay niektóre z nich formantu. Można użyć wskazówki hello w powyższej sekcji hello "[wybrać określone kolumny](#selecting)" tooselect toodisplay określonych kolumn w hello interfejsu użytkownika.

### <a name="pagesize"></a>Witaj zmiany rozmiaru strony
Aplikacje mobilne platformy Azure zwraca maksymalnie 50 elementów na żądanie domyślnie.  Można zmienić hello stronicowania, zwiększając hello maksymalny rozmiar strony na powitania klienta i serwera.  tooincrease hello rozmiar żądanej strony, należy określić `PullOptions` przy użyciu `PullAsync()`:

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

Zakładając, że zostały wykonane hello `PageSize` tooor równy większa niż 100 w ramach serwera hello żądanie zwraca maksymalnie 100 elementów.

## <a name="#offlinesync"></a>Praca z tabelami w trybie Offline
Tabele w trybie offline używają lokalnych danych toostore magazynu SQLite do użycia w trybie offline.  Tabela wszystkie operacje są wykonywane przed hello SQLite lokalnego magazynu zamiast powitania serwera zdalnego magazynu.  toocreate tabelę w trybie offline, najpierw przygotować projektu:

1. W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello > **Zarządzaj pakietami NuGet rozwiązania...** , następnie wyszukaj i zainstaluj **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet dla wszystkich projektów w rozwiązaniu hello.
2. Urządzeń z systemem Windows (opcjonalnie) toosupport zainstalować jednego z powitania po SQLite środowiska uruchomieniowego pakiety:

   * **Środowisko uruchomieniowe Windows 8.1:** zainstalować [SQLite dla Windows 8.1][3].
   * **Windows Phone 8.1:** zainstalować [SQLite dla Windows Phone 8.1][4].
   * **Platforma uniwersalna systemu Windows** zainstalować [SQLite dla uniwersalnych systemu Windows hello][5].
3. (Opcjonalnie). Dla urządzeń z systemem Windows, kliknij przycisk **odwołania** > **Dodawanie odwołania...** , rozwiń hello **Windows** folder > **rozszerzenia**, następnie włącz hello odpowiednie **SQLite dla systemu Windows** zestawu SDK oraz hello  **2013 środowiska uruchomieniowego Visual C++ dla systemu Windows** zestawu SDK.
    Witaj nazwy zestawu SDK SQLite się nieco różnić z każdej z platform Windows.

Aby można było utworzyć odwołania do tabeli, należy przygotować hello lokalnego magazynu:

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

Zainicjowanie magazynu odbywa się normalnie natychmiast po utworzeniu powitania klienta.  Witaj **OfflineDbPath** powinny być odpowiednie do użycia na wszystkich platformach obsługiwanych nazwę pliku.  Jeśli ścieżka hello jest w pełni kwalifikowana (to znaczy rozpoczyna się od ukośnika), zostanie użyta w tej ścieżce.  Jeśli ścieżka hello nie jest w pełni kwalifikowana, plik hello jest umieszczany w lokalizacji specyficzne dla platformy.

* Dla urządzeń iOS i Android hello domyślna ścieżka to folder "Osobiste pliki" hello.
* W przypadku urządzeń z systemem Windows hello domyślna ścieżka to folder "AppData" specyficzne dla aplikacji hello.

Odwołanie do tabeli można uzyskać za pomocą hello `GetSyncTable<>` metody:

```
var table = client.GetSyncTable<TodoItem>();
```

Nie trzeba toouse tooauthenticate tabelę w trybie offline.  Wystarczy tooauthenticate, gdy komunikują się hello usługi wewnętrznej bazy danych.

### <a name="syncoffline"></a>Trwa synchronizowanie tabelę w trybie Offline
Tabele w trybie offline nie są zsynchronizowane z zaplecza hello domyślnie.  Synchronizacja jest podzielony na dwie części.  Wypchnij zmiany oddzielnie pobierania nowych elementów.  Oto metoda typowe synchronizacji:

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //hello first parameter is a query name that is used internally by hello client SDK tooimplement incremental sync.
            //Use a different query name for each unique query in your program
            "allTodoItems",
            this.todoTable.CreateQuery());
    }
    catch (MobileServicePushFailedException exc)
    {
        if (exc.PushResult != null)
        {
            syncErrors = exc.PushResult.Errors;
        }
    }

    // Simple error/conflict handling. A real application would handle hello various errors like network conditions,
    // server conflicts and others via hello IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting tooserver's copy.
                await error.CancelAndUpdateItemAsync(error.Result);
            }
            else
            {
                // Discard local change.
                await error.CancelAndDiscardItemAsync();
            }

            Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.", error.TableName, error.Item["id"]);
        }
    }
}
```

Jeśli zbyt hello pierwszy argument`PullAsync` ma wartość null, synchronizacja przyrostowa nie będzie używana.  Każda operacja synchronizacji powoduje pobranie wszystkich rekordów.

niejawny wykonuje Hello SDK `PushAsync()` przed ściąganie rekordów.

Obsługa konflikt się dzieje na `PullAsync()` metody.  Możesz można biznesowych w radzeniu sobie z konfliktami w hello sam sposób jak tabele online.  konflikt Hello jest generowany po `PullAsync()` jest wywoływana zamiast podczas hello insert, update lub delete. Jeśli wystąpi konflikt wiele, są one dołączone do pojedynczego MobileServicePushFailedException.  Obsługi każdego błędów oddzielnie.

## <a name="#customapi"></a>Praca z niestandardowego interfejsu API
Niestandardowy interfejs API umożliwia toodefine niestandardowe punkty końcowe, które udostępniają funkcje serwera które nie mapy tooan insert, update, usuwania lub operacja odczytu. Przy użyciu niestandardowego interfejsu API, może mieć większą kontrolę nad wiadomości, w tym odczytywanie ustawienie nagłówki komunikatów HTTP i Definiowanie formatu treści wiadomości innych niż JSON.

Niestandardowy interfejs API należy wywołać wywołując jedną hello [InvokeApiAsync] metod na powitania klienta. Na przykład po wierszu kodu hello wysyła toohello żądania POST **completeAll** interfejsu API hello wewnętrznej bazy danych:

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

Ten formularz jest wywołanie metody typu i wymaga tego hello **MarkAllResult** zwracany typ jest zdefiniowany. Obsługiwane są zarówno typu, jak i bez typu metody.

Witaj metody InvokeApiAsync() dołącza/api/API toohello chcesz toocall, chyba że hello interfejsu API, który rozpoczyna się od '/'.
Na przykład:

* `InvokeApiAsync("completeAll",...)`wywołuje /api/completeAll hello wewnętrznej bazy danych
* `InvokeApiAsync("/.auth/me",...)`wywołuje /.auth/me hello wewnętrznej bazy danych

InvokeApiAsync toocall można użyć dowolnego WebAPI, łącznie z tymi WebAPIs, które nie są zdefiniowane z usługą Azure Mobile Apps.  Gdy używasz InvokeApiAsync() hello odpowiednie nagłówki, włącznie z nagłówkami uwierzytelniania są wysyłane z żądaniem hello.

## <a name="authentication"></a>Uwierzytelnianie użytkowników
Aplikacje mobilne obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account, Twitter i Azure Active Directory. Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy. Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera. Aby uzyskać więcej informacji, zobacz samouczek hello [aplikacji tooyour authentication Dodaj].

Obsługiwane są dwa przepływy uwierzytelniania: *zarządzanych przez klienta* i *serwer zarządzany* przepływu. Przepływ serwer zarządzany Hello zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello. Przepływ zarządzanych przez klienta Hello umożliwia lepszą integrację z możliwości specyficznych dla urządzeń zależy od zestawy SDK urządzenia specyficznego dla dostawcy.

> [!NOTE]
> Zalecamy używanie przepływem zarządzanych przez klienta w aplikacjach produkcyjnych.

tooset się uwierzytelniania, musisz zarejestrować aplikację z co najmniej jednego dostawcy tożsamości.  Dostawca tożsamości Hello generuje identyfikator klienta i klucz tajny klienta aplikacji.  Te wartości są ustawiane następnie w tooenable Twojego wewnętrznej bazy danych usługi Azure App Service uwierzytelniania/autoryzacji.  Aby uzyskać więcej informacji, wykonaj hello szczegółowe instrukcje w samouczku [aplikacji tooyour authentication Dodaj].

w tej sekcji opisano Hello następujące tematy:

* [Zarządzane przez klienta do uwierzytelniania](#clientflow)
* [Serwer zarządzany uwierzytelniania](#serverflow)
* [Token uwierzytelniania hello buforowania](#caching)

### <a name="clientflow"></a>Zarządzane przez klienta do uwierzytelniania
Aplikację można niezależnie skontaktuj się z dostawcą tożsamości hello, a następnie podaj token zwrócony hello podczas logowania, z poziomu zaplecza. Ten przepływ klienta umożliwia tooprovide pojedynczego jednokrotnego dla użytkowników lub tooretrieve użytkownika dodatkowe dane z hello dostawcy tożsamości. Uwierzytelnianie klienta przepływu jest preferowany toousing przepływu serwera jako dostawca tożsamości hello SDK zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.

Przykłady są dostępne dla powitania od klienta przepływach uwierzytelniania:

* [Biblioteki uwierzytelniania usługi Active Directory](#adal)
* [Facebook lub Google](#client-facebook)
* [Zestaw Live SDK](#client-livesdk)

#### <a name="adal"></a>Uwierzytelnianie użytkowników z hello biblioteki uwierzytelniania usługi Active Directory
Można użyć uwierzytelniania użytkownika tooinitiate hello Active Directory Authentication Library (ADAL) z powitania klienta przy użyciu uwierzytelniania usługi Azure Active Directory.

1. Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] samouczka. Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client.
2. W programie Visual Studio lub Xamarin Studio Otwórz projekt, a następnie dodaj toothe odwołanie `Microsoft.IdentityModel.CLients.ActiveDirectory` pakietu NuGet. Podczas wyszukiwania, obejmują wersje wstępne.
3. Dodaj hello następującego kodu tooyour aplikacji, zgodnie z platformy toohello, którego używasz. W każdej wprowadź hello następujące elementy zastępcze:

   * Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji. Format powinien być https://login.microsoftonline.com/contoso.onmicrosoft.com. Ta wartość może zostać skopiowany z hello kartę domeny w usłudze Azure Active Directory w hello [klasycznego portalu Azure].
   * Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej. Identyfikator klienta hello można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.
   * Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.
   * Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS. Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.

     następujący kod Hello wymagane dla każdej platformy:

     **System Windows:**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        while (user == null)
        {
            string message;
            try
            {
                AuthenticationContext ac = new AuthenticationContext(authority);
                AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                    new Uri(redirectUri), new PlatformParameters(PromptBehavior.Auto, false) );
                JObject payload = new JObject();
                payload["access_token"] = ar.AccessToken;
                user = await App.MobileService.LoginAsync(
                    MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
                message = string.Format("You are now logged in - {0}", user.UserId);
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
    ```

     **Xamarin.iOS**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync(UIViewController view)
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(view));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine(@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
        }
    }
    ```

     **Xamarin.Android**

    ```
    private MobileServiceUser user;
    private async Task AuthenticateAsync()
    {

        string authority = "INSERT-AUTHORITY-HERE";
        string resourceId = "INSERT-RESOURCE-ID-HERE";
        string clientId = "INSERT-CLIENT-ID-HERE";
        string redirectUri = "INSERT-REDIRECT-URI-HERE";
        try
        {
            AuthenticationContext ac = new AuthenticationContext(authority);
            AuthenticationResult ar = await ac.AcquireTokenAsync(resourceId, clientId,
                new Uri(redirectUri), new PlatformParameters(this));
            JObject payload = new JObject();
            payload["access_token"] = ar.AccessToken;
            user = await client.LoginAsync(
                MobileServiceAuthenticationProvider.WindowsAzureActiveDirectory, payload);
        }
        catch (Exception ex)
        {
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(ex.Message);
            builder.SetTitle("You must log in. Login Required");
            builder.Create().Show();
        }
    }
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {

        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ```

#### <a name="client-facebook"></a>Logowanie jednokrotne przy użyciu tokenu z usługi Facebook lub Google
Można użyć powitania klienta przepływ, jak pokazano w ta Wstawka kodu dla usługi Facebook lub Google.

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using hello Facebook or Google SDK.
token.Add("access_token", "access_token_value");

private MobileServiceUser user;
private async Task AuthenticateAsync()
{
    while (user == null)
    {
        string message;
        try
        {
            // Change MobileServiceAuthenticationProvider.Facebook
            // tooMobileServiceAuthenticationProvider.Google if using Google auth.
            user = await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
            message = string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

#### <a name="client-livesdk"></a>Rejestracja jednokrotna przy użyciu Account Microsoft z hello zestaw Live SDK
tooauthenticate użytkowników, musisz zarejestrować aplikację w hello konta Microsoft Developer Center. Skonfiguruj szczegóły rejestracji na zaplecza aplikacji mobilnej. toocreate Microsoft rejestracja konta podłączyć tooyour zaplecza aplikacji mobilnej, pełną hello czynnościach w ramach [zarejestrować Twojej aplikacji toouse logowania konta Microsoft]. Jeśli masz zarówno Sklep Windows i Windows Phone 8/Silverlight wersje aplikacji, najpierw zarejestrować wersji Sklepu Windows hello.

Witaj poniższy kod jest uwierzytelniany przy użyciu zestaw Live SDK i używa hello zwrócił token toosign w tooyour zaplecza aplikacji mobilnej.

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get hello URL hello Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create hello authentication client for Windows Store using hello service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create hello authentication client for Windows Phone using hello client ID of hello registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request hello authentication token from hello Live authentication service.
        // hello wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about hello logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use hello Microsoft account auth token toosign in tooApp Service.
            MobileServiceUser loginResult = await App.MobileService
                .LoginWithMicrosoftAccountAsync(result.Session.AuthenticationToken);

            // Display a personalized sign-in greeting.
            string title = string.Format("Welcome {0}!", meResult.Result["first_name"]);
            var message = string.Format("You are now logged in - {0}", loginResult.UserId);
            var dialog = new MessageDialog(message, title);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
        else
        {
            session = null;
            var dialog = new MessageDialog("You must log in.", "Login Required");
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
    }
}
```

Aby uzyskać więcej informacji, zobacz hello [Windows Live SDK] dokumentacji.

### <a name="serverflow"></a>Serwer zarządzany uwierzytelniania
Po zarejestrowaniu dostawcy tożsamości, wywołaj hello [LoginAsync] metody na powitania [MobileServiceClient] z hello [MobileServiceAuthenticationProvider] wartość dostawcy. Na przykład hello następujący kod inicjuje serwera przepływu logowania za pomocą usługi Facebook.

```
private MobileServiceUser user;
private async System.Threading.Tasks.Task Authenticate()
{
    while (user == null)
    {
        string message;
        try
        {
            user = await client
                .LoginAsync(MobileServiceAuthenticationProvider.Facebook);
            message =
                string.Format("You are now logged in - {0}", user.UserId);
        }
        catch (InvalidOperationException)
        {
            message = "You must log in. Login Required";
        }

        var dialog = new MessageDialog(message);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
}
```

Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello [MobileServiceAuthenticationProvider] toohello wartość dla dostawcy.

W przepływie serwera usługi Azure App Service zarządza przepływ uwierzytelniania OAuth hello hello logowania strona hello wybranego dostawcy.  Raz zwraca hello do dostawcy tożsamości, usługa aplikacji Azure generuje token uwierzytelniania usługi aplikacji. Hello [LoginAsync] metoda zwraca [MobileServiceUser], co umożliwia zarówno hello [UserId] z hello uwierzytelniony użytkownik i hello [ MobileServiceAuthenticationToken], jako tokenu web JSON (JWT). Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie. Aby uzyskać więcej informacji, zobacz [token uwierzytelniania hello buforowanie](#caching).

### <a name="caching"></a>Token uwierzytelniania hello buforowania
W niektórych przypadkach metoda logowania toohello hello można uniknąć po pierwszym pomyślnym uwierzytelnieniu hello przechowując hello tokenu uwierzytelniania z hello dostawcy.  Aplikacje Sklepu Windows i platformy uniwersalnej systemu Windows mogą używać [PasswordVault] toocache bieżącego uwierzytelniania tokenu po pomyślnym zalogowaniu, w następujący sposób:

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

Hello UserId wartość jest przechowywana jako hello UserName hello poświadczeń i hello token jest hello przechowywane jako hello hasła. Na kolejnych rozruchów, możesz sprawdzić hello **PasswordVault** dla buforowanych poświadczeń. Witaj poniższy przykład korzysta buforowanych poświadczeń, gdy zostaną znalezione, a w przeciwnym razie próby tooauthenticate ponownie, podając hello wewnętrznej bazy danych:

```
// Try tooretrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create hello current user from hello stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache hello token as shown above.
}
```

Po zalogowaniu się użytkownika należy również usunąć hello przechowywanych poświadczeń, w następujący sposób:

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

Aplikacje platformy Xamarin używać hello [Xamarin.Auth] interfejsów API toosecurely magazynu poświadczeń w **konta** obiektu. Na przykład za pomocą tych interfejsów API, zobacz hello [AuthStore.cs] pliku kodu w hello [udostępniania próbki zdjęć ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).

Korzystając z uwierzytelniania zarządzanych przez klienta, można buforować tokenu dostępu hello uzyskane od dostawcy, takich jak Facebook lub Twitter. Token ten może być dostarczony toorequest nowy token uwierzytelniania z zaplecza hello w następujący sposób:

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <a name="pushnotifications"></a>Powiadomienia wypychane
Witaj następujących tematach opisano powiadomień wypychanych:

* [Zarejestruj się, aby powiadomienia wypychane](#register-for-push)
* [Uzyskaj identyfikator SID pakietu Sklepu Windows](#package-sid)
* [Rejestrowanie przy użyciu szablonów i platform](#register-xplat)

### <a name="register-for-push"></a>Porady: rejestrowanie się w celu powiadomienia wypychane
powitania klienta Mobile Apps umożliwia tooregister dla powiadomień wypychanych przy użyciu usługi Azure Notification Hubs. Podczas rejestrowania, można uzyskać dojścia uzyskanej od specyficzne dla platformy hello Push Notification Service (PNS). Podczas tworzenia rejestracji hello, następnie podaj tę wartość, wraz ze wszystkimi tagami. Witaj następujący kod rejestruje aplikację systemu Windows dla powiadomień wypychanych hello powiadomienia usługi WNS (Windows):

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

Jeśli push tooWNS, a następnie należy [pobrania identyfikatora SID pakietu Sklepu Windows](#package-sid).  Aby uzyskać więcej informacji na temat aplikacji systemu Windows łącznie ze sposobem tooregister do rejestracji szablonów, zobacz [aplikacji tooyour powiadomień wypychanych Dodaj].

Żądanie tagi powitania klienta nie jest obsługiwana.  Tag żądań dyskretnie są usuwane z rejestracji.
W razie potrzeby tooregister urządzenia przy użyciu tagów, należy utworzyć niestandardowego interfejsu API, używającej hello API centra powiadomień tooperform hello rejestracji w Twoim imieniu.  [Wywołaj hello niestandardowego interfejsu API](#customapi) zamiast hello `RegisterNativeAsync()` metody.

### <a name="package-sid"></a>Porady: uzyskiwanie identyfikatora SID pakietu Sklepu Windows
Dla Włączanie powiadomień wypychanych w aplikacji ze Sklepu Windows wymagany jest identyfikator SID pakietu.  tooreceive pakietu identyfikatora SID, rejestrowanie aplikacji ze Sklepu Windows hello.

tooobtain tej wartości:

1. W programie Visual Studio Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows hello, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepu hello...** .
2. W Kreatorze powitania kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.
3. Po rejestracji aplikacji hello jest hello został pomyślnie utworzony, wybierz nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.
4. Zaloguj się za toohello [Centrum deweloperów systemu Windows] przy użyciu Account firmy Microsoft. W obszarze **Moje aplikacje**, kliknij przycisk hello rejestracji aplikacji utworzony.
5. Kliknij przycisk **Zarządzanie aplikacjami** > **tożsamości aplikacji**, a następnie przewiń w dół toofind Twojego **identyfikatora SID pakietu**.

Wiele zastosowań identyfikator SID pakietu hello traktować go jako identyfikatora URI, w którym to przypadku należy toouse *ms-app: / /* hello schemat. Zwróć uwagę na powitania wersji pakietu utworzonego przez łączenie tej wartości jako prefiks identyfikatora SID.

Xamarin aplikacje wymagają niektórych tooregister stanie toobe dodatkowy kod aplikacji uruchomionej na powitania z systemem iOS lub Android platform. Aby uzyskać więcej informacji zobacz temat powitania dla danej platformy:

* [Xamarin.Android](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [Xamarin.iOS](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <a name="register-xplat"></a>Porady: rejestr wypychania szablony toosend wieloplatformowych powiadomienia
Szablony tooregister Użyj hello `RegisterAsync()` metody za pomocą szablonów hello, w następujący sposób:

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

Szablony powinna być `JObject` typów i może zawierać wiele szablonów w hello następującego formatu JSON:

```
public JObject myTemplates()
{
    // single template for Windows Notification Service toast
    var template = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(message)</text></binding></visual></toast>";

    var templates = new JObject
    {
        ["generic-message"] = new JObject
        {
            ["body"] = template,
            ["headers"] = new JObject
            {
                ["X-WNS-Type"] = "wns/toast"
            },
            ["tags"] = new JArray()
        },
        ["more-templates"] = new JObject {...}
    };
    return templates;
}
```

Witaj metody **RegisterAsync()** również akceptuje dodatkowej Kafelki:

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

Wszystkie tagi są odrzucane optymalizacji podczas rejestracji dla zabezpieczeń. znaczniki tooadd tooinstallations lub szablonów w ramach instalacji, zobacz [Praca z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps].

powiadomienia toosend przy użyciu tych szablonów w zarejestrowany, można znaleźć toohello [interfejsów API centra powiadomień].

## <a name="misc"></a>Tematy dodatkowe
### <a name="errors"></a>Porady: obsługa błędów
Po wystąpieniu błędu w zapleczu hello, powitania klienta SDK zgłasza `MobileServiceInvalidOperationException`.  W poniższym przykładzie przedstawiono sposób toohandle wyjątek, który jest zwracany przez zaplecze hello:

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into hello database. When hello operation completes
    // and App Service has assigned an Id, hello item is added toohello CollectionView
    try
    {
        await todoTable.InsertAsync(todoItem);
        items.Add(todoItem);
    }
    catch (MobileServiceInvalidOperationException e)
    {
        // Handle error
    }
}
```

Innym przykładem dotyczącym warunki błędów można znaleźć w hello [Mobile Apps pliki przykładowe]. [LoggingHandler] przykład udostępnia delegata rejestrowania żądań hello toolog obsługi wykonywane toohello wewnętrznej bazy danych.

### <a name="headers"></a>Porady: dostosowywanie nagłówki żądań
toosupport scenariusza specyficzne dla aplikacji, może być konieczne toocustomize komunikację z hello zaplecza aplikacji mobilnej. Może na przykład chcesz tooadd niestandardowy nagłówek żądania wychodzącego tooevery lub nawet zmienić kody stanu odpowiedzi. Można użyć niestandardowego [DelegatingHandler]w hello poniższy przykład:

```
public async Task CallClientWithHandler()
{
    MobileServiceClient client = new MobileServiceClient("AppUrl", new MyHandler());
    IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
    var newItem = new TodoItem { Text = "Hello world", Complete = false };
    await todoTable.InsertAsync(newItem);
}

public class MyHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage>
        SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        // Change hello request-side here based on hello HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do hello request
        var response = await base.SendAsync(request, cancellationToken);

        // Change hello response-side here based on hello HttpResponseMessage

        // Return hello modified response
        return response;
    }
}
```


<!-- Anchors. -->


<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-windows-store-dotnet-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[4]: https://msdn.microsoft.com/en-us/library/azure/mt419521(v=azure.10).aspx
[5]: https://github.com/Azure-Samples
[6]: http://www.newtonsoft.com/json/help/html/Properties_T_Newtonsoft_Json_JsonPropertyAttribute.htm
[7]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[8]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[9]: https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/
[10]: http://www.symbolsource.org/
[11]: http://www.symbolsource.org/Public/Wiki/Using
[12]: https://msdn.microsoft.com/en-us/library/azure/microsoft.windowsazure.mobileservices.mobileserviceclient(v=azure.10).aspx

[aplikacji tooyour authentication Dodaj]: app-service-mobile-windows-store-dotnet-get-started-users.md
[w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md
[aplikacji tooyour powiadomień wypychanych Dodaj]: app-service-mobile-windows-store-dotnet-get-started-push.md
[zarejestrować Twojej aplikacji toouse logowania konta Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md
[jak tooconfigure aplikacji usługi dla usługi Active Directory logowania]: app-service-mobile-how-to-configure-active-directory-authentication.md

<!-- Microsoft URLs. -->
[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx
[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx
[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx
[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx
[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx
[Metoda GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx
[tworzy tabelę bez typu tooan odwołanie]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx
[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx
[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx
[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx
[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx
[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx
[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx
[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx
[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx
[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx
[zająć]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx
[wybierz]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx
[Pomiń]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx
[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx
[Nazwa użytkownika]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx
[gdzie]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx
[portalu Azure]: https://portal.azure.com/
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx
[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx
[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx
[Centrum deweloperów systemu Windows]: https://dev.windows.com/en-us/overview
[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx
[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx
[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
[interfejsów API centra powiadomień]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[Mobile Apps pliki przykładowe]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files
[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63

<!-- External URLs -->
[OData v3 dokumentacji]: http://www.odata.org/documentation/odata-version-3-0/
[Fiddler]: http://www.telerik.com/fiddler
[Json.NET]: http://www.newtonsoft.com/json
[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/
[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
