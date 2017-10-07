---
title: "wprowadzenie do usługi Azure Search w środowisku Node.js aaaGet | Dokumentacja firmy Microsoft"
description: "Zapoznaj się z procesem tworzenia aplikacji wyszukiwania w hostowanej usłudze wyszukiwania w chmurze na platformie Azure przy użyciu języka programowania Node.js."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="7258e-103">Wprowadzenie do usługi Azure Search w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="7258e-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7258e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7258e-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="7258e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7258e-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="7258e-106">Dowiedz się, jak toobuild niestandardowych Node.js Wyszukaj aplikację, która używa usługi Azure Search jako środowiska wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7258e-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="7258e-107">W tym samouczku używana hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello obiekty i operacje używane w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="7258e-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="7258e-108">My używamy [Node.js](https://Nodejs.org) i NPM, [Sublime Text 3](http://www.sublimetext.com/3)i środowiska Windows PowerShell na toodevelop Windows 8.1 i przetestowania tego kodu.</span><span class="sxs-lookup"><span data-stu-id="7258e-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="7258e-109">toorun tej próbki, musi mieć usługi Azure Search, której możesz zarejestrować się w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7258e-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="7258e-110">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="7258e-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="7258e-111">Dane hello — informacje</span><span class="sxs-lookup"><span data-stu-id="7258e-111">About hello data</span></span>
<span data-ttu-id="7258e-112">Ta przykładowa aplikacja korzysta z danych z hello [Stanów Zjednoczonych Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)zawężonych hello stanu Rhode Island tooreduce hello dataset rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="7258e-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="7258e-113">Użyjemy tego toobuild danych aplikacji wyszukiwania, która zwraca punkty orientacyjne, takie jak szpitale i szkoły, jak również geologiczne, takie jak strumienie, jeziora i szczyty.</span><span class="sxs-lookup"><span data-stu-id="7258e-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="7258e-114">W tej aplikacji hello **DataIndexer** budowania i obciążeń hello indeksu przy użyciu [indeksatora](https://msdn.microsoft.com/library/azure/dn798918.aspx) konstrukcja pobierania hello filtrowane danych agencji USGS z publicznej usługi Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7258e-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="7258e-115">Poświadczenia i połączenia źródło danych w trybie online toohello informacji znajduje się w kodzie programu hello.</span><span class="sxs-lookup"><span data-stu-id="7258e-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="7258e-116">Nie jest konieczna żadna dodatkowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="7258e-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="7258e-117">Zastosowaliśmy filtr na toostay tego zestawu danych w obszarze hello 10 000 dokumentów limit hello warstwy cenowej bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="7258e-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="7258e-118">Jeśli używasz hello warstwy standardowa, ten limit nie ma zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7258e-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="7258e-119">Aby uzyskać szczegółowe informacje o pojemności dla każdej warstwy cenowej, zobacz [Search service limits](search-limits-quotas-capacity.md) (Limity usługi wyszukiwania).</span><span class="sxs-lookup"><span data-stu-id="7258e-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="7258e-120">Znajdź hello nazwę usługi i klucza interfejsu api usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="7258e-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="7258e-121">Po utworzeniu usługi hello adres zwrotny URL hello portalu tooget toohello lub `api-key`.</span><span class="sxs-lookup"><span data-stu-id="7258e-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="7258e-122">Tooyour połączenia usługi wyszukiwania wymagają zarówno adresu URL hello i `api-key` tooauthenticate hello wywołania.</span><span class="sxs-lookup"><span data-stu-id="7258e-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="7258e-123">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7258e-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7258e-124">Na pasku skok hello, kliknij przycisk **usługi wyszukiwania** toolist wszystkie usługi Azure Search aprowizowanych dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7258e-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="7258e-125">Wybierz usługę hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="7258e-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="7258e-126">Na pulpicie nawigacyjnym usługi hello i powinna zostać wyświetlona Kafelki z istotnymi informacjami, takich jak ikonę klucza hello dla uzyskiwania dostępu do kluczy administratora hello.</span><span class="sxs-lookup"><span data-stu-id="7258e-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="7258e-127">Skopiuj adres URL usługi hello, klucz administratora i klucz zapytania.</span><span class="sxs-lookup"><span data-stu-id="7258e-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="7258e-128">Należy wszystkie trzy później podczas dodawania ich toohello pliku config.js.</span><span class="sxs-lookup"><span data-stu-id="7258e-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="7258e-129">Pobieranie plików przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="7258e-129">Download hello sample files</span></span>
<span data-ttu-id="7258e-130">Za pomocą jednej z hello następujące przykładowe hello toodownload podejścia.</span><span class="sxs-lookup"><span data-stu-id="7258e-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="7258e-131">Przejdź za[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="7258e-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="7258e-132">Kliknij przycisk **Pobierz ZIP**, Zapisz plik zip hello, a następnie Wyodrębnij wszystkie pliki hello zawiera.</span><span class="sxs-lookup"><span data-stu-id="7258e-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="7258e-133">Wszystkie kolejne modyfikacje plików i instrukcje uruchamiania będą wykonywane względem plików w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="7258e-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="7258e-134">Zaktualizuj hello config.js.</span><span class="sxs-lookup"><span data-stu-id="7258e-134">Update hello config.js.</span></span> <span data-ttu-id="7258e-135">przy użyciu adresu URL usługi wyszukiwania i klucza api-key</span><span class="sxs-lookup"><span data-stu-id="7258e-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="7258e-136">Przy użyciu hello adresu URL i klucza api-key skopiowanego wcześniej, podaj adres URL hello, klucz administratora i klucz zapytania w pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7258e-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="7258e-137">Klucze administratora przyznają pełną kontrolę nad operacjami usługi, w tym nad tworzeniem i usuwaniem indeksu oraz ładowaniem dokumentów.</span><span class="sxs-lookup"><span data-stu-id="7258e-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="7258e-138">Z kolei klucze zapytania są dla operacji tylko do odczytu, zwykle używanych przez aplikacje klienckie, łączących tooAzure wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7258e-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="7258e-139">W tym przykładzie uwzględniamy zapytania hello klucza toohelp zapamiętaniu najlepszego rozwiązania hello przy użyciu klucza zapytania hello w aplikacjach klienckich.</span><span class="sxs-lookup"><span data-stu-id="7258e-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="7258e-140">Zrzut ekranu przedstawia następujące Hello **config.js** otwarty w edytorze tekstów, z hello odpowiednimi wpisami tak aby były widoczne, gdy plik hello tooupdate o hello wartości, które są prawidłowe dla usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="7258e-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="7258e-141">Hostowanie środowiska uruchomieniowego dla przykładu hello</span><span class="sxs-lookup"><span data-stu-id="7258e-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="7258e-142">przykład Witaj wymaga serwera HTTP, które można zainstalować globalnie za pomocą programu npm.</span><span class="sxs-lookup"><span data-stu-id="7258e-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="7258e-143">Okno programu PowerShell dla hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="7258e-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="7258e-144">Przejdź do folderu toohello, który zawiera hello **package.json** pliku.</span><span class="sxs-lookup"><span data-stu-id="7258e-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="7258e-145">Wpisz polecenie `npm install`.</span><span class="sxs-lookup"><span data-stu-id="7258e-145">Type `npm install`.</span></span>
3. <span data-ttu-id="7258e-146">Wpisz polecenie `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="7258e-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="7258e-147">Tworzenie indeksu hello i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7258e-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="7258e-148">Wpisz polecenie `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="7258e-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="7258e-149">Wpisz polecenie `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="7258e-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="7258e-150">Wpisz polecenie `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="7258e-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="7258e-151">Za pomocą przeglądarki przejdź do strony `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="7258e-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="7258e-152">Przeszukiwanie danych agencji USGS</span><span class="sxs-lookup"><span data-stu-id="7258e-152">Search on USGS data</span></span>
<span data-ttu-id="7258e-153">zestaw danych agencji USGS Hello zawiera rekordy, które są odpowiednie toohello stanu Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="7258e-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="7258e-154">Jeśli klikniesz przycisk **wyszukiwania** na pole wyszukiwania puste, możesz uzyskać hello 50 pierwszych wpisów, który jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="7258e-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="7258e-155">Wprowadzenie terminu zapewnia aparat wyszukiwania hello coś toogo na.</span><span class="sxs-lookup"><span data-stu-id="7258e-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="7258e-156">Spróbuj wprowadzić nazwę regionalną.</span><span class="sxs-lookup"><span data-stu-id="7258e-156">Try entering a regional name.</span></span> <span data-ttu-id="7258e-157">"Roger Williams" był pierwszym gubernatorem stanu Rhode Island hello.</span><span class="sxs-lookup"><span data-stu-id="7258e-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="7258e-158">Liczne parki, budynki i szkoły są nazwane jego imieniem.</span><span class="sxs-lookup"><span data-stu-id="7258e-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="7258e-159">Możesz też wprowadzić jeden z poniższych terminów:</span><span class="sxs-lookup"><span data-stu-id="7258e-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="7258e-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="7258e-160">Pawtucket</span></span>
* <span data-ttu-id="7258e-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="7258e-161">Pembroke</span></span>
* <span data-ttu-id="7258e-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="7258e-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="7258e-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7258e-163">Next steps</span></span>
<span data-ttu-id="7258e-164">To jest pierwszy samouczek usługi Azure Search hello, na podstawie Node.js i hello danych agencji USGS.</span><span class="sxs-lookup"><span data-stu-id="7258e-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="7258e-165">Wraz z upływem czasu będziemy rozszerzać ten samouczek toodemonstrate dodatkowe funkcje wyszukiwania może być toouse w rozwiązaniach niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="7258e-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="7258e-166">Jeśli masz już jakieś doświadczenie z usługą Azure Search, możesz użyć tego przykładu jako punktu wyjścia do wypróbowania sugestorów (uzupełnianie przy wpisywaniu lub autouzupełnianie zapytań), filtrów i nawigacji aspektowej.</span><span class="sxs-lookup"><span data-stu-id="7258e-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="7258e-167">Możesz również ulepszyć stronę wyników wyszukiwania hello przez dodanie liczników i łączenie dokumentów w partie, dzięki czemu użytkownicy mogą przeglądania wyników hello.</span><span class="sxs-lookup"><span data-stu-id="7258e-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="7258e-168">TooAzure nowego wyszukiwania?</span><span class="sxs-lookup"><span data-stu-id="7258e-168">New tooAzure Search?</span></span> <span data-ttu-id="7258e-169">Zaleca się podjęcie próby toodevelop innych samouczków zrozumienia można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="7258e-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="7258e-170">Można znaleźć w naszych [stronę dokumentacji](https://azure.microsoft.com/documentation/services/search/) toofind więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="7258e-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="7258e-171">Można również wyświetlić hello łącza w naszym [listy filmów wideo i samouczków](search-video-demo-tutorial-list.md) tooaccess więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="7258e-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
