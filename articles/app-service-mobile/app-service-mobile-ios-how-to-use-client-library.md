---
title: "aaaHow tooUse iOS SDK dla usługi Azure Mobile Apps"
description: "Jak tooUse iOS SDK dla usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a><span data-ttu-id="1d03e-103">Jak iOS tooUse biblioteki klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="1d03e-103">How tooUse iOS Client Library for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

<span data-ttu-id="1d03e-104">Ten przewodnik zawiera wskazówki, tooperform typowych scenariuszy przy użyciu hello najnowszych [iOS Azure Mobile Apps SDK][1].</span><span class="sxs-lookup"><span data-stu-id="1d03e-104">This guide teaches you tooperform common scenarios using hello latest [Azure Mobile Apps iOS SDK][1].</span></span> <span data-ttu-id="1d03e-105">W przypadku nowych aplikacji mobilnej tooAzure najpierw zakończyć [Azure Mobile Apps Szybki Start] toocreate zaplecza, Utwórz tabelę i Pobierz projektu wbudowanych systemu iOS w programie Xcode.</span><span class="sxs-lookup"><span data-stu-id="1d03e-105">If you are new tooAzure Mobile Apps, first complete [Azure Mobile Apps Quick Start] toocreate a backend, create a table, and download a pre-built iOS Xcode project.</span></span> <span data-ttu-id="1d03e-106">W tym przewodniku możemy skupić się na powitania klienta z systemem iOS SDK.</span><span class="sxs-lookup"><span data-stu-id="1d03e-106">In this guide, we focus on hello client-side iOS SDK.</span></span> <span data-ttu-id="1d03e-107">toolearn więcej na temat hello SDK po stronie serwera na powitania wewnętrznej bazy danych, zobacz powitania serwera SDK HOWTOs.</span><span class="sxs-lookup"><span data-stu-id="1d03e-107">toolearn more about hello server-side SDK for hello backend, see hello Server SDK HOWTOs.</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="1d03e-108">Dokumentacja referencyjna</span><span class="sxs-lookup"><span data-stu-id="1d03e-108">Reference documentation</span></span>
<span data-ttu-id="1d03e-109">Witaj dokumentacji dla powitania klienta z systemem iOS SDK jest zlokalizowana tutaj: [iOS Azure Mobile Apps odwołanie klienta][2].</span><span class="sxs-lookup"><span data-stu-id="1d03e-109">hello reference documentation for hello iOS client SDK is located here: [Azure Mobile Apps iOS Client Reference][2].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="1d03e-110">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="1d03e-110">Supported Platforms</span></span>
<span data-ttu-id="1d03e-111">Hello iOS SDK obsługuje projekty języka Objective-C, Swift 2.2 projektów i Swift 2.3 projektów dla systemu iOS w wersji 8.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="1d03e-111">hello iOS SDK supports Objective-C projects, Swift 2.2 projects, and Swift 2.3 projects for iOS versions 8.0 or later.</span></span>

<span data-ttu-id="1d03e-112">Hello "serwer flow" uwierzytelnianie przy użyciu widoku sieci Web dla hello przedstawione interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1d03e-112">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="1d03e-113">W przypadku hello urządzenie nie jest możliwe toopresent WebView interfejsu użytkownika, innej metody uwierzytelniania jest wymagane, który jest poza zakresem hello hello produktu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-113">If hello device is not able toopresent a WebView UI, then another method of authentication is required that is outside hello scope of hello product.</span></span>  
<span data-ttu-id="1d03e-114">Zestaw SDK w związku z tym nie jest odpowiedni dla typu czujki lub podobnie ograniczeniami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1d03e-114">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="1d03e-115"><a name="Setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1d03e-115"><a name="Setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="1d03e-116">W tym przewodniku założono, że utworzono wewnętrznej bazie danych z tabeli.</span><span class="sxs-lookup"><span data-stu-id="1d03e-116">This guide assumes that you have created a backend with a table.</span></span> <span data-ttu-id="1d03e-117">W tym przewodniku przyjęto założenie, że ta tabela hello ma ten sam schemat jako tabele hello w tych samouczkach.</span><span class="sxs-lookup"><span data-stu-id="1d03e-117">This guide assumes that hello table has the same schema as hello tables in those tutorials.</span></span> <span data-ttu-id="1d03e-118">W tym przewodniku założono, że w kodzie, można się odwołać `MicrosoftAzureMobile.framework` i zaimportować `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-118">This guide also assumes that in your code, you reference `MicrosoftAzureMobile.framework` and import `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.</span></span>

## <span data-ttu-id="1d03e-119"><a name="create-client"></a>Porady: Tworzenie klienta</span><span class="sxs-lookup"><span data-stu-id="1d03e-119"><a name="create-client"></a>How to: Create Client</span></span>
<span data-ttu-id="1d03e-120">Utwórz tooaccess zaplecza Azure Mobile Apps w projekcie, `MSClient`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-120">tooaccess an Azure Mobile Apps backend in your project, create an `MSClient`.</span></span> <span data-ttu-id="1d03e-121">Zastąp `AppUrl` z adresem URL aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1d03e-121">Replace `AppUrl` with hello app URL.</span></span> <span data-ttu-id="1d03e-122">Można pozostawić `gatewayURLString` i `applicationKey` puste.</span><span class="sxs-lookup"><span data-stu-id="1d03e-122">You may leave `gatewayURLString` and `applicationKey` empty.</span></span> <span data-ttu-id="1d03e-123">Skonfigurowanie bramy uwierzytelniania wypełnić `gatewayURLString` o hello bramy w adresie URL.</span><span class="sxs-lookup"><span data-stu-id="1d03e-123">If you set up a gateway for authentication, populate `gatewayURLString` with hello gateway URL.</span></span>

<span data-ttu-id="1d03e-124">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-124">**Objective-C**:</span></span>

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

<span data-ttu-id="1d03e-125">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-125">**Swift**:</span></span>

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <span data-ttu-id="1d03e-126"><a name="table-reference"></a>Porady: Tworzenie tabeli odwołania</span><span class="sxs-lookup"><span data-stu-id="1d03e-126"><a name="table-reference"></a>How to: Create Table Reference</span></span>
<span data-ttu-id="1d03e-127">dane tooaccess lub aktualizacji, tworzy tabelę odwołania toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d03e-127">tooaccess or update data, create a reference toohello backend table.</span></span> <span data-ttu-id="1d03e-128">Zastąp `TodoItem` o nazwie hello tabeli</span><span class="sxs-lookup"><span data-stu-id="1d03e-128">Replace `TodoItem` with hello name of your table</span></span>

<span data-ttu-id="1d03e-129">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-129">**Objective-C**:</span></span>

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

<span data-ttu-id="1d03e-130">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-130">**Swift**:</span></span>

```
let table = client.tableWithName("TodoItem")
```


## <span data-ttu-id="1d03e-131"><a name="querying"></a>Porady: zapytania na danych</span><span class="sxs-lookup"><span data-stu-id="1d03e-131"><a name="querying"></a>How to: Query Data</span></span>
<span data-ttu-id="1d03e-132">toocreate kwerendę bazy danych zapytania hello `MSTable` obiektu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-132">toocreate a database query, query hello `MSTable` object.</span></span> <span data-ttu-id="1d03e-133">Witaj następujące zapytanie pobiera wszystkie elementy hello w `TodoItem` i dzienniki hello tekst każdego elementu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-133">hello following query gets all hello items in `TodoItem` and logs hello text of each item.</span></span>

<span data-ttu-id="1d03e-134">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-134">**Objective-C**:</span></span>

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1d03e-135">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-135">**Swift**:</span></span>

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="1d03e-136"><a name="filtering"></a>Porady: Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="1d03e-136"><a name="filtering"></a>How to: Filter Returned Data</span></span>
<span data-ttu-id="1d03e-137">wyniki toofilter, istnieje wiele dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-137">toofilter results, there are many available options.</span></span>

<span data-ttu-id="1d03e-138">używając predykatu, użyj toofilter `NSPredicate` i `readWithPredicate`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-138">toofilter using a predicate, use an `NSPredicate` and `readWithPredicate`.</span></span> <span data-ttu-id="1d03e-139">następujące Hello filtruje dane zwrotne toofind tylko niezakończonych elementów Todo.</span><span class="sxs-lookup"><span data-stu-id="1d03e-139">hello following filters returned data toofind only incomplete Todo items.</span></span>

<span data-ttu-id="1d03e-140">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-140">**Objective-C**:</span></span>

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1d03e-141">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-141">**Swift**:</span></span>

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <span data-ttu-id="1d03e-142"><a name="query-object"></a>Porady: Użyj MSQuery</span><span class="sxs-lookup"><span data-stu-id="1d03e-142"><a name="query-object"></a>How to: Use MSQuery</span></span>
<span data-ttu-id="1d03e-143">tooperform Tworzenie złożonego zapytania (w tym sortowanie i stronicowanie), `MSQuery` obiekt bezpośrednio lub za pomocą predykat:</span><span class="sxs-lookup"><span data-stu-id="1d03e-143">tooperform a complex query (including sorting and paging), create an `MSQuery` object, directly or by using a predicate:</span></span>

<span data-ttu-id="1d03e-144">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-144">**Objective-C**:</span></span>

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

<span data-ttu-id="1d03e-145">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-145">**Swift**:</span></span>

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

<span data-ttu-id="1d03e-146">`MSQuery`Umożliwia sterowanie różne zachowania zapytania.</span><span class="sxs-lookup"><span data-stu-id="1d03e-146">`MSQuery` lets you control several query behaviors.</span></span>

* <span data-ttu-id="1d03e-147">Określ kolejność wyników</span><span class="sxs-lookup"><span data-stu-id="1d03e-147">Specify order of results</span></span>
* <span data-ttu-id="1d03e-148">Limit, które pola tooreturn</span><span class="sxs-lookup"><span data-stu-id="1d03e-148">Limit which fields tooreturn</span></span>
* <span data-ttu-id="1d03e-149">Ogranicz liczbę rekordów tooreturn</span><span class="sxs-lookup"><span data-stu-id="1d03e-149">Limit how many records tooreturn</span></span>
* <span data-ttu-id="1d03e-150">Określ liczbę całkowitą w odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="1d03e-150">Specify total count in response</span></span>
* <span data-ttu-id="1d03e-151">Określ parametry ciągu zapytania niestandardowe w żądaniu</span><span class="sxs-lookup"><span data-stu-id="1d03e-151">Specify custom query string parameters in request</span></span>
* <span data-ttu-id="1d03e-152">Zastosuj dodatkowe funkcje</span><span class="sxs-lookup"><span data-stu-id="1d03e-152">Apply additional functions</span></span>

<span data-ttu-id="1d03e-153">Wykonanie `MSQuery` zapytania przez wywołanie metody `readWithCompletion` hello obiektu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-153">Execute an `MSQuery` query by calling `readWithCompletion` on hello object.</span></span>

## <span data-ttu-id="1d03e-154"><a name="sorting"></a>Porady: sortowanie danych za pomocą MSQuery</span><span class="sxs-lookup"><span data-stu-id="1d03e-154"><a name="sorting"></a>How to: Sort Data with MSQuery</span></span>
<span data-ttu-id="1d03e-155">wyniki toosort Przyjrzyjmy się przykładem.</span><span class="sxs-lookup"><span data-stu-id="1d03e-155">toosort results, let's look at an example.</span></span> <span data-ttu-id="1d03e-156">Wywołanie toosort rosnącej pola 'text', a następnie "Pełna" malejąco `MSQuery` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d03e-156">toosort by field 'text' ascending, then by 'complete' descending, invoke `MSQuery` like so:</span></span>

<span data-ttu-id="1d03e-157">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-157">**Objective-C**:</span></span>

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

<span data-ttu-id="1d03e-158">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-158">**Swift**:</span></span>

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <span data-ttu-id="1d03e-159"><a name="selecting"></a><a name="parameters"></a>Porady: ograniczyć pól i parametrów ciągu zapytania z MSQuery rozwiń</span><span class="sxs-lookup"><span data-stu-id="1d03e-159"><a name="selecting"></a><a name="parameters"></a>How to: Limit Fields and Expand Query String Parameters with MSQuery</span></span>
<span data-ttu-id="1d03e-160">toobe pola toolimit zwracane w zapytaniu, określ hello nazwy pól hello w hello **selectFields** właściwości.</span><span class="sxs-lookup"><span data-stu-id="1d03e-160">toolimit fields toobe returned in a query, specify hello names of hello fields in hello **selectFields** property.</span></span> <span data-ttu-id="1d03e-161">W tym przykładzie zwraca tylko tekst hello i wypełnionego pola:</span><span class="sxs-lookup"><span data-stu-id="1d03e-161">This example returns only hello text and completed fields:</span></span>

<span data-ttu-id="1d03e-162">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-162">**Objective-C**:</span></span>

```
query.selectFields = @[@"text", @"complete"];
```

<span data-ttu-id="1d03e-163">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-163">**Swift**:</span></span>

```
query.selectFields = ["text", "complete"]
```

<span data-ttu-id="1d03e-164">parametrów ciągu zapytania dodatkowe tooinclude Server hello żądania (na przykład, ponieważ używa niestandardowego skryptu po stronie serwera, ich), wypełnij `query.parameters` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1d03e-164">tooinclude additional query string parameters in hello server request (for example, because a custom server-side script uses them), populate `query.parameters` like so:</span></span>

<span data-ttu-id="1d03e-165">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-165">**Objective-C**:</span></span>

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

<span data-ttu-id="1d03e-166">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-166">**Swift**:</span></span>

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <span data-ttu-id="1d03e-167"><a name="paging"></a>Porady: Konfigurowanie rozmiar strony</span><span class="sxs-lookup"><span data-stu-id="1d03e-167"><a name="paging"></a>How to: Configure Page Size</span></span>
<span data-ttu-id="1d03e-168">Z usługą Azure Mobile Apps formantów rozmiar strony hello hello liczba rekordów, które są pobierane w czasie z hello tabel wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d03e-168">With Azure Mobile Apps, hello page size controls hello number of records that are pulled at a time from hello backend tables.</span></span> <span data-ttu-id="1d03e-169">A wywołać zbyt`pull` zapasową danych na podstawie tej strony rozmiaru, dopóki nie ma żadnych więcej rekordów toopull następnie partii danych.</span><span class="sxs-lookup"><span data-stu-id="1d03e-169">A call too`pull` data would then batch up data, based on this page size, until there are no more records toopull.</span></span>

<span data-ttu-id="1d03e-170">Jest możliwe tooconfigure rozmiar strony przy użyciu **MSPullSettings** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1d03e-170">It's possible tooconfigure a page size using **MSPullSettings** as shown below.</span></span> <span data-ttu-id="1d03e-171">Domyślny rozmiar strony Hello wynosi 50, a w poniższym przykładzie hello zmienia too3.</span><span class="sxs-lookup"><span data-stu-id="1d03e-171">hello default page size is 50, and hello example below changes it too3.</span></span>

<span data-ttu-id="1d03e-172">Można skonfigurować inny rozmiar strony ze względu na wydajność.</span><span class="sxs-lookup"><span data-stu-id="1d03e-172">You could configure a different page size for performance reasons.</span></span> <span data-ttu-id="1d03e-173">Jeśli masz dużą liczbę rekordów danych mały rozmiar strony wysokiej zmniejsza hello liczbę operacji serwera.</span><span class="sxs-lookup"><span data-stu-id="1d03e-173">If you have a large number of small data records, a high page size reduces hello number of server round-trips.</span></span>

<span data-ttu-id="1d03e-174">To ustawienie określa tylko rozmiar strony hello na powitania po stronie klienta.</span><span class="sxs-lookup"><span data-stu-id="1d03e-174">This setting controls only hello page size on hello client side.</span></span> <span data-ttu-id="1d03e-175">Jeśli hello klient żąda większy rozmiar strony nie obsługuje hello zaplecza aplikacji mobilnej, rozmiar strony hello jest ograniczona do maksymalnej hello hello wewnętrznej bazy danych jest toosupport skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="1d03e-175">If hello client asks for a larger page size than hello Mobile Apps backend supports, hello page size is capped at hello maximum hello backend is configured toosupport.</span></span>

<span data-ttu-id="1d03e-176">To ustawienie jest również hello *numer* rekordów danych nie hello *rozmiar w bajtach*.</span><span class="sxs-lookup"><span data-stu-id="1d03e-176">This setting is also hello *number* of data records, not hello *byte size*.</span></span>

<span data-ttu-id="1d03e-177">Zwiększenie rozmiaru strony powitania klienta, należy również zwiększyć rozmiar strony hello na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="1d03e-177">If you increase hello client page size, you should also increase hello page size on hello server.</span></span> <span data-ttu-id="1d03e-178">Zobacz ["porady: dopasowywanie hello tabeli stronicowania"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) dla hello kroki toodo to.</span><span class="sxs-lookup"><span data-stu-id="1d03e-178">See ["How to: Adjust hello table paging size"](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for hello steps toodo this.</span></span>

<span data-ttu-id="1d03e-179">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-179">**Objective-C**:</span></span>

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


<span data-ttu-id="1d03e-180">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-180">**Swift**:</span></span>

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <span data-ttu-id="1d03e-181"><a name="inserting"></a>Porady: wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="1d03e-181"><a name="inserting"></a>How to: Insert Data</span></span>
<span data-ttu-id="1d03e-182">Utwórz tooinsert nowego wiersza tabeli, `NSDictionary` i wywoływać `table insert`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-182">tooinsert a new table row, create a `NSDictionary` and invoke `table insert`.</span></span> <span data-ttu-id="1d03e-183">Jeśli [dynamiczne schematu] jest włączona, hello zaplecza aplikacji mobilnych usługi aplikacji Azure automatycznie generuje nowe kolumny oparte na powitania `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-183">If [Dynamic Schema] is enabled, hello Azure App Service mobile backend automatically generates new columns based on hello `NSDictionary`.</span></span>

<span data-ttu-id="1d03e-184">Jeśli `id` nie zostanie podany, zaplecza hello automatycznie generuje nowy unikatowy identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1d03e-184">If `id` is not provided, hello backend automatically generates a new unique ID.</span></span> <span data-ttu-id="1d03e-185">Podaj własny `id` toouse e-mail adresy, nazwy użytkowników lub własne wartości jako identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="1d03e-185">Provide your own `id` toouse email addresses, usernames, or your own custom values as ID.</span></span> <span data-ttu-id="1d03e-186">Własnego Identyfikatora zapewnienie może ułatwić sprzężenia i logiki firmowe bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d03e-186">Providing your own ID may ease joins and business-oriented database logic.</span></span>

<span data-ttu-id="1d03e-187">Witaj `result` zawiera hello nowy element, który został wstawiony.</span><span class="sxs-lookup"><span data-stu-id="1d03e-187">hello `result` contains hello new item that was inserted.</span></span> <span data-ttu-id="1d03e-188">Zależnie od logiki serwera mogą mieć dodatkowe lub zmodyfikowane dane w porównaniu toowhat przekazano toohello serwera.</span><span class="sxs-lookup"><span data-stu-id="1d03e-188">Depending on your server logic, it may have additional or modified data compared toowhat was passed toohello server.</span></span>

<span data-ttu-id="1d03e-189">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-189">**Objective-C**:</span></span>

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1d03e-190">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-190">**Swift**:</span></span>

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <span data-ttu-id="1d03e-191"><a name="modifying"></a>Porady: modyfikowanie danych</span><span class="sxs-lookup"><span data-stu-id="1d03e-191"><a name="modifying"></a>How to: Modify Data</span></span>
<span data-ttu-id="1d03e-192">tooupdate istniejącego wiersza, zmodyfikuj element i wywołanie `update`:</span><span class="sxs-lookup"><span data-stu-id="1d03e-192">tooupdate an existing row, modify an item and call `update`:</span></span>

<span data-ttu-id="1d03e-193">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-193">**Objective-C**:</span></span>

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1d03e-194">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-194">**Swift**:</span></span>

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

<span data-ttu-id="1d03e-195">Można również podać identyfikator wiersza hello i pola hello zaktualizowane:</span><span class="sxs-lookup"><span data-stu-id="1d03e-195">Alternatively, supply hello row ID and hello updated field:</span></span>

<span data-ttu-id="1d03e-196">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-196">**Objective-C**:</span></span>

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

<span data-ttu-id="1d03e-197">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-197">**Swift**:</span></span>

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

<span data-ttu-id="1d03e-198">Co najmniej hello `id` należy ustawić podczas wprowadzania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-198">At minimum, hello `id` attribute must be set when making updates.</span></span>

## <span data-ttu-id="1d03e-199"><a name="deleting"></a>Porady: usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="1d03e-199"><a name="deleting"></a>How to: Delete Data</span></span>
<span data-ttu-id="1d03e-200">Wywołanie toodelete element, `delete` z elementem hello:</span><span class="sxs-lookup"><span data-stu-id="1d03e-200">toodelete an item, invoke `delete` with hello item:</span></span>

<span data-ttu-id="1d03e-201">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-201">**Objective-C**:</span></span>

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="1d03e-202">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-202">**Swift**:</span></span>

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="1d03e-203">Alternatywnie usunięcia, podając identyfikator wiersza:</span><span class="sxs-lookup"><span data-stu-id="1d03e-203">Alternatively, delete by providing a row ID:</span></span>

<span data-ttu-id="1d03e-204">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-204">**Objective-C**:</span></span>

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

<span data-ttu-id="1d03e-205">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-205">**Swift**:</span></span>

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

<span data-ttu-id="1d03e-206">Co najmniej hello `id` atrybut musi być ustawiony w przypadku usunięcia wprowadzania.</span><span class="sxs-lookup"><span data-stu-id="1d03e-206">At minimum, hello `id` attribute must be set when making deletes.</span></span>

## <span data-ttu-id="1d03e-207"><a name="customapi"></a>Porady: wywołanie niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1d03e-207"><a name="customapi"></a>How to: Call Custom API</span></span>
<span data-ttu-id="1d03e-208">Z niestandardowego interfejsu API pozwala udostępnić wszystkie funkcje wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1d03e-208">With a custom API, you can expose any backend functionality.</span></span> <span data-ttu-id="1d03e-209">Nie ma operacji tabeli tooa toomap.</span><span class="sxs-lookup"><span data-stu-id="1d03e-209">It doesn't have toomap tooa table operation.</span></span> <span data-ttu-id="1d03e-210">Nie tylko możesz uzyskać większą kontrolę nad wiadomości, można nawet odczytu/ustawiania nagłówków i zmień format treści odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="1d03e-210">Not only do you gain more control over messaging, you can even read/set headers and change hello response body format.</span></span> <span data-ttu-id="1d03e-211">toolearn, w jaki sposób odczytać toocreate niestandardowego interfejsu API hello wewnętrznej bazy danych, [niestandardowych interfejsów API](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span><span class="sxs-lookup"><span data-stu-id="1d03e-211">toolearn how toocreate a custom API on hello backend, read [Custom APIs](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)</span></span>

<span data-ttu-id="1d03e-212">Wywołanie toocall niestandardowego interfejsu API `MSClient.invokeAPI`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-212">toocall a custom API, call `MSClient.invokeAPI`.</span></span> <span data-ttu-id="1d03e-213">Witaj żądań i odpowiedzi zawartości są traktowane jako JSON.</span><span class="sxs-lookup"><span data-stu-id="1d03e-213">hello request and response content are treated as JSON.</span></span> <span data-ttu-id="1d03e-214">toouse inne typy nośników [Użyj hello inne przeciążenia `invokeAPI` ] [ 5].</span><span class="sxs-lookup"><span data-stu-id="1d03e-214">toouse other media types, [use hello other overload of `invokeAPI`][5].</span></span>  <span data-ttu-id="1d03e-215">toomake `GET` żądania zamiast `POST` żądania, ustaw parametr `HTTPMethod` za`"GET"` i parametru `body` zbyt`nil` (ponieważ żądania GET nie ma treści wiadomości.) Niestandardowy interfejs API obsługuje inne zleceń HTTP, zmiana `HTTPMethod` odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="1d03e-215">toomake a `GET` request instead of a `POST` request, set parameter `HTTPMethod` too`"GET"` and parameter `body` too`nil` (since GET requests do not have message bodies.) If your custom API supports other HTTP verbs, change `HTTPMethod` appropriately.</span></span>

<span data-ttu-id="1d03e-216">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-216">**Objective-C**:</span></span>

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

<span data-ttu-id="1d03e-217">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-217">**Swift**:</span></span>

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <span data-ttu-id="1d03e-218"><a name="templates"></a>Porady: rejestr wypychania szablony toosend wieloplatformowych powiadomienia</span><span class="sxs-lookup"><span data-stu-id="1d03e-218"><a name="templates"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="1d03e-219">Szablony tooregister przekazać szablony z Twojej **client.push registerDeviceToken** metody w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="1d03e-219">tooregister templates, pass templates with your **client.push registerDeviceToken** method in your client app.</span></span>

<span data-ttu-id="1d03e-220">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-220">**Objective-C**:</span></span>

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

<span data-ttu-id="1d03e-221">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-221">**Swift**:</span></span>

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

<span data-ttu-id="1d03e-222">Szablony typu NSDictionary i mogą zawierać wiele szablonów w hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="1d03e-222">Your templates are of type NSDictionary and can contain multiple templates in hello following format:</span></span>

<span data-ttu-id="1d03e-223">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-223">**Objective-C**:</span></span>

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

<span data-ttu-id="1d03e-224">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-224">**Swift**:</span></span>

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

<span data-ttu-id="1d03e-225">Wszystkie tagi są usuwane z żądania hello zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1d03e-225">All tags are stripped from hello request for security.</span></span>  <span data-ttu-id="1d03e-226">znaczniki tooadd tooinstallations lub szablonów w ramach instalacji, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps][4].</span><span class="sxs-lookup"><span data-stu-id="1d03e-226">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps][4].</span></span>  <span data-ttu-id="1d03e-227">toosend powiadomienia za pomocą tych szablonów zarejestrowanych pracować z [interfejsów API centra powiadomień][3].</span><span class="sxs-lookup"><span data-stu-id="1d03e-227">toosend notifications using these registered templates, work with [Notification Hubs APIs][3].</span></span>

## <span data-ttu-id="1d03e-228"><a name="errors"></a>Porady: obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="1d03e-228"><a name="errors"></a>How to: Handle Errors</span></span>
<span data-ttu-id="1d03e-229">Podczas wywoływania zaplecze aplikacji mobilnej Azure App Service zawiera bloku ukończenia hello `NSError` parametru.</span><span class="sxs-lookup"><span data-stu-id="1d03e-229">When you call an Azure App Service mobile backend, hello completion block contains an `NSError` parameter.</span></span> <span data-ttu-id="1d03e-230">Gdy wystąpi błąd, ten parametr jest tokenem nil.</span><span class="sxs-lookup"><span data-stu-id="1d03e-230">When an error occurs, this parameter is non-nil.</span></span> <span data-ttu-id="1d03e-231">W kodzie należy sprawdzić ten parametr i obsługi błędu hello zgodnie z potrzebami, jak pokazano w hello poprzedzających fragmentów kodu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-231">In your code, you should check this parameter and handle hello error as needed, as demonstrated in hello preceding code snippets.</span></span>

<span data-ttu-id="1d03e-232">Plik Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] definiuje stałe hello `MSErrorResponseKey`, `MSErrorRequestKey`, i `MSErrorServerItemKey`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-232">hello file [`<WindowsAzureMobileServices/MSError.h>`][6] defines hello constants `MSErrorResponseKey`, `MSErrorRequestKey`, and `MSErrorServerItemKey`.</span></span> <span data-ttu-id="1d03e-233">tooget toohello błąd związany z większej ilości danych:</span><span class="sxs-lookup"><span data-stu-id="1d03e-233">tooget more data related toohello error:</span></span>

<span data-ttu-id="1d03e-234">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-234">**Objective-C**:</span></span>

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

<span data-ttu-id="1d03e-235">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-235">**Swift**:</span></span>

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

<span data-ttu-id="1d03e-236">Ponadto plik hello definiuje stałe dla każdego kod błędu:</span><span class="sxs-lookup"><span data-stu-id="1d03e-236">In addition, hello file defines constants for each error code:</span></span>

<span data-ttu-id="1d03e-237">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-237">**Objective-C**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

<span data-ttu-id="1d03e-238">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-238">**Swift**:</span></span>

```
if (error.code == MSErrorPreconditionFailed) {
```

## <span data-ttu-id="1d03e-239"><a name="adal"></a>Porady: uwierzytelniać użytkowników za pomocą hello biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1d03e-239"><a name="adal"></a>How to: Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="1d03e-240">Witaj Active Directory Authentication Library (ADAL) toosign użytkowników służy do aplikacji przy użyciu usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1d03e-240">You can use hello Active Directory Authentication Library (ADAL) toosign users into your application using Azure Active Directory.</span></span> <span data-ttu-id="1d03e-241">Przepływ uwierzytelnianie przy użyciu dostawcy tożsamości zestawu SDK jest preferowana toousing hello `loginWithProvider:completion:` metody.</span><span class="sxs-lookup"><span data-stu-id="1d03e-241">Client flow authentication using an identity provider SDK is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="1d03e-242">Uwierzytelnianie klienta przepływu zapewnia bardziej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="1d03e-242">Client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1d03e-243">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] [ 7] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-243">Configure your mobile app backend for AAD sign-in by following hello [How tooconfigure App Service for Active Directory login][7] tutorial.</span></span> <span data-ttu-id="1d03e-244">Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="1d03e-244">Make sure toocomplete hello optional step of registering a native client application.</span></span> <span data-ttu-id="1d03e-245">Dla systemu iOS, zaleca się tym przekierowania hello URI ma formę hello `<app-scheme>://<bundle-id>`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-245">For iOS, we recommend that hello redirect URI is of hello form `<app-scheme>://<bundle-id>`.</span></span> <span data-ttu-id="1d03e-246">Aby uzyskać więcej informacji, zobacz hello [ADAL dla systemu iOS — Szybki Start][8].</span><span class="sxs-lookup"><span data-stu-id="1d03e-246">For more information, see hello [ADAL iOS quickstart][8].</span></span>
2. <span data-ttu-id="1d03e-247">Instalowanie przy użyciu programu Cocoapods biblioteki ADAL.</span><span class="sxs-lookup"><span data-stu-id="1d03e-247">Install ADAL using Cocoapods.</span></span> <span data-ttu-id="1d03e-248">Edytuj hello tooinclude Podfile po definicji, zastępując **YOUR PROJECT** o nazwie hello projektu Xcode:</span><span class="sxs-lookup"><span data-stu-id="1d03e-248">Edit your Podfile tooinclude hello following definition, replacing **YOUR-PROJECT** with hello name of your Xcode project:</span></span>

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   <span data-ttu-id="1d03e-249">i hello Pod:</span><span class="sxs-lookup"><span data-stu-id="1d03e-249">and hello Pod:</span></span>

        pod 'ADALiOS'
3. <span data-ttu-id="1d03e-250">Przy użyciu hello Terminal, uruchom `pod install` z katalogu hello zawierający projektu, a następnie otwórz wygenerowany hello obszaru roboczego Xcode (nie projekt hello).</span><span class="sxs-lookup"><span data-stu-id="1d03e-250">Using hello Terminal, run `pod install` from hello directory containing your project, and then open hello generated Xcode workspace (not hello project).</span></span>
4. <span data-ttu-id="1d03e-251">Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1d03e-251">Add hello following code tooyour application, according toohello language you are using.</span></span> <span data-ttu-id="1d03e-252">W każdym należy te elementy zastępcze:</span><span class="sxs-lookup"><span data-stu-id="1d03e-252">In each, make these replacements:</span></span>

   * <span data-ttu-id="1d03e-253">Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-253">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="1d03e-254">Format powinien być https://login.microsoftonline.com/contoso.onmicrosoft.com. Ta wartość może zostać skopiowany z hello kartę domeny w usłudze Azure Active Directory w hello [klasyczny portal Azure].</span><span class="sxs-lookup"><span data-stu-id="1d03e-254">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="1d03e-255">Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1d03e-255">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="1d03e-256">Identyfikator klienta można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="1d03e-256">You can obtain the client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="1d03e-257">Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="1d03e-257">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="1d03e-258">Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1d03e-258">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="1d03e-259">Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="1d03e-259">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

<span data-ttu-id="1d03e-260">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-260">**Objective-C**:</span></span>

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


<span data-ttu-id="1d03e-261">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-261">**Swift**:</span></span>

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <span data-ttu-id="1d03e-262"><a name="facebook-sdk"></a>Porady: uwierzytelniać użytkowników za pomocą hello Facebook zestawu SDK dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1d03e-262"><a name="facebook-sdk"></a>How to: Authenticate users with hello Facebook SDK for iOS</span></span>
<span data-ttu-id="1d03e-263">Witaj zestawu SDK usługi Facebook dla użytkowników systemu iOS toosign służy do aplikacji za pomocą usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="1d03e-263">You can use hello Facebook SDK for iOS toosign users into your application using Facebook.</span></span>  <span data-ttu-id="1d03e-264">Przy użyciu uwierzytelniania przepływu klienta jest preferowana toousing hello `loginWithProvider:completion:` metody.</span><span class="sxs-lookup"><span data-stu-id="1d03e-264">Using a client flow authentication is preferable toousing hello `loginWithProvider:completion:` method.</span></span>  <span data-ttu-id="1d03e-265">powitania klienta przepływ uwierzytelniania zapewnia bardziej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="1d03e-265">hello client flow authentication provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1d03e-266">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w witrynie Facebook, wykonując [jak tooconfigure aplikacji usługi Facebook logowania] [ 9] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-266">Configure your mobile app backend for Facebook sign-in by following the [How tooconfigure App Service for Facebook login][9] tutorial.</span></span>
2. <span data-ttu-id="1d03e-267">Zainstaluj hello Facebook zestawu SDK dla systemu iOS przez następujące hello [Facebook SDK dla systemu iOS — wprowadzenie] [ 10] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-267">Install hello Facebook SDK for iOS by following hello [Facebook SDK for iOS - Getting Started][10] documentation.</span></span> <span data-ttu-id="1d03e-268">Zamiast tworzenia aplikacji, można dodać hello iOS platform tooyour istniejącej rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-268">Instead of creating an app, you can add hello iOS platform tooyour existing registration.</span></span>
3. <span data-ttu-id="1d03e-269">Dokumentacja w serwisie Facebook zawiera kod języka Objective-C w hello delegata aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-269">Facebook's documentation includes some Objective-C code in hello App Delegate.</span></span> <span data-ttu-id="1d03e-270">Jeśli używasz **Swift**, można użyć następującego tłumaczenia AppDelegate.swift hello:</span><span class="sxs-lookup"><span data-stu-id="1d03e-270">If you are using **Swift**, you can use hello following translations for AppDelegate.swift:</span></span>

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. <span data-ttu-id="1d03e-271">W dodatku tooadding `FBSDKCoreKit.framework` tooyour projektu, również dodać odwołanie za`FBSDKLoginKit.framework` w hello tak samo.</span><span class="sxs-lookup"><span data-stu-id="1d03e-271">In addition tooadding `FBSDKCoreKit.framework` tooyour project, also add a reference too`FBSDKLoginKit.framework` in hello same way.</span></span>
5. <span data-ttu-id="1d03e-272">Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1d03e-272">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="1d03e-273">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-273">**Objective-C**:</span></span>

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

<span data-ttu-id="1d03e-274">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-274">**Swift**:</span></span>

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <span data-ttu-id="1d03e-275"><a name="twitter-fabric"></a>Porady: uwierzytelniać użytkowników za pomocą usługi Twitter sieci szkieletowej dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1d03e-275"><a name="twitter-fabric"></a>How to: Authenticate users with Twitter Fabric for iOS</span></span>
<span data-ttu-id="1d03e-276">Sieci szkieletowej dla użytkowników systemu iOS toosign służy do aplikacji przy użyciu usługi Twitter.</span><span class="sxs-lookup"><span data-stu-id="1d03e-276">You can use Fabric for iOS toosign users into your application using Twitter.</span></span> <span data-ttu-id="1d03e-277">Uwierzytelnianie przepływu klienta jest preferowanym toousing hello `loginWithProvider:completion:` metody, ponieważ zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="1d03e-277">Client Flow authentication is preferable toousing hello `loginWithProvider:completion:` method, as it provides a more native UX feel and allows for additional customization.</span></span>

1. <span data-ttu-id="1d03e-278">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w serwisie Twitter przy powitania po [jak tooconfigure aplikacji usługi Twitter logowania](app-service-mobile-how-to-configure-twitter-authentication.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-278">Configure your mobile app backend for Twitter sign-in by following hello [How tooconfigure App Service for Twitter login](app-service-mobile-how-to-configure-twitter-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="1d03e-279">Dodaj projekt tooyour sieci szkieletowej przez następujące hello [sieci szkieletowej dla systemu iOS — wprowadzenie] dokumentacji i konfigurując TwitterKit.</span><span class="sxs-lookup"><span data-stu-id="1d03e-279">Add Fabric tooyour project by following hello [Fabric for iOS - Getting Started] documentation and setting up TwitterKit.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1d03e-280">Domyślnie sieci szkieletowej tworzy aplikację usługi Twitter dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="1d03e-280">By default, Fabric creates a Twitter application for you.</span></span> <span data-ttu-id="1d03e-281">Można uniknąć tworzenia aplikacji, rejestrując hello klucz klienta i klucz tajny klienta został utworzony wcześniej przy użyciu powitania po wstawki kodu.</span><span class="sxs-lookup"><span data-stu-id="1d03e-281">You can avoid creating an application by registering hello Consumer Key and Consumer Secret you created earlier using hello following code snippets.</span></span>    <span data-ttu-id="1d03e-282">Alternatywnie można zastąpić hello konsumenta i tooApp usługi z hello wartości, należy podać wartości klucz tajny klienta, zobacz w hello [pulpitu nawigacyjnego sieci szkieletowej].</span><span class="sxs-lookup"><span data-stu-id="1d03e-282">Alternatively, you can replace hello Consumer Key and Consumer Secret values that you provide tooApp Service with hello values you see in hello [Fabric Dashboard].</span></span> <span data-ttu-id="1d03e-283">Jeśli wybierzesz tę opcję, należy się tooset hello wywołania zwrotnego adresu URL tooa wartości symbolu zastępczego, takich jak `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span><span class="sxs-lookup"><span data-stu-id="1d03e-283">If you choose this option, be sure tooset hello callback URL tooa placeholder value, such as `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.</span></span>
   >
   >

    <span data-ttu-id="1d03e-284">Jeśli wybierzesz toouse hello klucze tajne, utworzony wcześniej, Dodaj następujące tooyour kodu delegata aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="1d03e-284">If you choose toouse hello secrets you created earlier, add hello following code tooyour App Delegate:</span></span>

    <span data-ttu-id="1d03e-285">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-285">**Objective-C**:</span></span>

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    <span data-ttu-id="1d03e-286">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-286">**Swift**:</span></span>

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. <span data-ttu-id="1d03e-287">Dodaj hello następującego kodu tooyour aplikacji, zgodnie z toohello język, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="1d03e-287">Add hello following code tooyour application, according toohello language you are using.</span></span>

<span data-ttu-id="1d03e-288">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-288">**Objective-C**:</span></span>

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

<span data-ttu-id="1d03e-289">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-289">**Swift**:</span></span>

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <span data-ttu-id="1d03e-290"><a name="google-sdk"></a>Porady: uwierzytelniać użytkowników za pomocą hello Google logowania zestawu SDK dla systemu iOS</span><span class="sxs-lookup"><span data-stu-id="1d03e-290"><a name="google-sdk"></a>How to: Authenticate users with hello Google Sign-In SDK for iOS</span></span>
<span data-ttu-id="1d03e-291">Hello Google logowania zestawu SDK dla systemu iOS toosign użytkowników służy do aplikacji przy użyciu konta Google.</span><span class="sxs-lookup"><span data-stu-id="1d03e-291">You can use hello Google Sign-In SDK for iOS toosign users into your application using a Google account.</span></span>  <span data-ttu-id="1d03e-292">Google zapowiedziała niedawno zasady zabezpieczeń OAuth tootheir zmiany.</span><span class="sxs-lookup"><span data-stu-id="1d03e-292">Google recently announced changes tootheir OAuth security policies.</span></span>  <span data-ttu-id="1d03e-293">Te zmiany zasad wymaga stosowania hello zestaw SDK Google w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="1d03e-293">These policy changes will require hello use of the Google SDK in hello future.</span></span>

1. <span data-ttu-id="1d03e-294">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w witrynie Google przez następujące hello [jak tooconfigure aplikacji usługi Google logowania](app-service-mobile-how-to-configure-google-authentication.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-294">Configure your mobile app backend for Google sign-in by following hello [How tooconfigure App Service for Google login](app-service-mobile-how-to-configure-google-authentication.md) tutorial.</span></span>
2. <span data-ttu-id="1d03e-295">Zainstaluj hello Google zestawu SDK dla systemu iOS przez następujące hello [Google logowania dla systemu iOS — rozpocząć integrowanie](https://developers.google.com/identity/sign-in/ios/start-integrating) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-295">Install hello Google SDK for iOS by following hello [Google Sign-In for iOS - Start integrating](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation.</span></span> <span data-ttu-id="1d03e-296">Możesz pominąć hello sekcji "Uwierzytelnianie z serwera wewnętrznej bazy danych".</span><span class="sxs-lookup"><span data-stu-id="1d03e-296">You may skip hello "Authenticate with a Backend Server" section.</span></span>
3. <span data-ttu-id="1d03e-297">Dodaj powitania po delegata tooyour `signIn:didSignInForUser:withError:` metody, zgodnie z toohello języka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-297">Add hello following tooyour delegate's `signIn:didSignInForUser:withError:` method, according toohello language you are using.</span></span>

<span data-ttu-id="1d03e-298">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-298">**Objective-C**:</span></span>

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

<span data-ttu-id="1d03e-299">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-299">**Swift**:</span></span>

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. <span data-ttu-id="1d03e-300">Upewnij się, że można również dodać powitania po zbyt`application:didFinishLaunchingWithOptions:` w aplikacji delegować, zastępując "SERVER_CLIENT_ID" hello sam identyfikator tej należy używać tooconfigure App Service w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="1d03e-300">Make sure you also add hello following too`application:didFinishLaunchingWithOptions:` in your app delegate, replacing "SERVER_CLIENT_ID" with hello same ID that you used tooconfigure App Service in step 1.</span></span>

<span data-ttu-id="1d03e-301">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-301">**Objective-C**:</span></span>

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 <span data-ttu-id="1d03e-302">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-302">**Swift**:</span></span>

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. <span data-ttu-id="1d03e-303">Dodaj następującego kodu aplikacji tooyour UIViewController, który implementuje hello hello `GIDSignInUIDelegate` protokołu, zgodnie z toohello języka.</span><span class="sxs-lookup"><span data-stu-id="1d03e-303">Add hello following code tooyour application in a UIViewController that implements hello `GIDSignInUIDelegate` protocol, according toohello language you are using.</span></span>  <span data-ttu-id="1d03e-304">Zalogowano przed Trwa logowanie ponownie, a mimo że nie ma potrzeby tooenter poświadczenia ponownie, zobacz okno dialogowe zgody.</span><span class="sxs-lookup"><span data-stu-id="1d03e-304">You are signed out before being signed in again, and although you don't need tooenter your credentials again, you see a consent dialog.</span></span>  <span data-ttu-id="1d03e-305">Tę metodę należy wywoływać tylko wtedy, gdy wygaśnie hello tokenu sesji.</span><span class="sxs-lookup"><span data-stu-id="1d03e-305">Only call this method when hello session token has expired.</span></span>

   <span data-ttu-id="1d03e-306">**Objective-C**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-306">**Objective-C**:</span></span>

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   <span data-ttu-id="1d03e-307">**Kod SWIFT**:</span><span class="sxs-lookup"><span data-stu-id="1d03e-307">**Swift**:</span></span>

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[Azure Mobile Apps Szybki Start]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[dynamiczne schematu]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[pulpitu nawigacyjnego sieci szkieletowej]: https://www.fabric.io/home
[sieci szkieletowej dla systemu iOS — wprowadzenie]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
