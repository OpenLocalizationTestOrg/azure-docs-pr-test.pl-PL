---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3a632825-db5b-49ec-98bd-887138798bc4
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: deb2e52dd03f5beb2ad6a927bd2d03e47d20b691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="mapping-an-existing-web-service-tooodata-through-csdl"></a><span data-ttu-id="4df64-103">Mapowanie istniejących tooOData usługi sieci web za pomocą pliku CSDL</span><span class="sxs-lookup"><span data-stu-id="4df64-103">Mapping an existing web service tooOData through CSDL</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4df64-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="4df64-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="4df64-105">Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="4df64-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="4df64-106">Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="4df64-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="4df64-107">Ten artykuł zawiera omówienie dotyczące toouse toomap CSDL tooan istniejącej usługi zgodne usługi OData.</span><span class="sxs-lookup"><span data-stu-id="4df64-107">This article gives an overview on how toouse a CSDL toomap an existing service tooan OData compatible service.</span></span> <span data-ttu-id="4df64-108">Wyjaśniono, jak toocreate hello dokumentu mapowania (CSDL) przekształcającą żądanie wejściowe hello z powitania klienta za pośrednictwem wywołania usługi i hello output (dane) ponownie toohello klienta za pośrednictwem zgodne źródła strumieniowego OData.</span><span class="sxs-lookup"><span data-stu-id="4df64-108">It explains how toocreate hello mapping document (CSDL) that transforms hello input request from hello client via a service call and hello output (data) back toohello client via an OData compatible feed.</span></span> <span data-ttu-id="4df64-109">Microsoft Azure Marketplace udostępnia użytkownikom końcowym toohello usług przy użyciu protokołu OData hello.</span><span class="sxs-lookup"><span data-stu-id="4df64-109">Microsoft’s Azure Marketplace exposes services toohello end-users by using hello OData protocol.</span></span> <span data-ttu-id="4df64-110">Usługi, które są udostępniane przez dostawców zawartości (właścicielom danych) są widoczne w różnych formularzy, takich jak REST protokołu SOAP, itp.</span><span class="sxs-lookup"><span data-stu-id="4df64-110">Services that are exposed by content providers (Data Owners) are exposed in a variety of forms, such as REST, SOAP, etc.</span></span>

## <a name="what-is-a-csdl-and-its-structure"></a><span data-ttu-id="4df64-111">Co to jest plik CSDL, a jego struktury?</span><span class="sxs-lookup"><span data-stu-id="4df64-111">What is a CSDL and its structure?</span></span>
<span data-ttu-id="4df64-112">CSDL (koncepcyjnej Schema Definition Language) jest specyfikacją określające, jak bazy danych lub usługa sieci web toodescribe wspólnych usługi XML wyrażenia toohello portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4df64-112">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span>

<span data-ttu-id="4df64-113">Proste omówienie hello **żądania przepływu:**</span><span class="sxs-lookup"><span data-stu-id="4df64-113">Simple overview of hello **request flow:**</span></span>

  `Client -> Azure Marketplace -> Content Provider’s Web Service (Get, Post, Delete, Put)`

<span data-ttu-id="4df64-114">Witaj **przepływ danych** znajduje się w hello przeciwne kierunek:</span><span class="sxs-lookup"><span data-stu-id="4df64-114">hello **data flow** is in hello opposite direction:</span></span>

  `Client <- Azure Marketplace <- Content Provider’s WebService`

<span data-ttu-id="4df64-115">**Rysunek 1** diagramy jak klienta może uzyskiwać dane z dostawcy zawartości (usługi) za pośrednictwem hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4df64-115">**Figure 1** diagrams how a client would obtain data from a content provider (your service) by going through hello Azure Marketplace.</span></span>  <span data-ttu-id="4df64-116">Hello CSDL jest używany przez hello mapowania/przekształcenia składnika toohandle hello żądania i przekazywania danych między hello zawartości dostawcy usług i hello żądania klienta.</span><span class="sxs-lookup"><span data-stu-id="4df64-116">hello CSDL is used by hello Mapping/Transformation component toohandle hello request and data pass between hello content provider’s service(s) and hello requesting client.</span></span>

<span data-ttu-id="4df64-117">*Rysunek 1: Szczegółowy przepływ żądaniom dostawca toocontent klienta za pośrednictwem portalu Azure Marketplace*</span><span class="sxs-lookup"><span data-stu-id="4df64-117">*Figure 1: Detailed flow from requesting client toocontent provider via Azure Marketplace*</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-1.png)

<span data-ttu-id="4df64-119">W tle na Atom, protokołu Atom i hello protokołu OData, na które hello kompilacji rozszerzenia portalu Azure Marketplace, zapoznaj się z tematem: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span><span class="sxs-lookup"><span data-stu-id="4df64-119">For background on Atom, Atom Pub, and hello OData protocol upon which hello Azure Marketplace extensions build, please review: [http://msdn.microsoft.com/library/ff478141.aspx](http://msdn.microsoft.com/library/ff478141.aspx)</span></span>

<span data-ttu-id="4df64-120">Fragment powyższego łącza: *"hello hello protokołu Open Data (OData poniżej określonego tooas) służy protokół tooprovide opartego na interfejsie REST dla operacji CRUD stylu (tworzenia, odczytu, aktualizacji i usuwania) względem zasobów udostępniony jako usługi danych. "Usługa danych" jest punktem końcowym w przypadku, gdy dane widoczne z co najmniej jeden "kolekcji" każdego z zero lub więcej "pozycje", które składają się z pary wartości o nazwie wpisany. OData jest opublikowane przez firmę Microsoft w obszarze standardów języka OASIS (organizacji hello przejścia z strukturalnych informacji standardów) tak, aby każdy użytkownik, który chce toocan kompilacji serwerów, klientów lub narzędzia bez ograniczeń lub opłat licencyjnych. "*</span><span class="sxs-lookup"><span data-stu-id="4df64-120">Excerpt from above link: *“hello purpose of hello Open Data protocol (hereafter referred tooas OData) is tooprovide a REST-based protocol for CRUD-style operations (Create, Read, Update and Delete) against resources exposed as data services. A “data service” is an endpoint where there is data exposed from one or more “collections” each with zero or more “entries”, which consist of typed named-value pairs. OData is published by Microsoft under OASIS (Organization for hello Advancement of Structured Information Standards) Standards so that anyone that wants toocan build servers, clients or tools without royalties or restrictions.”*</span></span>

### <a name="three-critical-pieces-that-have-toobe-defined-by-hello-csdl-are"></a><span data-ttu-id="4df64-121">Są trzy najistotniejsze mających toobe zdefiniowane przez hello CSDL:</span><span class="sxs-lookup"><span data-stu-id="4df64-121">Three Critical Pieces that have toobe defined by hello CSDL are:</span></span>
* <span data-ttu-id="4df64-122">Witaj **punktu końcowego** z hello usługodawcy hello sieci Web adres URI hello usługi</span><span class="sxs-lookup"><span data-stu-id="4df64-122">hello **endpoint** of hello Service Provider hello Web Address (URI) of hello Service</span></span>
* <span data-ttu-id="4df64-123">Witaj **parametry danych** przekazywany jako wejściowych toohello usługodawcy definicje hello parametrów hello wysyłane usługi toohello dostawcy zawartości w dół toohello — typ danych.</span><span class="sxs-lookup"><span data-stu-id="4df64-123">hello **data parameters** being passed as input toohello Service Provider hello definitions of hello parameters being sent toohello Content Provider’s service down toohello data type.</span></span>
* <span data-ttu-id="4df64-124">**Schemat** hello danych zwracanych schematu hello żądanie usługi toohello hello dane są dostarczane przez usługę hello dostawcy zawartości, w tym kontenerze, kolekcje/tabel, kolumn/zmiennych i typy danych.</span><span class="sxs-lookup"><span data-stu-id="4df64-124">**Schema** of hello data being returned toohello Requesting Service hello schema of hello data being delivered by hello Content Provider’s service, including Container, collections/tables, variables/columns, and data types.</span></span>

<span data-ttu-id="4df64-125">powitania po diagram zawiera omówienie przepływu hello, z którym powitania klienta wprowadza hello OData instrukcji (usługa sieci web wywołania toohello dostawcy zawartości) toogetting hello wyników/dane ponownie.</span><span class="sxs-lookup"><span data-stu-id="4df64-125">hello following diagram shows an overview of hello flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-2.png)

### <a name="steps"></a><span data-ttu-id="4df64-127">kroki:</span><span class="sxs-lookup"><span data-stu-id="4df64-127">Steps:</span></span>
1. <span data-ttu-id="4df64-128">Klient wysyła żądanie za pośrednictwem wywołania usługi z parametry wejściowe zdefiniowane w XML toohello portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4df64-128">Client sends request via Service call complete with Input Parameters defined in XML toohello Azure Marketplace</span></span>
2. <span data-ttu-id="4df64-129">Plik CSDL jest używane toovalidate hello wywołania usługi.</span><span class="sxs-lookup"><span data-stu-id="4df64-129">CSDL is used toovalidate hello Service call.</span></span>
   * <span data-ttu-id="4df64-130">Witaj sformatowany zgłoszenia serwisowego jest następnie wysyłana toohello usługi dostawców zawartości przez hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4df64-130">hello Formatted Service Call is then sent toohello Content Providers Service by hello Azure Marketplace</span></span>
3. <span data-ttu-id="4df64-131">Witaj Usługa sieci Web wykonuje i preforms hello akcji hello zlecenie Http (tj. GET) hello dane są zwracane, tooAzure Marketplace, gdzie hello żądanych danych (jeżeli istniał) jest ujawnia w formacie XML toohello klienta przy użyciu mapowania zdefiniowane w pliku CSDL hello hello.</span><span class="sxs-lookup"><span data-stu-id="4df64-131">hello Webservice executes and preforms hello action of hello Http Verb (i.e. GET) hello data is returned tooAzure Marketplace where hello requested data (if any) is exposes in XML Format toohello Client using hello Mapping defined in hello CSDL.</span></span>
4. <span data-ttu-id="4df64-132">Klient jest wiadomości powitania hello danych (jeżeli istniał) w formacie XML lub JSON</span><span class="sxs-lookup"><span data-stu-id="4df64-132">hello Client is sent hello data (if any) in XML or JSON format</span></span>

## <a name="definitions"></a><span data-ttu-id="4df64-133">Definicje</span><span class="sxs-lookup"><span data-stu-id="4df64-133">Definitions</span></span>
### <a name="odata-atom-pub"></a><span data-ttu-id="4df64-134">Protokołu OData ATOM</span><span class="sxs-lookup"><span data-stu-id="4df64-134">OData ATOM pub</span></span>
<span data-ttu-id="4df64-135">Ustaw rozszerzenie protokołu ATOM toohello, gdzie każdy wpis reprezentuje jeden wiersz wyniku.</span><span class="sxs-lookup"><span data-stu-id="4df64-135">An extension toohello ATOM pub where each entry represents one row of a result set.</span></span> <span data-ttu-id="4df64-136">Hello zawartości część wpis hello jest rozszerzony toocontain hello wartości wiersza hello — jako pary wartości klucza.</span><span class="sxs-lookup"><span data-stu-id="4df64-136">hello content part of hello entry is enhanced toocontain hello values of hello row – as key value pairs.</span></span> <span data-ttu-id="4df64-137">Więcej informacji znajduje się w tym miejscu: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span><span class="sxs-lookup"><span data-stu-id="4df64-137">More information is found here: [https://www.odata.org/documentation/odata-version-3-0/atom-format/](https://www.odata.org/documentation/odata-version-3-0/atom-format/)</span></span>

### <a name="csdl---conceptual-schema-definition-language"></a><span data-ttu-id="4df64-138">Plik CSDL - Conceptual Schema Definition Language</span><span class="sxs-lookup"><span data-stu-id="4df64-138">CSDL - Conceptual Schema Definition Language</span></span>
<span data-ttu-id="4df64-139">Umożliwia zdefiniowanie funkcji (SPROCs) i jednostek, które są dostępne za pośrednictwem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4df64-139">Allows defining functions (SPROCs) and entities that are exposed through a database.</span></span> <span data-ttu-id="4df64-140">Więcej informacji znaleźć tutaj: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span><span class="sxs-lookup"><span data-stu-id="4df64-140">More information found here: [http://msdn.microsoft.com/library/bb399292.aspx](http://msdn.microsoft.com/library/bb399292.aspx)</span></span>  

> [!TIP]
> <span data-ttu-id="4df64-141">Kliknij przycisk hello **inne wersje** listy rozwijanej i wybierz wersję, jeśli nie widzisz hello artykułu.</span><span class="sxs-lookup"><span data-stu-id="4df64-141">Click hello **other versions** dropdown and select a version if you don’t see hello article.</span></span>
> 
> 

### <a name="edm---entry-data-model"></a><span data-ttu-id="4df64-142">EDM - wpis modelu danych</span><span class="sxs-lookup"><span data-stu-id="4df64-142">EDM - Entry Data Model</span></span>
* <span data-ttu-id="4df64-143">Omówienie: [http://msdn.microsoft.com/library/vstudio/ee382825 (v=vs.100).aspx][OverviewLink]</span><span class="sxs-lookup"><span data-stu-id="4df64-143">Overview: [http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx][OverviewLink]</span></span>

[OverviewLink]:http://msdn.microsoft.com/library/vstudio/ee382825(v=vs.100).aspx
* <span data-ttu-id="4df64-144">Podgląd: [http://msdn.microsoft.com/library/aa697428 (v=vs.80).aspx][PreviewLink]</span><span class="sxs-lookup"><span data-stu-id="4df64-144">Preview: [http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx][PreviewLink]</span></span>

[PreviewLink]:http://msdn.microsoft.com/library/aa697428(v=vs.80).aspx
* <span data-ttu-id="4df64-145">Typy danych: [http://msdn.microsoft.com/library/bb399548 (v=VS.100).aspx][DataTypesLink]</span><span class="sxs-lookup"><span data-stu-id="4df64-145">Data types: [http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx][DataTypesLink]</span></span>

[DataTypesLink]:http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx

<span data-ttu-id="4df64-146">Witaj poniżej pokazano hello szczegółowych przepływu tooRight po lewej stronie, z którym powitania klienta wprowadza hello OData instrukcji (usługa sieci web wywołania toohello dostawcy zawartości) toogetting hello wyników/dane ponownie:</span><span class="sxs-lookup"><span data-stu-id="4df64-146">hello following shows hello detailed Left tooRight flow from where hello client enters hello OData statement (call toohello content provider’s web service) toogetting hello results/data back:</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation-odata-mapping/figure-3.png)

## <a name="csdl-basics"></a><span data-ttu-id="4df64-148">Podstawowe informacje o pliku CSDL</span><span class="sxs-lookup"><span data-stu-id="4df64-148">CSDL Basics</span></span>
<span data-ttu-id="4df64-149">CSDL (koncepcyjnej Schema Definition Language) jest specyfikacją określające, jak bazy danych lub usługa sieci web toodescribe wspólnych usługi XML wyrażenia toohello portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4df64-149">A CSDL (Conceptual Schema Definition Language) is a specification defining how toodescribe web service or database service in common XML verbiage toohello Azure Marketplace.</span></span> <span data-ttu-id="4df64-150">W tym artykule opisano CSDL kawałków hello krytyczny, który **umożliwia przekazywanie hello danych z toohello źródła danych hello Azure Marketplace.**</span><span class="sxs-lookup"><span data-stu-id="4df64-150">CSDL describes hello critical pieces that **makes hello passing of data from hello Data Source toohello Azure Marketplace possible.**</span></span> <span data-ttu-id="4df64-151">elementy główne Hello są opisane w tym miejscu:</span><span class="sxs-lookup"><span data-stu-id="4df64-151">hello main pieces are described here:</span></span>

* <span data-ttu-id="4df64-152">Informacje o interfejsie opisem wszystkich funkcji dostępnych publicznie (FunctionImport węzeł)</span><span class="sxs-lookup"><span data-stu-id="4df64-152">Interface information describing all publicly available functions (FunctionImport Node)</span></span>
* <span data-ttu-id="4df64-153">Informacje o typie danych dla wszystkich wiadomości requests(input) i responses(outputs) komunikatu (EntityContainer/EntitySet/EntityType węzłów)</span><span class="sxs-lookup"><span data-stu-id="4df64-153">Data type information for all message requests(input) and message responses(outputs) (EntityContainer/EntitySet/EntityType Nodes)</span></span>
* <span data-ttu-id="4df64-154">Informacje o toobe protokołu transportu hello powiązania używane (węzeł nagłówka)</span><span class="sxs-lookup"><span data-stu-id="4df64-154">Binding information about hello transport protocol toobe used (Header Node)</span></span>
* <span data-ttu-id="4df64-155">Informacje o adresie do lokalizowania hello określonej usługi (atrybut BaseURI)</span><span class="sxs-lookup"><span data-stu-id="4df64-155">Address information for locating hello specified service (BaseURI attribute)</span></span>

<span data-ttu-id="4df64-156">Mówiąc hello CSDL reprezentuje kontraktu platformy - i niezależny od języka między żądający usługi hello i hello dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="4df64-156">In a nutshell, hello CSDL represents a platform- and language-independent contract between hello service requestor and hello service provider.</span></span> <span data-ttu-id="4df64-157">Przy użyciu hello CSDL, klient można zlokalizować usługi bazy danych i usługi sieci web i wywołać żadnego ze swoich publicznie dostępnych funkcji.</span><span class="sxs-lookup"><span data-stu-id="4df64-157">Using hello CSDL, a client can locate a web service/database service and invoke any of its publicly available functions.</span></span>

### <a name="relating-a-csdl-tooa-database-or-a-collection"></a><span data-ttu-id="4df64-158">Dotyczących tooa CSDL bazy danych lub kolekcji</span><span class="sxs-lookup"><span data-stu-id="4df64-158">Relating a CSDL tooa Database or a Collection</span></span>
<span data-ttu-id="4df64-159">**Witaj Specyfikacja pliku CSDL**</span><span class="sxs-lookup"><span data-stu-id="4df64-159">**hello CSDL Specification**</span></span>

<span data-ttu-id="4df64-160">Plik CSDL jest opis gramatyki języka XML opisu usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="4df64-160">CSDL is XML grammar for describing a web service.</span></span> <span data-ttu-id="4df64-161">Specyfikacja Hello, sam jest podzielony na 4 główne elementy: EntitySet, FunctionImport; Przestrzeń nazw, a dla obiektu.</span><span class="sxs-lookup"><span data-stu-id="4df64-161">hello specification itself is divided into 4 major elements:  EntitySet, FunctionImport; NameSpace, and EntityType.</span></span>

<span data-ttu-id="4df64-162">toomake toounderstand ułatwia to Abstrakcja umożliwia powiązać tabelę tooa pliku CSDL.</span><span class="sxs-lookup"><span data-stu-id="4df64-162">toomake this abstraction easier toounderstand lets relate a CSDL tooa table.</span></span>

<span data-ttu-id="4df64-163">Pamiętaj;</span><span class="sxs-lookup"><span data-stu-id="4df64-163">Remember;</span></span>

  <span data-ttu-id="4df64-164">Kontrakt i język-niezależne od platformy między hello reprezentuje CSDL **obiektu żądającego usługi** i hello **usługodawcy**.</span><span class="sxs-lookup"><span data-stu-id="4df64-164">CSDL represents a platform- and language-independent contract between hello **service requestor** and hello **service provider**.</span></span> <span data-ttu-id="4df64-165">Przy użyciu pliku CSDL, **klienta** mogą zlokalizować **usługi bazy danych i usługi sieci web** i wywołać żadnego ze swoich publicznie dostępnych **funkcji.**</span><span class="sxs-lookup"><span data-stu-id="4df64-165">Using CSDL, a **client** can locate a **web service/database service** and invoke any of its publicly available **functions.**</span></span>

<span data-ttu-id="4df64-166">Dla hello Usługa danych czterech części pliku CSDL można traktować pod względem bazy danych, tabeli, kolumny i procedura składowana.</span><span class="sxs-lookup"><span data-stu-id="4df64-166">For a Data Service hello four parts of a CSDL can be thought of in terms of a Database, Table, Column, and Store Procedure.</span></span>

<span data-ttu-id="4df64-167">Następujący dla usługi danych dotyczących:</span><span class="sxs-lookup"><span data-stu-id="4df64-167">Relating these as follows for a Data Service:</span></span>

* <span data-ttu-id="4df64-168">Obiekt EntityContainer ~ = bazy danych</span><span class="sxs-lookup"><span data-stu-id="4df64-168">EntityContainer  ~=  Database</span></span>
* <span data-ttu-id="4df64-169">Obiekt EntitySet ~ = tabeli</span><span class="sxs-lookup"><span data-stu-id="4df64-169">EntitySet  ~=  Table</span></span>
* <span data-ttu-id="4df64-170">Obiekt EntityType ~ = kolumn</span><span class="sxs-lookup"><span data-stu-id="4df64-170">EntityType  ~= Columns</span></span>
* <span data-ttu-id="4df64-171">Element FunctionImport ~ = procedury składowanej</span><span class="sxs-lookup"><span data-stu-id="4df64-171">FunctionImport  ~=  Stored Procedure</span></span>

<span data-ttu-id="4df64-172">**Dozwolone zlecenia HTTP**</span><span class="sxs-lookup"><span data-stu-id="4df64-172">**HTTP Verbs allowed**</span></span>

* <span data-ttu-id="4df64-173">GET — zwraca wartości z bazy danych hello (zwraca kolekcję)</span><span class="sxs-lookup"><span data-stu-id="4df64-173">GET – returns values from hello db (returns a Collection)</span></span>
* <span data-ttu-id="4df64-174">POST — używane toopass danych tooand opcjonalne wartości zwracanych z hello bazy danych (Utwórz nowy wpis w kolekcji hello, zwracany identyfikator/URI)</span><span class="sxs-lookup"><span data-stu-id="4df64-174">POST – used toopass data tooand optional return values from hello db (Create a new entry in hello collection, return id/URI)</span></span>
* <span data-ttu-id="4df64-175">Usuń — Usuwa dane z hello bazy danych (spowoduje usunięcie kolekcji)</span><span class="sxs-lookup"><span data-stu-id="4df64-175">DELETE – Deletes data from hello DB (Deletes a collection)</span></span>
* <span data-ttu-id="4df64-176">PUT — aktualizacji danych w bazie danych (Zastąp kolekcji lub utwórz taki)</span><span class="sxs-lookup"><span data-stu-id="4df64-176">PUT – Update data into a DB (replace a collection or create one)</span></span>

## <a name="metadatamapping-document"></a><span data-ttu-id="4df64-177">Dokument metadanych/mapowania</span><span class="sxs-lookup"><span data-stu-id="4df64-177">Metadata/Mapping Document</span></span>
<span data-ttu-id="4df64-178">Dokument metadanych/mapowanie Hello jest używany toomap, który istniejącą witrynę sieci web dostawcy zawartości usług, dzięki czemu może być udostępniany jako usługi sieci web OData przez system Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="4df64-178">hello metadata/mapping document is used toomap a content provider’s existing web services so that it can be exposed as an OData web service by hello Azure Marketplace system.</span></span> <span data-ttu-id="4df64-179">Jest on oparty na pliku CSDL i implementuje kilka rozszerzeń tooCSDL tooaccommodate hello potrzeb REST na podstawie usług sieci web za pośrednictwem portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="4df64-179">It is based on CSDL and implements a few extensions tooCSDL tooaccommodate hello needs of REST based web services exposed through Azure Marketplace.</span></span> <span data-ttu-id="4df64-180">rozszerzenia Hello znajdują się w hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="4df64-180">hello extensions are found in hello [http://schemas.microsoft.com/dallas/2010/04](http://schemas.microsoft.com/dallas/2010/04) namespace.</span></span>

<span data-ttu-id="4df64-181">Przykład Witaj CSDL: (kopiowania i wklejania hello w poniższym przykładzie plik CSDL w edytorze XML i zmień toomatch usługi.</span><span class="sxs-lookup"><span data-stu-id="4df64-181">An example of hello CSDL follows:  (Copy and paste hello below example CSDL into an XML editor and change toomatch your Service.</span></span>  <span data-ttu-id="4df64-182">Wklej do mapowania pliku CSDL karcie DataService podczas tworzenia usługi na powitania [publikowania portalu Marketplace Azure](https://publish.windowsazure.com)).</span><span class="sxs-lookup"><span data-stu-id="4df64-182">Then paste into CSDL Mapping under DataService tab when creating your service in hello  [Azure Marketplace Publishing Portal](https://publish.windowsazure.com)).</span></span>

<span data-ttu-id="4df64-183">**Warunki:** toohello warunki dotyczące hello CSDL [Portal publikowania](https://publish.windowsazure.com) warunki interfejsu użytkownika (PPUI).</span><span class="sxs-lookup"><span data-stu-id="4df64-183">**Terms:** Relating hello CSDL terms toohello [Publishing Portal](https://publish.windowsazure.com) UI (PPUI) terms.</span></span>

* <span data-ttu-id="4df64-184">Oferują "Title" w hello PPUI odnosi się tooMyWebOffer</span><span class="sxs-lookup"><span data-stu-id="4df64-184">Offer “Title” in hello PPUI relates tooMyWebOffer</span></span>
* <span data-ttu-id="4df64-185">Moja firma w hello PPUI odnosi się zbyt**wydawcy, nazwa wyświetlana** w hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="4df64-185">MyCompany in hello PPUI relates too**Publisher Display Name** in hello [Microsoft Developer Center](http://dev.windows.com/registration?accountprogram=azure) UI</span></span>
* <span data-ttu-id="4df64-186">Interfejs API odnosi się tooa sieci Web lub usługi danych (Plan hello PPUI)</span><span class="sxs-lookup"><span data-stu-id="4df64-186">Your API relates tooa Web or Data Service (a Plan in hello PPUI)</span></span>

<span data-ttu-id="4df64-187">**Hierarchia:** oferty, która ma plany właścicielem firmy (dostawcy zawartości), czyli service(s), który wiersz w górę z interfejsem API.</span><span class="sxs-lookup"><span data-stu-id="4df64-187">**Hierarchy:** A Company (Content Provider) owns Offer(s) which have Plan(s), namely service(s), which line up with an API.</span></span>

### <a name="webservice-csdl-example"></a><span data-ttu-id="4df64-188">Przykład CSDL usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="4df64-188">WebService CSDL Example</span></span>
<span data-ttu-id="4df64-189">Łączy tooa usługi, która jest ujawniany przez punkt końcowy aplikacji sieci web (np. aplikacji C#)</span><span class="sxs-lookup"><span data-stu-id="4df64-189">Connects tooa service that is exposing an web application endpoint (like a C# application)</span></span>

        <?xml version="1.0" encoding="utf-8"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyWebOffer" Alias="MyOffer" xmlns="http://schemas.microsoft.com/ado/2009/08/edm" xmlns:d="http://schemas.microsoft.com/dallas/2010/04" >
        <!-- EntityContainer groups all hello web service calls together into a single offering. Every web service call has a FunctionImport definition. -->
          <EntityContainer Name="MyOffer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
        @Name is used as reference by FunctionImport @EntitySet. And is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition near hello bottom of this file. -->
            <EntitySet Name="MyEntities" EntityType="MyOffer.MyEntityType" />
        <!-- Add a FunctionImport for every service method. Multiple FunctionImports can share a single return type (EntityType). -->
        <!-- ReturnType is either Raw() for a stream or Collection() for an Atom feed. Ex. of Raw: ReturnType=”Raw(text/plain)” -->
        <!—EntitySet is hello entityset defined above, and is needed if ReturnType is not Raw -->
        <!-- BaseURI attribute defines hello service call, replace & with hello encode value (&amp;).
        In hello input name value pairs {param} represents passed in value.
        Or hello value can be hard coded as with AccountKey. -->
        <!-- AllowedHttpMethods optional (default = “GET”), allows hello CSDL toospecifically specify hello verb of hello service, “Get”, “Post”, “Put”, or “Delete”. -->
        <!-- EncodeParameterValues, True encodes hello parameter values, false does not. -->
        <!-- BaseURI is translated into an URITemplate which defines how hello web service call is exposed toomarketplace customers.
        Ex. https://api.datamarket.azure.com/mycompany/MyOfferPlan?name={name}
        BaseURI is XML encoded, hello {...} point toohello parameters defined below.
        Marketplace will read hello parameters from this URITemplate and fill hello values into hello corresponding parameters of hello BaseUri or RequestBody (below) during calls tooyour service.  
        It is okay for @d:BaseUri tooinclude information only for Marketplace consumption, it will not be exposed tooend users. i.e. hello hardcoded AccountKey in hello above BaseURI does not show up in hello client facing URITemplate. -->
            <FunctionImport Name="MyWebServiceMethod"
                            EntitySet="MyEntities"
                            ReturnType="Collection(MyOffer.MyEntityType)"
        d:AllowedHttpMethods="GET"
        d:EncodeParameterValues="true"
        d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <!-- Definition of hello RequestBody is only required for HTTP POST requests and is optional for HTTP GET requests. -->
        <d:RequestBody d:httpMethod="POST">
                <!-- Use {} for placeholders tooinsert parameters. -->
                <!-- This example uses SOAP formatting, but any POST body can be used. -->
            <!-- This example shows how toopass userid and password via hello header -->
                <![CDATA[<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:MyOffer="http://services.organization.net/MyServicePath">
                  <soapenv:Header/>
                  <soapenv:Body>
                    <MyOffer:ws_MyWebServiceMethod>
                      <myWebServiceMethodRequest>
                        <!--This information is not exposed tooend users. -->
                        <UserId>userid</UserId>
                        <Password>password</Password>
                        <!-- {name} is replaced with hello value read from @d:UriTemplate above -->
                        <Name>{name}</Name>
                        <!-- Parameters can be used more than once and are not limited tooappearing as hello value of an element -->
                        <CustomField Name="{name}" />
                        <MyField>Static content</MyField>
                      </myWebServiceMethodRequest>
                    </MyOffer:ws_MyWebServiceMethod>
                  </soapenv:Body>
                </soapenv:Envelope>      
              ]]>
        </d:RequestBody>
        <!-- Title, Rights and Description are optional and used toospecify values tooinsert into hello ATOM feed returned toohello end user.  You can specify hello element toocontain a fixed message by providing a value for hello element (this is hello default value).  @d:Map is an XPath expression that points into hello response returned by your service and is optional.  -->
        <d:Title d:Map="/MyResponse/Title">Default title.</d:Title>
        <d:Rights>© My copyright. This is a fixed response. It is okay tooalso add a d:Map attribute toooverride this text.</d:Rights>
        <d:Description d:Map="/MyResponse/Description"></d:Description>
        <d:Namespaces>
        <d:Namespace d:Prefix="p"  d:Uri="http://schemas.organization.net/2010/04/myNamespace" />
        <d:Namespace d:Prefix="p2" d:Uri="http://schemas.organization.net/2010/04/MyNamespace2" />
        </d:Namespaces>
        <!-- Parameters of hello web service call:
        @Name should match exactly (case sensitive) hello {…} placeholders in hello @d:BaseUri, @d:UriTemplate, and d:RequestBody, i.e. “name” parameter in above BaseURI.
        @Mode is always "In", compatibility with CSDL
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx
        @d:Nullable indicates whether hello parameter is required.
        @d:Regex - optional, attribute toodescribe hello string, limiting unwanted input at hello entry of hello system
        @d:Description - optional, is used by Service Explorer as help information
        @d:SampleValues - optional, is used by Service Explorer as help information. Multiple Sample values are separated by '|', e.g. "804735132|234534224|23409823234"
        @d:Enum - optional for string type. Contains an enumeration of possible values separated by a '|', e.g. d:enum="english|metric|raw". Will be converted in a dropdown list in hello Service Explorer.
        -->
        <Parameter name="name" Mode="In" Type="String" d:Nullable="false" d:Regex="^[a-zA-Z]*$" d:Description="A name that cannot contain any spaces or non-alpha non-English characters"
        d:Enum="George|John|Thomas|James"
        d:SampleValues="George"/>
        <Parameter Name=" AccountKey" Mode="In" Type="String" d:Nullable="false" />

        <!-- d:ErrorHandling is an optional element. Use it define standardized errors by evaluating hello service response. -->
        <d:ErrorHandling>
        <!-- Any number of d:Condition elements are allowed, they are evaluated in hello order listed.
        @d:Match is an Xpath query on hello service response, it should return true or false where true indicates an error.
        @d:httpStatusCode is hello error code tooreturn if an response matches hello error.
        @d:errorMessage is hello user friendly message tooreturn when an error occurs.
        -->
        <d:Condition d:Match="/Result/ErrorMessage[text()='Invalid token']" d:HttpStatusCode="403" d:ErrorMessage="User cannot connect toohello service." />
        </d:ErrorHandling>
           </FunctionImport>

            <!-- hello EntityContainer defines hello output data schema -->
        </EntityContainer>
        <!-- hello EntityType @d:Map defines hello repeating node (an XPath query) in hello response (output data schema). -->
        <!-- If these nodes are outside a namespace, add hello prefix in hello xpath. -->
        <!--
        @Name - define your user readable name, will become an XML element in hello ATOM feed, so comply with hello XML element naming restrictions (no spaces or other illegal characters).
        @Type is hello EDM.SimpleType of hello parameter, see http://msdn.microsoft.com/library/bb399548(v=VS.100).aspx.
        @d:Map uses an Xpath query toopoint at hello location tooextract hello content from your services response.
        hello "." is relative toohello repeating node in hello EntityType @d:Map Xpath expression.
        -->
            <EntityType Name="MyEntityType" d:Map="/MyResponse/MyEntities">
        <Property Name="ID"    d:IsPrimaryKey="True" Type="Int32"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="Amount"    Type="Double"    Nullable="false" d:Map="./Remaining[@Amount]"/>
        <Property Name="City"    Type="String"    Nullable="false" d:Map="./City"/>
        <Property Name="State"    Type="String"    Nullable="false" d:Map="./State"/>
        <Property Name="Zip"    Type="Int32"    Nullable="false" d:Map="./Zip"/>
        <Property Name="Updated"    Type="DateTime"    Nullable="false" d:Map="./Updated"/>
        <Property Name="AdditionalInfo" Type="String" Nullable="true"
        d:Map="./Info/More[1]"/>
            </EntityType>
        </Schema>

> [!TIP]
> <span data-ttu-id="4df64-190">Wyświetl więcej przykładów CSDL usługi sieci Web w artykule hello [przykłady mapowania istniejące sieci web tooOData usługi za pośrednictwem CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span><span class="sxs-lookup"><span data-stu-id="4df64-190">View more CSDL Web Service examples in hello article [Examples of mapping an existing web service tooOData through CSDLs](marketplace-publishing-data-service-creation-odata-mapping-examples.md)</span></span>
> 
> 

### <a name="dataservice-csdl-example"></a><span data-ttu-id="4df64-191">Przykład CSDL usługi danych</span><span class="sxs-lookup"><span data-stu-id="4df64-191">DataService CSDL Example</span></span>
<span data-ttu-id="4df64-192">Łączy tooa usługi, która jest ujawniany tabelę lub widok jako punkt końcowy w poniższym przykładzie przedstawiono dwa interfejsy API dla bazy danych na podstawie pliku CSDL interfejsu API (możesz użyć widoków zamiast tabel).</span><span class="sxs-lookup"><span data-stu-id="4df64-192">Connects tooa service that is exposing a database table or view as an endpoint Below example shows two APIs for Data base based API CSDL (can use views rather than tables).</span></span>

        <?xml version="1.0"?>
        <!-- hello namespace attribute below is used by our system toogenerate C#. You can change “MyCompany.MyOffer” toosomething that makes sense for you, but change “MyOffer” consistently throughout hello document. -->
        <Schema Namespace="MyCompany.MyDataOffer" Alias="MyOffer" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ado/2009/08/edm">
        <!-- EntityContainer groups all hello data service calls together into a single offering. Every web service call has a FunctionImport definition. -->
        <EntityContainer Name="MyOfferContainer">
        <!-- EntitySet is defined for CSDL compatibility reasons, not required for ReturnType=”Raw”
            Think of hello EntitySet as a Service
        @Name is used in hello customer facing UI as name of hello Service.
        @EntityType is used toopoint at hello type definition (returned set of table columns). -->
        <EntitySet Name="CompanyInfoEntitySet" EntityType="MyOffer.CompanyInfo" />
        <EntitySet Name="ProductInfoEntitySet" EntityType="MyOffer.ProductInfo" />
        </EntityContainer>
        <!-- EntityType defines result (output); hello table (or view) and columns toobe returned by hello data service.)
            Map is hello schema.tabel or schema.view
            dals.TableName is hello table Name
            Name is hello name identifier for hello EntityType and hello Name of hello service exposed toohello client via hello UI.
            dals:IsExposed determines if hello table schema is exposed (generally true).
            dals:IsView (optional) true if this is based on a view rather than a table
            dals:TableSchema is hello schema name of hello table/view
        -->
        <EntityType
        Map="[dbo].[CompanyInfo]"
        dals:TableName="CompanyInfo"
        Name="CompanyInfo"
        dals:IsExposed="true"
        dals:IsView="false"
        dals:TableSchema="dbo"
        xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <!-- Property defines hello column properties and hello output of hello service.
            dals:ColumnName is hello name of hello column in hello table /view.
            Type is hello emd.SimpleType
            Nullable determines if NULL is a valid output value
            dals.CharMaxLenght is hello maximum length of hello output value
            Name is hello name of hello Property and is exposed toohello client facing UI
            dals:IsReturned is hello Boolean that determines if hello Service exposes this value toohello client.
            IsQueryable is hello Boolean that determines if hello column can be used in a database query
            (For data Services: tooimprove Performance make sure that columns marked ISQueryable=”true” are in an index.)
            dals:OrdinalPosition is hello numerical position x in hello table or hello View, where x is from 1 toohello number of columns in hello table.
            dals:DatabaseDataType is hello data type of hello column in hello database, i.e. SQL data type dals:IsPrimaryKey indicates if hello column is hello Primary key in hello table/view.  (hello columns marked ISPrimaryKey are used in hello Order by clause when returning data.)
        -->
        <Property dals:ColumnName="data" Type="String" Nullable="true" dals:CharMaxLength="-1" Name="data" dals:IsReturned="true" dals:IsQueryable="false" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="ticker" Type="String" Nullable="true" dals:CharMaxLength="10" Name="ticker" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        <EntityType Map="[dbo].[ProductInfo]" dals:TableName="ProductInfo" Name="ProductInfo" dals:IsExposed="true" dals:IsView="false" dals:TableSchema="dbo" xmlns:dals="http://schemas.microsoft.com/dallas/2010/04">
        <Property dals:ColumnName="companyid" Type="Int32" Nullable="true" Name="companyid" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="2" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="id" Type="Int32" Nullable="false" Name="id" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="true" dals:OrdinalPosition="1" dals:NumericPrecision="10" dals:DatabaseDataType="int" />
        <Property dals:ColumnName="product" Type="String" Nullable="true" dals:CharMaxLength="50" Name="product" dals:IsReturned="true" dals:IsQueryable="true" dals:IsPrimaryKey="false" dals:OrdinalPosition="3" dals:DatabaseDataType="nvarchar" />
        </EntityType>
        </Schema>

## <a name="see-also"></a><span data-ttu-id="4df64-193">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4df64-193">See Also</span></span>
* <span data-ttu-id="4df64-194">Jeśli interesuje Cię learning oraz opis hello określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="4df64-194">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="4df64-195">Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee przykładowy kod i zrozumienie Składnia kodu i kontekstu.</span><span class="sxs-lookup"><span data-stu-id="4df64-195">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>
* <span data-ttu-id="4df64-196">toohello tooreturn określonej ścieżki do publikowania toohello danych usługi Azure Marketplace, przeczytaj ten artykuł [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="4df64-196">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

