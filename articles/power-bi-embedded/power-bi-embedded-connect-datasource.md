---
title: "Power BI Embedded — połączenia źródła danych tooa aaaMicrosoft"
description: "Power BI Embedded, Połącz toodata źródeł"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="35c89-103">Łączenie ze źródłem danych tooa</span><span class="sxs-lookup"><span data-stu-id="35c89-103">Connect tooa data source</span></span>
<span data-ttu-id="35c89-104">Z **Power BI Embedded**, raporty można osadzić w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35c89-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="35c89-105">Po osadzeniu raportu usługi Power BI w swojej aplikacji hello raport łączy toohello bazowy danych przez **importowania** kopii danych hello lub przez **połączenie bezpośrednio** toohello źródła danych przy użyciu  **Zapytania bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="35c89-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="35c89-106">Poniżej przedstawiono różnice hello przy użyciu **importu** i **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="35c89-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="35c89-107">Import</span><span class="sxs-lookup"><span data-stu-id="35c89-107">Import</span></span> | <span data-ttu-id="35c89-108">Tryb DirectQuery</span><span class="sxs-lookup"><span data-stu-id="35c89-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="35c89-109">Tabele, kolumny, *i dane* są importowane lub kopiowane do raportu hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="35c89-110">toosee zmiany danych podstawowych toohello wystąpił, należy odświeżyć lub zaimportować pełny bieżący zestaw danych ponownie.</span><span class="sxs-lookup"><span data-stu-id="35c89-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="35c89-111">Tylko *tabel i kolumn* są importowane lub kopiowane do raportu hello zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="35c89-112">Zawsze Przeglądaj hello najbardziej aktualne dane.</span><span class="sxs-lookup"><span data-stu-id="35c89-112">You always view hello most current data.</span></span> |

<span data-ttu-id="35c89-113">Z Power BI Embedded możesz za pomocą zapytania bezpośredniego źródeł danych w chmurze, ale nie lokalnych źródeł danych w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="35c89-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="35c89-114">Hello bramy danych lokalnych jest nieobsługiwane w przypadku używania Power BI Embedded w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="35c89-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="35c89-115">Oznacza to, że nie można użyć zapytania bezpośredniego z lokalnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="35c89-116">Obsługiwane źródła danych</span><span class="sxs-lookup"><span data-stu-id="35c89-116">Supported data sources</span></span>

<span data-ttu-id="35c89-117">**Zapytania bezpośredniego**</span><span class="sxs-lookup"><span data-stu-id="35c89-117">**DirectQuery**</span></span>
* <span data-ttu-id="35c89-118">Baza danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="35c89-118">Azure SQL database</span></span>
* <span data-ttu-id="35c89-119">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="35c89-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="35c89-120">**Importowanie**</span><span class="sxs-lookup"><span data-stu-id="35c89-120">**Import**</span></span>

<span data-ttu-id="35c89-121">Możesz zaimportować przy użyciu wszystkich hello dostępnych źródeł danych w ramach Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="35c89-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="35c89-122">Będzie **nie** być stanie toorefresh danych w usłudze Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="35c89-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="35c89-123">Konieczne będzie tooupload zmiany tooPower BI Embedded plików tooyour PBIX.</span><span class="sxs-lookup"><span data-stu-id="35c89-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="35c89-124">Jest to powodu toono dostępnej bramy.</span><span class="sxs-lookup"><span data-stu-id="35c89-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="35c89-125">Zalety używania zapytania bezpośredniego</span><span class="sxs-lookup"><span data-stu-id="35c89-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="35c89-126">Istnieją dwie podstawowe zalety, korzystając z **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="35c89-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="35c89-127">**Zapytania bezpośredniego** umożliwia kompilacja z wizualizacji w bardzo dużych zestawów danych, gdzie w przeciwnym razie byłoby importu toofirst będzie niemożliwe, na wszystkich hello danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="35c89-128">Bazowy zmian danych może wymagać odświeżenia danych, a w przypadku niektórych raportów hello muszą toodisplay bieżące dane mogą wymagać dużych transferów danych, co będzie niemożliwe ponownego importowania danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="35c89-129">Z kolei **DirectQuery** raporty zawsze używać bieżących danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="35c89-130">Ograniczenia DirectQuery</span><span class="sxs-lookup"><span data-stu-id="35c89-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="35c89-131">Istnieje kilka ograniczeń toousing **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="35c89-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="35c89-132">Wszystkie tabele muszą pochodzić z jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="35c89-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="35c89-133">Jeśli zapytanie hello jest zbyt skomplikowane, zostanie przeprowadzona wystąpił błąd.</span><span class="sxs-lookup"><span data-stu-id="35c89-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="35c89-134">Błąd hello tooremedy musi Refaktoryzuj hello zapytania, jest mniej złożona.</span><span class="sxs-lookup"><span data-stu-id="35c89-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="35c89-135">Jeśli zapytanie hello musi być złożony, konieczne będzie tooimport hello danych zamiast **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="35c89-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="35c89-136">Filtrowanie relacji jest ograniczona tooa w jednym kierunku, a nie w obu kierunkach.</span><span class="sxs-lookup"><span data-stu-id="35c89-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="35c89-137">Nie można zmienić hello typu danych kolumny.</span><span class="sxs-lookup"><span data-stu-id="35c89-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="35c89-138">Domyślnie ograniczenia są umieszczane na dozwolone w miarach wyrażenia języka DAX.</span><span class="sxs-lookup"><span data-stu-id="35c89-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="35c89-139">Zobacz [zapytania bezpośredniego i środków](#measures).</span><span class="sxs-lookup"><span data-stu-id="35c89-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="35c89-140">Zapytania bezpośredniego i miary</span><span class="sxs-lookup"><span data-stu-id="35c89-140">DirectQuery and measures</span></span>
<span data-ttu-id="35c89-141">zapytania tooensure wysyłane toohello źródła danych ma akceptowalną wydajność, ograniczenia nakłada się na miary.</span><span class="sxs-lookup"><span data-stu-id="35c89-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="35c89-142">Korzystając z **Power BI Desktop**zaawansowanego użytkownicy mogą wybrać toobypass to ograniczenie, wybierając **Plik > Opcje i Ustawienia > Opcje**.</span><span class="sxs-lookup"><span data-stu-id="35c89-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="35c89-143">W hello **opcje** okno dialogowe, wybierz **DirectQuery**i wybierz opcję hello **Zezwalaj na nieograniczoną środki w trybie zapytania bezpośredniego**.</span><span class="sxs-lookup"><span data-stu-id="35c89-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="35c89-144">Gdy ta opcja jest wybrana, można dowolne wyrażenie języka DAX, który jest prawidłowy dla miary.</span><span class="sxs-lookup"><span data-stu-id="35c89-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="35c89-145">Użytkownicy muszą być świadome; jednak, że niektóre wyrażenia które wykonują bardzo dobrze podczas importowania danych hello może spowodować zacznie działać bardzo wolno zapytania toohello wewnętrznej bazy danych w czasie źródła **DirectQuery** tryb.</span><span class="sxs-lookup"><span data-stu-id="35c89-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="35c89-146">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="35c89-146">See Also</span></span>
* [<span data-ttu-id="35c89-147">Wprowadzenie do programu Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="35c89-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="35c89-148">Program Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="35c89-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="35c89-149">Masz więcej pytań?</span><span class="sxs-lookup"><span data-stu-id="35c89-149">More questions?</span></span> [<span data-ttu-id="35c89-150">Spróbuj hello Power BI społeczności</span><span class="sxs-lookup"><span data-stu-id="35c89-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

