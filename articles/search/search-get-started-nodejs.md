---
title: "Wprowadzenie do usługi Azure Search w środowisku Node.js | Microsoft Docs"
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
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="bfb7b-103">Wprowadzenie do usługi Azure Search w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="bfb7b-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bfb7b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bfb7b-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="bfb7b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="bfb7b-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="bfb7b-106">Dowiedz się, jak utworzyć niestandardową aplikację wyszukiwania Node.js, która korzysta z usługi Azure Search jako środowiska wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="bfb7b-107">Ten samouczek używa [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/dn798935.aspx), aby konstruować obiekty i operacje używane w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="bfb7b-108">Do napisania i przetestowania tego kodu zostało użyte środowisko [Node.js](https://Nodejs.org) i menedżer pakietów NPM oraz programy [Sublime Text 3](http://www.sublimetext.com/3) i Windows PowerShell w systemie Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="bfb7b-109">Do uruchomienia tego przykładu jest potrzebna usługa Azure Search, do której możesz zarejestrować się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="bfb7b-110">Aby uzyskać szczegółowe instrukcje, zobacz [Create an Azure Search service in the portal](search-create-service-portal.md) (Tworzenie usługi Azure Search w portalu).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="bfb7b-111">Informacje o danych</span><span class="sxs-lookup"><span data-stu-id="bfb7b-111">About the data</span></span>
<span data-ttu-id="bfb7b-112">Ta przykładowa aplikacja korzysta z danych agencji [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm) zawężonych do stanu Rhode Island w celu zmniejszenia rozmiaru zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="bfb7b-113">Użyjemy tych danych do utworzenia aplikacji wyszukiwania, która zwraca punkty orientacyjne, takie jak szpitale i szkoły, jak również formy geologiczne, takie jak strumienie, jeziora i szczyty.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="bfb7b-114">W tej aplikacji program **DataIndexer** tworzy i ładuje indeks, używając konstrukcji [indeksatora](https://msdn.microsoft.com/library/azure/dn798918.aspx), a zawężony zestaw danych z agencji USGS jest pobierany z publicznej usługi Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="bfb7b-115">Poświadczenia oraz informacje o połączeniu ze źródłem danych w trybie online są zawarte w kodzie programu.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="bfb7b-116">Nie jest konieczna żadna dodatkowa konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="bfb7b-117">Zastosowaliśmy filtr dla tego zestawu danych, aby nie przekroczyć limitu 10 000 dokumentów obowiązującego w warstwie cenowej Bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="bfb7b-118">Jeśli korzystasz z warstwy cenowej Standardowa, ten limit nie ma zastosowania.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="bfb7b-119">Aby uzyskać szczegółowe informacje o pojemności dla każdej warstwy cenowej, zobacz [Search service limits](search-limits-quotas-capacity.md) (Limity usługi wyszukiwania).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="bfb7b-120">Znajdowanie nazwy usługi oraz klucza interfejsu API usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="bfb7b-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="bfb7b-121">Po utworzeniu usługi wróć do portalu, aby uzyskać adres URL lub klucz `api-key`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="bfb7b-122">Połączenia z usługą wyszukiwania wymagają zarówno adresu URL, jak i klucza `api-key` do uwierzytelnienia wywołania.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="bfb7b-123">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="bfb7b-124">Na pasku przechodzenia kliknij pozycję **Usługa wyszukiwania**, aby wyświetlić listę wszystkich usług Azure Search aprowizowanych dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="bfb7b-125">Wybierz usługę, której chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="bfb7b-126">Na pulpicie nawigacyjnym usługi zobaczysz kafelki z istotnymi informacjami, takimi jak ikona klucza, służąca do uzyskiwania dostępu do kluczy administratora.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="bfb7b-127">Skopiuj adres URL usługi, klucz administratora i klucz zapytania.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="bfb7b-128">Wszystkie te elementy trzeba będzie później dodać do pliku config.js.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="bfb7b-129">Pobieranie plików przykładowych</span><span class="sxs-lookup"><span data-stu-id="bfb7b-129">Download the sample files</span></span>
<span data-ttu-id="bfb7b-130">Pobierz przykład za pomocą jednej z następujących metod.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="bfb7b-131">Przejdź do strony [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="bfb7b-132">Kliknij przycisk **Download ZIP** (Pobierz ZIP), zapisz plik zip, a następnie wyodrębnij wszystkie pliki w nim zawarte.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="bfb7b-133">Wszystkie kolejne modyfikacje plików i instrukcje uruchamiania będą wykonywane względem plików w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="bfb7b-134">Aktualizowanie pliku config.js</span><span class="sxs-lookup"><span data-stu-id="bfb7b-134">Update the config.js.</span></span> <span data-ttu-id="bfb7b-135">przy użyciu adresu URL usługi wyszukiwania i klucza api-key</span><span class="sxs-lookup"><span data-stu-id="bfb7b-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="bfb7b-136">Korzystając ze skopiowanego wcześniej adresu URL i klucza api-key, podaj adres URL, klucz administratora i klucz zapytania w pliku konfiguracyjnym.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="bfb7b-137">Klucze administratora przyznają pełną kontrolę nad operacjami usługi, w tym nad tworzeniem i usuwaniem indeksu oraz ładowaniem dokumentów.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="bfb7b-138">Z kolei klucze zapytania są przeznaczone dla operacji tylko do odczytu i są zwykle używane przez aplikacje klienckie, które nawiązują połączenie z usługą Azure Search.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="bfb7b-139">W tym przykładzie uwzględniamy klucz zapytania, aby pomóc w zapamiętaniu najlepszego rozwiązania, jakim jest używanie klucza zapytania w aplikacjach klienckich.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="bfb7b-140">Poniższy zrzut ekranu przedstawia plik **config.js** otwarty w edytorze tekstu, z zaznaczonymi odpowiednimi wpisami, które należy zaktualizować przy użyciu wartości odpowiednich dla usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="bfb7b-141">Hostowanie środowiska uruchomieniowego dla przykładu</span><span class="sxs-lookup"><span data-stu-id="bfb7b-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="bfb7b-142">Przykład wymaga serwera HTTP, który można zainstalować globalnie za pomocą menedżera pakietów npm.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="bfb7b-143">Dla poniższych poleceń użyj okna programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="bfb7b-144">Przejdź do folderu, który zawiera plik **package.json**.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="bfb7b-145">Wpisz polecenie `npm install`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-145">Type `npm install`.</span></span>
3. <span data-ttu-id="bfb7b-146">Wpisz polecenie `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="bfb7b-147">Tworzenie indeksu i uruchamianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="bfb7b-147">Build the index and run the application</span></span>
1. <span data-ttu-id="bfb7b-148">Wpisz polecenie `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="bfb7b-149">Wpisz polecenie `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="bfb7b-150">Wpisz polecenie `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="bfb7b-151">Za pomocą przeglądarki przejdź do strony `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="bfb7b-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="bfb7b-152">Przeszukiwanie danych agencji USGS</span><span class="sxs-lookup"><span data-stu-id="bfb7b-152">Search on USGS data</span></span>
<span data-ttu-id="bfb7b-153">Zestaw danych agencji USGS zawiera rekordy, które odnoszą się do stanu Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="bfb7b-154">Jeśli klikniesz przycisk **Szukaj**, pozostawiając pole wyszukiwania puste, zostanie wyświetlonych 50 pierwszych wpisów, co jest ustawieniem domyślnym.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="bfb7b-155">Wprowadzenie terminu wyszukiwania zaangażuje do pracy wyszukiwarkę.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="bfb7b-156">Spróbuj wprowadzić nazwę regionalną.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-156">Try entering a regional name.</span></span> <span data-ttu-id="bfb7b-157">„Roger Williams” był pierwszym gubernatorem stanu Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="bfb7b-158">Liczne parki, budynki i szkoły są nazwane jego imieniem.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="bfb7b-159">Możesz też wprowadzić jeden z poniższych terminów:</span><span class="sxs-lookup"><span data-stu-id="bfb7b-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="bfb7b-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="bfb7b-160">Pawtucket</span></span>
* <span data-ttu-id="bfb7b-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="bfb7b-161">Pembroke</span></span>
* <span data-ttu-id="bfb7b-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="bfb7b-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfb7b-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bfb7b-163">Next steps</span></span>
<span data-ttu-id="bfb7b-164">To jest pierwszy samouczek usługi Azure Search oparty na środowisku Node.js i zestawie danych agencji USGS.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="bfb7b-165">Wraz z upływem czasu będziemy rozszerzać ten samouczek, aby zademonstrować dodatkowe funkcje wyszukiwania, których mogą być przydatne w rozwiązaniach niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="bfb7b-166">Jeśli masz już jakieś doświadczenie z usługą Azure Search, możesz użyć tego przykładu jako punktu wyjścia do wypróbowania sugestorów (uzupełnianie przy wpisywaniu lub autouzupełnianie zapytań), filtrów i nawigacji aspektowej.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="bfb7b-167">Możesz również ulepszyć stronę wyników wyszukiwania przez dodanie liczników i łączenie dokumentów w partie, aby użytkownicy mogli przechodzić do kolejnych stron wyników.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="bfb7b-168">Dopiero zaczynasz korzystać z usługi Azure Search?</span><span class="sxs-lookup"><span data-stu-id="bfb7b-168">New to Azure Search?</span></span> <span data-ttu-id="bfb7b-169">Zalecamy wypróbować inne samouczki, aby poznać możliwości tworzenia w usłudze.</span><span class="sxs-lookup"><span data-stu-id="bfb7b-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="bfb7b-170">Aby znaleźć więcej zasobów, odwiedź naszą [stronę dokumentacji](https://azure.microsoft.com/documentation/services/search/).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="bfb7b-171">Aby uzyskać więcej informacji, możesz również zobaczyć linki z naszej [listy filmów wideo i samouczków](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="bfb7b-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
