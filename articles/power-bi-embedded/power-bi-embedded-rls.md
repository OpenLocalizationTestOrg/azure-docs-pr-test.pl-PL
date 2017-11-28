---
title: zabezpieczenia na poziomie aaaRow z Power BI Embedded
description: "Szczegółowe informacje dotyczące zabezpieczeń na poziomie wiersza z Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="0fb8b-103">Zabezpieczenia na poziomie wierszy w usłudze Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0fb8b-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="0fb8b-104">Zabezpieczeń na poziomie wiersza (kontrola dostępu) może być danych tooparticular dostępu użytkownika toorestrict używanych w obrębie raportu lub zestawu danych, co pozwala na wielu różnych użytkowników toouse hello jednym raporcie podczas oglądanie wszystkie inne dane.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="0fb8b-105">Usługa Power BI Embedded obsługuje teraz skonfigurowane odświeżania zestawów danych.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="0fb8b-106">W kolejności tootake zaletą zabezpieczenia na poziomie wiersza jest ważne, że rozumiesz trzy główne pojęcia; Użytkownicy, role i zasady.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="0fb8b-107">Spójrzmy bliższe spojrzenie na każdym:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="0fb8b-108">**Użytkownicy** — te są użytkownicy końcowi rzeczywiste hello wyświetlania raportów.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="0fb8b-109">W usłudze Power BI Embedded użytkownicy są identyfikowani na podstawie hello właściwości nazwy użytkownika w tokenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="0fb8b-110">**Role** — użytkownicy należą tooroles.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="0fb8b-111">Rola to kontener dla reguły i może być nazwana "Menedżer sprzedaży" lub "Przedstawiciel".</span><span class="sxs-lookup"><span data-stu-id="0fb8b-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="0fb8b-112">W usłudze Power BI Embedded użytkownicy są identyfikowani przez właściwość role hello w tokenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="0fb8b-113">**Reguły** — role mają zasady, a zasady te są hello rzeczywiste filtry, które będą stosowane toobe toohello danych.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="0fb8b-114">Może to być tak proste, jak "kraju = USA" lub coś bardziej dynamiczne.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="0fb8b-115">Przykład</span><span class="sxs-lookup"><span data-stu-id="0fb8b-115">Example</span></span>

<span data-ttu-id="0fb8b-116">Witaj pozostałej części tego artykułu udostępnimy przykładem tworzenia zabezpieczenia na poziomie wiersza i wykorzystywanie który w osadzonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="0fb8b-117">Przedstawiony przykład używa hello [Retail Analysis próbki](http://go.microsoft.com/fwlink/?LinkID=780547) plików PBIX.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="0fb8b-118">Naszej próbki Retail Analysis przedstawia sprzedaż dla wszystkich magazynów hello w łańcuchu określonego sprzedaży detalicznej.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="0fb8b-119">Bez zabezpieczenia na poziomie wiersza niezależnie od tego, które regionalnego Menedżera loguje i widoków hello raport, będzie zobaczy hello tych samych danych.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="0fb8b-120">Kierownictwo wykrył, że Menedżer każdy region powinien zobaczyć tylko sprzedaży hello hello magazynów, którymi zarządzają i toodo to, możemy użyć zabezpieczenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="0fb8b-121">Kontrola dostępu jest tworzone w programie Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="0fb8b-122">Po otwarciu hello zestawu danych i raportów, możemy przełącznika toodiagram widoku toosee hello schematu:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="0fb8b-123">Oto kilka rzeczy toonotice tego schematu:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="0fb8b-124">Wszystkie miary, takich jak **Total Sales**, są przechowywane w hello **sprzedaży** tabeli faktów.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="0fb8b-125">Istnieją cztery tabele wymiarów powiązane dodatkowe: **elementu**, **czasu**, **magazynu**, i **regionalnego**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="0fb8b-126">strzałki Hello wierszach relacji hello wskazują jaki sposób filtry mogą przepływać z tooanother jedna tabela.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="0fb8b-127">Na przykład, jeśli filtr jest umieszczona na **czasu [Date]**, w bieżącym schemacie hello go tylko filtruje wartości w hello **sprzedaży** tabeli.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="0fb8b-128">Nie inne tabele może niekorzystnie wpływać filtru wszystkie strzałki hello na powitania relacji wierszy toohello punktu sprzedaży tabeli i nie optymalizacji.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="0fb8b-129">Witaj **regionalnego** tabela wskazuje będącego dla każdego regionalnego Menedżera hello:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="0fb8b-130">Na podstawie tego schematu, jeśli Trwa stosowanie toohello filtru **Menedżera regionalnego** kolumny w hello regionalnego tabeli, a jeśli z filtrem zgodne użytkownika hello wyświetlanie raportu hello, że filtr zostanie również filtrować dół hello **magazynu**i **sprzedaży** tooonly tabel Pokaż dane dla tego konkretnego regionalnego menedżera.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="0fb8b-131">Oto jak:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-131">Here’s how:</span></span>

1. <span data-ttu-id="0fb8b-132">Na karcie modelowania powitania kliknij **Zarządzanie rolami**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="0fb8b-133">Utwórz nową rolę o nazwie **Menedżera**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="0fb8b-134">W hello **regionalnego** tabeli wprowadź następujące wyrażenie DAX hello: **[regionalnego Manager] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="0fb8b-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="0fb8b-135">toomake się, że reguły hello pracuje na powitania **modelowania** , kliknij pozycję **widoku w postaci ról**, a następnie wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="0fb8b-136">Witaj raporty będą teraz wyświetlane dane tak, jakby użytkownik był zalogowany jako **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="0fb8b-137">Stosowanie filtru hello, w tym miejscu opisano sposób hello spowoduje odfiltrowanie dół wszystkie rekordy z hello **regionalnego**, **magazynu**, i **sprzedaży** tabel.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="0fb8b-138">Jednak ze względu na kierunek filtru hello na powitania relacje między **sprzedaży** i **czasu**, **sprzedaży** i **elementu**i **Elementu** i **czasu** tabele nie będą filtrowane w dół.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="0fb8b-139">Może to być ok tego wymagania, jednak nie chcemy, menedżerów toosee elementy, dla których nie ma żadnej sprzedaży, firma Microsoft może włączyć dwukierunkowego filtrowania krzyżowego hello relacja i przepływu hello filtru zabezpieczeń w obu kierunkach.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="0fb8b-140">Można to zrobić, edytując hello relacji między **sprzedaży** i **elementu**, podobnie do następującej:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="0fb8b-141">Teraz, filtry również mogą przepływać z hello sprzedaży tabeli toohello **elementu** tabeli:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="0fb8b-142">Jeśli używasz trybu zapytania bezpośredniego dla danych, konieczne będzie tooenable dwukierunkowego między filtrowania zaznaczając te dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="0fb8b-143">**Plik** -> **opcji i ustawień** -> **funkcje w wersji zapoznawczej** -> **Włącz filtrowanie krzyżowe w obu kierunkach dla zapytania bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="0fb8b-144">**Plik** -> **opcji i ustawień** -> **DirectQuery** -> **Zezwalaj na nieograniczoną miar w trybie zapytania bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="0fb8b-145">więcej informacji na temat dwukierunkowego filtrowania krzyżowego, pobierania hello toolearn [dwukierunkowego filtrowania krzyżowego w SQL Server Analysis Services 2016 i Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) oficjalny dokument.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="0fb8b-146">To opakowuje pracy hello wszystkich wymagające toobe zrobić w programie Power BI Desktop, ale ma jednego więcej element pracy musi wykonać toobe toomake zasady hello zabezpieczenia na poziomie wiersza zdefiniowanego w usłudze Power BI Embedded pracy.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="0fb8b-147">Użytkownicy uwierzytelniania i autoryzacji przez aplikację i tokenów aplikacji są używane toogrant tego użytkownika dostępu tooa określonego Power BI Embedded raportu.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="0fb8b-148">Usługa Power BI Embedded nie ma żadnych określone informacje, na który jest użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="0fb8b-149">Toowork zabezpieczenia na poziomie wiersza wymagany będzie toopass niektórych dodatkowy kontekst jako część token aplikacji:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="0fb8b-150">**Nazwa użytkownika** (opcjonalnie) — używane zabezpieczenia na poziomie wiersza jest ciągiem, który może służyć toohelp identyfikowania hello użytkownika, stosując zasady zabezpieczenia na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="0fb8b-151">Zobacz wiersz zabezpieczeń na poziomie przy użyciu usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0fb8b-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="0fb8b-152">**role** — ciąg zawierający tooselect ról hello podczas stosowania zasad zabezpieczeń na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="0fb8b-153">Jeśli przekazywanie więcej niż jednej roli, powinien zostać przekazany jako tablicy ciągów.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="0fb8b-154">Utwórz hello token przy użyciu hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) metody.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="0fb8b-155">Jeśli właściwość username hello jest obecny, należy także podać co najmniej jedną wartość w rolach.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="0fb8b-156">Na przykład można zmienić hello EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="0fb8b-157">Wiersz DashboardController 55 może być aktualizowane z</span><span class="sxs-lookup"><span data-stu-id="0fb8b-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="0fb8b-158">na</span><span class="sxs-lookup"><span data-stu-id="0fb8b-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="0fb8b-159">token pełnej aplikacji Hello będzie wyglądać mniej więcej tak:</span><span class="sxs-lookup"><span data-stu-id="0fb8b-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="0fb8b-160">Teraz z wszystkich elementów hello razem, podczas logowania użytkownika do naszej aplikacji tooview tego raportu, aby tylko były stanie toosee hello danych, że mogą one toosee, zgodnie z definicją w naszym zabezpieczeń na poziomie wiersza.</span><span class="sxs-lookup"><span data-stu-id="0fb8b-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="0fb8b-161">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="0fb8b-161">See also</span></span>

[<span data-ttu-id="0fb8b-162">Zabezpieczenia na poziomie wiersza (kontrola dostępu) z zasilania</span><span class="sxs-lookup"><span data-stu-id="0fb8b-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="0fb8b-163">Uwierzytelnianie i autoryzowanie za pomocą usługi Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0fb8b-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="0fb8b-164">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0fb8b-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="0fb8b-165">Przykład osadzania skryptu JavaScript</span><span class="sxs-lookup"><span data-stu-id="0fb8b-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="0fb8b-166">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="0fb8b-166">More questions?</span></span> [<span data-ttu-id="0fb8b-167">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="0fb8b-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

