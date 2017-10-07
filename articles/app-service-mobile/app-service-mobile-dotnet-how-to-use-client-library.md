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
# <a name="how-toouse-hello-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="38b69-103">Jak toouse hello zarządzanego klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="38b69-103">How toouse hello managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="38b69-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="38b69-104">Overview</span></span>
<span data-ttu-id="38b69-105">W tym przewodniku przedstawiono sposób tooperform typowych scenariuszy przy użyciu hello zarządzania biblioteki klienta dla aplikacji usługi Azure App Service Mobile aplikacji dla systemu Windows i Xamarin.</span><span class="sxs-lookup"><span data-stu-id="38b69-105">This guide shows you how tooperform common scenarios using hello managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="38b69-106">W przypadku nowych aplikacji tooMobile należy rozważyć pierwszy hello Kończenie [szybkiego startu usługi Azure Mobile Apps] [ 1] samouczka.</span><span class="sxs-lookup"><span data-stu-id="38b69-106">If you are new tooMobile Apps, you should consider first completing hello [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="38b69-107">W tym przewodniku, możemy skupić się na powitania klienta zarządzanego zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="38b69-107">In this guide, we focus on hello client-side managed SDK.</span></span> <span data-ttu-id="38b69-108">toolearn więcej na temat hello zestawów SDK po stronie serwera dla Mobile Apps, zobacz dokumentację hello na powitania [.NET SDK serwera] [ 2] lub [Node.js Server SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="38b69-108">toolearn more about hello server-side SDKs for Mobile Apps, see hello documentation for hello [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="38b69-109">Dokumentacja referencyjna</span><span class="sxs-lookup"><span data-stu-id="38b69-109">Reference documentation</span></span>
<span data-ttu-id="38b69-110">Witaj dokumentacji powitania klienta SDK znajduje się tutaj: [odwołania klienta usługi Azure Mobile Apps .NET][4].</span><span class="sxs-lookup"><span data-stu-id="38b69-110">hello reference documentation for hello client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="38b69-111">Możesz również znaleźć kilka przykładów klienta w hello [repozytorium GitHub przykłady Azure][5].</span><span class="sxs-lookup"><span data-stu-id="38b69-111">You can also find several client samples in hello [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="38b69-112">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="38b69-112">Supported Platforms</span></span>
<span data-ttu-id="38b69-113">Witaj platformy .NET obsługuje hello następujące platformy:</span><span class="sxs-lookup"><span data-stu-id="38b69-113">hello .NET Platform supports hello following platforms:</span></span>

* <span data-ttu-id="38b69-114">Dla systemu Xamarin Android wersje interfejsu API 19 do 24 (KitKat za pośrednictwem nugacie)</span><span class="sxs-lookup"><span data-stu-id="38b69-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="38b69-115">Zwalnia systemu Xamarin iOS dla systemu iOS w wersji 8.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="38b69-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="38b69-116">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38b69-116">Universal Windows Platform</span></span>
* <span data-ttu-id="38b69-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="38b69-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="38b69-118">Windows Phone 8.0, z wyjątkiem aplikacji Silverlight</span><span class="sxs-lookup"><span data-stu-id="38b69-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="38b69-119">Hello "serwer flow" uwierzytelnianie przy użyciu widoku sieci Web dla hello przedstawione interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38b69-119">hello "server-flow" authentication uses a WebView for hello presented UI.</span></span>  <span data-ttu-id="38b69-120">Jeśli hello urządzenie nie jest możliwe toopresent UI widoku sieci Web, potrzebne są inne metody uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="38b69-120">If hello device is not able toopresent a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="38b69-121">Zestaw SDK w związku z tym nie jest odpowiedni dla typu czujki lub podobnie ograniczeniami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="38b69-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="38b69-122"><a name="setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="38b69-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="38b69-123">Przyjęto założenie, że możesz już utworzono i opublikowano projektu zaplecza aplikacji mobilnej, który zawiera co najmniej jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="38b69-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="38b69-124">W kodzie hello używane w tym temacie, nosi nazwę tabeli hello `TodoItem` i ma hello następujące kolumny: `Id`, `Text`, i `Complete`.</span><span class="sxs-lookup"><span data-stu-id="38b69-124">In hello code used in this topic, hello table is named `TodoItem` and it has hello following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="38b69-125">Ta tabela jest hello tej samej tabeli utworzone po zakończeniu [szybkiego startu usługi Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="38b69-125">This table is hello same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="38b69-126">Witaj odpowiedniego typu po stronie klienta typu w języku C# jest hello następujące klasy:</span><span class="sxs-lookup"><span data-stu-id="38b69-126">hello corresponding typed client-side type in C# is hello following class:</span></span>

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

<span data-ttu-id="38b69-127">Witaj [JsonPropertyAttribute] [ 6] jest używane toodefine hello *PropertyName* mapowanie między powitania klienta hello tabeli pola i.</span><span class="sxs-lookup"><span data-stu-id="38b69-127">hello [JsonPropertyAttribute][6] is used toodefine hello *PropertyName* mapping between hello client field and hello table field.</span></span>

<span data-ttu-id="38b69-128">toolearn jak toocreate tabel w zapleczu swojej Mobile Apps, zobacz hello [temacie .NET SDK serwera] [ 7] lub hello [tematu Node.js Server SDK] [ 8] .</span><span class="sxs-lookup"><span data-stu-id="38b69-128">toolearn how toocreate tables in your Mobile Apps backend, see hello [.NET Server SDK topic][7] or hello [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="38b69-129">Jeśli utworzono zaplecza aplikacji mobilnej hello Azure za pomocą portalu hello szybkiego startu, można również użyć hello **łatwe tabel** ustawienie w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="38b69-129">If you created your Mobile App backend in hello Azure portal using hello QuickStart, you can also use hello **Easy tables** setting in hello [Azure portal].</span></span>

### <a name="how-to-install-hello-managed-client-sdk-package"></a><span data-ttu-id="38b69-130">Porady: hello instalacji zarządzany pakiet SDK klienta</span><span class="sxs-lookup"><span data-stu-id="38b69-130">How to: Install hello managed client SDK package</span></span>
<span data-ttu-id="38b69-131">Użyj hello następujące metody tooinstall hello zarządzany pakiet SDK klienta dla aplikacji mobilnych z [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="38b69-131">Use one of hello following methods tooinstall hello managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="38b69-132">**Visual Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj hello `Microsoft.Azure.Mobile.Client` pakietu, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="38b69-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="38b69-133">**Program Xamarin Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj** > **Dodawanie pakietów NuGet**, wyszukaj hello `Microsoft.Azure.Mobile.Client `pakietu, a następnie kliknij przycisk **Dodaj Pakiet**.</span><span class="sxs-lookup"><span data-stu-id="38b69-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for hello `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="38b69-134">W pliku głównym działaniu Pamiętaj następujące hello tooadd **przy użyciu** instrukcji:</span><span class="sxs-lookup"><span data-stu-id="38b69-134">In your main activity file, remember tooadd hello following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="38b69-135"><a name="symbolsource"></a>Porady: Praca z symboli debugowania w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38b69-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="38b69-136">są dostępne na powitania symbole dla przestrzeni nazw Microsoft.Azure.Mobile hello [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="38b69-136">hello symbols for hello Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="38b69-137">Zobacz toothe [instrukcje SymbolSource] [ 11] toointegrate SymbolSource z programem Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38b69-137">Refer toothe [SymbolSource instructions][11] toointegrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="38b69-138"><a name="create-client"></a>Utwórz powitania klienta Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="38b69-138"><a name="create-client"></a>Create hello Mobile Apps client</span></span>
<span data-ttu-id="38b69-139">Witaj poniższy kod tworzy hello [MobileServiceClient] [ 12] obiekt, który jest używany tooaccess zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-139">hello following code creates hello [MobileServiceClient][12] object that is used tooaccess your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="38b69-140">W hello poprzedzających kodu, Zastąp `MOBILE_APP_URL` z adresem URL hello hello zaplecza aplikacji mobilnej, który znajduje się w bloku dla zaplecza aplikacji mobilnej w hello [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="38b69-140">In hello preceding code, replace `MOBILE_APP_URL` with hello URL of hello Mobile App backend, which is found in the blade for your Mobile App backend in hello [Azure portal].</span></span> <span data-ttu-id="38b69-141">Obiekt MobileServiceClient Hello powinna być klasą pojedynczą.</span><span class="sxs-lookup"><span data-stu-id="38b69-141">hello MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="38b69-142">Praca z tabelami</span><span class="sxs-lookup"><span data-stu-id="38b69-142">Work with Tables</span></span>
<span data-ttu-id="38b69-143">Witaj, jak poniższe informacje sekcji toosearch i pobieranie rekordów i modyfikowanie danych hello hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="38b69-143">hello following section details how toosearch and retrieve records and modify hello data within hello table.</span></span>  <span data-ttu-id="38b69-144">obejmuje Hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="38b69-144">hello following topics are covered:</span></span>

* [<span data-ttu-id="38b69-145">Tworzenie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="38b69-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="38b69-146">Dane zapytania</span><span class="sxs-lookup"><span data-stu-id="38b69-146">Query data</span></span>](#querying)
* [<span data-ttu-id="38b69-147">Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="38b69-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="38b69-148">Sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="38b69-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="38b69-149">Zwróć dane strony</span><span class="sxs-lookup"><span data-stu-id="38b69-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="38b69-150">Wybrać określone kolumny</span><span class="sxs-lookup"><span data-stu-id="38b69-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="38b69-151">Wyszukaj według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="38b69-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="38b69-152">Dotyczących zapytań bez typu</span><span class="sxs-lookup"><span data-stu-id="38b69-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="38b69-153">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="38b69-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="38b69-154">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="38b69-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="38b69-155">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="38b69-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="38b69-156">Rozwiązywanie konfliktów i optymistycznej współbieżności</span><span class="sxs-lookup"><span data-stu-id="38b69-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="38b69-157">Powiązanie tooa interfejsu użytkownika systemu Windows</span><span class="sxs-lookup"><span data-stu-id="38b69-157">Binding tooa Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="38b69-158">Zmiana rozmiaru strony hello</span><span class="sxs-lookup"><span data-stu-id="38b69-158">Changing hello Page Size</span></span>](#pagesize)

### <span data-ttu-id="38b69-159"><a name="instantiating"></a>Porady: Tworzenie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="38b69-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="38b69-160">Cały kod hello, który uzyskuje dostęp do lub modyfikuje dane w tabeli wewnętrznej bazy danych wymaga funkcji na powitania `MobileServiceTable` obiektu.</span><span class="sxs-lookup"><span data-stu-id="38b69-160">All hello code that accesses or modifies data in a backend table calls functions on hello `MobileServiceTable` object.</span></span> <span data-ttu-id="38b69-161">Uzyskaj odwołanie do tabeli toohello za hello wywoływania [Metoda GetTable] metody, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-161">Obtain a reference toohello table by calling hello [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="38b69-162">Witaj zwrócony obiekt używa hello serializacji typu modelu.</span><span class="sxs-lookup"><span data-stu-id="38b69-162">hello returned object uses hello typed serialization model.</span></span> <span data-ttu-id="38b69-163">Obsługiwane jest również modelem serializacji bez typu.</span><span class="sxs-lookup"><span data-stu-id="38b69-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="38b69-164">Poniższy przykład [tworzy tabelę bez typu tooan odwołanie]:</span><span class="sxs-lookup"><span data-stu-id="38b69-164">The following example [creates a reference tooan untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="38b69-165">W zapytaniach bez typu należy określić hello bazowy ciągu zapytania OData.</span><span class="sxs-lookup"><span data-stu-id="38b69-165">In untyped queries, you must specify hello underlying OData query string.</span></span>

### <span data-ttu-id="38b69-166"><a name="querying"></a>Porady: zapytania na danych z aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="38b69-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="38b69-167">W tej sekcji opisano, jak tooissue odpytuje toohello zaplecza aplikacji mobilnej, która obejmuje następujące funkcje hello:</span><span class="sxs-lookup"><span data-stu-id="38b69-167">This section describes how tooissue queries toohello Mobile App backend, which includes hello following functionality:</span></span>

* [<span data-ttu-id="38b69-168">Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="38b69-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="38b69-169">Sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="38b69-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="38b69-170">Zwróć dane strony</span><span class="sxs-lookup"><span data-stu-id="38b69-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="38b69-171">Wybrać określone kolumny</span><span class="sxs-lookup"><span data-stu-id="38b69-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="38b69-172">Wyszukiwać dane według Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="38b69-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="38b69-173">Rozmiar strony oparte na serwerze jest wymuszone tooprevent wszystkich wierszy zwracanych.</span><span class="sxs-lookup"><span data-stu-id="38b69-173">A server-driven page size is enforced tooprevent all rows from being returned.</span></span>  <span data-ttu-id="38b69-174">Stronicowania zachowuje żądań domyślny dla dużych zestawów danych z niekorzystnego wpływu na powitania usługi.</span><span class="sxs-lookup"><span data-stu-id="38b69-174">Paging keeps default requests for large data sets from negatively impacting hello service.</span></span>  <span data-ttu-id="38b69-175">tooreturn więcej niż 50 wierszy, użyj hello `Skip` i `Take` metody, zgodnie z opisem w [zwrócić dane na stronach](#paging).</span><span class="sxs-lookup"><span data-stu-id="38b69-175">tooreturn more than 50 rows, use hello `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="38b69-176"><a name="filtering"></a>Porady: Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="38b69-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="38b69-177">Witaj poniższy kod ilustruje sposób danych toofilter, umieszczając w niej `Where` klauzuli w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="38b69-177">hello following code illustrates how toofilter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="38b69-178">Zwraca wszystkie elementy z `todoTable` których `Complete` właściwości jest równa za`false`.</span><span class="sxs-lookup"><span data-stu-id="38b69-178">It returns all items from `todoTable` whose `Complete` property is equal too`false`.</span></span> <span data-ttu-id="38b69-179">Witaj [gdzie] funkcja ma zastosowanie filtrowania predykatu do hello zapytania dotyczącego tabeli hello wiersza.</span><span class="sxs-lookup"><span data-stu-id="38b69-179">hello [Where] function applies a row filtering predicate to hello query against hello table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="38b69-180">Możesz wyświetlić hello URI hello żądanie wysłane toohello wewnętrznej bazy danych za pomocą komunikatów inspekcji oprogramowania, takich jak narzędzia dla deweloperów w przeglądarce lub [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="38b69-180">You can view hello URI of hello request sent toohello backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="38b69-181">Jeśli przyjrzymy się identyfikator URI żądania hello, zwróć uwagę zmodyfikowania ciągu kwerendy hello:</span><span class="sxs-lookup"><span data-stu-id="38b69-181">If you look at hello request URI, notice that hello query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="38b69-182">To żądanie OData jest przekształcana na kwerendę SQL przez powitania serwera SDK:</span><span class="sxs-lookup"><span data-stu-id="38b69-182">This OData request is translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="38b69-183">Funkcja, która została przekazana toohello Hello `Where` metody może mieć dowolną liczbę warunków.</span><span class="sxs-lookup"><span data-stu-id="38b69-183">hello function that is passed toohello `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="38b69-184">W tym przykładzie będzie można przetłumaczyć kwerendę SQL przez powitania serwera SDK:</span><span class="sxs-lookup"><span data-stu-id="38b69-184">This example would be translated into an SQL query by hello Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="38b69-185">To zapytanie również może zostać podzielony na wiele klauzul:</span><span class="sxs-lookup"><span data-stu-id="38b69-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="38b69-186">Witaj dwie metody są równoważne i mogą być używane zamiennie.</span><span class="sxs-lookup"><span data-stu-id="38b69-186">hello two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="38b69-187">Witaj wcześniejsze opcji&mdash;z łączenie wielu predykatów w jednym zapytaniu&mdash;jest bardziej compact i zalecanym.</span><span class="sxs-lookup"><span data-stu-id="38b69-187">hello former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="38b69-188">Witaj `Where` klauzuli obsługuje operacje, które można przetłumaczyć hello podzestawu OData.</span><span class="sxs-lookup"><span data-stu-id="38b69-188">hello `Where` clause supports operations that be translated into hello OData subset.</span></span> <span data-ttu-id="38b69-189">Dostępne są następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="38b69-189">Operations include:</span></span>

* <span data-ttu-id="38b69-190">Operatory relacyjne (==,! =, <, < =, >, > =),</span><span class="sxs-lookup"><span data-stu-id="38b69-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="38b69-191">Operatory arytmetyczne (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="38b69-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="38b69-192">Liczba precision (Math.Floor —, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="38b69-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="38b69-193">Funkcje ciągów (długość, Substring, Zamień, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="38b69-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="38b69-194">Data właściwości (rok, miesiąc, dzień, godzina, minuty, sekundy),</span><span class="sxs-lookup"><span data-stu-id="38b69-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="38b69-195">Dostęp do właściwości obiektu i</span><span class="sxs-lookup"><span data-stu-id="38b69-195">Access properties of an object, and</span></span>
* <span data-ttu-id="38b69-196">Każdej z tych operacji łączenia wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="38b69-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="38b69-197">Gdy biorąc pod uwagę co hello serwera SDK obsługuje, można rozważyć hello [OData v3 dokumentacji].</span><span class="sxs-lookup"><span data-stu-id="38b69-197">When considering what hello Server SDK supports, you can consider hello [OData v3 Documentation].</span></span>

### <span data-ttu-id="38b69-198"><a name="sorting"></a>Porady: sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="38b69-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="38b69-199">Witaj poniższy kod ilustruje sposób danych toosort, umieszczając w niej [OrderBy] lub [OrderByDescending] funkcji w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-199">hello following code illustrates how toosort data by including an [OrderBy] or [OrderByDescending] function in hello query.</span></span> <span data-ttu-id="38b69-200">Zwraca elementy z `todoTable` sortowane rosnąco przez hello `Text` pola.</span><span class="sxs-lookup"><span data-stu-id="38b69-200">It returns items from `todoTable` sorted ascending by hello `Text` field.</span></span>

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

### <span data-ttu-id="38b69-201"><a name="paging"></a>Porady: zwrócić dane na stronach</span><span class="sxs-lookup"><span data-stu-id="38b69-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="38b69-202">Domyślnie program hello wewnętrznej bazy danych zwraca tylko hello 50 pierwszych wierszy.</span><span class="sxs-lookup"><span data-stu-id="38b69-202">By default, hello backend returns only hello first 50 rows.</span></span> <span data-ttu-id="38b69-203">Można zwiększyć hello liczbę wierszy zwróconych przez wywołanie hello [zająć] metody.</span><span class="sxs-lookup"><span data-stu-id="38b69-203">You can increase hello number of returned rows by calling hello [Take] method.</span></span> <span data-ttu-id="38b69-204">Użyj `Take` wraz z hello [Pomiń] toorequest metody określonej "strony" hello całkowita zestawu danych zwróconych przez zapytanie hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-204">Use `Take` along with hello [Skip] method toorequest a specific "page" of hello total dataset returned by hello query.</span></span> <span data-ttu-id="38b69-205">Witaj następującej kwerendy, po wykonaniu zwraca hello pierwszych trzech elementów hello tabeli.</span><span class="sxs-lookup"><span data-stu-id="38b69-205">hello following query, when executed, returns hello top three items in hello table.</span></span>

```
// Define a filtered query that returns hello top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="38b69-206">Hello następujące zapytanie poprawione pomija hello pierwsze trzy wyniki i zwraca hello trzech kolejnych wyników.</span><span class="sxs-lookup"><span data-stu-id="38b69-206">hello following revised query skips hello first three results and returns hello next three results.</span></span> <span data-ttu-id="38b69-207">To zapytanie tworzy hello drugi "page" danych, których rozmiar strony hello jest trzy elementy.</span><span class="sxs-lookup"><span data-stu-id="38b69-207">This query produces hello second "page" of data, where hello page size is three items.</span></span>

```
// Define a filtered query that skips hello top 3 items and returns hello next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="38b69-208">Witaj [IncludeTotalCount] metoda żąda hello łączną liczbę dla *wszystkie* hello rekordów, które mogłyby być zwracane, ignorowanie klauzuli stronicowania/limit określony:</span><span class="sxs-lookup"><span data-stu-id="38b69-208">hello [IncludeTotalCount] method requests hello total count for *all* hello records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="38b69-209">W aplikacji rzeczywistych można użyć zapytania toohello podobne poprzedzających przykład z formantem pagera lub porównywalny interfejsu użytkownika do przechodzenia między stronami.</span><span class="sxs-lookup"><span data-stu-id="38b69-209">In a real world app, you can use queries similar toohello preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="38b69-210">limit wierszy 50 hello toooverride w zaplecza aplikacji mobilnej, należy także zastosować hello [EnableQueryAttribute] toohello publicznego GET, metoda i Określ zachowanie stronicowania hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-210">toooverride hello 50-row limit in a Mobile App backend, you must also apply hello [EnableQueryAttribute] toohello public GET method and specify hello paging behavior.</span></span> <span data-ttu-id="38b69-211">Gdy metoda toohello zastosowane, powitania po ustawia too1000 maksymalna liczba wierszy zwróconych:</span><span class="sxs-lookup"><span data-stu-id="38b69-211">When applied toohello method, hello following sets the maximum returned rows too1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="38b69-212"><a name="selecting"></a>Porady: Wybieranie określonych kolumn</span><span class="sxs-lookup"><span data-stu-id="38b69-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="38b69-213">Można określić, który zestaw właściwości tooinclude w hello powoduje dodanie [wybierz] klauzuli tooyour zapytania.</span><span class="sxs-lookup"><span data-stu-id="38b69-213">You can specify which set of properties tooinclude in hello results by adding a [Select] clause tooyour query.</span></span> <span data-ttu-id="38b69-214">Na przykład Witaj następującego kodu pokazuje sposób tooselect tylko jednego pola, a także sposób tooselect i formatowanie wielu pól:</span><span class="sxs-lookup"><span data-stu-id="38b69-214">For example, hello following code shows how tooselect just one field and also how tooselect and format multiple fields:</span></span>

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

<span data-ttu-id="38b69-215">Witaj wszystkie funkcje do tej pory opisane są addytywne, dlatego firma Microsoft może zapewnić łańcucha je.</span><span class="sxs-lookup"><span data-stu-id="38b69-215">All hello functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="38b69-216">Każde wywołanie łańcuchowa ma wpływ na więcej hello zapytania.</span><span class="sxs-lookup"><span data-stu-id="38b69-216">Each chained call affects more of hello query.</span></span> <span data-ttu-id="38b69-217">Przykładem więcej:</span><span class="sxs-lookup"><span data-stu-id="38b69-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="38b69-218"><a name="lookingup"></a>Porady: wyszukiwanie danych według Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="38b69-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="38b69-219">Witaj [LookupAsync] funkcja może być używane toolook zapasową obiektów z bazy danych hello o określonym identyfikatorze.</span><span class="sxs-lookup"><span data-stu-id="38b69-219">hello [LookupAsync] function can be used toolook up objects from hello database with a particular ID.</span></span>

```
// This query filters out hello item with hello ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="38b69-220"><a name="untypedqueries"></a>Porady: wykonywanie zapytań bez typu</span><span class="sxs-lookup"><span data-stu-id="38b69-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="38b69-221">Podczas wykonywania zapytania za pomocą obiektu tabeli bez typu, należy jawnie określić ciąg zapytania OData hello, wywołując [ReadAsync]w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="38b69-221">When executing a query using an untyped table object, you must explicitly specify hello OData query string by calling [ReadAsync], as in hello following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="38b69-222">Możesz odzyskać wartości JSON, które można używać jak zbioru właściwości.</span><span class="sxs-lookup"><span data-stu-id="38b69-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="38b69-223">Aby uzyskać więcej informacji na JToken i Newtonsoft Json.NET, zobacz hello [Json.NET] lokacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-223">For more information on JToken and Newtonsoft Json.NET, see hello [Json.NET] site.</span></span>

### <span data-ttu-id="38b69-224"><a name="inserting"></a>Porady: wstawianie danych do zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="38b69-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="38b69-225">Wszystkie typy klientów musi zawierać element członkowski o nazwie **identyfikator**, który jest domyślnie ciąg.</span><span class="sxs-lookup"><span data-stu-id="38b69-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="38b69-226">To **identyfikator** jest wymagane do przeprowadzenia operacji CRUD i dla synchronizacji w trybie offline. hello następującego kodu ilustruje sposób toouse hello [InsertAsync] metody tooinsert nowych wierszy do tabeli.</span><span class="sxs-lookup"><span data-stu-id="38b69-226">This **Id** is required to perform CRUD operations and for offline sync. hello following code illustrates how toouse hello [InsertAsync] method tooinsert new rows into a table.</span></span> <span data-ttu-id="38b69-227">Parametr Hello zawiera hello toobe dane wstawiane jak dla obiektu .NET.</span><span class="sxs-lookup"><span data-stu-id="38b69-227">hello parameter contains hello data toobe inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="38b69-228">Jeśli wartość Unikatowy identyfikator niestandardowych nie jest objęta hello `todoItem` podczas wstawiania identyfikator GUID jest generowany przez serwer hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-228">If a unique custom ID value is not included in hello `todoItem` during an insert, a GUID is generated by hello server.</span></span>
<span data-ttu-id="38b69-229">Możesz pobrać hello generowany identyfikator sprawdzając hello obiektu po wywołaniu hello zwraca.</span><span class="sxs-lookup"><span data-stu-id="38b69-229">You can retrieve hello generated Id by inspecting hello object after hello call returns.</span></span>

<span data-ttu-id="38b69-230">tooinsert bez typu danych, użytkownik może skorzystać z Json.NET:</span><span class="sxs-lookup"><span data-stu-id="38b69-230">tooinsert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="38b69-231">Oto przykład przy użyciu adresu e-mail jako identyfikator unikatowy ciąg:</span><span class="sxs-lookup"><span data-stu-id="38b69-231">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="38b69-232">Praca z wartościami identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="38b69-232">Working with ID values</span></span>
<span data-ttu-id="38b69-233">Aplikacje mobilne obsługuje wartości unikatowe niestandardowy ciąg hello tabeli **identyfikator** kolumny.</span><span class="sxs-lookup"><span data-stu-id="38b69-233">Mobile Apps supports unique custom string values for hello table's **id** column.</span></span> <span data-ttu-id="38b69-234">Wartość ciągu umożliwia aplikacjom toouse wartości niestandardowych, takich jak adresy e-mail lub nazwy użytkownika dla identyfikatora hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-234">A string value allows applications toouse custom values such as email addresses or user names for hello ID.</span></span>  <span data-ttu-id="38b69-235">Identyfikatory ciągów dostarczyć hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="38b69-235">String IDs provide you with hello following benefits:</span></span>

* <span data-ttu-id="38b69-236">Identyfikatory są generowane bez wprowadzania toohello obiegu bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-236">IDs are generated without making a round trip toohello database.</span></span>
* <span data-ttu-id="38b69-237">Rekordy są łatwiejsze toomerge z różnych tabel lub baz danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-237">Records are easier toomerge from different tables or databases.</span></span>
* <span data-ttu-id="38b69-238">Wartości identyfikatorów można lepiej zintegrować z logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-238">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="38b69-239">Jeśli wartość Identyfikatora ciągu nie jest ustawiony na wstawionego rekordu, zaplecza aplikacji mobilnej hello generuje unikatową wartość dla identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="38b69-239">When a string ID value is not set on an inserted record, hello Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="38b69-240">Można użyć hello [Guid.NewGuid] toogenerate metody własnego Identyfikatora wartości na powitania klienta lub w hello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-240">You can use hello [Guid.NewGuid] method toogenerate your own ID values, either on hello client or in hello backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="38b69-241"><a name="modifying"></a>Porady: modyfikowanie danych w zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="38b69-241"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="38b69-242">Witaj poniższy kod ilustruje sposób toouse hello [UpdateAsync] tooupdate metody istniejący rekord z hello sam identyfikator nowymi informacjami.</span><span class="sxs-lookup"><span data-stu-id="38b69-242">hello following code illustrates how toouse hello [UpdateAsync] method tooupdate an existing record with hello same ID with new information.</span></span> <span data-ttu-id="38b69-243">Parametr Hello zawiera toobe danych hello zaktualizowane jak dla obiektu .NET.</span><span class="sxs-lookup"><span data-stu-id="38b69-243">hello parameter contains hello data toobe updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="38b69-244">tooupdate bez typu danych, użytkownik może skorzystać z [Json.NET] w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-244">tooupdate untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="38b69-245">`id` Należy podać wartość pola podczas wprowadzania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-245">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="38b69-246">Hello wewnętrznej bazy danych używa hello `id` tooidentify pola, które tooupdate wiersz.</span><span class="sxs-lookup"><span data-stu-id="38b69-246">hello backend uses hello `id` field tooidentify which row tooupdate.</span></span> <span data-ttu-id="38b69-247">Witaj `id` pola można uzyskać od wyniku hello hello `InsertAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="38b69-247">hello `id` field can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="38b69-248">`ArgumentException` Jest wywoływane przy próbie tooupdate elementu bez podawania hello `id` wartość.</span><span class="sxs-lookup"><span data-stu-id="38b69-248">An `ArgumentException` is raised if you try tooupdate an item without providing hello `id` value.</span></span>

### <span data-ttu-id="38b69-249"><a name="deleting"></a>Porady: usuwanie danych zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="38b69-249"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="38b69-250">Witaj poniższy kod ilustruje sposób toouse hello [DeleteAsync] toodelete metody istniejącego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="38b69-250">hello following code illustrates how toouse hello [DeleteAsync] method toodelete an existing instance.</span></span> <span data-ttu-id="38b69-251">wystąpienie Hello jest identyfikowane przez hello `id` pola zestawu na powitania `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="38b69-251">hello instance is identified by hello `id` field set on hello `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="38b69-252">toodelete bez typu danych, użytkownik może skorzystać z struktury Json.NET w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-252">toodelete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="38b69-253">Po wprowadzeniu żądanie usunięcia, należy określić identyfikator.</span><span class="sxs-lookup"><span data-stu-id="38b69-253">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="38b69-254">Inne właściwości nie są one przekazywane toohello usługi lub są ignorowane w hello usług.</span><span class="sxs-lookup"><span data-stu-id="38b69-254">Other properties are not passed toohello service or are ignored at hello service.</span></span> <span data-ttu-id="38b69-255">Witaj wynik `DeleteAsync` wywołanie jest zwykle `null`.</span><span class="sxs-lookup"><span data-stu-id="38b69-255">hello result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="38b69-256">toopass identyfikator Hello w można uzyskać od wyniku hello hello `InsertAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="38b69-256">hello ID toopass in can be obtained from hello result of hello `InsertAsync` call.</span></span> <span data-ttu-id="38b69-257">A `MobileServiceInvalidOperationException` jest generowany, gdy spróbujesz toodelete elementu bez określania hello `id` pola.</span><span class="sxs-lookup"><span data-stu-id="38b69-257">A `MobileServiceInvalidOperationException` is thrown when you try toodelete an item without specifying hello `id` field.</span></span>

### <span data-ttu-id="38b69-258"><a name="optimisticconcurrency"></a>Porady: użycie optymistycznej współbieżności do rozwiązywania konfliktów</span><span class="sxs-lookup"><span data-stu-id="38b69-258"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="38b69-259">Dwa lub więcej klientów może zapisać zmian toohello sam element na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="38b69-259">Two or more clients may write changes toohello same item at hello same time.</span></span> <span data-ttu-id="38b69-260">Bez wykrywania konfliktów hello ostatniego zapisu zastąpiłaby wszelkie poprzednie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="38b69-260">Without conflict detection, hello last write would overwrite any previous updates.</span></span> <span data-ttu-id="38b69-261">**Optymistyczne sterowanie współbieżnością** założono, że każdej transakcji można zatwierdzić i dlatego nie używa żadnych zasobów blokowania.</span><span class="sxs-lookup"><span data-stu-id="38b69-261">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="38b69-262">Przed zatwierdzeniem transakcji, optymistyczne sterowanie współbieżnością sprawdza, czy nie inne transakcje nie zmienione hello danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-262">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified hello data.</span></span> <span data-ttu-id="38b69-263">W przypadku modyfikacji danych hello hello zatwierdzania transakcji została wycofana.</span><span class="sxs-lookup"><span data-stu-id="38b69-263">If hello data has been modified, hello committing transaction is rolled back.</span></span>

<span data-ttu-id="38b69-264">Aplikacje mobilne obsługuje optymistyczne sterowanie współbieżnością za śledzenia zmian elementu tooeach przy użyciu hello `version` kolumny właściwości systemu, który jest zdefiniowany dla każdej tabeli w zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-264">Mobile Apps supports optimistic concurrency control by tracking changes tooeach item using hello `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="38b69-265">Przy każdym aktualizacji rekordu Mobile Apps ustawia hello `version` właściwości w tym rejestrowania tooa nową wartość.</span><span class="sxs-lookup"><span data-stu-id="38b69-265">Each time a record is updated, Mobile Apps sets hello `version` property for that record tooa new value.</span></span> <span data-ttu-id="38b69-266">Podczas każdego żądania aktualizacji hello `version` Właściwość rekordu hello dołączone do żądania hello jest porównywany toohello tę samą właściwość dla rekordu hello na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="38b69-266">During each update request, hello `version` property of hello record included with hello request is compared toohello same property for hello record on hello server.</span></span> <span data-ttu-id="38b69-267">Jeśli wersja przekazaną za pomocą żądania hello jest niezgodna z hello wewnętrznej bazy danych, a następnie wywołuje powitania klienta biblioteki `MobileServicePreconditionFailedException<T>` wyjątku.</span><span class="sxs-lookup"><span data-stu-id="38b69-267">If the version passed with hello request does not match hello backend, then hello client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="38b69-268">Typ Hello dołączonego wyjątek hello jest hello rekord na podstawie hello wersja wewnętrznej bazy danych zawierające hello serwerów hello rekordu.</span><span class="sxs-lookup"><span data-stu-id="38b69-268">hello type included with hello exception is hello record from hello backend containing hello servers version of hello record.</span></span> <span data-ttu-id="38b69-269">Witaj aplikacji można używać tego toodecide informacji czy tooexecute hello aktualizacji żądanie ponownie, podając poprawną hello `version` wartość z zakresu od hello zaplecza toocommit zmiany.</span><span class="sxs-lookup"><span data-stu-id="38b69-269">hello application can then use this information toodecide whether tooexecute hello update request again with hello correct `version` value from hello backend toocommit changes.</span></span>

<span data-ttu-id="38b69-270">Zdefiniować kolumnę na powitania klasy tabeli dla hello `version` optymistycznej współbieżności tooenable właściwości systemu.</span><span class="sxs-lookup"><span data-stu-id="38b69-270">Define a column on hello table class for hello `version` system property tooenable optimistic concurrency.</span></span> <span data-ttu-id="38b69-271">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="38b69-271">For example:</span></span>

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

<span data-ttu-id="38b69-272">Aplikacje przy użyciu tabel bez typu włączyć optymistycznej współbieżności przez ustawienie hello `Version` Flaga na `SystemProperties` z hello tabeli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="38b69-272">Applications using untyped tables enable optimistic concurrency by setting hello `Version` flag on the `SystemProperties` of hello table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="38b69-273">W dodatku tooenabling optymistycznej współbieżności, musi również catch hello `MobileServicePreconditionFailedException<T>` wyjątek w kodzie podczas wywoływania metody [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="38b69-273">In addition tooenabling optimistic concurrency, you must also catch hello `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="38b69-274">Rozwiąż konflikt hello stosując hello poprawne `version` toothe zaktualizować rekord i wywołanie [UpdateAsync] z hello rozpoznać rekordu.</span><span class="sxs-lookup"><span data-stu-id="38b69-274">Resolve hello conflict by applying hello correct `version` toothe updated record and call [UpdateAsync] with hello resolved record.</span></span> <span data-ttu-id="38b69-275">Witaj następującego kodu pokazano, jak tooresolve zapisu raz wykryty konflikt:</span><span class="sxs-lookup"><span data-stu-id="38b69-275">hello following code shows how tooresolve a write conflict once detected:</span></span>

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

<span data-ttu-id="38b69-276">Aby uzyskać więcej informacji, zobacz hello [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps] tematu.</span><span class="sxs-lookup"><span data-stu-id="38b69-276">For more information, see hello [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="38b69-277"><a name="binding"></a>Porady: interfejs użytkownika systemu Windows tooa danych Bind Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="38b69-277"><a name="binding"></a>How to: Bind Mobile Apps data tooa Windows user interface</span></span>
<span data-ttu-id="38b69-278">W tej sekcji przedstawiono, jak toodisplay zwróciło obiektów danych, za pomocą elementów interfejsu użytkownika w aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="38b69-278">This section shows how toodisplay returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="38b69-279">Poniższy przykładowy kod wiąże toohello źródła hello listy przy użyciu zapytania niezakończonych elementów.</span><span class="sxs-lookup"><span data-stu-id="38b69-279">The following example code binds toohello source of hello list with a query for incomplete items.</span></span> <span data-ttu-id="38b69-280">[MobileServiceCollection] tworzy kolekcję przenośnych aplikacji obsługujących powiązania.</span><span class="sxs-lookup"><span data-stu-id="38b69-280">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

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

<span data-ttu-id="38b69-281">Niektóre formanty w hello zarządzane Obsługa środowiska uruchomieniowego interfejs o nazwie [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="38b69-281">Some controls in hello managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="38b69-282">Ten interfejs umożliwia toorequest formanty dodatkowe dane, gdy hello użytkownik przewija widok.</span><span class="sxs-lookup"><span data-stu-id="38b69-282">This interface allows controls toorequest extra data when hello user scrolls.</span></span> <span data-ttu-id="38b69-283">Jest wbudowaną obsługę ten interfejs dla uniwersalnych aplikacji systemu Windows za pośrednictwem [MobileServiceIncrementalLoadingCollection], który automatycznie obsługuje wywołań z hello formantów.</span><span class="sxs-lookup"><span data-stu-id="38b69-283">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from hello controls.</span></span> <span data-ttu-id="38b69-284">Użyj `MobileServiceIncrementalLoadingCollection` w aplikacjach systemu Windows w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-284">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="38b69-285">toouse hello nowej kolekcji w aplikacji Windows Phone 8 i "Silverlight" hello użyj `ToCollection` metody rozszerzenia na `IMobileServiceTableQuery<T>` i `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="38b69-285">toouse hello new collection on Windows Phone 8 and "Silverlight" apps, use hello `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="38b69-286">Wywołaj danych tooload `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="38b69-286">tooload data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="38b69-287">Jeśli używasz kolekcji hello utworzona przez wywołanie metody `ToCollectionAsync` lub `ToCollection`, pobrać kolekcję, która może być powiązane tooUI formantów.</span><span class="sxs-lookup"><span data-stu-id="38b69-287">When you use hello collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound tooUI controls.</span></span>  <span data-ttu-id="38b69-288">Ta kolekcja jest obsługujący stronicowania.</span><span class="sxs-lookup"><span data-stu-id="38b69-288">This collection is paging-aware.</span></span>  <span data-ttu-id="38b69-289">Ponieważ kolekcji hello ładuje dane z sieci, podczas ładowania czasami kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="38b69-289">Since hello collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="38b69-290">toohandle takie błędy zastąpienie hello `OnException` metoda `MobileServiceIncrementalLoadingCollection` wyjątki toohandle wyniku wywołania zbyt`LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="38b69-290">toohandle such failures, override hello `OnException` method on `MobileServiceIncrementalLoadingCollection` toohandle exceptions resulting from calls too`LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="38b69-291">Należy wziąć pod uwagę, jeśli ta tabela ma wiele pól, ale mają toodisplay niektóre z nich formantu.</span><span class="sxs-lookup"><span data-stu-id="38b69-291">Consider if your table has many fields but you only want toodisplay some of them in your control.</span></span> <span data-ttu-id="38b69-292">Można użyć wskazówki hello w powyższej sekcji hello "[wybrać określone kolumny](#selecting)" tooselect toodisplay określonych kolumn w hello interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="38b69-292">You may use hello guidance in hello preceding section "[Select specific columns](#selecting)" tooselect specific columns toodisplay in hello UI.</span></span>

### <span data-ttu-id="38b69-293"><a name="pagesize"></a>Witaj zmiany rozmiaru strony</span><span class="sxs-lookup"><span data-stu-id="38b69-293"><a name="pagesize"></a>Change hello Page size</span></span>
<span data-ttu-id="38b69-294">Aplikacje mobilne platformy Azure zwraca maksymalnie 50 elementów na żądanie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="38b69-294">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="38b69-295">Można zmienić hello stronicowania, zwiększając hello maksymalny rozmiar strony na powitania klienta i serwera.</span><span class="sxs-lookup"><span data-stu-id="38b69-295">You can change hello paging size by increasing hello maximum page size on both hello client and server.</span></span>  <span data-ttu-id="38b69-296">tooincrease hello rozmiar żądanej strony, należy określić `PullOptions` przy użyciu `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="38b69-296">tooincrease hello requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="38b69-297">Zakładając, że zostały wykonane hello `PageSize` tooor równy większa niż 100 w ramach serwera hello żądanie zwraca maksymalnie 100 elementów.</span><span class="sxs-lookup"><span data-stu-id="38b69-297">Assuming you have made hello `PageSize` equal tooor greater than 100 within hello server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="38b69-298"><a name="#offlinesync"></a>Praca z tabelami w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="38b69-298"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="38b69-299">Tabele w trybie offline używają lokalnych danych toostore magazynu SQLite do użycia w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="38b69-299">Offline tables use a local SQLite store toostore data for use when offline.</span></span>  <span data-ttu-id="38b69-300">Tabela wszystkie operacje są wykonywane przed hello SQLite lokalnego magazynu zamiast powitania serwera zdalnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="38b69-300">All table operations are done against hello local SQLite store instead of hello remote server store.</span></span>  <span data-ttu-id="38b69-301">toocreate tabelę w trybie offline, najpierw przygotować projektu:</span><span class="sxs-lookup"><span data-stu-id="38b69-301">toocreate an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="38b69-302">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie hello > **Zarządzaj pakietami NuGet rozwiązania...** , następnie wyszukaj i zainstaluj **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet dla wszystkich projektów w rozwiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-302">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="38b69-303">Urządzeń z systemem Windows (opcjonalnie) toosupport zainstalować jednego z powitania po SQLite środowiska uruchomieniowego pakiety:</span><span class="sxs-lookup"><span data-stu-id="38b69-303">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="38b69-304">**Środowisko uruchomieniowe Windows 8.1:** zainstalować [SQLite dla Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="38b69-304">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="38b69-305">**Windows Phone 8.1:** zainstalować [SQLite dla Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="38b69-305">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="38b69-306">**Platforma uniwersalna systemu Windows** zainstalować [SQLite dla uniwersalnych systemu Windows hello][5].</span><span class="sxs-lookup"><span data-stu-id="38b69-306">**Universal Windows Platform** Install [SQLite for hello Universal Windows][5].</span></span>
3. <span data-ttu-id="38b69-307">(Opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="38b69-307">(Optional).</span></span> <span data-ttu-id="38b69-308">Dla urządzeń z systemem Windows, kliknij przycisk **odwołania** > **Dodawanie odwołania...** , rozwiń hello **Windows** folder > **rozszerzenia**, następnie włącz hello odpowiednie **SQLite dla systemu Windows** zestawu SDK oraz hello  **2013 środowiska uruchomieniowego Visual C++ dla systemu Windows** zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="38b69-308">For Windows devices, click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**, then enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="38b69-309">Witaj nazwy zestawu SDK SQLite się nieco różnić z każdej z platform Windows.</span><span class="sxs-lookup"><span data-stu-id="38b69-309">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="38b69-310">Aby można było utworzyć odwołania do tabeli, należy przygotować hello lokalnego magazynu:</span><span class="sxs-lookup"><span data-stu-id="38b69-310">Before a table reference can be created, hello local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="38b69-311">Zainicjowanie magazynu odbywa się normalnie natychmiast po utworzeniu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="38b69-311">Store initialization is normally done immediately after hello client is created.</span></span>  <span data-ttu-id="38b69-312">Witaj **OfflineDbPath** powinny być odpowiednie do użycia na wszystkich platformach obsługiwanych nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="38b69-312">hello **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="38b69-313">Jeśli ścieżka hello jest w pełni kwalifikowana (to znaczy rozpoczyna się od ukośnika), zostanie użyta w tej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="38b69-313">If hello path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="38b69-314">Jeśli ścieżka hello nie jest w pełni kwalifikowana, plik hello jest umieszczany w lokalizacji specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="38b69-314">If hello path is not fully qualified, hello file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="38b69-315">Dla urządzeń iOS i Android hello domyślna ścieżka to folder "Osobiste pliki" hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-315">For iOS and Android devices, hello default path is hello "Personal Files" folder.</span></span>
* <span data-ttu-id="38b69-316">W przypadku urządzeń z systemem Windows hello domyślna ścieżka to folder "AppData" specyficzne dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-316">For Windows devices, hello default path is hello application-specific "AppData" folder.</span></span>

<span data-ttu-id="38b69-317">Odwołanie do tabeli można uzyskać za pomocą hello `GetSyncTable<>` metody:</span><span class="sxs-lookup"><span data-stu-id="38b69-317">A table reference can be obtained using hello `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="38b69-318">Nie trzeba toouse tooauthenticate tabelę w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="38b69-318">You do not need tooauthenticate toouse an offline table.</span></span>  <span data-ttu-id="38b69-319">Wystarczy tooauthenticate, gdy komunikują się hello usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-319">You only need tooauthenticate when you are communicating with hello backend service.</span></span>

### <span data-ttu-id="38b69-320"><a name="syncoffline"></a>Trwa synchronizowanie tabelę w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="38b69-320"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="38b69-321">Tabele w trybie offline nie są zsynchronizowane z zaplecza hello domyślnie.</span><span class="sxs-lookup"><span data-stu-id="38b69-321">Offline tables are not synchronized with hello backend by default.</span></span>  <span data-ttu-id="38b69-322">Synchronizacja jest podzielony na dwie części.</span><span class="sxs-lookup"><span data-stu-id="38b69-322">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="38b69-323">Wypchnij zmiany oddzielnie pobierania nowych elementów.</span><span class="sxs-lookup"><span data-stu-id="38b69-323">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="38b69-324">Oto metoda typowe synchronizacji:</span><span class="sxs-lookup"><span data-stu-id="38b69-324">Here is a typical sync method:</span></span>

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

<span data-ttu-id="38b69-325">Jeśli zbyt hello pierwszy argument`PullAsync` ma wartość null, synchronizacja przyrostowa nie będzie używana.</span><span class="sxs-lookup"><span data-stu-id="38b69-325">If hello first argument too`PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="38b69-326">Każda operacja synchronizacji powoduje pobranie wszystkich rekordów.</span><span class="sxs-lookup"><span data-stu-id="38b69-326">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="38b69-327">niejawny wykonuje Hello SDK `PushAsync()` przed ściąganie rekordów.</span><span class="sxs-lookup"><span data-stu-id="38b69-327">hello SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="38b69-328">Obsługa konflikt się dzieje na `PullAsync()` metody.</span><span class="sxs-lookup"><span data-stu-id="38b69-328">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="38b69-329">Możesz można biznesowych w radzeniu sobie z konfliktami w hello sam sposób jak tabele online.</span><span class="sxs-lookup"><span data-stu-id="38b69-329">You can deal with conflicts in hello same way as online tables.</span></span>  <span data-ttu-id="38b69-330">konflikt Hello jest generowany po `PullAsync()` jest wywoływana zamiast podczas hello insert, update lub delete.</span><span class="sxs-lookup"><span data-stu-id="38b69-330">hello conflict is produced when `PullAsync()` is called instead of during hello insert, update, or delete.</span></span> <span data-ttu-id="38b69-331">Jeśli wystąpi konflikt wiele, są one dołączone do pojedynczego MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="38b69-331">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="38b69-332">Obsługi każdego błędów oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="38b69-332">Handle each failure separately.</span></span>

## <span data-ttu-id="38b69-333"><a name="#customapi"></a>Praca z niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="38b69-333"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="38b69-334">Niestandardowy interfejs API umożliwia toodefine niestandardowe punkty końcowe, które udostępniają funkcje serwera które nie mapy tooan insert, update, usuwania lub operacja odczytu.</span><span class="sxs-lookup"><span data-stu-id="38b69-334">A custom API enables you toodefine custom endpoints that expose server functionality that does not map tooan insert, update, delete, or read operation.</span></span> <span data-ttu-id="38b69-335">Przy użyciu niestandardowego interfejsu API, może mieć większą kontrolę nad wiadomości, w tym odczytywanie ustawienie nagłówki komunikatów HTTP i Definiowanie formatu treści wiadomości innych niż JSON.</span><span class="sxs-lookup"><span data-stu-id="38b69-335">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="38b69-336">Niestandardowy interfejs API należy wywołać wywołując jedną hello [InvokeApiAsync] metod na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="38b69-336">You call a custom API by calling one of hello [InvokeApiAsync] methods on hello client.</span></span> <span data-ttu-id="38b69-337">Na przykład po wierszu kodu hello wysyła toohello żądania POST **completeAll** interfejsu API hello wewnętrznej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="38b69-337">For example, hello following line of code sends a POST request toohello **completeAll** API on hello backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="38b69-338">Ten formularz jest wywołanie metody typu i wymaga tego hello **MarkAllResult** zwracany typ jest zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="38b69-338">This form is a typed method call and requires that hello **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="38b69-339">Obsługiwane są zarówno typu, jak i bez typu metody.</span><span class="sxs-lookup"><span data-stu-id="38b69-339">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="38b69-340">Witaj metody InvokeApiAsync() dołącza/api/API toohello chcesz toocall, chyba że hello interfejsu API, który rozpoczyna się od '/'.</span><span class="sxs-lookup"><span data-stu-id="38b69-340">hello InvokeApiAsync() method prepends '/api/' toohello API that you wish toocall unless hello API starts with a '/'.</span></span>
<span data-ttu-id="38b69-341">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="38b69-341">For example:</span></span>

* <span data-ttu-id="38b69-342">`InvokeApiAsync("completeAll",...)`wywołuje /api/completeAll hello wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="38b69-342">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on hello backend</span></span>
* <span data-ttu-id="38b69-343">`InvokeApiAsync("/.auth/me",...)`wywołuje /.auth/me hello wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="38b69-343">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on hello backend</span></span>

<span data-ttu-id="38b69-344">InvokeApiAsync toocall można użyć dowolnego WebAPI, łącznie z tymi WebAPIs, które nie są zdefiniowane z usługą Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="38b69-344">You can use InvokeApiAsync toocall any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="38b69-345">Gdy używasz InvokeApiAsync() hello odpowiednie nagłówki, włącznie z nagłówkami uwierzytelniania są wysyłane z żądaniem hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-345">When you use InvokeApiAsync(), hello appropriate headers, including authentication headers, are sent with hello request.</span></span>

## <span data-ttu-id="38b69-346"><a name="authentication"></a>Uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="38b69-346"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="38b69-347">Aplikacje mobilne obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account, Twitter i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38b69-347">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="38b69-348">Możesz ustawić uprawnienia na dostęp do tabel toorestrict dla określonych operacji tooonly uwierzytelnieni użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="38b69-348">You can set permissions on tables toorestrict access for specific operations tooonly authenticated users.</span></span> <span data-ttu-id="38b69-349">Umożliwia także tożsamości hello reguł autoryzacji użytkowników uwierzytelnionych tooimplement w skryptach serwera.</span><span class="sxs-lookup"><span data-stu-id="38b69-349">You can also use hello identity of authenticated users tooimplement authorization rules in server scripts.</span></span> <span data-ttu-id="38b69-350">Aby uzyskać więcej informacji, zobacz samouczek hello [aplikacji tooyour authentication Dodaj].</span><span class="sxs-lookup"><span data-stu-id="38b69-350">For more information, see hello tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="38b69-351">Obsługiwane są dwa przepływy uwierzytelniania: *zarządzanych przez klienta* i *serwer zarządzany* przepływu.</span><span class="sxs-lookup"><span data-stu-id="38b69-351">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="38b69-352">Przepływ serwer zarządzany Hello zapewnia hello najprostszym uwierzytelniania, ponieważ zależy od interfejsu uwierzytelniania sieci web dostawcy hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-352">hello server-managed flow provides hello simplest authentication experience, as it relies on hello provider's web authentication interface.</span></span> <span data-ttu-id="38b69-353">Przepływ zarządzanych przez klienta Hello umożliwia lepszą integrację z możliwości specyficznych dla urządzeń zależy od zestawy SDK urządzenia specyficznego dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="38b69-353">hello client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="38b69-354">Zalecamy używanie przepływem zarządzanych przez klienta w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="38b69-354">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="38b69-355">tooset się uwierzytelniania, musisz zarejestrować aplikację z co najmniej jednego dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="38b69-355">tooset up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="38b69-356">Dostawca tożsamości Hello generuje identyfikator klienta i klucz tajny klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-356">hello identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="38b69-357">Te wartości są ustawiane następnie w tooenable Twojego wewnętrznej bazy danych usługi Azure App Service uwierzytelniania/autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-357">These values are then set in your backend tooenable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="38b69-358">Aby uzyskać więcej informacji, wykonaj hello szczegółowe instrukcje w samouczku [aplikacji tooyour authentication Dodaj].</span><span class="sxs-lookup"><span data-stu-id="38b69-358">For more information, follow hello detailed instructions in the tutorial [Add authentication tooyour app].</span></span>

<span data-ttu-id="38b69-359">w tej sekcji opisano Hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="38b69-359">hello following topics are covered in this section:</span></span>

* [<span data-ttu-id="38b69-360">Zarządzane przez klienta do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="38b69-360">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="38b69-361">Serwer zarządzany uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="38b69-361">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="38b69-362">Token uwierzytelniania hello buforowania</span><span class="sxs-lookup"><span data-stu-id="38b69-362">Caching hello authentication token</span></span>](#caching)

### <span data-ttu-id="38b69-363"><a name="clientflow"></a>Zarządzane przez klienta do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="38b69-363"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="38b69-364">Aplikację można niezależnie skontaktuj się z dostawcą tożsamości hello, a następnie podaj token zwrócony hello podczas logowania, z poziomu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="38b69-364">Your app can independently contact hello identity provider and then provide hello returned token during login with your backend.</span></span> <span data-ttu-id="38b69-365">Ten przepływ klienta umożliwia tooprovide pojedynczego jednokrotnego dla użytkowników lub tooretrieve użytkownika dodatkowe dane z hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="38b69-365">This client flow enables you tooprovide a single sign-on experience for users or tooretrieve additional user data from hello identity provider.</span></span> <span data-ttu-id="38b69-366">Uwierzytelnianie klienta przepływu jest preferowany toousing przepływu serwera jako dostawca tożsamości hello SDK zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="38b69-366">Client flow authentication is preferred toousing a server flow as hello identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="38b69-367">Przykłady są dostępne dla powitania od klienta przepływach uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="38b69-367">Examples are provided for hello following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="38b69-368">Biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="38b69-368">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="38b69-369">Facebook lub Google</span><span class="sxs-lookup"><span data-stu-id="38b69-369">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="38b69-370">Zestaw Live SDK</span><span class="sxs-lookup"><span data-stu-id="38b69-370">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="38b69-371"><a name="adal"></a>Uwierzytelnianie użytkowników z hello biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="38b69-371"><a name="adal"></a>Authenticate users with hello Active Directory Authentication Library</span></span>
<span data-ttu-id="38b69-372">Można użyć uwierzytelniania użytkownika tooinitiate hello Active Directory Authentication Library (ADAL) z powitania klienta przy użyciu uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="38b69-372">You can use hello Active Directory Authentication Library (ADAL) tooinitiate user authentication from hello client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="38b69-373">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD przez następujące hello [jak tooconfigure aplikacji usługi dla usługi Active Directory logowania] samouczka.</span><span class="sxs-lookup"><span data-stu-id="38b69-373">Configure your mobile app backend for AAD sign-on by following hello [How tooconfigure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="38b69-374">Upewnij się, że toocomplete hello opcjonalny krok rejestrowania aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="38b69-374">Make sure toocomplete hello optional step of registering a native client application.</span></span>
2. <span data-ttu-id="38b69-375">W programie Visual Studio lub Xamarin Studio Otwórz projekt, a następnie dodaj toothe odwołanie `Microsoft.IdentityModel.CLients.ActiveDirectory` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="38b69-375">In Visual Studio or Xamarin Studio, open your project and add a reference toothe `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="38b69-376">Podczas wyszukiwania, obejmują wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="38b69-376">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="38b69-377">Dodaj hello następującego kodu tooyour aplikacji, zgodnie z platformy toohello, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="38b69-377">Add hello following code tooyour application, according toohello platform you are using.</span></span> <span data-ttu-id="38b69-378">W każdej wprowadź hello następujące elementy zastępcze:</span><span class="sxs-lookup"><span data-stu-id="38b69-378">In each, make hello following replacements:</span></span>

   * <span data-ttu-id="38b69-379">Zastąp **INSERT urzędu tutaj** o nazwie hello hello dzierżawy, w którym są udostępniane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-379">Replace **INSERT-AUTHORITY-HERE** with hello name of hello tenant in which you provisioned your application.</span></span> <span data-ttu-id="38b69-380">Format powinien być https://login.microsoftonline.com/contoso.onmicrosoft.com. Ta wartość może zostać skopiowany z hello kartę domeny w usłudze Azure Active Directory w hello [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="38b69-380">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com. This value can be copied from hello Domain tab in your Azure Active Directory in hello [Azure classic portal].</span></span>
   * <span data-ttu-id="38b69-381">Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta powitania dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-381">Replace **INSERT-RESOURCE-ID-HERE** with hello client ID for your mobile app backend.</span></span> <span data-ttu-id="38b69-382">Identyfikator klienta hello można uzyskać z hello **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-382">You can obtain hello client ID from hello **Advanced** tab under **Azure Active Directory Settings** in hello portal.</span></span>
   * <span data-ttu-id="38b69-383">Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta hello skopiowany z hello aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="38b69-383">Replace **INSERT-CLIENT-ID-HERE** with hello client ID you copied from hello native client application.</span></span>
   * <span data-ttu-id="38b69-384">Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="38b69-384">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using hello HTTPS scheme.</span></span> <span data-ttu-id="38b69-385">Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="38b69-385">This value should be similar too*https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="38b69-386">następujący kod Hello wymagane dla każdej platformy:</span><span class="sxs-lookup"><span data-stu-id="38b69-386">hello code needed for each platform follows:</span></span>

     <span data-ttu-id="38b69-387">**System Windows:**</span><span class="sxs-lookup"><span data-stu-id="38b69-387">**Windows:**</span></span>

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

     <span data-ttu-id="38b69-388">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="38b69-388">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="38b69-389">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="38b69-389">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="38b69-390"><a name="client-facebook"></a>Logowanie jednokrotne przy użyciu tokenu z usługi Facebook lub Google</span><span class="sxs-lookup"><span data-stu-id="38b69-390"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="38b69-391">Można użyć powitania klienta przepływ, jak pokazano w ta Wstawka kodu dla usługi Facebook lub Google.</span><span class="sxs-lookup"><span data-stu-id="38b69-391">You can use hello client flow as shown in this snippet for Facebook or Google.</span></span>

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

#### <span data-ttu-id="38b69-392"><a name="client-livesdk"></a>Rejestracja jednokrotna przy użyciu Account Microsoft z hello zestaw Live SDK</span><span class="sxs-lookup"><span data-stu-id="38b69-392"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with hello Live SDK</span></span>
<span data-ttu-id="38b69-393">tooauthenticate użytkowników, musisz zarejestrować aplikację w hello konta Microsoft Developer Center.</span><span class="sxs-lookup"><span data-stu-id="38b69-393">tooauthenticate users, you must register your app at hello Microsoft account Developer Center.</span></span> <span data-ttu-id="38b69-394">Skonfiguruj szczegóły rejestracji na zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-394">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="38b69-395">toocreate Microsoft rejestracja konta podłączyć tooyour zaplecza aplikacji mobilnej, pełną hello czynnościach w ramach [zarejestrować Twojej aplikacji toouse logowania konta Microsoft].</span><span class="sxs-lookup"><span data-stu-id="38b69-395">toocreate a Microsoft account registration and connect it tooyour Mobile App backend, complete hello steps in [Register your app toouse a Microsoft account login].</span></span> <span data-ttu-id="38b69-396">Jeśli masz zarówno Sklep Windows i Windows Phone 8/Silverlight wersje aplikacji, najpierw zarejestrować wersji Sklepu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-396">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register hello Windows Store version first.</span></span>

<span data-ttu-id="38b69-397">Witaj poniższy kod jest uwierzytelniany przy użyciu zestaw Live SDK i używa hello zwrócił token toosign w tooyour zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-397">hello following code authenticates using Live SDK and uses hello returned token toosign in tooyour Mobile App backend.</span></span>

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

<span data-ttu-id="38b69-398">Aby uzyskać więcej informacji, zobacz hello [Windows Live SDK] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-398">For more information, see hello [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="38b69-399"><a name="serverflow"></a>Serwer zarządzany uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="38b69-399"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="38b69-400">Po zarejestrowaniu dostawcy tożsamości, wywołaj hello [LoginAsync] metody na powitania [MobileServiceClient] z hello [MobileServiceAuthenticationProvider] wartość dostawcy.</span><span class="sxs-lookup"><span data-stu-id="38b69-400">Once you have registered your identity provider, call hello [LoginAsync] method on hello [MobileServiceClient] with hello [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="38b69-401">Na przykład hello następujący kod inicjuje serwera przepływu logowania za pomocą usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="38b69-401">For example, hello following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="38b69-402">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello [MobileServiceAuthenticationProvider] toohello wartość dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="38b69-402">If you are using an identity provider other than Facebook, change hello value of [MobileServiceAuthenticationProvider] toohello value for your provider.</span></span>

<span data-ttu-id="38b69-403">W przepływie serwera usługi Azure App Service zarządza przepływ uwierzytelniania OAuth hello hello logowania strona hello wybranego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="38b69-403">In a server flow, Azure App Service manages hello OAuth authentication flow by displaying hello sign-in page of hello selected provider.</span></span>  <span data-ttu-id="38b69-404">Raz zwraca hello do dostawcy tożsamości, usługa aplikacji Azure generuje token uwierzytelniania usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38b69-404">Once hello identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="38b69-405">Hello [LoginAsync] metoda zwraca [MobileServiceUser], co umożliwia zarówno hello [UserId] z hello uwierzytelniony użytkownik i hello [ MobileServiceAuthenticationToken], jako tokenu web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="38b69-405">hello [LoginAsync] method returns a [MobileServiceUser], which provides both hello [UserId] of hello authenticated user and hello [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="38b69-406">Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="38b69-406">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="38b69-407">Aby uzyskać więcej informacji, zobacz [token uwierzytelniania hello buforowanie](#caching).</span><span class="sxs-lookup"><span data-stu-id="38b69-407">For more information, see [Caching hello authentication token](#caching).</span></span>

### <span data-ttu-id="38b69-408"><a name="caching"></a>Token uwierzytelniania hello buforowania</span><span class="sxs-lookup"><span data-stu-id="38b69-408"><a name="caching"></a>Caching hello authentication token</span></span>
<span data-ttu-id="38b69-409">W niektórych przypadkach metoda logowania toohello hello można uniknąć po pierwszym pomyślnym uwierzytelnieniu hello przechowując hello tokenu uwierzytelniania z hello dostawcy.</span><span class="sxs-lookup"><span data-stu-id="38b69-409">In some cases, hello call toohello login method can be avoided after hello first successful authentication by storing hello authentication token from hello provider.</span></span>  <span data-ttu-id="38b69-410">Aplikacje Sklepu Windows i platformy uniwersalnej systemu Windows mogą używać [PasswordVault] toocache bieżącego uwierzytelniania tokenu po pomyślnym zalogowaniu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-410">Windows Store and UWP apps can use [PasswordVault] toocache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="38b69-411">Hello UserId wartość jest przechowywana jako hello UserName hello poświadczeń i hello token jest hello przechowywane jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="38b69-411">hello UserId value is stored as hello UserName of hello credential and hello token is hello stored as hello Password.</span></span> <span data-ttu-id="38b69-412">Na kolejnych rozruchów, możesz sprawdzić hello **PasswordVault** dla buforowanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="38b69-412">On subsequent start-ups, you can check hello **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="38b69-413">Witaj poniższy przykład korzysta buforowanych poświadczeń, gdy zostaną znalezione, a w przeciwnym razie próby tooauthenticate ponownie, podając hello wewnętrznej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="38b69-413">hello following example uses cached credentials when they are found, and otherwise attempts tooauthenticate again with hello backend:</span></span>

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

<span data-ttu-id="38b69-414">Po zalogowaniu się użytkownika należy również usunąć hello przechowywanych poświadczeń, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-414">When you sign out a user, you must also remove hello stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="38b69-415">Aplikacje platformy Xamarin używać hello [Xamarin.Auth] interfejsów API toosecurely magazynu poświadczeń w **konta** obiektu.</span><span class="sxs-lookup"><span data-stu-id="38b69-415">Xamarin    apps use hello [Xamarin.Auth] APIs toosecurely store credentials in an **Account** object.</span></span> <span data-ttu-id="38b69-416">Na przykład za pomocą tych interfejsów API, zobacz hello [AuthStore.cs] pliku kodu w hello [udostępniania próbki zdjęć ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="38b69-416">For an example of using these APIs, see hello [AuthStore.cs] code file in hello [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="38b69-417">Korzystając z uwierzytelniania zarządzanych przez klienta, można buforować tokenu dostępu hello uzyskane od dostawcy, takich jak Facebook lub Twitter.</span><span class="sxs-lookup"><span data-stu-id="38b69-417">When you use client-managed authentication, you can also cache hello access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="38b69-418">Token ten może być dostarczony toorequest nowy token uwierzytelniania z zaplecza hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-418">This token can be supplied toorequest a new authentication token from hello backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using hello access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="38b69-419"><a name="pushnotifications"></a>Powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="38b69-419"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="38b69-420">Witaj następujących tematach opisano powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="38b69-420">hello following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="38b69-421">Zarejestruj się, aby powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="38b69-421">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="38b69-422">Uzyskaj identyfikator SID pakietu Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="38b69-422">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="38b69-423">Rejestrowanie przy użyciu szablonów i platform</span><span class="sxs-lookup"><span data-stu-id="38b69-423">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="38b69-424"><a name="register-for-push"></a>Porady: rejestrowanie się w celu powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="38b69-424"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="38b69-425">powitania klienta Mobile Apps umożliwia tooregister dla powiadomień wypychanych przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="38b69-425">hello Mobile Apps client enables you tooregister for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="38b69-426">Podczas rejestrowania, można uzyskać dojścia uzyskanej od specyficzne dla platformy hello Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="38b69-426">When registering, you obtain a handle that you obtain from hello platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="38b69-427">Podczas tworzenia rejestracji hello, następnie podaj tę wartość, wraz ze wszystkimi tagami.</span><span class="sxs-lookup"><span data-stu-id="38b69-427">You then provide this value along with any tags when you create hello registration.</span></span> <span data-ttu-id="38b69-428">Witaj następujący kod rejestruje aplikację systemu Windows dla powiadomień wypychanych hello powiadomienia usługi WNS (Windows):</span><span class="sxs-lookup"><span data-stu-id="38b69-428">hello following code registers your Windows app for push notifications with hello Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using hello new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="38b69-429">Jeśli push tooWNS, a następnie należy [pobrania identyfikatora SID pakietu Sklepu Windows](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="38b69-429">If you are pushing tooWNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="38b69-430">Aby uzyskać więcej informacji na temat aplikacji systemu Windows łącznie ze sposobem tooregister do rejestracji szablonów, zobacz [aplikacji tooyour powiadomień wypychanych Dodaj].</span><span class="sxs-lookup"><span data-stu-id="38b69-430">For more information on Windows apps, including how tooregister for template registrations, see [Add push notifications tooyour app].</span></span>

<span data-ttu-id="38b69-431">Żądanie tagi powitania klienta nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="38b69-431">Requesting tags from hello client is not supported.</span></span>  <span data-ttu-id="38b69-432">Tag żądań dyskretnie są usuwane z rejestracji.</span><span class="sxs-lookup"><span data-stu-id="38b69-432">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="38b69-433">W razie potrzeby tooregister urządzenia przy użyciu tagów, należy utworzyć niestandardowego interfejsu API, używającej hello API centra powiadomień tooperform hello rejestracji w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="38b69-433">If you wish tooregister your device with tags, create a Custom API that uses hello Notification Hubs API tooperform hello registration on your behalf.</span></span>  <span data-ttu-id="38b69-434">[Wywołaj hello niestandardowego interfejsu API](#customapi) zamiast hello `RegisterNativeAsync()` metody.</span><span class="sxs-lookup"><span data-stu-id="38b69-434">[Call hello Custom API](#customapi) instead of hello `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="38b69-435"><a name="package-sid"></a>Porady: uzyskiwanie identyfikatora SID pakietu Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="38b69-435"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="38b69-436">Dla Włączanie powiadomień wypychanych w aplikacji ze Sklepu Windows wymagany jest identyfikator SID pakietu.</span><span class="sxs-lookup"><span data-stu-id="38b69-436">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="38b69-437">tooreceive pakietu identyfikatora SID, rejestrowanie aplikacji ze Sklepu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="38b69-437">tooreceive a package SID, register your application with hello Windows Store.</span></span>

<span data-ttu-id="38b69-438">tooobtain tej wartości:</span><span class="sxs-lookup"><span data-stu-id="38b69-438">tooobtain this value:</span></span>

1. <span data-ttu-id="38b69-439">W programie Visual Studio Eksploratorze rozwiązań kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows hello, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepu hello...** .</span><span class="sxs-lookup"><span data-stu-id="38b69-439">In Visual Studio Solution Explorer, right-click hello Windows Store app project, click **Store** > **Associate App with hello Store...**.</span></span>
2. <span data-ttu-id="38b69-440">W Kreatorze powitania kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.</span><span class="sxs-lookup"><span data-stu-id="38b69-440">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="38b69-441">Po rejestracji aplikacji hello jest hello został pomyślnie utworzony, wybierz nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="38b69-441">After hello app registration is successfully created, select hello app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="38b69-442">Zaloguj się za toohello [Centrum deweloperów systemu Windows] przy użyciu Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="38b69-442">Log in toohello [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="38b69-443">W obszarze **Moje aplikacje**, kliknij przycisk hello rejestracji aplikacji utworzony.</span><span class="sxs-lookup"><span data-stu-id="38b69-443">Under **My apps**, click hello app registration you created.</span></span>
5. <span data-ttu-id="38b69-444">Kliknij przycisk **Zarządzanie aplikacjami** > **tożsamości aplikacji**, a następnie przewiń w dół toofind Twojego **identyfikatora SID pakietu**.</span><span class="sxs-lookup"><span data-stu-id="38b69-444">Click **App management** > **App identity**, and then scroll down toofind your **Package SID**.</span></span>

<span data-ttu-id="38b69-445">Wiele zastosowań identyfikator SID pakietu hello traktować go jako identyfikatora URI, w którym to przypadku należy toouse *ms-app: / /* hello schemat.</span><span class="sxs-lookup"><span data-stu-id="38b69-445">Many uses of hello package SID treat it as a URI, in which case you need toouse *ms-app://* as hello scheme.</span></span> <span data-ttu-id="38b69-446">Zwróć uwagę na powitania wersji pakietu utworzonego przez łączenie tej wartości jako prefiks identyfikatora SID.</span><span class="sxs-lookup"><span data-stu-id="38b69-446">Make note of hello version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="38b69-447">Xamarin aplikacje wymagają niektórych tooregister stanie toobe dodatkowy kod aplikacji uruchomionej na powitania z systemem iOS lub Android platform.</span><span class="sxs-lookup"><span data-stu-id="38b69-447">Xamarin apps require some additional code toobe able tooregister an app running on hello iOS or Android platforms.</span></span> <span data-ttu-id="38b69-448">Aby uzyskać więcej informacji zobacz temat powitania dla danej platformy:</span><span class="sxs-lookup"><span data-stu-id="38b69-448">For more information, see hello topic for your platform:</span></span>

* [<span data-ttu-id="38b69-449">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="38b69-449">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="38b69-450">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="38b69-450">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="38b69-451"><a name="register-xplat"></a>Porady: rejestr wypychania szablony toosend wieloplatformowych powiadomienia</span><span class="sxs-lookup"><span data-stu-id="38b69-451"><a name="register-xplat"></a>How to: Register push templates toosend cross-platform notifications</span></span>
<span data-ttu-id="38b69-452">Szablony tooregister Użyj hello `RegisterAsync()` metody za pomocą szablonów hello, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="38b69-452">tooregister templates, use hello `RegisterAsync()` method with hello templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="38b69-453">Szablony powinna być `JObject` typów i może zawierać wiele szablonów w hello następującego formatu JSON:</span><span class="sxs-lookup"><span data-stu-id="38b69-453">Your templates should be `JObject` types and can contain multiple templates in hello following JSON format:</span></span>

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

<span data-ttu-id="38b69-454">Witaj metody **RegisterAsync()** również akceptuje dodatkowej Kafelki:</span><span class="sxs-lookup"><span data-stu-id="38b69-454">hello method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="38b69-455">Wszystkie tagi są odrzucane optymalizacji podczas rejestracji dla zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="38b69-455">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="38b69-456">znaczniki tooadd tooinstallations lub szablonów w ramach instalacji, zobacz [Praca z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="38b69-456">tooadd tags tooinstallations or templates within installations, see [Work with hello .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="38b69-457">powiadomienia toosend przy użyciu tych szablonów w zarejestrowany, można znaleźć toohello [interfejsów API centra powiadomień].</span><span class="sxs-lookup"><span data-stu-id="38b69-457">toosend notifications utilizing these registered templates, refer toohello [Notification Hubs APIs].</span></span>

## <span data-ttu-id="38b69-458"><a name="misc"></a>Tematy dodatkowe</span><span class="sxs-lookup"><span data-stu-id="38b69-458"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="38b69-459"><a name="errors"></a>Porady: obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="38b69-459"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="38b69-460">Po wystąpieniu błędu w zapleczu hello, powitania klienta SDK zgłasza `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="38b69-460">When an error occurs in hello backend, hello client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="38b69-461">W poniższym przykładzie przedstawiono sposób toohandle wyjątek, który jest zwracany przez zaplecze hello:</span><span class="sxs-lookup"><span data-stu-id="38b69-461">The following example shows how toohandle an exception that is returned by hello backend:</span></span>

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

<span data-ttu-id="38b69-462">Innym przykładem dotyczącym warunki błędów można znaleźć w hello [Mobile Apps pliki przykładowe].</span><span class="sxs-lookup"><span data-stu-id="38b69-462">Another example of dealing with error conditions can be found in hello [Mobile Apps Files Sample].</span></span> <span data-ttu-id="38b69-463">[LoggingHandler] przykład udostępnia delegata rejestrowania żądań hello toolog obsługi wykonywane toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="38b69-463">The [LoggingHandler] example provides a logging delegate handler toolog hello requests being made toohello backend.</span></span>

### <span data-ttu-id="38b69-464"><a name="headers"></a>Porady: dostosowywanie nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="38b69-464"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="38b69-465">toosupport scenariusza specyficzne dla aplikacji, może być konieczne toocustomize komunikację z hello zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="38b69-465">toosupport your specific app scenario, you might need toocustomize communication with hello Mobile App backend.</span></span> <span data-ttu-id="38b69-466">Może na przykład chcesz tooadd niestandardowy nagłówek żądania wychodzącego tooevery lub nawet zmienić kody stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="38b69-466">For example, you may want tooadd a custom header tooevery outgoing request or even change responses status codes.</span></span> <span data-ttu-id="38b69-467">Można użyć niestandardowego [DelegatingHandler]w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="38b69-467">You can use a custom [DelegatingHandler], as in hello following example:</span></span>

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
