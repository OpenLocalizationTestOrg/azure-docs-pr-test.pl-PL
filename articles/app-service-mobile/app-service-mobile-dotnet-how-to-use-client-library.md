---
title: "Praca z biblioteką klientów zarządzanych aplikacji usługi Mobile Apps (z systemem Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą klienta .NET dla usługi Azure App Service Mobile Apps w aplikacjach systemu Windows i Xamarin."
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
ms.openlocfilehash: 5f4cc3e97ba7adde2aaac471951a3130d79910f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-managed-client-for-azure-mobile-apps"></a><span data-ttu-id="1b039-103">Jak używać zarządzanego klienta usługi Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="1b039-103">How to use the managed client for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

## <a name="overview"></a><span data-ttu-id="1b039-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1b039-104">Overview</span></span>
<span data-ttu-id="1b039-105">W tym przewodniku przedstawiono sposób wykonywania typowych scenariuszy przy użyciu biblioteki zarządzanego klienta dla usługi Azure App Service Mobile aplikacji dla systemu Windows i aplikacje platformy Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1b039-105">This guide shows you how to perform common scenarios using the managed client library for Azure App Service Mobile Apps for Windows and Xamarin apps.</span></span> <span data-ttu-id="1b039-106">Jeśli jesteś nowym użytkownikiem Mobile Apps, należy rozważyć wykonanie najpierw [szybkiego startu usługi Azure Mobile Apps] [ 1] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1b039-106">If you are new to Mobile Apps, you should consider first completing the [Azure Mobile Apps quickstart][1] tutorial.</span></span> <span data-ttu-id="1b039-107">W tym przewodniku możemy skupić się na SDK zarządzanego klienta.</span><span class="sxs-lookup"><span data-stu-id="1b039-107">In this guide, we focus on the client-side managed SDK.</span></span> <span data-ttu-id="1b039-108">Aby dowiedzieć się więcej o zestawów SDK po stronie serwera dla aplikacji mobilnych, zobacz dokumentację [.NET SDK serwera] [ 2] lub [Node.js Server SDK] [ 3].</span><span class="sxs-lookup"><span data-stu-id="1b039-108">To learn more about the server-side SDKs for Mobile Apps, see the documentation for the [.NET Server SDK][2] or the [Node.js Server SDK][3].</span></span>

## <a name="reference-documentation"></a><span data-ttu-id="1b039-109">Dokumentacja referencyjna</span><span class="sxs-lookup"><span data-stu-id="1b039-109">Reference documentation</span></span>
<span data-ttu-id="1b039-110">Dokumentacji zestawu SDK klienta jest zlokalizowana tutaj: [odwołania klienta usługi Azure Mobile Apps .NET][4].</span><span class="sxs-lookup"><span data-stu-id="1b039-110">The reference documentation for the client SDK is located here: [Azure Mobile Apps .NET client reference][4].</span></span>
<span data-ttu-id="1b039-111">Możesz również znaleźć kilka przykładów klienta w [repozytorium GitHub przykłady Azure][5].</span><span class="sxs-lookup"><span data-stu-id="1b039-111">You can also find several client samples in the [Azure-Samples GitHub repository][5].</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="1b039-112">Obsługiwane platformy</span><span class="sxs-lookup"><span data-stu-id="1b039-112">Supported Platforms</span></span>
<span data-ttu-id="1b039-113">Platforma .NET obsługuje następujące platformy:</span><span class="sxs-lookup"><span data-stu-id="1b039-113">The .NET Platform supports the following platforms:</span></span>

* <span data-ttu-id="1b039-114">Dla systemu Xamarin Android wersje interfejsu API 19 do 24 (KitKat za pośrednictwem nugacie)</span><span class="sxs-lookup"><span data-stu-id="1b039-114">Xamarin Android releases for API 19 through 24 (KitKat through Nougat)</span></span>
* <span data-ttu-id="1b039-115">Zwalnia systemu Xamarin iOS dla systemu iOS w wersji 8.0 lub nowszej</span><span class="sxs-lookup"><span data-stu-id="1b039-115">Xamarin iOS releases for iOS versions 8.0 and later</span></span>
* <span data-ttu-id="1b039-116">Platforma uniwersalna systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1b039-116">Universal Windows Platform</span></span>
* <span data-ttu-id="1b039-117">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="1b039-117">Windows Phone 8.1</span></span>
* <span data-ttu-id="1b039-118">Windows Phone 8.0, z wyjątkiem aplikacji Silverlight</span><span class="sxs-lookup"><span data-stu-id="1b039-118">Windows Phone 8.0 except for Silverlight applications</span></span>

<span data-ttu-id="1b039-119">Uwierzytelnianie "serwer flow" używa WebView przedstawioną interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b039-119">The "server-flow" authentication uses a WebView for the presented UI.</span></span>  <span data-ttu-id="1b039-120">Jeśli urządzenie nie jest w stanie przedstawić WebView interfejsu użytkownika, potrzebne są inne metody uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1b039-120">If the device is not able to present a WebView UI, then other methods of authentication are needed.</span></span>  <span data-ttu-id="1b039-121">Zestaw SDK w związku z tym nie jest odpowiedni dla typu czujki lub podobnie ograniczeniami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1b039-121">This SDK is thus not suitable for Watch-type or similarly restricted devices.</span></span>

## <span data-ttu-id="1b039-122"><a name="setup"></a>Instalacji i wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1b039-122"><a name="setup"></a>Setup and Prerequisites</span></span>
<span data-ttu-id="1b039-123">Przyjęto założenie, że możesz już utworzono i opublikowano projektu zaplecza aplikacji mobilnej, który zawiera co najmniej jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="1b039-123">We assume that you have already created and published your Mobile App backend project, which includes at least one table.</span></span>  <span data-ttu-id="1b039-124">Kod używany w tym temacie, nosi nazwę tabeli `TodoItem` i ma następujące kolumny: `Id`, `Text`, i `Complete`.</span><span class="sxs-lookup"><span data-stu-id="1b039-124">In the code used in this topic, the table is named `TodoItem` and it has the following columns: `Id`, `Text`, and `Complete`.</span></span> <span data-ttu-id="1b039-125">Ta tabela jest tej samej tabeli utworzone po zakończeniu [szybkiego startu usługi Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="1b039-125">This table is the same table created when you complete the [Azure Mobile Apps quickstart][1].</span></span>

<span data-ttu-id="1b039-126">Odpowiedni typ maszynowy po stronie klienta w języku C# jest następującej klasy:</span><span class="sxs-lookup"><span data-stu-id="1b039-126">The corresponding typed client-side type in C# is the following class:</span></span>

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

<span data-ttu-id="1b039-127">[JsonPropertyAttribute] [ 6] służy do definiowania *PropertyName* mapowanie między pole klienta i pola w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-127">The [JsonPropertyAttribute][6] is used to define the *PropertyName* mapping between the client field and the table field.</span></span>

<span data-ttu-id="1b039-128">Informacje na temat tworzenia tabel w zapleczu swojej Mobile Apps, zobacz [temacie .NET SDK serwera] [ 7] lub [tematu Node.js Server SDK][8].</span><span class="sxs-lookup"><span data-stu-id="1b039-128">To learn how to create tables in your Mobile Apps backend, see the [.NET Server SDK topic][7] or the [Node.js Server SDK topic][8].</span></span> <span data-ttu-id="1b039-129">Jeśli utworzono zaplecza aplikacji mobilnej w portalu Azure przy użyciu opcji szybkiego startu, można również użyć **łatwe tabel** w [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="1b039-129">If you created your Mobile App backend in the Azure portal using the QuickStart, you can also use the **Easy tables** setting in the [Azure portal].</span></span>

### <a name="how-to-install-the-managed-client-sdk-package"></a><span data-ttu-id="1b039-130">Porady: Instalowanie pakietu SDK zarządzanego klienta</span><span class="sxs-lookup"><span data-stu-id="1b039-130">How to: Install the managed client SDK package</span></span>
<span data-ttu-id="1b039-131">Użyj jednej z następujących metod można zainstalować pakietu SDK zarządzanego klienta dla aplikacji mobilnych z [NuGet][9]:</span><span class="sxs-lookup"><span data-stu-id="1b039-131">Use one of the following methods to install the managed client SDK package for Mobile Apps from [NuGet][9]:</span></span>

* <span data-ttu-id="1b039-132">**Visual Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Zarządzaj pakietami NuGet**, wyszukaj `Microsoft.Azure.Mobile.Client` pakietu, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="1b039-132">**Visual Studio** Right-click your project, click **Manage NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client` package, then click **Install**.</span></span>
* <span data-ttu-id="1b039-133">**Program Xamarin Studio** kliknij prawym przyciskiem myszy projekt, kliknij przycisk **Dodaj** > **Dodawanie pakietów NuGet**, wyszukaj `Microsoft.Azure.Mobile.Client `pakietu, a następnie kliknij przycisk **Dodaj Pakiet**.</span><span class="sxs-lookup"><span data-stu-id="1b039-133">**Xamarin Studio** Right-click your project, click **Add** > **Add NuGet Packages**, search for the `Microsoft.Azure.Mobile.Client `package, and then click **Add Package**.</span></span>

<span data-ttu-id="1b039-134">W pliku głównym działaniu, pamiętaj, aby dodać następujące **przy użyciu** instrukcji:</span><span class="sxs-lookup"><span data-stu-id="1b039-134">In your main activity file, remember to add the following **using** statement:</span></span>

```
using Microsoft.WindowsAzure.MobileServices;
```

### <span data-ttu-id="1b039-135"><a name="symbolsource"></a>Porady: Praca z symboli debugowania w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b039-135"><a name="symbolsource"></a>How to: Work with debug symbols in Visual Studio</span></span>
<span data-ttu-id="1b039-136">Symbole dla przestrzeni nazw Microsoft.Azure.Mobile są dostępne na [SymbolSource][10].</span><span class="sxs-lookup"><span data-stu-id="1b039-136">The symbols for the Microsoft.Azure.Mobile namespace are available on [SymbolSource][10].</span></span>  <span data-ttu-id="1b039-137">Zapoznaj się [instrukcje SymbolSource] [ 11] SymbolSource jest integrowana z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b039-137">Refer to the [SymbolSource instructions][11] to integrate SymbolSource with Visual Studio.</span></span>

## <span data-ttu-id="1b039-138"><a name="create-client"></a>Tworzenie klienta Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="1b039-138"><a name="create-client"></a>Create the Mobile Apps client</span></span>
<span data-ttu-id="1b039-139">Poniższy kod tworzy [MobileServiceClient] [ 12] obiekt, który umożliwia dostęp do zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-139">The following code creates the [MobileServiceClient][12] object that is used to access your Mobile App backend.</span></span>

```
var client = new MobileServiceClient("MOBILE_APP_URL");
```

<span data-ttu-id="1b039-140">W powyższym kodzie Zamień `MOBILE_APP_URL` z adresem URL zaplecza aplikacji mobilnej, który znajduje się w bloku dla zaplecza aplikacji mobilnej w [portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="1b039-140">In the preceding code, replace `MOBILE_APP_URL` with the URL of the Mobile App backend, which is found in the blade for your Mobile App backend in the [Azure portal].</span></span> <span data-ttu-id="1b039-141">Obiekt MobileServiceClient powinny być jako pojedyncza.</span><span class="sxs-lookup"><span data-stu-id="1b039-141">The MobileServiceClient object should be a singleton.</span></span>

## <a name="work-with-tables"></a><span data-ttu-id="1b039-142">Praca z tabelami</span><span class="sxs-lookup"><span data-stu-id="1b039-142">Work with Tables</span></span>
<span data-ttu-id="1b039-143">Poniższa sekcja zawiera szczegóły dotyczące jak wyszukiwanie i pobieranie rekordów i modyfikować danych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-143">The following section details how to search and retrieve records and modify the data within the table.</span></span>  <span data-ttu-id="1b039-144">Omówiono następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="1b039-144">The following topics are covered:</span></span>

* [<span data-ttu-id="1b039-145">Tworzenie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="1b039-145">Create a table reference</span></span>](#instantiating)
* [<span data-ttu-id="1b039-146">Dane zapytania</span><span class="sxs-lookup"><span data-stu-id="1b039-146">Query data</span></span>](#querying)
* [<span data-ttu-id="1b039-147">Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="1b039-147">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="1b039-148">Sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="1b039-148">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="1b039-149">Zwróć dane strony</span><span class="sxs-lookup"><span data-stu-id="1b039-149">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="1b039-150">Wybrać określone kolumny</span><span class="sxs-lookup"><span data-stu-id="1b039-150">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="1b039-151">Wyszukaj według identyfikatora</span><span class="sxs-lookup"><span data-stu-id="1b039-151">Look up a record by Id</span></span>](#lookingup)
* [<span data-ttu-id="1b039-152">Dotyczących zapytań bez typu</span><span class="sxs-lookup"><span data-stu-id="1b039-152">Dealing with untyped queries</span></span>](#untypedqueries)
* [<span data-ttu-id="1b039-153">Wstawianie danych</span><span class="sxs-lookup"><span data-stu-id="1b039-153">Inserting data</span></span>](#inserting)
* [<span data-ttu-id="1b039-154">Aktualizowanie danych</span><span class="sxs-lookup"><span data-stu-id="1b039-154">Updating data</span></span>](#updating)
* [<span data-ttu-id="1b039-155">Usuwanie danych</span><span class="sxs-lookup"><span data-stu-id="1b039-155">Deleting data</span></span>](#deleting)
* [<span data-ttu-id="1b039-156">Rozwiązywanie konfliktów i optymistycznej współbieżności</span><span class="sxs-lookup"><span data-stu-id="1b039-156">Conflict Resolution and Optimistic Concurrency</span></span>](#optimisticconcurrency)
* [<span data-ttu-id="1b039-157">Powiązanie z interfejsem użytkownika systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1b039-157">Binding to a Windows User Interface</span></span>](#binding)
* [<span data-ttu-id="1b039-158">Zmiana rozmiaru strony</span><span class="sxs-lookup"><span data-stu-id="1b039-158">Changing the Page Size</span></span>](#pagesize)

### <span data-ttu-id="1b039-159"><a name="instantiating"></a>Porady: Tworzenie odwołania do tabeli</span><span class="sxs-lookup"><span data-stu-id="1b039-159"><a name="instantiating"></a>How to: Create a table reference</span></span>
<span data-ttu-id="1b039-160">Kod, który uzyskuje dostęp do lub modyfikuje dane w tabeli wewnętrznej bazy danych wymaga funkcji na `MobileServiceTable` obiektu.</span><span class="sxs-lookup"><span data-stu-id="1b039-160">All the code that accesses or modifies data in a backend table calls functions on the `MobileServiceTable` object.</span></span> <span data-ttu-id="1b039-161">Uzyskaj odwołanie do tabeli przez wywołanie metody [Metoda GetTable] metody, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-161">Obtain a reference to the table by calling the [GetTable] method, as follows:</span></span>

```
IMobileServiceTable<TodoItem> todoTable = client.GetTable<TodoItem>();
```

<span data-ttu-id="1b039-162">Zwrócony obiekt korzysta z modelu typu serializacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-162">The returned object uses the typed serialization model.</span></span> <span data-ttu-id="1b039-163">Obsługiwane jest również modelem serializacji bez typu.</span><span class="sxs-lookup"><span data-stu-id="1b039-163">An untyped serialization model is also supported.</span></span> <span data-ttu-id="1b039-164">Poniższy przykład [tworzy odwołania do tabeli bez typu]:</span><span class="sxs-lookup"><span data-stu-id="1b039-164">The following example [creates a reference to an untyped table]:</span></span>

```
// Get an untyped table reference
IMobileServiceTable untypedTodoTable = client.GetTable("TodoItem");
```

<span data-ttu-id="1b039-165">W zapytaniach bez typu należy określić podstawowy ciąg zapytania OData.</span><span class="sxs-lookup"><span data-stu-id="1b039-165">In untyped queries, you must specify the underlying OData query string.</span></span>

### <span data-ttu-id="1b039-166"><a name="querying"></a>Porady: zapytania na danych z aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="1b039-166"><a name="querying"></a>How to: Query data from your Mobile App</span></span>
<span data-ttu-id="1b039-167">W tej sekcji opisano sposób wysyłania zapytań do zaplecza aplikacji mobilnej, która obejmuje następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="1b039-167">This section describes how to issue queries to the Mobile App backend, which includes the following functionality:</span></span>

* [<span data-ttu-id="1b039-168">Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="1b039-168">Filter returned data</span></span>](#filtering)
* [<span data-ttu-id="1b039-169">Sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="1b039-169">Sort returned data</span></span>](#sorting)
* [<span data-ttu-id="1b039-170">Zwróć dane strony</span><span class="sxs-lookup"><span data-stu-id="1b039-170">Return data in pages</span></span>](#paging)
* [<span data-ttu-id="1b039-171">Wybrać określone kolumny</span><span class="sxs-lookup"><span data-stu-id="1b039-171">Select specific columns</span></span>](#selecting)
* [<span data-ttu-id="1b039-172">Wyszukiwać dane według Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="1b039-172">Look up data by ID</span></span>](#lookingup)

> [!NOTE]
> <span data-ttu-id="1b039-173">Rozmiar strony oparte na serwerze jest wymuszana aby uniemożliwić wszystkie wiersze zostały zwrócone.</span><span class="sxs-lookup"><span data-stu-id="1b039-173">A server-driven page size is enforced to prevent all rows from being returned.</span></span>  <span data-ttu-id="1b039-174">Stronicowanie zachowuje żądań domyślny dla dużych zestawów danych z niekorzystnego wpływu na usługi.</span><span class="sxs-lookup"><span data-stu-id="1b039-174">Paging keeps default requests for large data sets from negatively impacting the service.</span></span>  <span data-ttu-id="1b039-175">Aby przywrócić więcej niż 50 wierszy, użyj `Skip` i `Take` metody, zgodnie z opisem w [zwrócić dane na stronach](#paging).</span><span class="sxs-lookup"><span data-stu-id="1b039-175">To return more than 50 rows, use the `Skip` and `Take` method, as described in [Return data in pages](#paging).</span></span>

### <span data-ttu-id="1b039-176"><a name="filtering"></a>Porady: Filtr zwrócił danych</span><span class="sxs-lookup"><span data-stu-id="1b039-176"><a name="filtering"></a>How to: Filter returned data</span></span>
<span data-ttu-id="1b039-177">Poniższy kod ilustruje sposób filtrowania danych, umieszczając w niej `Where` klauzuli w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="1b039-177">The following code illustrates how to filter data by including a `Where` clause in a query.</span></span> <span data-ttu-id="1b039-178">Zwraca wszystkie elementy z `todoTable` których `Complete` właściwości jest równa `false`.</span><span class="sxs-lookup"><span data-stu-id="1b039-178">It returns all items from `todoTable` whose `Complete` property is equal to `false`.</span></span> <span data-ttu-id="1b039-179">[Gdzie] funkcja ma zastosowanie wiersza filtrowania predykatu do zapytania dotyczącego tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-179">The [Where] function applies a row filtering predicate to the query against the table.</span></span>

```
// This query filters out completed TodoItems and items without a timestamp.
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToListAsync();
```

<span data-ttu-id="1b039-180">Możesz wyświetlić identyfikator URI żądania wysyłane do wewnętrznej bazy danych za pomocą komunikatów inspekcji oprogramowania, takich jak narzędzia dla deweloperów w przeglądarce lub [Fiddler].</span><span class="sxs-lookup"><span data-stu-id="1b039-180">You can view the URI of the request sent to the backend by using message inspection software, such as browser developer tools or [Fiddler].</span></span> <span data-ttu-id="1b039-181">Jeśli przyjrzymy się identyfikator URI żądania, zwróć uwagę zmodyfikowania ciągu kwerendy:</span><span class="sxs-lookup"><span data-stu-id="1b039-181">If you look at the request URI, notice that the query string is modified:</span></span>

```
GET /tables/todoitem?$filter=(complete+eq+false) HTTP/1.1
```

<span data-ttu-id="1b039-182">To żądanie OData jest przekształcana na zapytanie SQL przez zestaw SDK serwera:</span><span class="sxs-lookup"><span data-stu-id="1b039-182">This OData request is translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
```

<span data-ttu-id="1b039-183">Funkcję, która została przekazana do `Where` metody może mieć dowolną liczbę warunków.</span><span class="sxs-lookup"><span data-stu-id="1b039-183">The function that is passed to the `Where` method can have an arbitrary number of conditions.</span></span>

```
// This query filters out completed TodoItems where Text isn't null
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false && todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="1b039-184">W tym przykładzie będzie można przekształcić w kwerendzie SQL przez zestaw SDK serwera:</span><span class="sxs-lookup"><span data-stu-id="1b039-184">This example would be translated into an SQL query by the Server SDK:</span></span>

```
SELECT *
    FROM TodoItem
    WHERE ISNULL(complete, 0) = 0
          AND ISNULL(text, 0) = 0
```

<span data-ttu-id="1b039-185">To zapytanie również może zostać podzielony na wiele klauzul:</span><span class="sxs-lookup"><span data-stu-id="1b039-185">This query can also be split into multiple clauses:</span></span>

```
List<TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .Where(todoItem => todoItem.Text != null)
    .ToListAsync();
```

<span data-ttu-id="1b039-186">Te dwie metody są równoważne i mogą być używane zamiennie.</span><span class="sxs-lookup"><span data-stu-id="1b039-186">The two methods are equivalent and may be used interchangeably.</span></span>  <span data-ttu-id="1b039-187">Opcja wcześniejsze&mdash;z łączenie wielu predykatów w jednym zapytaniu&mdash;jest bardziej compact i zalecanym.</span><span class="sxs-lookup"><span data-stu-id="1b039-187">The former option&mdash;of concatenating multiple predicates in one query&mdash;is more compact and recommended.</span></span>

<span data-ttu-id="1b039-188">`Where` Klauzuli obsługuje operacje, które można przetłumaczyć podzestawu OData.</span><span class="sxs-lookup"><span data-stu-id="1b039-188">The `Where` clause supports operations that be translated into the OData subset.</span></span> <span data-ttu-id="1b039-189">Dostępne są następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="1b039-189">Operations include:</span></span>

* <span data-ttu-id="1b039-190">Operatory relacyjne (==,! =, <, < =, >, > =),</span><span class="sxs-lookup"><span data-stu-id="1b039-190">Relational operators (==, !=, <, <=, >, >=),</span></span>
* <span data-ttu-id="1b039-191">Operatory arytmetyczne (+, -, /, *, %),</span><span class="sxs-lookup"><span data-stu-id="1b039-191">Arithmetic operators (+, -, /, *, %),</span></span>
* <span data-ttu-id="1b039-192">Liczba precision (Math.Floor —, Math.Ceiling)</span><span class="sxs-lookup"><span data-stu-id="1b039-192">Number precision (Math.Floor, Math.Ceiling),</span></span>
* <span data-ttu-id="1b039-193">Funkcje ciągów (długość, Substring, Zamień, IndexOf, StartsWith, EndsWith)</span><span class="sxs-lookup"><span data-stu-id="1b039-193">String functions (Length, Substring, Replace, IndexOf, StartsWith, EndsWith),</span></span>
* <span data-ttu-id="1b039-194">Data właściwości (rok, miesiąc, dzień, godzina, minuty, sekundy),</span><span class="sxs-lookup"><span data-stu-id="1b039-194">Date properties (Year, Month, Day, Hour, Minute, Second),</span></span>
* <span data-ttu-id="1b039-195">Dostęp do właściwości obiektu i</span><span class="sxs-lookup"><span data-stu-id="1b039-195">Access properties of an object, and</span></span>
* <span data-ttu-id="1b039-196">Każdej z tych operacji łączenia wyrażenia.</span><span class="sxs-lookup"><span data-stu-id="1b039-196">Expressions combining any of these operations.</span></span>

<span data-ttu-id="1b039-197">Rozważając Server SDK obsługuje, można rozważyć [OData v3 dokumentacji].</span><span class="sxs-lookup"><span data-stu-id="1b039-197">When considering what the Server SDK supports, you can consider the [OData v3 Documentation].</span></span>

### <span data-ttu-id="1b039-198"><a name="sorting"></a>Porady: sortowanie zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="1b039-198"><a name="sorting"></a>How to: Sort returned data</span></span>
<span data-ttu-id="1b039-199">Poniższy kod ilustruje sposób sortowania danych w tym [OrderBy] lub [OrderByDescending] funkcji w zapytaniu.</span><span class="sxs-lookup"><span data-stu-id="1b039-199">The following code illustrates how to sort data by including an [OrderBy] or [OrderByDescending] function in the query.</span></span> <span data-ttu-id="1b039-200">Zwraca elementy z `todoTable` sortowane w kolejności rosnącej przez `Text` pola.</span><span class="sxs-lookup"><span data-stu-id="1b039-200">It returns items from `todoTable` sorted ascending by the `Text` field.</span></span>

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

### <span data-ttu-id="1b039-201"><a name="paging"></a>Porady: zwrócić dane na stronach</span><span class="sxs-lookup"><span data-stu-id="1b039-201"><a name="paging"></a>How to: Return data in pages</span></span>
<span data-ttu-id="1b039-202">Domyślnie wewnętrznej bazy danych zwraca tylko pierwsze 50 wierszy.</span><span class="sxs-lookup"><span data-stu-id="1b039-202">By default, the backend returns only the first 50 rows.</span></span> <span data-ttu-id="1b039-203">Można zwiększyć liczbę wierszy zwróconych przez wywołanie metody [zająć] metody.</span><span class="sxs-lookup"><span data-stu-id="1b039-203">You can increase the number of returned rows by calling the [Take] method.</span></span> <span data-ttu-id="1b039-204">Użyj `Take` wraz z [Pomiń] metodę, aby żądania dotyczące "page" całkowita zestawu danych zwróconych przez kwerendę.</span><span class="sxs-lookup"><span data-stu-id="1b039-204">Use `Take` along with the [Skip] method to request a specific "page" of the total dataset returned by the query.</span></span> <span data-ttu-id="1b039-205">Następujące zapytanie po wykonaniu zwraca pierwszych trzech elementów w tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-205">The following query, when executed, returns the top three items in the table.</span></span>

```
// Define a filtered query that returns the top 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="1b039-206">Następujące zapytanie poprawione pomija pierwszych trzech wyniki i zwraca wyniki trzech kolejnych.</span><span class="sxs-lookup"><span data-stu-id="1b039-206">The following revised query skips the first three results and returns the next three results.</span></span> <span data-ttu-id="1b039-207">To zapytanie tworzy drugi "page" dane, których rozmiar strony jest trzy elementy.</span><span class="sxs-lookup"><span data-stu-id="1b039-207">This query produces the second "page" of data, where the page size is three items.</span></span>

```
// Define a filtered query that skips the top 3 items and returns the next 3 items.
MobileServiceTableQuery<TodoItem> query = todoTable.Skip(3).Take(3);
List<TodoItem> items = await query.ToListAsync();
```

<span data-ttu-id="1b039-208">[IncludeTotalCount] metoda żąda łączną liczbę dla *wszystkie* rekordów, które mogłyby być zwracane, ignorowanie klauzuli stronicowania/limit określony:</span><span class="sxs-lookup"><span data-stu-id="1b039-208">The [IncludeTotalCount] method requests the total count for *all* the records that would have been returned, ignoring any paging/limit clause specified:</span></span>

```
query = query.IncludeTotalCount();
```

<span data-ttu-id="1b039-209">W aplikacji rzeczywistych służy zapytania podobne jak w poprzednim przykładzie z formantem pagera lub porównywalny interfejsu użytkownika do przechodzenia między stronami.</span><span class="sxs-lookup"><span data-stu-id="1b039-209">In a real world app, you can use queries similar to the preceding example with a pager control or comparable UI to navigate between pages.</span></span>

> [!NOTE]
> <span data-ttu-id="1b039-210">Aby zastąpić limit 50 wiersza w zaplecza aplikacji mobilnej, również należy zastosować [EnableQueryAttribute] publicznie GET, metoda i Określ zachowanie stronicowania.</span><span class="sxs-lookup"><span data-stu-id="1b039-210">To override the 50-row limit in a Mobile App backend, you must also apply the [EnableQueryAttribute] to the public GET method and specify the paging behavior.</span></span> <span data-ttu-id="1b039-211">Po zastosowaniu do metody poniżej maksymalny ustawiony zwrócone wiersze do 1000:</span><span class="sxs-lookup"><span data-stu-id="1b039-211">When applied to the method, the following sets the maximum returned rows to 1000:</span></span>
>
> `[EnableQuery(MaxTop=1000)]`


### <span data-ttu-id="1b039-212"><a name="selecting"></a>Porady: Wybieranie określonych kolumn</span><span class="sxs-lookup"><span data-stu-id="1b039-212"><a name="selecting"></a>How to: Select specific columns</span></span>
<span data-ttu-id="1b039-213">Można określić, do uwzględnienia w wynikach, dodając zbiór właściwości [wybierz] klauzuli do zapytania.</span><span class="sxs-lookup"><span data-stu-id="1b039-213">You can specify which set of properties to include in the results by adding a [Select] clause to your query.</span></span> <span data-ttu-id="1b039-214">Na przykład poniższy kod przedstawia sposób wybierania tylko jednego pola, a także jak wybierz i format wielu pól:</span><span class="sxs-lookup"><span data-stu-id="1b039-214">For example, the following code shows how to select just one field and also how to select and format multiple fields:</span></span>

```
// Select one field -- just the Text
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

<span data-ttu-id="1b039-215">Wszystkie funkcje opisane dotąd są dodatku, dlatego firma Microsoft może zapewnić łańcucha je.</span><span class="sxs-lookup"><span data-stu-id="1b039-215">All the functions described so far are additive, so we can keep chaining them.</span></span> <span data-ttu-id="1b039-216">Każde wywołanie łańcuchowa dotyczy jednego zapytania.</span><span class="sxs-lookup"><span data-stu-id="1b039-216">Each chained call affects more of the query.</span></span> <span data-ttu-id="1b039-217">Przykładem więcej:</span><span class="sxs-lookup"><span data-stu-id="1b039-217">One more example:</span></span>

```
MobileServiceTableQuery<TodoItem> query = todoTable
                .Where(todoItem => todoItem.Complete == false)
                .Select(todoItem => todoItem.Text)
                .Skip(3).
                .Take(3);
List<string> items = await query.ToListAsync();
```

### <span data-ttu-id="1b039-218"><a name="lookingup"></a>Porady: wyszukiwanie danych według Identyfikatora</span><span class="sxs-lookup"><span data-stu-id="1b039-218"><a name="lookingup"></a>How to: Look up data by ID</span></span>
<span data-ttu-id="1b039-219">[LookupAsync] funkcja może służyć do wyszukiwania obiektów z bazy danych przy użyciu określonego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="1b039-219">The [LookupAsync] function can be used to look up objects from the database with a particular ID.</span></span>

```
// This query filters out the item with the ID of 37BBF396-11F0-4B39-85C8-B319C729AF6D
TodoItem item = await todoTable.LookupAsync("37BBF396-11F0-4B39-85C8-B319C729AF6D");
```

### <span data-ttu-id="1b039-220"><a name="untypedqueries"></a>Porady: wykonywanie zapytań bez typu</span><span class="sxs-lookup"><span data-stu-id="1b039-220"><a name="untypedqueries"></a>How to: Execute untyped queries</span></span>
<span data-ttu-id="1b039-221">Podczas wykonywania zapytania za pomocą obiektu tabeli bez typu, należy jawnie określić parametry zapytania OData, wywołując [ReadAsync], jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1b039-221">When executing a query using an untyped table object, you must explicitly specify the OData query string by calling [ReadAsync], as in the following example:</span></span>

```
// Lookup untyped data using OData
JToken untypedItems = await untypedTodoTable.ReadAsync("$filter=complete eq 0&$orderby=text");
```

<span data-ttu-id="1b039-222">Możesz odzyskać wartości JSON, które można używać jak zbioru właściwości.</span><span class="sxs-lookup"><span data-stu-id="1b039-222">You get back JSON values that you can use like a property bag.</span></span> <span data-ttu-id="1b039-223">Aby uzyskać więcej informacji dotyczących JToken i Newtonsoft Json.NET, zobacz [Json.NET] lokacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-223">For more information on JToken and Newtonsoft Json.NET, see the [Json.NET] site.</span></span>

### <span data-ttu-id="1b039-224"><a name="inserting"></a>Porady: wstawianie danych do zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="1b039-224"><a name="inserting"></a>How to: Insert data into a Mobile App backend</span></span>
<span data-ttu-id="1b039-225">Wszystkie typy klientów musi zawierać element członkowski o nazwie **identyfikator**, który jest domyślnie ciąg.</span><span class="sxs-lookup"><span data-stu-id="1b039-225">All client types must contain a member named **Id**, which is by default a string.</span></span> <span data-ttu-id="1b039-226">To **identyfikator** jest wymagane do przeprowadzenia operacji CRUD i synchronizacji w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1b039-226">This **Id** is required to perform CRUD operations and for offline sync.</span></span> <span data-ttu-id="1b039-227">Poniższy kod przedstawia sposób użycia [InsertAsync] metodę, aby wstawić nowe wiersze do tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-227">The following code illustrates how to use the [InsertAsync] method to insert new rows into a table.</span></span> <span data-ttu-id="1b039-228">Parametr zawiera dane są wstawiane jako obiektu .NET.</span><span class="sxs-lookup"><span data-stu-id="1b039-228">The parameter contains the data to be inserted as a .NET object.</span></span>

```
await todoTable.InsertAsync(todoItem);
```

<span data-ttu-id="1b039-229">Jeśli wartość Unikatowy identyfikator niestandardową nie wchodzi w `todoItem` podczas wstawiania identyfikator GUID jest generowany przez serwer.</span><span class="sxs-lookup"><span data-stu-id="1b039-229">If a unique custom ID value is not included in the `todoItem` during an insert, a GUID is generated by the server.</span></span>
<span data-ttu-id="1b039-230">Możesz pobrać wygenerowanego identyfikatora, sprawdzając obiektu po wywołaniu zwraca.</span><span class="sxs-lookup"><span data-stu-id="1b039-230">You can retrieve the generated Id by inspecting the object after the call returns.</span></span>

<span data-ttu-id="1b039-231">Do wstawiania danych bez typu, może korzystać z Json.NET:</span><span class="sxs-lookup"><span data-stu-id="1b039-231">To insert untyped data, you may take advantage of Json.NET:</span></span>

```
JObject jo = new JObject();
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

<span data-ttu-id="1b039-232">Oto przykład przy użyciu adresu e-mail jako identyfikator unikatowy ciąg:</span><span class="sxs-lookup"><span data-stu-id="1b039-232">Here is an example using an email address as a unique string id:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "myemail@emaildomain.com");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.InsertAsync(jo);
```

### <a name="working-with-id-values"></a><span data-ttu-id="1b039-233">Praca z wartościami identyfikatorów</span><span class="sxs-lookup"><span data-stu-id="1b039-233">Working with ID values</span></span>
<span data-ttu-id="1b039-234">Aplikacje mobilne obsługuje niestandardowy ciąg unikatowe wartości w tabeli **identyfikator** kolumny.</span><span class="sxs-lookup"><span data-stu-id="1b039-234">Mobile Apps supports unique custom string values for the table's **id** column.</span></span> <span data-ttu-id="1b039-235">Wartość ciągu umożliwia aplikacjom użyć niestandardowej wartości, takie jak adresy e-mail lub nazwy użytkownika dla identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="1b039-235">A string value allows applications to use custom values such as email addresses or user names for the ID.</span></span>  <span data-ttu-id="1b039-236">Identyfikatory ciągów dostarczyć następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1b039-236">String IDs provide you with the following benefits:</span></span>

* <span data-ttu-id="1b039-237">Identyfikatory są generowane bez wprowadzania podróż do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1b039-237">IDs are generated without making a round trip to the database.</span></span>
* <span data-ttu-id="1b039-238">Rekordy są łatwiejsze do scalenia z różnych tabel lub baz danych.</span><span class="sxs-lookup"><span data-stu-id="1b039-238">Records are easier to merge from different tables or databases.</span></span>
* <span data-ttu-id="1b039-239">Wartości identyfikatorów można lepiej zintegrować z logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-239">IDs values can integrate better with an application's logic.</span></span>

<span data-ttu-id="1b039-240">Jeśli wartość Identyfikatora ciągu nie jest ustawiony na wstawionego rekordu, zaplecza aplikacji mobilnej generuje unikatową wartość dla identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="1b039-240">When a string ID value is not set on an inserted record, the Mobile App backend generates a unique value for the ID.</span></span> <span data-ttu-id="1b039-241">Można użyć [Guid.NewGuid] do generowania własnych wartości Identyfikatora klienta albo w wewnętrznej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="1b039-241">You can use the [Guid.NewGuid] method to generate your own ID values, either on the client or in the backend.</span></span>

```
JObject jo = new JObject();
jo.Add("id", Guid.NewGuid().ToString("N"));
```

### <span data-ttu-id="1b039-242"><a name="modifying"></a>Porady: modyfikowanie danych w zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="1b039-242"><a name="modifying"></a>How to: Modify data in a Mobile App backend</span></span>
<span data-ttu-id="1b039-243">Poniższy kod przedstawia sposób użycia [UpdateAsync] metodę, aby zaktualizować istniejący rekord z tym samym Identyfikatorem nowymi informacjami.</span><span class="sxs-lookup"><span data-stu-id="1b039-243">The following code illustrates how to use the [UpdateAsync] method to update an existing record with the same ID with new information.</span></span> <span data-ttu-id="1b039-244">Parametr zawiera dane mają zostać zaktualizowane w obiektu .NET.</span><span class="sxs-lookup"><span data-stu-id="1b039-244">The parameter contains the data to be updated as a .NET object.</span></span>

```
await todoTable.UpdateAsync(todoItem);
```

<span data-ttu-id="1b039-245">Aby zaktualizować dane bez typu, użytkownik może skorzystać z [Json.NET] w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-245">To update untyped data, you may take advantage of [Json.NET] as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
jo.Add("Text", "Hello World");
jo.Add("Complete", false);
var inserted = await table.UpdateAsync(jo);
```

<span data-ttu-id="1b039-246">`id` Należy podać wartość pola podczas wprowadzania aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-246">An `id` field must be specified when making an update.</span></span> <span data-ttu-id="1b039-247">Używa wewnętrznej bazy danych `id` pola do identyfikowania wiersza, który do aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-247">The backend uses the `id` field to identify which row to update.</span></span> <span data-ttu-id="1b039-248">`id` Pola można uzyskać od wyniku `InsertAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="1b039-248">The `id` field can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="1b039-249">`ArgumentException` Jest zgłaszane, gdy zostanie podjęta próba zaktualizowania elementu bez podawania `id` wartość.</span><span class="sxs-lookup"><span data-stu-id="1b039-249">An `ArgumentException` is raised if you try to update an item without providing the `id` value.</span></span>

### <span data-ttu-id="1b039-250"><a name="deleting"></a>Porady: usuwanie danych zaplecza aplikacji mobilnej</span><span class="sxs-lookup"><span data-stu-id="1b039-250"><a name="deleting"></a>How to: Delete data in a Mobile App backend</span></span>
<span data-ttu-id="1b039-251">Poniższy kod przedstawia sposób użycia [DeleteAsync] do usunięcia istniejącego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="1b039-251">The following code illustrates how to use the [DeleteAsync] method to delete an existing instance.</span></span> <span data-ttu-id="1b039-252">Wystąpienie jest identyfikowane przez `id` zestawie pól na `todoItem`.</span><span class="sxs-lookup"><span data-stu-id="1b039-252">The instance is identified by the `id` field set on the `todoItem`.</span></span>

```
await todoTable.DeleteAsync(todoItem);
```

<span data-ttu-id="1b039-253">Aby usunąć dane bez typu, możesz może korzystać z struktury Json.NET w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-253">To delete untyped data, you may take advantage of Json.NET as follows:</span></span>

```
JObject jo = new JObject();
jo.Add("id", "37BBF396-11F0-4B39-85C8-B319C729AF6D");
await table.DeleteAsync(jo);
```

<span data-ttu-id="1b039-254">Po wprowadzeniu żądanie usunięcia, należy określić identyfikator.</span><span class="sxs-lookup"><span data-stu-id="1b039-254">When you make a delete request, an ID must be specified.</span></span> <span data-ttu-id="1b039-255">Inne właściwości nie są przekazywane do usługi lub są ignorowane w usłudze.</span><span class="sxs-lookup"><span data-stu-id="1b039-255">Other properties are not passed to the service or are ignored at the service.</span></span> <span data-ttu-id="1b039-256">Wynik `DeleteAsync` wywołanie jest zwykle `null`.</span><span class="sxs-lookup"><span data-stu-id="1b039-256">The result of a `DeleteAsync` call is usually `null`.</span></span> <span data-ttu-id="1b039-257">Identyfikator, który umożliwia przekazywanie można uzyskać od wyniku `InsertAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="1b039-257">The ID to pass in can be obtained from the result of the `InsertAsync` call.</span></span> <span data-ttu-id="1b039-258">A `MobileServiceInvalidOperationException` jest generowany podczas próby usunięcia elementu bez określania `id` pola.</span><span class="sxs-lookup"><span data-stu-id="1b039-258">A `MobileServiceInvalidOperationException` is thrown when you try to delete an item without specifying the `id` field.</span></span>

### <span data-ttu-id="1b039-259"><a name="optimisticconcurrency"></a>Porady: użycie optymistycznej współbieżności do rozwiązywania konfliktów</span><span class="sxs-lookup"><span data-stu-id="1b039-259"><a name="optimisticconcurrency"></a>How to: Use Optimistic Concurrency for conflict resolution</span></span>
<span data-ttu-id="1b039-260">Dwa lub więcej klientów może zapisać zmiany na tym samym elemencie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="1b039-260">Two or more clients may write changes to the same item at the same time.</span></span> <span data-ttu-id="1b039-261">Bez wykrywania konfliktów ostatniego zapisu zastąpiłaby wszelkie poprzednie aktualizacje.</span><span class="sxs-lookup"><span data-stu-id="1b039-261">Without conflict detection, the last write would overwrite any previous updates.</span></span> <span data-ttu-id="1b039-262">**Optymistyczne sterowanie współbieżnością** założono, że każdej transakcji można zatwierdzić i dlatego nie używa żadnych zasobów blokowania.</span><span class="sxs-lookup"><span data-stu-id="1b039-262">**Optimistic concurrency control** assumes that each transaction can commit and therefore does not use any resource locking.</span></span>  <span data-ttu-id="1b039-263">Przed zatwierdzeniem transakcji, optymistyczne sterowanie współbieżnością sprawdza, czy nie inne transakcje nie zmienione dane.</span><span class="sxs-lookup"><span data-stu-id="1b039-263">Before committing a transaction, optimistic concurrency control verifies that no other transaction has modified the data.</span></span> <span data-ttu-id="1b039-264">W przypadku modyfikacji danych przekazywanie transakcja zostanie wycofana.</span><span class="sxs-lookup"><span data-stu-id="1b039-264">If the data has been modified, the committing transaction is rolled back.</span></span>

<span data-ttu-id="1b039-265">Aplikacje mobilne obsługuje optymistyczne sterowanie współbieżnością za śledzenie zmian przy użyciu każdego elementu `version` kolumny właściwości systemu, który jest zdefiniowany dla każdej tabeli w zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-265">Mobile Apps supports optimistic concurrency control by tracking changes to each item using the `version` system property column that is defined for each table in your Mobile App backend.</span></span> <span data-ttu-id="1b039-266">Przy każdym aktualizacji rekordu Mobile Apps ustawia `version` właściwości dla tego rekordu na nową wartość.</span><span class="sxs-lookup"><span data-stu-id="1b039-266">Each time a record is updated, Mobile Apps sets the `version` property for that record to a new value.</span></span> <span data-ttu-id="1b039-267">Podczas każdego żądania aktualizacji `version` właściwości rekordu dołączony do żądania jest porównywany z tą samą właściwością dla rekordu na serwerze.</span><span class="sxs-lookup"><span data-stu-id="1b039-267">During each update request, the `version` property of the record included with the request is compared to the same property for the record on the server.</span></span> <span data-ttu-id="1b039-268">Jeśli wersja przekazany z żądania jest niezgodna z wewnętrznej bazy danych, a następnie wywołuje biblioteki klienta `MobileServicePreconditionFailedException<T>` wyjątku.</span><span class="sxs-lookup"><span data-stu-id="1b039-268">If the version passed with the request does not match the backend, then the client library raises a `MobileServicePreconditionFailedException<T>` exception.</span></span> <span data-ttu-id="1b039-269">Typ dołączonego wyjątek jest rekord z wewnętrznej bazy danych zawierającą wersję serwerów rekordu.</span><span class="sxs-lookup"><span data-stu-id="1b039-269">The type included with the exception is the record from the backend containing the servers version of the record.</span></span> <span data-ttu-id="1b039-270">Aplikacja może następnie dzięki tym informacjom można zdecydować, czy można wykonać żądania aktualizacji ponownie, podając poprawny `version` wartość z wewnętrznej bazy danych w celu zatwierdzenia zmian.</span><span class="sxs-lookup"><span data-stu-id="1b039-270">The application can then use this information to decide whether to execute the update request again with the correct `version` value from the backend to commit changes.</span></span>

<span data-ttu-id="1b039-271">Zdefiniuj kolumny w klasie tabeli dla `version` właściwości systemu, aby włączyć optymistycznej współbieżności.</span><span class="sxs-lookup"><span data-stu-id="1b039-271">Define a column on the table class for the `version` system property to enable optimistic concurrency.</span></span> <span data-ttu-id="1b039-272">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1b039-272">For example:</span></span>

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

<span data-ttu-id="1b039-273">Aplikacje przy użyciu tabel bez typu Włącz optymistycznej współbieżności, ustawiając `Version` Flaga na `SystemProperties` tabeli w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="1b039-273">Applications using untyped tables enable optimistic concurrency by setting the `Version` flag on the `SystemProperties` of the table as follows.</span></span>

```
//Enable optimistic concurrency by retrieving version
todoTable.SystemProperties |= MobileServiceSystemProperties.Version;
```

<span data-ttu-id="1b039-274">Oprócz włączenia optymistycznej współbieżności, musi również catch `MobileServicePreconditionFailedException<T>` wyjątek w kodzie podczas wywoływania metody [UpdateAsync].</span><span class="sxs-lookup"><span data-stu-id="1b039-274">In addition to enabling optimistic concurrency, you must also catch the `MobileServicePreconditionFailedException<T>` exception in your code when calling [UpdateAsync].</span></span>  <span data-ttu-id="1b039-275">Rozwiąż konflikt, stosując poprawny `version` zaktualizowany rekord i wywołanie [UpdateAsync] z rekordem rozwiązane.</span><span class="sxs-lookup"><span data-stu-id="1b039-275">Resolve the conflict by applying the correct `version` to the updated record and call [UpdateAsync] with the resolved record.</span></span> <span data-ttu-id="1b039-276">Poniższy kod przedstawia sposób rozwiązania konfliktu zapisu raz wykryto:</span><span class="sxs-lookup"><span data-stu-id="1b039-276">The following code shows how to resolve a write conflict once detected:</span></span>

```
private async void UpdateToDoItem(TodoItem item)
{
    MobileServicePreconditionFailedException<TodoItem> exception = null;

    try
    {
        //update at the remote table
        await todoTable.UpdateAsync(item);
    }
    catch (MobileServicePreconditionFailedException<TodoItem> writeException)
    {
        exception = writeException;
    }

    if (exception != null)
    {
        // Conflict detected, the item has changed since the last query
        // Resolve the conflict between the local and server item
        await ResolveConflict(item, exception.Item);
    }
}


private async Task ResolveConflict(TodoItem localItem, TodoItem serverItem)
{
    //Ask user to choose the resoltion between versions
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
        // To resolve the conflict, update the version of the item being committed. Otherwise, you will keep
        // catching a MobileServicePreConditionFailedException.
        localItem.Version = serverItem.Version;

        // Updating recursively here just in case another change happened while the user was making a decision
        UpdateToDoItem(localItem);
    };

    ServerBtn.Invoked = async (IUICommand command) =>
    {
        RefreshTodoItems();
    };

    await msgDialog.ShowAsync();
}
```

<span data-ttu-id="1b039-277">Aby uzyskać więcej informacji, zobacz [w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps] tematu.</span><span class="sxs-lookup"><span data-stu-id="1b039-277">For more information, see the [Offline Data Sync in Azure Mobile Apps] topic.</span></span>

### <span data-ttu-id="1b039-278"><a name="binding"></a>Porady: powiązanie Mobile Apps danych interfejsu użytkownika systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1b039-278"><a name="binding"></a>How to: Bind Mobile Apps data to a Windows user interface</span></span>
<span data-ttu-id="1b039-279">W tej sekcji przedstawiono sposób wyświetlania obiektów zwracanych danych za pomocą elementów interfejsu użytkownika w aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1b039-279">This section shows how to display returned data objects using UI elements in a Windows app.</span></span>  <span data-ttu-id="1b039-280">Poniższy przykładowy kod wiąże źródła listy przy użyciu zapytania niezakończonych elementów.</span><span class="sxs-lookup"><span data-stu-id="1b039-280">The following example code binds to the source of the list with a query for incomplete items.</span></span> <span data-ttu-id="1b039-281">[MobileServiceCollection] tworzy kolekcję przenośnych aplikacji obsługujących powiązania.</span><span class="sxs-lookup"><span data-stu-id="1b039-281">The [MobileServiceCollection] creates a Mobile Apps-aware binding collection.</span></span>

```
// This query filters out completed TodoItems.
MobileServiceCollection<TodoItem, TodoItem> items = await todoTable
    .Where(todoItem => todoItem.Complete == false)
    .ToCollectionAsync();

// itemsControl is an IEnumerable that could be bound to a UI list control
IEnumerable itemsControl  = items;

// Bind this to a ListBox
ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="1b039-282">Niektóre formanty w zarządzanego środowiska wykonawczego obsługują interfejs o nazwie [ISupportIncrementalLoading].</span><span class="sxs-lookup"><span data-stu-id="1b039-282">Some controls in the managed runtime support an interface called [ISupportIncrementalLoading].</span></span> <span data-ttu-id="1b039-283">Ten interfejs umożliwia formantów zażądać dodatkowych danych, gdy użytkownik przewija.</span><span class="sxs-lookup"><span data-stu-id="1b039-283">This interface allows controls to request extra data when the user scrolls.</span></span> <span data-ttu-id="1b039-284">Jest wbudowaną obsługę ten interfejs dla uniwersalnych aplikacji systemu Windows za pośrednictwem [MobileServiceIncrementalLoadingCollection], który automatycznie obsługuje wywołania z kontrolki.</span><span class="sxs-lookup"><span data-stu-id="1b039-284">There is built-in support for this interface for universal Windows apps via [MobileServiceIncrementalLoadingCollection], which automatically handles the calls from the controls.</span></span> <span data-ttu-id="1b039-285">Użyj `MobileServiceIncrementalLoadingCollection` w aplikacjach systemu Windows w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-285">Use `MobileServiceIncrementalLoadingCollection` in Windows apps as follows:</span></span>

```
MobileServiceIncrementalLoadingCollection<TodoItem,TodoItem> items;
items = todoTable.Where(todoItem => todoItem.Complete == false).ToIncrementalLoadingCollection();

ListBox lb = new ListBox();
lb.ItemsSource = items;
```

<span data-ttu-id="1b039-286">Aby użyć nowej kolekcji na aplikacje dla systemu Windows Phone 8 i "Silverlight", użyj `ToCollection` metody rozszerzenia na `IMobileServiceTableQuery<T>` i `IMobileServiceTable<T>`.</span><span class="sxs-lookup"><span data-stu-id="1b039-286">To use the new collection on Windows Phone 8 and "Silverlight" apps, use the `ToCollection` extension methods on `IMobileServiceTableQuery<T>` and `IMobileServiceTable<T>`.</span></span> <span data-ttu-id="1b039-287">Aby załadować dane, należy wywołać `LoadMoreItemsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="1b039-287">To load data, call `LoadMoreItemsAsync()`.</span></span>

```
MobileServiceCollection<TodoItem, TodoItem> items = todoTable.Where(todoItem => todoItem.Complete==false).ToCollection();
await items.LoadMoreItemsAsync();
```

<span data-ttu-id="1b039-288">Jeśli używasz kolekcji utworzona przez wywołanie metody `ToCollectionAsync` lub `ToCollection`, pobrać kolekcję, która może być powiązana z kontrolek interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b039-288">When you use the collection created by calling `ToCollectionAsync` or `ToCollection`, you get a collection that can be bound to UI controls.</span></span>  <span data-ttu-id="1b039-289">Ta kolekcja jest obsługujący stronicowania.</span><span class="sxs-lookup"><span data-stu-id="1b039-289">This collection is paging-aware.</span></span>  <span data-ttu-id="1b039-290">Ponieważ kolekcja jest podczas ładowania danych z sieci, podczas ładowania czasami kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1b039-290">Since the collection is loading data from the network, loading sometimes fails.</span></span> <span data-ttu-id="1b039-291">Do obsługi tych błędów, należy zastąpić `OnException` metoda `MobileServiceIncrementalLoadingCollection` do obsługi wyjątków w wyniku wywołania `LoadMoreItemsAsync`.</span><span class="sxs-lookup"><span data-stu-id="1b039-291">To handle such failures, override the `OnException` method on `MobileServiceIncrementalLoadingCollection` to handle exceptions resulting from calls to `LoadMoreItemsAsync`.</span></span>

<span data-ttu-id="1b039-292">Należy wziąć pod uwagę, jeśli ta tabela ma wiele pól, ale chcesz wyświetlić niektóre z nich w formantu.</span><span class="sxs-lookup"><span data-stu-id="1b039-292">Consider if your table has many fields but you only want to display some of them in your control.</span></span> <span data-ttu-id="1b039-293">Wskazówki można używać w poprzedniej sekcji "[wybrać określone kolumny](#selecting)" Aby wybrać określone kolumny do wyświetlenia w interfejsie użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b039-293">You may use the guidance in the preceding section "[Select specific columns](#selecting)" to select specific columns to display in the UI.</span></span>

### <span data-ttu-id="1b039-294"><a name="pagesize"></a>Zmień rozmiar strony</span><span class="sxs-lookup"><span data-stu-id="1b039-294"><a name="pagesize"></a>Change the Page size</span></span>
<span data-ttu-id="1b039-295">Aplikacje mobilne platformy Azure zwraca maksymalnie 50 elementów na żądanie domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1b039-295">Azure Mobile Apps returns a maximum of 50 items per request by default.</span></span>  <span data-ttu-id="1b039-296">Aby zmienić rozmiar stronicowania, należy zwiększyć maksymalny rozmiar strony na kliencie i serwerze.</span><span class="sxs-lookup"><span data-stu-id="1b039-296">You can change the paging size by increasing the maximum page size on both the client and server.</span></span>  <span data-ttu-id="1b039-297">Aby zwiększyć rozmiar żądanej strony, określ `PullOptions` przy użyciu `PullAsync()`:</span><span class="sxs-lookup"><span data-stu-id="1b039-297">To increase the requested page size, specify `PullOptions` when using `PullAsync()`:</span></span>

```
PullOptions pullOptions = new PullOptions
    {
        MaxPageSize = 100
    };
```

<span data-ttu-id="1b039-298">Zakładając, że zostały wykonane `PageSize` równa lub większa niż 100 w ramach serwera żądanie zwraca maksymalnie 100 elementów.</span><span class="sxs-lookup"><span data-stu-id="1b039-298">Assuming you have made the `PageSize` equal to or greater than 100 within the server, a request returns up to 100 items.</span></span>

## <span data-ttu-id="1b039-299"><a name="#offlinesync"></a>Praca z tabelami w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="1b039-299"><a name="#offlinesync"></a>Work with Offline Tables</span></span>
<span data-ttu-id="1b039-300">Tabele w trybie offline używają lokalnych danych sklepu SQLite do użycia w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="1b039-300">Offline tables use a local SQLite store to store data for use when offline.</span></span>  <span data-ttu-id="1b039-301">Tabela wszystkie operacje są wykonywane na lokalnym serwerze SQLite przechowywać zamiast magazynu na serwerze zdalnym.</span><span class="sxs-lookup"><span data-stu-id="1b039-301">All table operations are done against the local SQLite store instead of the remote server store.</span></span>  <span data-ttu-id="1b039-302">Aby utworzyć tabelę w trybie offline, należy najpierw przygotować projektu:</span><span class="sxs-lookup"><span data-stu-id="1b039-302">To create an offline table, first prepare your project:</span></span>

1. <span data-ttu-id="1b039-303">W programie Visual Studio, kliknij prawym przyciskiem myszy rozwiązanie > **Zarządzaj pakietami NuGet rozwiązania...** , następnie wyszukaj i zainstaluj **Microsoft.Azure.Mobile.Client.SQLiteStore** pakietu NuGet dla wszystkich projektów w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="1b039-303">In Visual Studio, right-click the solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in the solution.</span></span>
2. <span data-ttu-id="1b039-304">(Opcjonalnie) Do obsługi urządzeń z systemem Windows, należy zainstalować jedną z następujących pakietów środowiska uruchomieniowego SQLite:</span><span class="sxs-lookup"><span data-stu-id="1b039-304">(Optional) To support Windows devices, install one of the following SQLite runtime packages:</span></span>

   * <span data-ttu-id="1b039-305">**Środowisko uruchomieniowe Windows 8.1:** zainstalować [SQLite dla Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="1b039-305">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="1b039-306">**Windows Phone 8.1:** zainstalować [SQLite dla Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="1b039-306">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="1b039-307">**Platforma uniwersalna systemu Windows** zainstalować [SQLite dla uniwersalnych systemu Windows][5].</span><span class="sxs-lookup"><span data-stu-id="1b039-307">**Universal Windows Platform** Install [SQLite for the Universal Windows][5].</span></span>
3. <span data-ttu-id="1b039-308">(Opcjonalnie).</span><span class="sxs-lookup"><span data-stu-id="1b039-308">(Optional).</span></span> <span data-ttu-id="1b039-309">Dla urządzeń z systemem Windows, kliknij przycisk **odwołania** > **Dodawanie odwołania...** , rozwiń węzeł **Windows** folder > **rozszerzenia**, następnie włączyć odpowiednie **SQLite dla systemu Windows** zestawu SDK oraz **2013 środowiska uruchomieniowego visual C++ dla systemu Windows** zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1b039-309">For Windows devices, click **References** > **Add Reference...**, expand the **Windows** folder > **Extensions**, then enable the appropriate **SQLite for Windows** SDK along with the **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="1b039-310">Nazwy zestawu SDK SQLite się nieco różnić z każdej z platform Windows.</span><span class="sxs-lookup"><span data-stu-id="1b039-310">The SQLite SDK names vary slightly with each Windows platform.</span></span>

<span data-ttu-id="1b039-311">Aby można było utworzyć odwołania do tabeli, należy przygotować magazynu lokalnego:</span><span class="sxs-lookup"><span data-stu-id="1b039-311">Before a table reference can be created, the local store must be prepared:</span></span>

```
var store = new MobileServiceSQLiteStore(Constants.OfflineDbPath);
store.DefineTable<TodoItem>();

//Initializes the SyncContext using the default IMobileServiceSyncHandler.
await this.client.SyncContext.InitializeAsync(store);
```

<span data-ttu-id="1b039-312">Zainicjowanie magazynu odbywa się normalnie natychmiast po utworzeniu klienta.</span><span class="sxs-lookup"><span data-stu-id="1b039-312">Store initialization is normally done immediately after the client is created.</span></span>  <span data-ttu-id="1b039-313">**OfflineDbPath** powinny być odpowiednie do użycia na wszystkich platformach obsługiwanych nazwę pliku.</span><span class="sxs-lookup"><span data-stu-id="1b039-313">The **OfflineDbPath** should be a filename suitable for use on all platforms that you support.</span></span>  <span data-ttu-id="1b039-314">Jeśli ścieżka jest w pełni kwalifikowana (to znaczy rozpoczyna się od ukośnika), zostanie użyta w tej ścieżce.</span><span class="sxs-lookup"><span data-stu-id="1b039-314">If the path is a fully qualified path (that is, it starts with a slash), then that path is used.</span></span>  <span data-ttu-id="1b039-315">Jeśli ścieżka nie jest w pełni kwalifikowana, plik jest umieszczany w lokalizacji specyficzne dla platformy.</span><span class="sxs-lookup"><span data-stu-id="1b039-315">If the path is not fully qualified, the file is placed in a platform-specific location.</span></span>

* <span data-ttu-id="1b039-316">Dla urządzeń iOS i Android domyślna ścieżka to folder "Osobiste pliki".</span><span class="sxs-lookup"><span data-stu-id="1b039-316">For iOS and Android devices, the default path is the "Personal Files" folder.</span></span>
* <span data-ttu-id="1b039-317">W przypadku urządzeń z systemem Windows domyślna ścieżka to folder "AppData" specyficzne dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-317">For Windows devices, the default path is the application-specific "AppData" folder.</span></span>

<span data-ttu-id="1b039-318">Odwołanie do tabeli można uzyskać za pomocą `GetSyncTable<>` metody:</span><span class="sxs-lookup"><span data-stu-id="1b039-318">A table reference can be obtained using the `GetSyncTable<>` method:</span></span>

```
var table = client.GetSyncTable<TodoItem>();
```

<span data-ttu-id="1b039-319">Nie trzeba przeprowadzać uwierzytelnienia do użycia w trybie offline tabeli.</span><span class="sxs-lookup"><span data-stu-id="1b039-319">You do not need to authenticate to use an offline table.</span></span>  <span data-ttu-id="1b039-320">Wystarczy do uwierzytelniania, gdy komunikują się przy użyciu usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1b039-320">You only need to authenticate when you are communicating with the backend service.</span></span>

### <span data-ttu-id="1b039-321"><a name="syncoffline"></a>Trwa synchronizowanie tabelę w trybie Offline</span><span class="sxs-lookup"><span data-stu-id="1b039-321"><a name="syncoffline"></a>Syncing an Offline Table</span></span>
<span data-ttu-id="1b039-322">Tabele w trybie offline nie są zsynchronizowane z wewnętrznej bazy danych domyślnie.</span><span class="sxs-lookup"><span data-stu-id="1b039-322">Offline tables are not synchronized with the backend by default.</span></span>  <span data-ttu-id="1b039-323">Synchronizacja jest podzielony na dwie części.</span><span class="sxs-lookup"><span data-stu-id="1b039-323">Synchronization is split into two pieces.</span></span>  <span data-ttu-id="1b039-324">Wypchnij zmiany oddzielnie pobierania nowych elementów.</span><span class="sxs-lookup"><span data-stu-id="1b039-324">You can push changes separately from downloading new items.</span></span>  <span data-ttu-id="1b039-325">Oto metoda typowe synchronizacji:</span><span class="sxs-lookup"><span data-stu-id="1b039-325">Here is a typical sync method:</span></span>

```
public async Task SyncAsync()
{
    ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

    try
    {
        await this.client.SyncContext.PushAsync();

        await this.todoTable.PullAsync(
            //The first parameter is a query name that is used internally by the client SDK to implement incremental sync.
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

    // Simple error/conflict handling. A real application would handle the various errors like network conditions,
    // server conflicts and others via the IMobileServiceSyncHandler.
    if (syncErrors != null)
    {
        foreach (var error in syncErrors)
        {
            if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
            {
                //Update failed, reverting to server's copy.
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

<span data-ttu-id="1b039-326">Jeśli pierwszy argument `PullAsync` ma wartość null, synchronizacja przyrostowa nie będzie używana.</span><span class="sxs-lookup"><span data-stu-id="1b039-326">If the first argument to `PullAsync` is null, then incremental sync is not used.</span></span>  <span data-ttu-id="1b039-327">Każda operacja synchronizacji powoduje pobranie wszystkich rekordów.</span><span class="sxs-lookup"><span data-stu-id="1b039-327">Each sync operation retrieves all records.</span></span>

<span data-ttu-id="1b039-328">Zestaw SDK wykonuje niejawny `PushAsync()` przed ściąganie rekordów.</span><span class="sxs-lookup"><span data-stu-id="1b039-328">The SDK performs an implicit `PushAsync()` before pulling records.</span></span>

<span data-ttu-id="1b039-329">Obsługa konflikt się dzieje na `PullAsync()` metody.</span><span class="sxs-lookup"><span data-stu-id="1b039-329">Conflict handling happens on a `PullAsync()` method.</span></span>  <span data-ttu-id="1b039-330">Konflikty mogą dotyczyć w taki sam sposób jak tabele online.</span><span class="sxs-lookup"><span data-stu-id="1b039-330">You can deal with conflicts in the same way as online tables.</span></span>  <span data-ttu-id="1b039-331">Konflikt jest generowany po `PullAsync()` jest wywoływana zamiast podczas insert, update lub delete.</span><span class="sxs-lookup"><span data-stu-id="1b039-331">The conflict is produced when `PullAsync()` is called instead of during the insert, update, or delete.</span></span> <span data-ttu-id="1b039-332">Jeśli wystąpi konflikt wiele, są one dołączone do pojedynczego MobileServicePushFailedException.</span><span class="sxs-lookup"><span data-stu-id="1b039-332">If multiple conflicts happen, they are bundled into a single MobileServicePushFailedException.</span></span>  <span data-ttu-id="1b039-333">Obsługi każdego błędów oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="1b039-333">Handle each failure separately.</span></span>

## <span data-ttu-id="1b039-334"><a name="#customapi"></a>Praca z niestandardowego interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1b039-334"><a name="#customapi"></a>Work with a custom API</span></span>
<span data-ttu-id="1b039-335">Niestandardowy interfejs API umożliwia zdefiniowanie niestandardowe punkty końcowe, które udostępniają funkcje serwera które nie mapowania insert, update, usuwania lub operacja odczytu.</span><span class="sxs-lookup"><span data-stu-id="1b039-335">A custom API enables you to define custom endpoints that expose server functionality that does not map to an insert, update, delete, or read operation.</span></span> <span data-ttu-id="1b039-336">Przy użyciu niestandardowego interfejsu API, może mieć większą kontrolę nad wiadomości, w tym odczytywanie ustawienie nagłówki komunikatów HTTP i Definiowanie formatu treści wiadomości innych niż JSON.</span><span class="sxs-lookup"><span data-stu-id="1b039-336">By using a custom API, you can have more control over messaging, including reading and setting HTTP message headers and defining a message body format other than JSON.</span></span>

<span data-ttu-id="1b039-337">Niestandardowy interfejs API należy wywołać przez wywoływanie jednej z [InvokeApiAsync] metod na kliencie.</span><span class="sxs-lookup"><span data-stu-id="1b039-337">You call a custom API by calling one of the [InvokeApiAsync] methods on the client.</span></span> <span data-ttu-id="1b039-338">Na przykład następujący wiersz kodu wysyła żądanie POST **completeAll** interfejsu API do wewnętrznej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="1b039-338">For example, the following line of code sends a POST request to the **completeAll** API on the backend:</span></span>

```
var result = await client.InvokeApiAsync<MarkAllResult>("completeAll", System.Net.Http.HttpMethod.Post, null);
```

<span data-ttu-id="1b039-339">Ten formularz jest wywołanie metody typu i wymaga, aby **MarkAllResult** zwracany typ jest zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="1b039-339">This form is a typed method call and requires that the **MarkAllResult** return type is defined.</span></span> <span data-ttu-id="1b039-340">Obsługiwane są zarówno typu, jak i bez typu metody.</span><span class="sxs-lookup"><span data-stu-id="1b039-340">Both typed and untyped methods are supported.</span></span>

<span data-ttu-id="1b039-341">Metoda InvokeApiAsync() dołącza "/ api /" do interfejsu API, którą chcesz wywołać, chyba że interfejsu API, który rozpoczyna się od '/'.</span><span class="sxs-lookup"><span data-stu-id="1b039-341">The InvokeApiAsync() method prepends '/api/' to the API that you wish to call unless the API starts with a '/'.</span></span>
<span data-ttu-id="1b039-342">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1b039-342">For example:</span></span>

* <span data-ttu-id="1b039-343">`InvokeApiAsync("completeAll",...)`wywołuje /api/completeAll do wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="1b039-343">`InvokeApiAsync("completeAll",...)` calls /api/completeAll on the backend</span></span>
* <span data-ttu-id="1b039-344">`InvokeApiAsync("/.auth/me",...)`/.auth/me wywołania do wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="1b039-344">`InvokeApiAsync("/.auth/me",...)` calls /.auth/me on the backend</span></span>

<span data-ttu-id="1b039-345">InvokeApiAsync służy do wywołań dowolnej WebAPI, łącznie z tymi WebAPIs, które nie są zdefiniowane z usługą Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="1b039-345">You can use InvokeApiAsync to call any WebAPI, including those WebAPIs that are not defined with Azure Mobile Apps.</span></span>  <span data-ttu-id="1b039-346">Gdy używasz InvokeApiAsync() odpowiednie nagłówki, włącznie z nagłówkami uwierzytelniania są wysyłane z żądaniem.</span><span class="sxs-lookup"><span data-stu-id="1b039-346">When you use InvokeApiAsync(), the appropriate headers, including authentication headers, are sent with the request.</span></span>

## <span data-ttu-id="1b039-347"><a name="authentication"></a>Uwierzytelnianie użytkowników</span><span class="sxs-lookup"><span data-stu-id="1b039-347"><a name="authentication"></a>Authenticate users</span></span>
<span data-ttu-id="1b039-348">Aplikacje mobilne obsługuje uwierzytelniania i autoryzacji użytkowników aplikacji przy użyciu różnych dostawców tożsamości zewnętrznych: Facebook, Google, Microsoft Account, Twitter i Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b039-348">Mobile Apps supports authenticating and authorizing app users using various external identity providers: Facebook, Google, Microsoft Account, Twitter, and Azure Active Directory.</span></span> <span data-ttu-id="1b039-349">Tabele, aby ograniczyć dostęp dla określonych operacji tylko do uwierzytelnionych użytkowników można ustawić uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="1b039-349">You can set permissions on tables to restrict access for specific operations to only authenticated users.</span></span> <span data-ttu-id="1b039-350">Umożliwia także tożsamość uwierzytelnionych użytkowników do zaimplementowania reguły autoryzacji w skryptach serwera.</span><span class="sxs-lookup"><span data-stu-id="1b039-350">You can also use the identity of authenticated users to implement authorization rules in server scripts.</span></span> <span data-ttu-id="1b039-351">Aby uzyskać więcej informacji, zapoznaj się z samouczkiem [Dodawanie uwierzytelniania do aplikacji].</span><span class="sxs-lookup"><span data-stu-id="1b039-351">For more information, see the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="1b039-352">Obsługiwane są dwa przepływy uwierzytelniania: *zarządzanych przez klienta* i *serwer zarządzany* przepływu.</span><span class="sxs-lookup"><span data-stu-id="1b039-352">Two authentication flows are supported: *client-managed* and *server-managed* flow.</span></span> <span data-ttu-id="1b039-353">Serwer zarządzany przepływu zapewnia najprostszą środowisko uwierzytelniania, zależy od interfejsu uwierzytelniania sieci web dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-353">The server-managed flow provides the simplest authentication experience, as it relies on the provider's web authentication interface.</span></span> <span data-ttu-id="1b039-354">Przepływ zarządzanych przez klienta umożliwia lepszą integrację z funkcji specyficznych dla urządzenia zależy od zestawy SDK urządzenia specyficznego dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-354">The client-managed flow allows for deeper integration with device-specific capabilities as it relies on provider-specific device-specific SDKs.</span></span>

> [!NOTE]
> <span data-ttu-id="1b039-355">Zalecamy używanie przepływem zarządzanych przez klienta w aplikacjach produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="1b039-355">We recommend using a client-managed flow in your production apps.</span></span>

<span data-ttu-id="1b039-356">Aby skonfigurować uwierzytelnianie, należy zarejestrować aplikację z co najmniej jednego dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1b039-356">To set up authentication, you must register your app with one or more identity providers.</span></span>  <span data-ttu-id="1b039-357">Dostawca tożsamości generuje identyfikator klienta i klucz tajny klienta aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-357">The identity provider generates a client ID and a client secret for your app.</span></span>  <span data-ttu-id="1b039-358">Te wartości są ustawiane następnie w sieci wewnętrznej bazy danych, aby umożliwić usłudze Azure App Service uwierzytelniania/autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-358">These values are then set in your backend to enable Azure App Service authentication/authorization.</span></span>  <span data-ttu-id="1b039-359">Aby uzyskać więcej informacji, postępuj zgodnie z instrukcjami szczegółowe samouczka [Dodawanie uwierzytelniania do aplikacji].</span><span class="sxs-lookup"><span data-stu-id="1b039-359">For more information, follow the detailed instructions in the tutorial [Add authentication to your app].</span></span>

<span data-ttu-id="1b039-360">W tej sekcji omówiono następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="1b039-360">The following topics are covered in this section:</span></span>

* [<span data-ttu-id="1b039-361">Zarządzane przez klienta do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-361">Client-managed authentication</span></span>](#clientflow)
* [<span data-ttu-id="1b039-362">Serwer zarządzany uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-362">Server-managed authentication</span></span>](#serverflow)
* [<span data-ttu-id="1b039-363">Buforowanie tokenu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-363">Caching the authentication token</span></span>](#caching)

### <span data-ttu-id="1b039-364"><a name="clientflow"></a>Zarządzane przez klienta do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-364"><a name="clientflow"></a>Client-managed authentication</span></span>
<span data-ttu-id="1b039-365">Aplikację można niezależnie skontaktuj się z dostawcą tożsamości, a następnie podaj token zwrócony podczas logowania, z poziomu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1b039-365">Your app can independently contact the identity provider and then provide the returned token during login with your backend.</span></span> <span data-ttu-id="1b039-366">Ten przepływ klienta umożliwia zapewnienie jednego środowiska logowania jednokrotnego dla użytkowników lub pobrać użytkownika dodatkowe dane dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1b039-366">This client flow enables you to provide a single sign-on experience for users or to retrieve additional user data from the identity provider.</span></span> <span data-ttu-id="1b039-367">Klient przepływ uwierzytelniania jest preferowana względem przy użyciu przepływu serwera jako dostawca tożsamości zestawu SDK zawiera więcej natywnego działania środowiska użytkownika i zezwala na dodatkowe dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="1b039-367">Client flow authentication is preferred to using a server flow as the identity provider SDK provides a more native UX feel and allows for additional customization.</span></span>

<span data-ttu-id="1b039-368">Przykłady są dostępne następujące wzorców uwierzytelniania przepływu klienta:</span><span class="sxs-lookup"><span data-stu-id="1b039-368">Examples are provided for the following client-flow authentication patterns:</span></span>

* [<span data-ttu-id="1b039-369">Biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b039-369">Active Directory Authentication Library</span></span>](#adal)
* [<span data-ttu-id="1b039-370">Facebook lub Google</span><span class="sxs-lookup"><span data-stu-id="1b039-370">Facebook or Google</span></span>](#client-facebook)
* [<span data-ttu-id="1b039-371">Zestaw Live SDK</span><span class="sxs-lookup"><span data-stu-id="1b039-371">Live SDK</span></span>](#client-livesdk)

#### <span data-ttu-id="1b039-372"><a name="adal"></a>Uwierzytelnianie użytkowników z biblioteki uwierzytelniania usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b039-372"><a name="adal"></a>Authenticate users with the Active Directory Authentication Library</span></span>
<span data-ttu-id="1b039-373">Active Directory Authentication Library (ADAL) do uwierzytelniania użytkowników inicjować służy od klienta przy użyciu uwierzytelniania usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b039-373">You can use the Active Directory Authentication Library (ADAL) to initiate user authentication from the client using Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="1b039-374">Konfigurowanie zaplecza aplikacji mobilnej dla logowania w usłudze AAD, postępując [konfigurowania aplikacji usługi logowania usługi Active Directory] samouczka.</span><span class="sxs-lookup"><span data-stu-id="1b039-374">Configure your mobile app backend for AAD sign-on by following the [How to configure App Service for Active Directory login] tutorial.</span></span> <span data-ttu-id="1b039-375">Upewnij się ukończyć opcjonalny krok rejestrowania aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="1b039-375">Make sure to complete the optional step of registering a native client application.</span></span>
2. <span data-ttu-id="1b039-376">W programie Visual Studio lub Xamarin Studio Otwórz projekt i Dodaj odwołanie do `Microsoft.IdentityModel.CLients.ActiveDirectory` pakietu NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b039-376">In Visual Studio or Xamarin Studio, open your project and add a reference to the `Microsoft.IdentityModel.CLients.ActiveDirectory` NuGet package.</span></span> <span data-ttu-id="1b039-377">Podczas wyszukiwania, obejmują wersje wstępne.</span><span class="sxs-lookup"><span data-stu-id="1b039-377">When searching, include pre-release versions.</span></span>
3. <span data-ttu-id="1b039-378">Dodaj następujący kod do aplikacji, zależnie od używanej platformy.</span><span class="sxs-lookup"><span data-stu-id="1b039-378">Add the following code to your application, according to the platform you are using.</span></span> <span data-ttu-id="1b039-379">W każdej wprowadź następujące elementy zastępcze:</span><span class="sxs-lookup"><span data-stu-id="1b039-379">In each, make the following replacements:</span></span>

   * <span data-ttu-id="1b039-380">Zastąp **INSERT urzędu tutaj** o nazwie dzierżawy, w którym są udostępniane aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-380">Replace **INSERT-AUTHORITY-HERE** with the name of the tenant in which you provisioned your application.</span></span> <span data-ttu-id="1b039-381">Format powinien być https://login.microsoftonline.com/contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="1b039-381">The format should be https://login.microsoftonline.com/contoso.onmicrosoft.com.</span></span> <span data-ttu-id="1b039-382">Tę wartość można skopiować na karcie domeny w usłudze Azure Active Directory w [klasycznego portalu Azure].</span><span class="sxs-lookup"><span data-stu-id="1b039-382">This value can be copied from the Domain tab in your Azure Active Directory in the [Azure classic portal].</span></span>
   * <span data-ttu-id="1b039-383">Zastąp **Wstaw zasób — identyfikator-tutaj** z Identyfikatorem klienta dla zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-383">Replace **INSERT-RESOURCE-ID-HERE** with the client ID for your mobile app backend.</span></span> <span data-ttu-id="1b039-384">Możesz uzyskać identyfikator klienta z **zaawansowane** w obszarze **ustawień usługi Azure Active Directory** w portalu.</span><span class="sxs-lookup"><span data-stu-id="1b039-384">You can obtain the client ID from the **Advanced** tab under **Azure Active Directory Settings** in the portal.</span></span>
   * <span data-ttu-id="1b039-385">Zastąp **INSERT klienta-ID-tutaj** z Identyfikatorem klienta, którego skopiowano aplikację native client.</span><span class="sxs-lookup"><span data-stu-id="1b039-385">Replace **INSERT-CLIENT-ID-HERE** with the client ID you copied from the native client application.</span></span>
   * <span data-ttu-id="1b039-386">Zastąp **INSERT PRZEKIEROWANIA-URI-tutaj** z witryny */.auth/login/done* punktu końcowego, za pomocą schematu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1b039-386">Replace **INSERT-REDIRECT-URI-HERE** with your site's */.auth/login/done* endpoint, using the HTTPS scheme.</span></span> <span data-ttu-id="1b039-387">Ta wartość powinna być podobna do *https://contoso.azurewebsites.net/.auth/login/done*.</span><span class="sxs-lookup"><span data-stu-id="1b039-387">This value should be similar to *https://contoso.azurewebsites.net/.auth/login/done*.</span></span>

     <span data-ttu-id="1b039-388">Następujący kod wymagane dla każdej platformy:</span><span class="sxs-lookup"><span data-stu-id="1b039-388">The code needed for each platform follows:</span></span>

     <span data-ttu-id="1b039-389">**System Windows:**</span><span class="sxs-lookup"><span data-stu-id="1b039-389">**Windows:**</span></span>

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

     <span data-ttu-id="1b039-390">**Xamarin.iOS**</span><span class="sxs-lookup"><span data-stu-id="1b039-390">**Xamarin.iOS**</span></span>

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

     <span data-ttu-id="1b039-391">**Xamarin.Android**</span><span class="sxs-lookup"><span data-stu-id="1b039-391">**Xamarin.Android**</span></span>

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

#### <span data-ttu-id="1b039-392"><a name="client-facebook"></a>Logowanie jednokrotne przy użyciu tokenu z usługi Facebook lub Google</span><span class="sxs-lookup"><span data-stu-id="1b039-392"><a name="client-facebook"></a>Single Sign-On using a token from Facebook or Google</span></span>
<span data-ttu-id="1b039-393">Można użyć przepływu klienta, jak pokazano w ta Wstawka kodu dla usługi Facebook lub Google.</span><span class="sxs-lookup"><span data-stu-id="1b039-393">You can use the client flow as shown in this snippet for Facebook or Google.</span></span>

```
var token = new JObject();
// Replace access_token_value with actual value of your access token obtained
// using the Facebook or Google SDK.
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
            // to MobileServiceAuthenticationProvider.Google if using Google auth.
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

#### <span data-ttu-id="1b039-394"><a name="client-livesdk"></a>Jednokrotne przy użyciu Account Microsoft przy użyciu zestawu SDK na żywo</span><span class="sxs-lookup"><span data-stu-id="1b039-394"><a name="client-livesdk"></a>Single Sign On using Microsoft Account with the Live SDK</span></span>
<span data-ttu-id="1b039-395">Do uwierzytelniania użytkowników, musisz zarejestrować aplikację w Centrum deweloperów konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b039-395">To authenticate users, you must register your app at the Microsoft account Developer Center.</span></span> <span data-ttu-id="1b039-396">Skonfiguruj szczegóły rejestracji na zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-396">Configure the registration details on your Mobile App backend.</span></span> <span data-ttu-id="1b039-397">Aby utworzyć rejestrację konta Microsoft i podłącz go do zaplecza aplikacji mobilnej, wykonaj czynności opisane w [rejestrowania aplikacji w celu użycia logowania konta Microsoft].</span><span class="sxs-lookup"><span data-stu-id="1b039-397">To create a Microsoft account registration and connect it to your Mobile App backend, complete the steps in [Register your app to use a Microsoft account login].</span></span> <span data-ttu-id="1b039-398">Jeżeli masz zarówno Sklep Windows i Windows Phone 8/Silverlight wersje aplikacji, należy najpierw zarejestrować wersję Sklepu Windows.</span><span class="sxs-lookup"><span data-stu-id="1b039-398">If you have both Windows Store and Windows Phone 8/Silverlight versions of your app, register the Windows Store version first.</span></span>

<span data-ttu-id="1b039-399">Poniższy kod jest uwierzytelniany przy użyciu zestaw Live SDK i używa tokenu zwrócony logować się do zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-399">The following code authenticates using Live SDK and uses the returned token to sign in to your Mobile App backend.</span></span>

```
private LiveConnectSession session;
    //private static string clientId = "<microsoft-account-client-id>";
private async System.Threading.Tasks.Task AuthenticateAsync()
{

    // Get the URL the Mobile App backend.
    var serviceUrl = App.MobileService.ApplicationUri.AbsoluteUri;

    // Create the authentication client for Windows Store using the service URL.
    LiveAuthClient liveIdClient = new LiveAuthClient(serviceUrl);
    //// Create the authentication client for Windows Phone using the client ID of the registration.
    //LiveAuthClient liveIdClient = new LiveAuthClient(clientId);

    while (session == null)
    {
        // Request the authentication token from the Live authentication service.
        // The wl.basic scope should always be requested.  Other scopes can be added
        LiveLoginResult result = await liveIdClient.LoginAsync(new string[] { "wl.basic" });
        if (result.Status == LiveConnectSessionStatus.Connected)
        {
            session = result.Session;

            // Get information about the logged-in user.
            LiveConnectClient client = new LiveConnectClient(session);
            LiveOperationResult meResult = await client.GetAsync("me");

            // Use the Microsoft account auth token to sign in to App Service.
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

<span data-ttu-id="1b039-400">Aby uzyskać więcej informacji, zobacz [Windows Live SDK] dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-400">For more information, see the [Windows Live SDK] documentation.</span></span>

### <span data-ttu-id="1b039-401"><a name="serverflow"></a>Serwer zarządzany uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-401"><a name="serverflow"></a>Server-managed authentication</span></span>
<span data-ttu-id="1b039-402">Po zarejestrowaniu dostawcy tożsamości, wywołaj [LoginAsync] metody w [MobileServiceClient] z [MobileServiceAuthenticationProvider] wartość dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-402">Once you have registered your identity provider, call the [LoginAsync] method on the [MobileServiceClient] with the [MobileServiceAuthenticationProvider] value of your provider.</span></span> <span data-ttu-id="1b039-403">Na przykład następujący kod inicjuje serwera przepływu logowania za pomocą usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="1b039-403">For example, the following code initiates a server flow sign-in by using Facebook.</span></span>

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

<span data-ttu-id="1b039-404">Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość [MobileServiceAuthenticationProvider] wartości dla dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-404">If you are using an identity provider other than Facebook, change the value of [MobileServiceAuthenticationProvider] to the value for your provider.</span></span>

<span data-ttu-id="1b039-405">W przepływie serwera usługi Azure App Service zarządza przepływ uwierzytelniania OAuth poprzez wyświetlenie strony logowania wybranego dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-405">In a server flow, Azure App Service manages the OAuth authentication flow by displaying the sign-in page of the selected provider.</span></span>  <span data-ttu-id="1b039-406">Po zwraca dostawcy tożsamości, usługa aplikacji Azure generuje token uwierzytelniania usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1b039-406">Once the identity provider returns, Azure App Service generates an App Service authentication token.</span></span> <span data-ttu-id="1b039-407">[LoginAsync] metoda zwraca [MobileServiceUser], który zapewnia zarówno [UserId] uwierzytelnionego użytkownika i [ MobileServiceAuthenticationToken], jako tokenu web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="1b039-407">The [LoginAsync] method returns a [MobileServiceUser], which provides both the [UserId] of the authenticated user and the [MobileServiceAuthenticationToken], as a JSON web token (JWT).</span></span> <span data-ttu-id="1b039-408">Ten token można zapisać w pamięci podręcznej i ponownie go używać, dopóki nie wygaśnie.</span><span class="sxs-lookup"><span data-stu-id="1b039-408">This token can be cached and reused until it expires.</span></span> <span data-ttu-id="1b039-409">Aby uzyskać więcej informacji, zobacz [buforowania tokenu uwierzytelniania](#caching).</span><span class="sxs-lookup"><span data-stu-id="1b039-409">For more information, see [Caching the authentication token](#caching).</span></span>

### <span data-ttu-id="1b039-410"><a name="caching"></a>Buforowanie tokenu uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="1b039-410"><a name="caching"></a>Caching the authentication token</span></span>
<span data-ttu-id="1b039-411">W niektórych przypadkach można uniknąć wywołanie do metody logowania po pierwszym pomyślnym uwierzytelnieniu przez zapisanie token uwierzytelniania od dostawcy.</span><span class="sxs-lookup"><span data-stu-id="1b039-411">In some cases, the call to the login method can be avoided after the first successful authentication by storing the authentication token from the provider.</span></span>  <span data-ttu-id="1b039-412">Aplikacje Sklepu Windows i platformy uniwersalnej systemu Windows mogą używać [PasswordVault] do buforowania tokenu uwierzytelniania bieżącego po pomyślnym zalogowaniu, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-412">Windows Store and UWP apps can use [PasswordVault] to cache the current authentication token after a successful sign-in, as follows:</span></span>

```
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook);

PasswordVault vault = new PasswordVault();
vault.Add(new PasswordCredential("Facebook", client.currentUser.UserId,
    client.currentUser.MobileServiceAuthenticationToken));
```

<span data-ttu-id="1b039-413">Wartość Nazwa użytkownika jest przechowywana jako nazwa użytkownika poświadczeń i token jest przechowywane jako hasło.</span><span class="sxs-lookup"><span data-stu-id="1b039-413">The UserId value is stored as the UserName of the credential and the token is the stored as the Password.</span></span> <span data-ttu-id="1b039-414">Na kolejnych rozruchów, możesz sprawdzić **PasswordVault** dla buforowanych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1b039-414">On subsequent start-ups, you can check the **PasswordVault** for cached credentials.</span></span> <span data-ttu-id="1b039-415">W poniższym przykładzie użyto buforowanych poświadczeń, gdy zostaną znalezione, a w przeciwnym razie podejmuje próbę uwierzytelnienia z wewnętrznej bazy danych:</span><span class="sxs-lookup"><span data-stu-id="1b039-415">The following example uses cached credentials when they are found, and otherwise attempts to authenticate again with the backend:</span></span>

```
// Try to retrieve stored credentials.
var creds = vault.FindAllByResource("Facebook").FirstOrDefault();
if (creds != null)
{
    // Create the current user from the stored credentials.
    client.currentUser = new MobileServiceUser(creds.UserName);
    client.currentUser.MobileServiceAuthenticationToken =
        vault.Retrieve("Facebook", creds.UserName).Password;
}
else
{
    // Regular login flow and cache the token as shown above.
}
```

<span data-ttu-id="1b039-416">Po zalogowaniu się użytkownika należy również usunąć przechowywanych poświadczeń w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-416">When you sign out a user, you must also remove the stored credential, as follows:</span></span>

```
client.Logout();
vault.Remove(vault.Retrieve("Facebook", client.currentUser.UserId));
```

<span data-ttu-id="1b039-417">Użyj aplikacji platformy Xamarin [Xamarin.Auth] interfejsy API w celu bezpiecznego przechowywania poświadczeń w **konta** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1b039-417">Xamarin    apps use the [Xamarin.Auth] APIs to securely store credentials in an **Account** object.</span></span> <span data-ttu-id="1b039-418">Na przykład za pomocą tych interfejsów API, zobacz [AuthStore.cs] pliku kodu w [udostępniania próbki zdjęć ContosoMoments](https://github.com/azure-appservice-samples/ContosoMoments).</span><span class="sxs-lookup"><span data-stu-id="1b039-418">For an example of using these APIs, see the [AuthStore.cs] code file in the [ContosoMoments photo sharing sample](https://github.com/azure-appservice-samples/ContosoMoments).</span></span>

<span data-ttu-id="1b039-419">Korzystając z uwierzytelniania zarządzanych przez klienta, można buforować tokenu dostępu uzyskane od dostawcy, takich jak Facebook lub Twitter.</span><span class="sxs-lookup"><span data-stu-id="1b039-419">When you use client-managed authentication, you can also cache the access token obtained from your provider such as Facebook or Twitter.</span></span> <span data-ttu-id="1b039-420">Token ten można podać, aby zażądać nowego tokenu uwierzytelniania z wewnętrznej bazy danych, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-420">This token can be supplied to request a new authentication token from the backend, as follows:</span></span>

```
var token = new JObject();
// Replace <your_access_token_value> with actual value of your access token
token.Add("access_token", "<your_access_token_value>");

// Authenticate using the access token.
await client.LoginAsync(MobileServiceAuthenticationProvider.Facebook, token);
```

## <span data-ttu-id="1b039-421"><a name="pushnotifications"></a>Powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="1b039-421"><a name="pushnotifications"></a>Push Notifications</span></span>
<span data-ttu-id="1b039-422">W poniższych tematach znajdziesz powiadomień wypychanych:</span><span class="sxs-lookup"><span data-stu-id="1b039-422">The following topics cover Push Notifications:</span></span>

* [<span data-ttu-id="1b039-423">Zarejestruj się, aby powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="1b039-423">Register for Push Notifications</span></span>](#register-for-push)
* [<span data-ttu-id="1b039-424">Uzyskaj identyfikator SID pakietu Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="1b039-424">Obtain a Windows Store package SID</span></span>](#package-sid)
* [<span data-ttu-id="1b039-425">Rejestrowanie przy użyciu szablonów i platform</span><span class="sxs-lookup"><span data-stu-id="1b039-425">Register with Cross-platform templates</span></span>](#register-xplat)

### <span data-ttu-id="1b039-426"><a name="register-for-push"></a>Porady: rejestrowanie się w celu powiadomienia wypychane</span><span class="sxs-lookup"><span data-stu-id="1b039-426"><a name="register-for-push"></a>How to: Register for Push Notifications</span></span>
<span data-ttu-id="1b039-427">Klient Mobile Apps umożliwia rejestrowanie do powiadomień wypychanych przy użyciu usługi Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="1b039-427">The Mobile Apps client enables you to register for push notifications with Azure Notification Hubs.</span></span> <span data-ttu-id="1b039-428">Podczas rejestrowania, można uzyskać uchwytu, którą można uzyskać z specyficzne dla platformy Push Notification Service (PNS).</span><span class="sxs-lookup"><span data-stu-id="1b039-428">When registering, you obtain a handle that you obtain from the platform-specific Push Notification Service (PNS).</span></span> <span data-ttu-id="1b039-429">Podczas tworzenia rejestracji, następnie podaj tę wartość, wraz ze wszystkimi tagami.</span><span class="sxs-lookup"><span data-stu-id="1b039-429">You then provide this value along with any tags when you create the registration.</span></span> <span data-ttu-id="1b039-430">Poniższy kod rejestruje aplikację systemu Windows, aby powiadomienia wypychane z usługi powiadomień systemu Windows (WNS):</span><span class="sxs-lookup"><span data-stu-id="1b039-430">The following code registers your Windows app for push notifications with the Windows Notification Service (WNS):</span></span>

```
private async void InitNotificationsAsync()
{
    // Request a push notification channel.
    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // Register for notifications using the new channel.
    await MobileService.GetPush().RegisterNativeAsync(channel.Uri, null);
}
```

<span data-ttu-id="1b039-431">Jeśli push usługi WNS, musisz [pobrania identyfikatora SID pakietu Sklepu Windows](#package-sid).</span><span class="sxs-lookup"><span data-stu-id="1b039-431">If you are pushing to WNS, then you MUST [obtain a Windows Store package SID](#package-sid).</span></span>  <span data-ttu-id="1b039-432">Aby uzyskać więcej informacji na aplikacje systemu Windows, w tym jak zarejestrować do rejestracji szablonów, zobacz [Dodawanie powiadomień wypychanych do aplikacji].</span><span class="sxs-lookup"><span data-stu-id="1b039-432">For more information on Windows apps, including how to register for template registrations, see [Add push notifications to your app].</span></span>

<span data-ttu-id="1b039-433">Żądanie tagi od klienta nie jest obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="1b039-433">Requesting tags from the client is not supported.</span></span>  <span data-ttu-id="1b039-434">Tag żądań dyskretnie są usuwane z rejestracji.</span><span class="sxs-lookup"><span data-stu-id="1b039-434">Tag Requests are silently dropped from registration.</span></span>
<span data-ttu-id="1b039-435">Jeśli chcesz zarejestrować urządzenie z tagami, należy utworzyć niestandardowego interfejsu API, który używa interfejsu API centra powiadomień w celu przeprowadzenia rejestracji w Twoim imieniu.</span><span class="sxs-lookup"><span data-stu-id="1b039-435">If you wish to register your device with tags, create a Custom API that uses the Notification Hubs API to perform the registration on your behalf.</span></span>  <span data-ttu-id="1b039-436">[Wywołanie interfejsu API niestandardowe](#customapi) zamiast `RegisterNativeAsync()` metody.</span><span class="sxs-lookup"><span data-stu-id="1b039-436">[Call the Custom API](#customapi) instead of the `RegisterNativeAsync()` method.</span></span>

### <span data-ttu-id="1b039-437"><a name="package-sid"></a>Porady: uzyskiwanie identyfikatora SID pakietu Sklepu Windows</span><span class="sxs-lookup"><span data-stu-id="1b039-437"><a name="package-sid"></a>How to: Obtain a Windows Store package SID</span></span>
<span data-ttu-id="1b039-438">Dla Włączanie powiadomień wypychanych w aplikacji ze Sklepu Windows wymagany jest identyfikator SID pakietu.</span><span class="sxs-lookup"><span data-stu-id="1b039-438">A package SID is needed for enabling push notifications in Windows Store apps.</span></span>  <span data-ttu-id="1b039-439">Aby uzyskać identyfikator SID pakietu, należy zarejestrować aplikację ze sklepem Windows.</span><span class="sxs-lookup"><span data-stu-id="1b039-439">To receive a package SID, register your application with the Windows Store.</span></span>

<span data-ttu-id="1b039-440">Aby uzyskać tę wartość:</span><span class="sxs-lookup"><span data-stu-id="1b039-440">To obtain this value:</span></span>

1. <span data-ttu-id="1b039-441">W Eksploratorze rozwiązań programu Visual Studio, kliknij prawym przyciskiem myszy projekt aplikacji Sklepu Windows, kliknij przycisk **magazynu** > **Skojarz aplikację ze sklepem...** .</span><span class="sxs-lookup"><span data-stu-id="1b039-441">In Visual Studio Solution Explorer, right-click the Windows Store app project, click **Store** > **Associate App with the Store...**.</span></span>
2. <span data-ttu-id="1b039-442">W kreatorze kliknij **dalej**, zaloguj się przy użyciu konta Microsoft, wpisz nazwę aplikacji w **Zarezerwuj nazwę nowej aplikacji**, następnie kliknij przycisk **rezerwy**.</span><span class="sxs-lookup"><span data-stu-id="1b039-442">In the wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="1b039-443">Po pomyślnym utworzeniu rejestracji aplikacji, wybierz nazwę aplikacji, kliknij przycisk **dalej**, a następnie kliknij przycisk **skojarzyć**.</span><span class="sxs-lookup"><span data-stu-id="1b039-443">After the app registration is successfully created, select the app name, click **Next**, and then click **Associate**.</span></span>
4. <span data-ttu-id="1b039-444">Zaloguj się do [Centrum deweloperów systemu Windows] przy użyciu Account firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1b039-444">Log in to the [Windows Dev Center] using your Microsoft Account.</span></span> <span data-ttu-id="1b039-445">W obszarze **Moje aplikacje**, kliknij przycisk rejestracji aplikacji utworzony.</span><span class="sxs-lookup"><span data-stu-id="1b039-445">Under **My apps**, click the app registration you created.</span></span>
5. <span data-ttu-id="1b039-446">Kliknij przycisk **Zarządzanie aplikacjami** > **tożsamości aplikacji**, a następnie przewiń w dół, aby znaleźć użytkownika **identyfikatora SID pakietu**.</span><span class="sxs-lookup"><span data-stu-id="1b039-446">Click **App management** > **App identity**, and then scroll down to find your **Package SID**.</span></span>

<span data-ttu-id="1b039-447">Wiele zastosowań identyfikator SID pakietu traktować go jako identyfikatora URI, w którym to przypadku należy użyć *ms-app: / /* schemat.</span><span class="sxs-lookup"><span data-stu-id="1b039-447">Many uses of the package SID treat it as a URI, in which case you need to use *ms-app://* as the scheme.</span></span> <span data-ttu-id="1b039-448">Zwróć uwagę na wersję pakietu utworzonego przez łączenie tej wartości jako prefiks identyfikatora SID.</span><span class="sxs-lookup"><span data-stu-id="1b039-448">Make note of the version of your package SID formed by concatenating this value as a prefix.</span></span>

<span data-ttu-id="1b039-449">Aplikacje platformy Xamarin wymagają niektórych dodatkowy kod, aby można było zarejestrować aplikację z systemem iOS lub Android platform.</span><span class="sxs-lookup"><span data-stu-id="1b039-449">Xamarin apps require some additional code to be able to register an app running on the iOS or Android platforms.</span></span> <span data-ttu-id="1b039-450">Aby uzyskać więcej informacji zobacz temat dla danej platformy:</span><span class="sxs-lookup"><span data-stu-id="1b039-450">For more information, see the topic for your platform:</span></span>

* [<span data-ttu-id="1b039-451">Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="1b039-451">Xamarin.Android</span></span>](app-service-mobile-xamarin-android-get-started-push.md#add-push)
* [<span data-ttu-id="1b039-452">Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="1b039-452">Xamarin.iOS</span></span>](app-service-mobile-xamarin-ios-get-started-push.md#add-push-notifications-to-your-app)

### <span data-ttu-id="1b039-453"><a name="register-xplat"></a>Porady: szablony wypychania rejestru do wysyłania powiadomień i platform</span><span class="sxs-lookup"><span data-stu-id="1b039-453"><a name="register-xplat"></a>How to: Register push templates to send cross-platform notifications</span></span>
<span data-ttu-id="1b039-454">Aby zarejestrować szablonów, należy użyć `RegisterAsync()` metody za pomocą szablonów, w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1b039-454">To register templates, use the `RegisterAsync()` method with the templates, as follows:</span></span>

```
JObject templates = myTemplates();
MobileService.GetPush().RegisterAsync(channel.Uri, templates);
```

<span data-ttu-id="1b039-455">Szablony powinna być `JObject` typów i może zawierać wiele szablonów w następującym formacie JSON:</span><span class="sxs-lookup"><span data-stu-id="1b039-455">Your templates should be `JObject` types and can contain multiple templates in the following JSON format:</span></span>

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

<span data-ttu-id="1b039-456">Metoda **RegisterAsync()** również akceptuje dodatkowej Kafelki:</span><span class="sxs-lookup"><span data-stu-id="1b039-456">The method **RegisterAsync()** also accepts Secondary Tiles:</span></span>

```
MobileService.GetPush().RegisterAsync(string channelUri, JObject templates, JObject secondaryTiles);
```

<span data-ttu-id="1b039-457">Wszystkie tagi są odrzucane optymalizacji podczas rejestracji dla zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1b039-457">All tags are stripped away during registration for security.</span></span> <span data-ttu-id="1b039-458">Aby dodać tagi do instalacji lub szablonów w ramach instalacji, zobacz [Praca z serwera wewnętrznej bazy danych .NET SDK usługi Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="1b039-458">To add tags to installations or templates within installations, see [Work with the .NET backend server SDK for Azure Mobile Apps].</span></span>

<span data-ttu-id="1b039-459">Aby wysyłać powiadomienia przy użyciu tych szablonów w zarejestrowany, zapoznaj się [interfejsów API centra powiadomień].</span><span class="sxs-lookup"><span data-stu-id="1b039-459">To send notifications utilizing these registered templates, refer to the [Notification Hubs APIs].</span></span>

## <span data-ttu-id="1b039-460"><a name="misc"></a>Tematy dodatkowe</span><span class="sxs-lookup"><span data-stu-id="1b039-460"><a name="misc"></a>Miscellaneous Topics</span></span>
### <span data-ttu-id="1b039-461"><a name="errors"></a>Porady: obsługa błędów</span><span class="sxs-lookup"><span data-stu-id="1b039-461"><a name="errors"></a>How to: Handle errors</span></span>
<span data-ttu-id="1b039-462">Po wystąpieniu błędu w wewnętrznej bazie danych, klient SDK zgłasza `MobileServiceInvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="1b039-462">When an error occurs in the backend, the client SDK raises a `MobileServiceInvalidOperationException`.</span></span>  <span data-ttu-id="1b039-463">Poniższy przykład przedstawia sposób obsługi wyjątku, który jest zwracany przez zaplecze:</span><span class="sxs-lookup"><span data-stu-id="1b039-463">The following example shows how to handle an exception that is returned by the backend:</span></span>

```
private async void InsertTodoItem(TodoItem todoItem)
{
    // This code inserts a new TodoItem into the database. When the operation completes
    // and App Service has assigned an Id, the item is added to the CollectionView
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

<span data-ttu-id="1b039-464">Innym przykładem dotyczącym warunki błędów można znaleźć w [Mobile Apps pliki przykładowe].</span><span class="sxs-lookup"><span data-stu-id="1b039-464">Another example of dealing with error conditions can be found in the [Mobile Apps Files Sample].</span></span> <span data-ttu-id="1b039-465">[LoggingHandler] przykładzie przedstawiono obsługi delegata rejestrowania do rejestrowania żądań wysyłanych do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1b039-465">The [LoggingHandler] example provides a logging delegate handler to log the requests being made to the backend.</span></span>

### <span data-ttu-id="1b039-466"><a name="headers"></a>Porady: dostosowywanie nagłówki żądań</span><span class="sxs-lookup"><span data-stu-id="1b039-466"><a name="headers"></a>How to: Customize request headers</span></span>
<span data-ttu-id="1b039-467">Do obsługi danego scenariusza specyficzne dla aplikacji, może być konieczne dostosowanie komunikację z zaplecza aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="1b039-467">To support your specific app scenario, you might need to customize communication with the Mobile App backend.</span></span> <span data-ttu-id="1b039-468">Na przykład można dodać niestandardowego nagłówka do wszystkich żądań wychodzących lub nawet zmienić kody stanu odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1b039-468">For example, you may want to add a custom header to every outgoing request or even change responses status codes.</span></span> <span data-ttu-id="1b039-469">Można użyć niestandardowego [DelegatingHandler], jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="1b039-469">You can use a custom [DelegatingHandler], as in the following example:</span></span>

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
        // Change the request-side here based on the HttpRequestMessage
        request.Headers.Add("x-my-header", "my value");

        // Do the request
        var response = await base.SendAsync(request, cancellationToken);

        // Change the response-side here based on the HttpResponseMessage

        // Return the modified response
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

<span data-ttu-id="1b039-470">[Dodawanie uwierzytelniania do aplikacji]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="1b039-470">[Add authentication to your app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>
<span data-ttu-id="1b039-471">[w trybie Offline synchronizacji danych w usłudze Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="1b039-471">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="1b039-472">[Dodawanie powiadomień wypychanych do aplikacji]: app-service-mobile-windows-store-dotnet-get-started-push.md</span><span class="sxs-lookup"><span data-stu-id="1b039-472">[Add push notifications to your app]: app-service-mobile-windows-store-dotnet-get-started-push.md</span></span>
<span data-ttu-id="1b039-473">[rejestrowania aplikacji w celu użycia logowania konta Microsoft]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="1b039-473">[Register your app to use a Microsoft account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="1b039-474">[konfigurowania aplikacji usługi logowania usługi Active Directory]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="1b039-474">[How to configure App Service for Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>

<!-- Microsoft URLs. -->
<span data-ttu-id="1b039-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-475">[MobileServiceCollection]: https://msdn.microsoft.com/en-us/library/azure/dn250636(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-476">[MobileServiceIncrementalLoadingCollection]: https://msdn.microsoft.com/en-us/library/azure/dn268408(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-477">[MobileServiceAuthenticationProvider]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceauthenticationprovider(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-478">[MobileServiceUser]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-479">[ MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-479">[MobileServiceAuthenticationToken]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.mobileserviceauthenticationtoken(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-480">[Metoda GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-480">[GetTable]: https://msdn.microsoft.com/en-us/library/azure/jj554275(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-481">[tworzy odwołania do tabeli bez typu]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-481">[creates a reference to an untyped table]: https://msdn.microsoft.com/en-us/library/azure/jj554278(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-482">[DeleteAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296407(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-483">[IncludeTotalCount]: https://msdn.microsoft.com/en-us/library/azure/dn250560(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-484">[InsertAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296400(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-485">[InvokeApiAsync]: https://msdn.microsoft.com/en-us/library/azure/dn268343(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-486">[LoginAsync]: https://msdn.microsoft.com/en-us/library/azure/dn296411(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-487">[LookupAsync]: https://msdn.microsoft.com/en-us/library/azure/jj871654(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-488">[OrderBy]: https://msdn.microsoft.com/en-us/library/azure/dn250572(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-489">[OrderByDescending]: https://msdn.microsoft.com/en-us/library/azure/dn250568(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-490">[ReadAsync]: https://msdn.microsoft.com/en-us/library/azure/mt691741(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-491">[zająć]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-491">[Take]: https://msdn.microsoft.com/en-us/library/azure/dn250574(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-492">[wybierz]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-492">[Select]: https://msdn.microsoft.com/en-us/library/azure/dn250569(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-493">[Pomiń]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-493">[Skip]: https://msdn.microsoft.com/en-us/library/azure/dn250573(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-494">[UpdateAsync]: https://msdn.microsoft.com/en-us/library/azure/dn250536.(v=azure.10)aspx</span></span>
<span data-ttu-id="1b039-495">[Nazwa użytkownika]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-495">[UserID]: http://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.mobileservices.mobileserviceuser.userid(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-496">[Gdzie]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-496">[Where]: https://msdn.microsoft.com/en-us/library/azure/dn250579(v=azure.10).aspx</span></span>
<span data-ttu-id="1b039-497">[portalu Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="1b039-497">[Azure portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="1b039-498">[klasycznego portalu Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="1b039-498">[Azure classic portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="1b039-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-499">[EnableQueryAttribute]: https://msdn.microsoft.com/library/system.web.http.odata.enablequeryattribute.aspx</span></span>
<span data-ttu-id="1b039-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-500">[Guid.NewGuid]: https://msdn.microsoft.com/en-us/library/system.guid.newguid(v=vs.110).aspx</span></span>
<span data-ttu-id="1b039-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-501">[ISupportIncrementalLoading]: http://msdn.microsoft.com/library/windows/apps/Hh701916.aspx</span></span>
<span data-ttu-id="1b039-502">[Centrum deweloperów systemu Windows]: https://dev.windows.com/en-us/overview</span><span class="sxs-lookup"><span data-stu-id="1b039-502">[Windows Dev Center]: https://dev.windows.com/en-us/overview</span></span>
<span data-ttu-id="1b039-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-503">[DelegatingHandler]: https://msdn.microsoft.com/library/system.net.http.delegatinghandler(v=vs.110).aspx</span></span>
<span data-ttu-id="1b039-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-504">[Windows Live SDK]: https://msdn.microsoft.com/en-us/library/bb404787.aspx</span></span>
<span data-ttu-id="1b039-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-505">[PasswordVault]: http://msdn.microsoft.com/library/windows/apps/windows.security.credentials.passwordvault.aspx</span></span>
[ProtectedData]: http://msdn.microsoft.com/library/system.security.cryptography.protecteddata%28VS.95%29.aspx
<span data-ttu-id="1b039-506">[interfejsów API centra powiadomień]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span><span class="sxs-lookup"><span data-stu-id="1b039-506">[Notification Hubs APIs]: https://msdn.microsoft.com/library/azure/dn495101.aspx</span></span>
<span data-ttu-id="1b039-507">[Mobile Apps pliki przykładowe]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span><span class="sxs-lookup"><span data-stu-id="1b039-507">[Mobile Apps Files Sample]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files</span></span>
<span data-ttu-id="1b039-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span><span class="sxs-lookup"><span data-stu-id="1b039-508">[LoggingHandler]: https://github.com/Azure-Samples/app-service-mobile-dotnet-todo-list-files/blob/master/src/client/MobileAppsFilesSample/Helpers/LoggingHandler.cs#L63</span></span>

<!-- External URLs -->
<span data-ttu-id="1b039-509">[OData v3 dokumentacji]: http://www.odata.org/documentation/odata-version-3-0/</span><span class="sxs-lookup"><span data-stu-id="1b039-509">[OData v3 Documentation]: http://www.odata.org/documentation/odata-version-3-0/</span></span>
<span data-ttu-id="1b039-510">[Fiddler]: http://www.telerik.com/fiddler</span><span class="sxs-lookup"><span data-stu-id="1b039-510">[Fiddler]: http://www.telerik.com/fiddler</span></span>
<span data-ttu-id="1b039-511">[Json.NET]: http://www.newtonsoft.com/json</span><span class="sxs-lookup"><span data-stu-id="1b039-511">[Json.NET]: http://www.newtonsoft.com/json</span></span>
<span data-ttu-id="1b039-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span><span class="sxs-lookup"><span data-stu-id="1b039-512">[Xamarin.Auth]: https://components.xamarin.com/view/xamarin.auth/</span></span>
<span data-ttu-id="1b039-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span><span class="sxs-lookup"><span data-stu-id="1b039-513">[AuthStore.cs]: https://github.com/azure-appservice-samples/ContosoMoments</span></span>
[ContosoMoments photo sharing sample]: https://github.com/azure-appservice-samples/ContosoMoments
