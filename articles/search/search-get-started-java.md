---
title: "aaaGet wprowadzenie do usługi Azure Search w języku Java | Dokumentacja firmy Microsoft"
description: "Jak toobuild chmury hostowanej wyszukiwanie aplikacji na platformie Azure przy użyciu języka Java jako języka programowania."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="f0960-103">Wprowadzenie do usługi Azure Search w języku Java</span><span class="sxs-lookup"><span data-stu-id="f0960-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0960-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f0960-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="f0960-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f0960-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="f0960-106">Dowiedz się, jak toobuild niestandardowych Java Wyszukaj aplikację, która używa usługi Azure Search jako środowiska wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="f0960-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="f0960-107">W tym samouczku używana hello [interfejsu API REST usługi Azure Search](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello obiekty i operacje używane w tym ćwiczeniu.</span><span class="sxs-lookup"><span data-stu-id="f0960-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="f0960-108">toorun tej próbki, musi mieć usługi Azure Search, której możesz zarejestrować się w hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0960-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="f0960-109">Zobacz [Tworzenie usługi Azure Search w portalu hello](search-create-service-portal.md) instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="f0960-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="f0960-110">Możemy użyć następującego oprogramowania toobuild hello i przetestowania przedstawionego przykładu:</span><span class="sxs-lookup"><span data-stu-id="f0960-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="f0960-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="f0960-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="f0960-112">Należy się wersję EE hello toodownload.</span><span class="sxs-lookup"><span data-stu-id="f0960-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="f0960-113">Jeden z kroków weryfikacji hello wymaga funkcji, która znajduje się tylko w tej wersji.</span><span class="sxs-lookup"><span data-stu-id="f0960-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="f0960-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="f0960-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="f0960-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="f0960-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="f0960-116">Dane hello — informacje</span><span class="sxs-lookup"><span data-stu-id="f0960-116">About hello data</span></span>
<span data-ttu-id="f0960-117">Ta przykładowa aplikacja korzysta z danych z hello [Stanów Zjednoczonych Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm)zawężonych hello stanu Rhode Island tooreduce hello dataset rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="f0960-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="f0960-118">Użyjemy tego toobuild danych aplikacji wyszukiwania, która zwraca punkty orientacyjne, takie jak szpitale i szkoły, jak również geologiczne, takie jak strumienie, jeziora i szczyty.</span><span class="sxs-lookup"><span data-stu-id="f0960-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="f0960-119">W tej aplikacji hello **SearchServlet.java** budowania i obciążeń hello indeksu przy użyciu [indeksatora](https://msdn.microsoft.com/library/azure/dn798918.aspx) konstrukcja pobierania hello filtrowane danych agencji USGS z publicznej usługi Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f0960-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="f0960-120">Wstępnie zdefiniowane poświadczenia oraz źródło danych w trybie online toohello informacji połączenia są zawarte w kodzie programu hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="f0960-121">W zakresie dostępu do danych nie jest konieczna dalsza konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="f0960-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="f0960-122">Zastosowaliśmy filtr na toostay tego zestawu danych w obszarze hello 10 000 dokumentów limit hello warstwy cenowej bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="f0960-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="f0960-123">Jeśli używasz hello warstwy standardowa, ten limit nie ma zastosowania i możesz zmodyfikować ten kod toouse większego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="f0960-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="f0960-124">Aby uzyskać szczegółowe informacje o pojemności dla każdej warstwy cenowej, zobacz [Limits and constraints](search-limits-quotas-capacity.md) (Limity i ograniczenia).</span><span class="sxs-lookup"><span data-stu-id="f0960-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="f0960-125">Informacje o plikach program hello</span><span class="sxs-lookup"><span data-stu-id="f0960-125">About hello program files</span></span>
<span data-ttu-id="f0960-126">Witaj Poniższa lista zawiera opis hello plików, które są odpowiednie toothis próbki.</span><span class="sxs-lookup"><span data-stu-id="f0960-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="f0960-127">Search.JSP: Udostępnia interfejs użytkownika hello</span><span class="sxs-lookup"><span data-stu-id="f0960-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="f0960-128">SearchServlet.java: Udostępnia metody (podobnie tooa kontroler na platformie MVC)</span><span class="sxs-lookup"><span data-stu-id="f0960-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="f0960-129">SearchServiceClient.java: obsługuje żądania HTTP</span><span class="sxs-lookup"><span data-stu-id="f0960-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="f0960-130">SearchServiceHelper.java: klasa pomocy, która udostępnia metody statyczne</span><span class="sxs-lookup"><span data-stu-id="f0960-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="f0960-131">Document.Java: Udostępnia model danych hello</span><span class="sxs-lookup"><span data-stu-id="f0960-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="f0960-132">config.Properties: ustawia adres URL usługi wyszukiwania hello i klucza api-key</span><span class="sxs-lookup"><span data-stu-id="f0960-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="f0960-133">Pom.xml: zależność narzędzia Maven</span><span class="sxs-lookup"><span data-stu-id="f0960-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="f0960-134">Znajdź hello nazwę usługi i klucza interfejsu api usługi Azure Search</span><span class="sxs-lookup"><span data-stu-id="f0960-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="f0960-135">Wszystkie wywołania interfejsu API REST usługi Azure Search wymagają podania adresu URL usługi hello i klucz interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="f0960-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="f0960-136">Zaloguj się toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0960-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f0960-137">Na pasku skok hello, kliknij przycisk **usługi wyszukiwania** toolist wszystkie hello usługi Azure Search aprowizowanych dla subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f0960-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="f0960-138">Wybierz usługę hello ma toouse.</span><span class="sxs-lookup"><span data-stu-id="f0960-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="f0960-139">Na powitania nawigacyjnym usługi zobaczysz Kafelki z istotnymi informacjami, jak również ikonę klucza hello dla uzyskiwania dostępu do kluczy administratora hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="f0960-140">Skopiuj adres URL usługi hello i klucz administratora.</span><span class="sxs-lookup"><span data-stu-id="f0960-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="f0960-141">Będą Ci potrzebne później, po dodaniu ich toohello **config.properties** pliku.</span><span class="sxs-lookup"><span data-stu-id="f0960-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="f0960-142">Pobieranie plików przykładowych hello</span><span class="sxs-lookup"><span data-stu-id="f0960-142">Download hello sample files</span></span>
1. <span data-ttu-id="f0960-143">Przejdź za[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="f0960-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="f0960-144">Kliknij przycisk **Pobierz ZIP**, Zapisz toodisk pliku zip hello, a następnie Wyodrębnij wszystkie pliki hello zawiera.</span><span class="sxs-lookup"><span data-stu-id="f0960-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="f0960-145">Rozważ wyodrębnienie hello plików do sieci toomake obszaru roboczego Java łatwiejsze projektu hello toofind później.</span><span class="sxs-lookup"><span data-stu-id="f0960-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="f0960-146">pliki przykładowe Hello są tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="f0960-146">hello sample files are read-only.</span></span> <span data-ttu-id="f0960-147">Kliknij prawym przyciskiem myszy folder właściwości i wyczyść hello atrybut tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="f0960-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="f0960-148">Wszystkie kolejne modyfikacje plików i instrukcje uruchamiania będą wykonywane względem plików w tym folderze.</span><span class="sxs-lookup"><span data-stu-id="f0960-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="f0960-149">Importowanie projektu</span><span class="sxs-lookup"><span data-stu-id="f0960-149">Import project</span></span>
1. <span data-ttu-id="f0960-150">W środowisku Eclipse wybierz pozycję **Plik** > **Importuj** > **Ogólne** > **Istniejące projekty do obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="f0960-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="f0960-151">W **wybierz katalog główny**, Przeglądaj toohello folderu zawierającego pliki przykładowe.</span><span class="sxs-lookup"><span data-stu-id="f0960-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="f0960-152">Wybierz folder hello, który zawiera hello .project folder.</span><span class="sxs-lookup"><span data-stu-id="f0960-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="f0960-153">Witaj projektu powinna być widoczna w hello **projekty** listy wybranego elementu.</span><span class="sxs-lookup"><span data-stu-id="f0960-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="f0960-154">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f0960-154">Click **Finish**.</span></span>
4. <span data-ttu-id="f0960-155">Użyj **Eksplorator projektów** tooview i edytuj pliki hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="f0960-156">Jeśli go nie jest jeszcze otwarty, kliknij przycisk **okna** > **Pokaż widok** > **Eksplorator projektów** lub użyj hello skrótów tooopen go.</span><span class="sxs-lookup"><span data-stu-id="f0960-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="f0960-157">Skonfiguruj adres URL usługi hello i klucza api-key</span><span class="sxs-lookup"><span data-stu-id="f0960-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="f0960-158">W **Eksplorator projektów**, kliknij dwukrotnie **config.properties** ustawienia konfiguracji hello tooedit zawierający hello nazwę serwera i klucz api-key.</span><span class="sxs-lookup"><span data-stu-id="f0960-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="f0960-159">Zobacz kroki toohello wcześniej w tym artykule, w których znaleziono hello adres URL usługi i klucza api-key w hello [Azure Portal](https://portal.azure.com), tooget hello wartości należy wpisać w **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="f0960-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="f0960-160">W **config.properties**, zastąp "Klucz interfejsu Api" hello interfejsu api-key dla Twojej usługi.</span><span class="sxs-lookup"><span data-stu-id="f0960-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="f0960-161">Następnie nazwy usługi (hello pierwszy składnik hello http://servicename.search.windows.net adres URL) zastępuje "Nazwa usługi" w hello tego samego pliku.</span><span class="sxs-lookup"><span data-stu-id="f0960-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="f0960-162">Konfigurowanie środowisk hello projektu, kompilacji i środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="f0960-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="f0960-163">W środowisku Eclipse, w obszarze Eksplorator projektów kliknij prawym przyciskiem myszy projekt hello > **właściwości** > **aspekty projektu**.</span><span class="sxs-lookup"><span data-stu-id="f0960-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="f0960-164">Wybierz pozycje: **Dynamiczny moduł WWW**, **Java** i **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="f0960-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="f0960-165">Kliknij przycisk **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="f0960-165">Click **Apply**.</span></span>
4. <span data-ttu-id="f0960-166">Wybierz pozycję **Okna** > **Preferencje** > **Serwer** > **Środowiska wykonawcze** > **Dodaj...**.</span><span class="sxs-lookup"><span data-stu-id="f0960-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="f0960-167">Rozwiń pozycję Apache i wybierz wersję hello hello serwer Apache Tomcat, która została wcześniej zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="f0960-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="f0960-168">W naszym systemie zainstalowano wersję 8.</span><span class="sxs-lookup"><span data-stu-id="f0960-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="f0960-169">Na następnej stronie powitania określ katalog instalacyjny serwera Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="f0960-170">Na komputerze z systemem Windows najprawdopodobniej będzie to katalog C:\Program Files\Apache Software Foundation\Tomcat *wersja*.</span><span class="sxs-lookup"><span data-stu-id="f0960-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="f0960-171">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f0960-171">Click **Finish**.</span></span>
8. <span data-ttu-id="f0960-172">Wybierz pozycję **Okna** > **Preferencje** > **Java** > **Zainstalowane środowiska JRE** > **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f0960-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="f0960-173">W obszarze **Dodawanie środowiska JRE** wybierz opcję **Standardowa maszyna VM**.</span><span class="sxs-lookup"><span data-stu-id="f0960-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="f0960-174">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0960-174">Click **Next**.</span></span>
11. <span data-ttu-id="f0960-175">W obszarze Katalog główny środowiska JRE sekcji Definicja środowiska JRE kliknij pozycję **Katalog**.</span><span class="sxs-lookup"><span data-stu-id="f0960-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="f0960-176">Przejdź za**Program Files** > **Java** i wybierz hello JDK została wcześniej zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="f0960-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="f0960-177">Jest ważne tooselect hello JDK jako hello środowiska JRE.</span><span class="sxs-lookup"><span data-stu-id="f0960-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="f0960-178">W obszarze zainstalowane środowiska JRE, wybierz hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="f0960-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="f0960-179">Twoje ustawienia powinny być podobne toohello następującego zrzutu ekranu.</span><span class="sxs-lookup"><span data-stu-id="f0960-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="f0960-180">Opcjonalnie wybierz **okna** > **przeglądarki sieci Web** > **programu Internet Explorer** aplikacji hello tooopen w oknie zewnętrznej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f0960-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="f0960-181">Używanie zewnętrznej przeglądarki zapewnia lepsze środowisko aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f0960-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="f0960-182">Zadania konfiguracji hello zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="f0960-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="f0960-183">Następnie możesz części skompilujesz i uruchomisz projekt hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="f0960-184">Tworzenie projektu hello</span><span class="sxs-lookup"><span data-stu-id="f0960-184">Build hello project</span></span>
1. <span data-ttu-id="f0960-185">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy nazwę projektu hello i wybierz polecenie **Uruchom jako** > **kompilacja Maven...**  tooconfigure hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f0960-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="f0960-186">W obszarze Edycja konfiguracji, w polu Cele wpisz „czysta instalacja”, a następnie kliknij pozycję **Wykonaj**.</span><span class="sxs-lookup"><span data-stu-id="f0960-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="f0960-187">Komunikaty o stanie są okna konsoli toohello danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f0960-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="f0960-188">BUDOWANIE powiodło wskazujące hello projektu zakończyło się bez błędów powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="f0960-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="f0960-189">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f0960-189">Run hello app</span></span>
<span data-ttu-id="f0960-190">W tym ostatnim kroku uruchomisz aplikacji hello w środowisko uruchomieniowe serwera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f0960-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="f0960-191">Jeśli nie zostało jeszcze określone środowisko uruchomieniowe serwera w środowisku Eclipse, potrzebujesz toodo ją najpierw.</span><span class="sxs-lookup"><span data-stu-id="f0960-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="f0960-192">W obszarze Eksplorator projektów rozwiń pozycję **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="f0960-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="f0960-193">Kliknij prawym przyciskiem myszy pozycję **Search.jsp** >  wybierz polecenie **Wykonaj jako** > **Wykonaj na serwerze**.</span><span class="sxs-lookup"><span data-stu-id="f0960-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="f0960-194">Wybierz serwer Apache Tomcat hello, a następnie kliknij przycisk **Uruchom**.</span><span class="sxs-lookup"><span data-stu-id="f0960-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="f0960-195">Jeśli używasz toostore z systemem innym niż domyślny obszar roboczy projektu, potrzebujesz toomodify **Konfiguracja Uruchom** toopoint toohello projektu lokalizacji tooavoid błędu podczas uruchamiania serwera.</span><span class="sxs-lookup"><span data-stu-id="f0960-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="f0960-196">W obszarze Eksplorator projektów kliknij prawym przyciskiem myszy pozycję **Search.jsp** >  wybierz polecenie **Wykonaj jako** > **Konfiguracje wykonywania**.</span><span class="sxs-lookup"><span data-stu-id="f0960-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="f0960-197">Wybierz serwer Apache Tomcat hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="f0960-198">Kliknij pozycję **Argumenty**.</span><span class="sxs-lookup"><span data-stu-id="f0960-198">Click **Arguments**.</span></span> <span data-ttu-id="f0960-199">Kliknij przycisk **obszaru roboczego** lub **systemu plików** tooset hello folderu zawierającego hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f0960-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="f0960-200">Po uruchomieniu aplikacji hello powinna zostać wyświetlona okno przeglądarki zawierające pole wyszukiwania służące do wprowadzania terminów.</span><span class="sxs-lookup"><span data-stu-id="f0960-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="f0960-201">Poczekaj około minutę przed kliknięciem przycisku **wyszukiwania** toogive hello usługi Czas toocreate i obciążenia hello indeksu.</span><span class="sxs-lookup"><span data-stu-id="f0960-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="f0960-202">Jeśli wystąpi błąd 404 protokołu HTTP, wystarczy toowait nieco dłużej przed podjęciem ponownej próby.</span><span class="sxs-lookup"><span data-stu-id="f0960-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="f0960-203">Przeszukiwanie danych agencji USGS</span><span class="sxs-lookup"><span data-stu-id="f0960-203">Search on USGS data</span></span>
<span data-ttu-id="f0960-204">zestaw danych agencji USGS Hello zawiera rekordy, które są odpowiednie toohello stanu Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="f0960-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="f0960-205">Jeśli klikniesz przycisk **wyszukiwania** na pole wyszukiwania puste, zostanie wyświetlony hello 50 pierwszych wpisów, który jest domyślnym hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="f0960-206">Wprowadzenie terminu zapewni hello wyszukiwarki coś toogo na.</span><span class="sxs-lookup"><span data-stu-id="f0960-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="f0960-207">Spróbuj wprowadzić nazwę regionalną.</span><span class="sxs-lookup"><span data-stu-id="f0960-207">Try entering a regional name.</span></span> <span data-ttu-id="f0960-208">"Roger Williams" był pierwszym gubernatorem stanu Rhode Island hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="f0960-209">Liczne parki, budynki i szkoły są nazwane jego imieniem.</span><span class="sxs-lookup"><span data-stu-id="f0960-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="f0960-210">Możesz też wprowadzić jeden z poniższych terminów:</span><span class="sxs-lookup"><span data-stu-id="f0960-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="f0960-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="f0960-211">Pawtucket</span></span>
* <span data-ttu-id="f0960-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="f0960-212">Pembroke</span></span>
* <span data-ttu-id="f0960-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="f0960-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0960-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0960-214">Next steps</span></span>
<span data-ttu-id="f0960-215">To jest pierwszy samouczek usługi Azure Search hello, oparty na języku Java i hello danych agencji USGS.</span><span class="sxs-lookup"><span data-stu-id="f0960-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="f0960-216">Wraz z upływem czasu będziemy rozszerzać ten samouczek toodemonstrate dodatkowe funkcje wyszukiwania może być toouse w rozwiązaniach niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="f0960-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="f0960-217">Jeśli masz już pewną wiedzę w usłudze Azure Search, możesz użyć tego przykładu jako podstawy do dalszych eksperymentów, prawdopodobnie rozbudować hello [stronę wyszukiwania](search-pagination-page-layout.md), lub implementacja [nawigacji aspektowej](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="f0960-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="f0960-218">Możesz również ulepszyć stronę wyników wyszukiwania hello przez dodanie liczników i łączenie dokumentów w partie, dzięki czemu użytkownicy mogą przeglądania wyników hello.</span><span class="sxs-lookup"><span data-stu-id="f0960-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="f0960-219">TooAzure nowego wyszukiwania?</span><span class="sxs-lookup"><span data-stu-id="f0960-219">New tooAzure Search?</span></span> <span data-ttu-id="f0960-220">Zaleca się podjęcie próby toodevelop innych samouczków zrozumienia można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="f0960-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="f0960-221">Można znaleźć w naszych [stronę dokumentacji](https://azure.microsoft.com/documentation/services/search/) toofind więcej zasobów.</span><span class="sxs-lookup"><span data-stu-id="f0960-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="f0960-222">Można również wyświetlić hello łącza w naszym [listy filmów wideo i samouczków](search-video-demo-tutorial-list.md) tooaccess więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f0960-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
