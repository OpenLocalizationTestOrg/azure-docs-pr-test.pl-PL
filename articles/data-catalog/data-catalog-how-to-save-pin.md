---
title: "aaaSave wyszukiwania i zasobów danych numeru pin w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Jak tooarticle wyróżnienia możliwości w wykazie danych Azure zapisywania źródła danych i zasobów danych do późniejszego użycia."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a><span data-ttu-id="500f8-103">Zapisz wyszukiwanie i zasobów danych numeru pin w wykazie danych Azure</span><span class="sxs-lookup"><span data-stu-id="500f8-103">Save searches and pin data assets in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="500f8-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="500f8-104">Introduction</span></span>
<span data-ttu-id="500f8-105">Azure Data Catalog oferuje możliwości dla odnajdywanie źródła danych.</span><span class="sxs-lookup"><span data-stu-id="500f8-105">Azure Data Catalog provides capabilities for data source discovery.</span></span> <span data-ttu-id="500f8-106">Można szybko wyszukiwania i filtrowania źródeł danych toolocate katalogu hello i zrozumieć ich przeznaczenie, dzięki czemu łatwiej toofind hello odpowiednich danych dla wykonywanego zadania hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-106">You can quickly search and filter hello catalog toolocate data sources and understand their intended purpose, making it easier toofind hello right data for hello job at hand.</span></span>

<span data-ttu-id="500f8-107">Ale co zrobić, jeśli należy tooregularly pracować z hello same dane?</span><span class="sxs-lookup"><span data-stu-id="500f8-107">But what if you need tooregularly work with hello same data?</span></span> <span data-ttu-id="500f8-108">I co zrobić, jeśli użytkownicy będą mieli regularnie współtworzenia toohello Twojej wiedzy tych samych źródeł danych w katalogu hello?</span><span class="sxs-lookup"><span data-stu-id="500f8-108">And what if you and other users regularly contribute your knowledge toohello same data sources in hello catalog?</span></span> <span data-ttu-id="500f8-109">W takich przypadkach o problem toorepeatedly hello same wyszukiwania może być mało wydajne.</span><span class="sxs-lookup"><span data-stu-id="500f8-109">In these situations, having toorepeatedly issue hello same searches can be inefficient.</span></span> <span data-ttu-id="500f8-110">Jest to, gdzie zapisanego wyszukiwania i zasobów danych przypięte może pomóc.</span><span class="sxs-lookup"><span data-stu-id="500f8-110">This is where saved search and pinned data assets can help.</span></span>

## <a name="saved-searches"></a><span data-ttu-id="500f8-111">Zapisane wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="500f8-111">Saved searches</span></span>
<span data-ttu-id="500f8-112">Zapisane wyszukiwanie w wykazie danych jest wielokrotnego użytku, definicji wyszukiwania dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="500f8-112">A saved search in Data Catalog is a reusable, per-user search definition.</span></span> <span data-ttu-id="500f8-113">Można zdefiniować wyszukiwania, w tym terminy wyszukiwania, znaczników i inne filtry i zapisz go.</span><span class="sxs-lookup"><span data-stu-id="500f8-113">You can define a search, including search terms, tags, and other filters, and then save it.</span></span> <span data-ttu-id="500f8-114">Można ponownie uruchomić hello zapisane wyszukiwania definicji tooreturn nowsze żadnych zasobów danych, które pasują do jej kryteriów wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-114">You can re-run hello saved search definition later tooreturn any data assets that match its search criteria.</span></span>

### <a name="create-a-saved-search"></a><span data-ttu-id="500f8-115">Utwórz zapisanego wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="500f8-115">Create a saved search</span></span>
<span data-ttu-id="500f8-116">zapisane wyszukiwanie toocreate hello następujące:</span><span class="sxs-lookup"><span data-stu-id="500f8-116">toocreate a saved search, do hello following:</span></span>
1. <span data-ttu-id="500f8-117">W portalu Azure Data Catalog hello w hello **bieżące wyszukiwanie** okna, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="500f8-117">In hello Azure Data Catalog portal, in hello **Current Search** window, click **Save**.</span></span> 

    ![Bieżące łącze Zapisz ustawienia wyszukiwania](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. <span data-ttu-id="500f8-119">Wprowadź kryteria wyszukiwania hello mają tooreuse, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="500f8-119">Enter hello search criteria that you want tooreuse, and then click **Save**.</span></span>

    ![Nazwa wyszukiwania zapisać bieżące ustawienia wyszukiwania](./media/data-catalog-how-to-save-pin/02-name.png)

3. <span data-ttu-id="500f8-121">Po wyświetleniu monitu wprowadź nazwę dla zapisanego wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-121">When you are prompted, enter a name for hello saved search.</span></span> <span data-ttu-id="500f8-122">Wybierz nazwę opisową i opisujący hello zasobów danych, które zostaną zwrócone przez wyszukiwanie hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-122">Pick a name that is meaningful and that describes hello data assets that will be returned by hello search.</span></span>

### <a name="manage-saved-searches"></a><span data-ttu-id="500f8-123">Zarządzanie zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="500f8-123">Manage saved searches</span></span>
<span data-ttu-id="500f8-124">Po zapisaniu jednego lub więcej wyszukiwań **zapisane wyszukiwania** opcja jest wyświetlana poniżej hello **bieżące wyszukiwanie** pole.</span><span class="sxs-lookup"><span data-stu-id="500f8-124">After you have saved one or more searches, a **Saved Searches** option is displayed beneath hello **Current Search** box.</span></span> <span data-ttu-id="500f8-125">Po rozwinięciu listy hello są wyświetlane wszystkie zapisane wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-125">When hello list is expanded, all saved searches are displayed.</span></span>

 ![Lista zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/03-list.png)

<span data-ttu-id="500f8-127">Wykonaj jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="500f8-127">Do any of hello following:</span></span>

* <span data-ttu-id="500f8-128">tooexecute wyszukiwanie, wybierz listy hello zapisanego kryterium wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-128">tooexecute a search, select a saved search in hello list.</span></span>

* <span data-ttu-id="500f8-129">tooview listę opcje zarządzania dla zapisanego kryterium wyszukiwania, kliknij przycisk hello dół strzałkę dalej toohello alias.</span><span class="sxs-lookup"><span data-stu-id="500f8-129">tooview a list of management options for a saved search, click hello down arrow next toohello search name.</span></span>

    ![Opcje zarządzania zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/04-managing.png)

* <span data-ttu-id="500f8-131">Wybierz nową nazwę dla hello zapisane wyszukiwania, tooenter **zmienić**.</span><span class="sxs-lookup"><span data-stu-id="500f8-131">tooenter a new name for hello saved search, select **Rename**.</span></span> <span data-ttu-id="500f8-132">Definicja wyszukiwania Hello nie ulega zmianie.</span><span class="sxs-lookup"><span data-stu-id="500f8-132">hello search definition is not changed.</span></span>

* <span data-ttu-id="500f8-133">tooremove hello zapisane wyszukiwania z listy, wybierz opcję **usunąć**, a następnie Potwierdź usunięcie hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-133">tooremove hello saved search from your list, select **Delete**, and then confirm hello deletion.</span></span>

* <span data-ttu-id="500f8-134">toomark hello zapisane wyszukiwanie jako wyszukiwania domyślne, wybierz opcję **Zapisz jako domyślne**.</span><span class="sxs-lookup"><span data-stu-id="500f8-134">toomark hello saved search as your default search, select **Save As Default**.</span></span> <span data-ttu-id="500f8-135">Jeśli wyszukiwaniu "pusty" ze strony głównej hello Azure Data Catalog, wyszukiwanie domyślny jest wykonywana.</span><span class="sxs-lookup"><span data-stu-id="500f8-135">If you perform an “empty” search from hello Azure Data Catalog home page, your default search is executed.</span></span> <span data-ttu-id="500f8-136">Ponadto hello wyszukiwania, który jest oznaczony jako hello domyślne wyszukiwanie jest wyświetlany u góry hello hello **zapisane wyszukiwania** listy.</span><span class="sxs-lookup"><span data-stu-id="500f8-136">In addition, hello search that's marked as hello default search is displayed at hello top of hello **Saved Searches** list.</span></span>

### <a name="organizational-saved-searches"></a><span data-ttu-id="500f8-137">Organizacyjnej zapisanych wyszukiwań</span><span class="sxs-lookup"><span data-stu-id="500f8-137">Organizational saved searches</span></span>
<span data-ttu-id="500f8-138">Wszystkich użytkowników w organizacji można zapisać wyszukiwanie na własny użytek.</span><span class="sxs-lookup"><span data-stu-id="500f8-138">All user in your organization can save searches for their own use.</span></span> <span data-ttu-id="500f8-139">Administratorzy katalogu danych można także zapisać wyszukiwanie wszystkich użytkowników w organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-139">Data Catalog administrators can also save searches for all users within hello organization.</span></span> <span data-ttu-id="500f8-140">Gdy Administratorzy, Zapisz wyszukiwanie, są one dostępne z **udziału w firmie hello** opcji.</span><span class="sxs-lookup"><span data-stu-id="500f8-140">When administrators save a search, they're presented with a **Share within hello company** option.</span></span> <span data-ttu-id="500f8-141">Wybranie tego hello udziałów opcja zapisanego wyszukiwania dla wszystkich użytkowników w organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-141">Selecting this option shares hello saved search for all users in hello organization.</span></span>

 ![Organizacyjnej zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a><span data-ttu-id="500f8-143">Zasoby danych przypięte</span><span class="sxs-lookup"><span data-stu-id="500f8-143">Pinned data assets</span></span>
<span data-ttu-id="500f8-144">Z zapisane wyszukiwania można zapisać i ponownie użyć definicji wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-144">With saved searches, you can save and reuse search definitions.</span></span> <span data-ttu-id="500f8-145">Hello zasobów danych, które są zwracane przez hello wyszukiwania może zmieniać się w czasie, gdy zawartość hello hello zmiany katalogu.</span><span class="sxs-lookup"><span data-stu-id="500f8-145">hello data assets that are returned by hello searches might change over time as hello contents of hello catalog change.</span></span> <span data-ttu-id="500f8-146">Po przypięciu zasobów danych, można zidentyfikować jawnie toomake zasoby danych specyficznych dla ich łatwiejsze tooaccess bez konieczności toouse wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-146">When you pin data assets, you can explicitly identify specific data assets toomake them easier tooaccess without needing toouse a search.</span></span>

<span data-ttu-id="500f8-147">Przypinanie zasobu danych jest prosta.</span><span class="sxs-lookup"><span data-stu-id="500f8-147">Pinning a data asset is straightforward.</span></span> <span data-ttu-id="500f8-148">Lista tooyour przypięty tooadd hello danych zasobów, należy po prostu kliknij hello **numeru pin** ikony.</span><span class="sxs-lookup"><span data-stu-id="500f8-148">tooadd hello data asset tooyour pinned list, you simply click hello **pin** icon.</span></span> <span data-ttu-id="500f8-149">Witaj ikona jest wyświetlana w hello rogu hello zasobów kafelka w widoku tile hello i hello lewej kolumny w widoku listy hello w portalu Azure Data Catalog hello.</span><span class="sxs-lookup"><span data-stu-id="500f8-149">hello icon is displayed in hello corner of hello asset tile in hello tile view, and in hello left-most column in hello list view in hello Azure Data Catalog portal.</span></span>

![ikonę pinezki Hello zasobów danych](./media/data-catalog-how-to-save-pin/05-pinning.png)

<span data-ttu-id="500f8-151">Cofnięcie unieruchomienia zasobu danych jest równie proste.</span><span class="sxs-lookup"><span data-stu-id="500f8-151">Unpinning a data asset is equally straightforward.</span></span> <span data-ttu-id="500f8-152">Po prostu kliknij hello **odpiąć** ikona tootoggle hello ustawienie hello wybranych zasobów.</span><span class="sxs-lookup"><span data-stu-id="500f8-152">Simply click hello **unpin** icon tootoggle hello setting for hello selected asset.</span></span>

![Ikona odpiąć zasobu danych Hello](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a><span data-ttu-id="500f8-154">Witaj sekcji Moje zasoby</span><span class="sxs-lookup"><span data-stu-id="500f8-154">hello My Assets section</span></span>
<span data-ttu-id="500f8-155">Witaj Data Catalog zawiera strony głównej portalu **Moje zasoby** sekcja, która zawiera zasoby odsetek toohello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="500f8-155">hello Data Catalog portal home page includes a **My Assets** section that displays assets of interest toohello current user.</span></span> <span data-ttu-id="500f8-156">Ta sekcja zawiera oba zasoby przypięty i zapisane wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="500f8-156">This section includes both pinned assets and saved searches.</span></span>

![Witaj sekcji Moje zasoby na stronie głównej hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a><span data-ttu-id="500f8-158">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="500f8-158">Summary</span></span>
<span data-ttu-id="500f8-159">Wykaz danych Azure zapewnia możliwości stał się łatwiejsze toodiscover hello źródeł danych, które chcesz dodać, innych członków organizacji może poświęcać mniej czasu wyszukiwania danych i więcej czasu korzystania z niego.</span><span class="sxs-lookup"><span data-stu-id="500f8-159">Azure Data Catalog provides capabilities that make it easier toodiscover hello data sources you need, so you and other organization members can spend less time looking for data and more time working with it.</span></span> <span data-ttu-id="500f8-160">Zapisane wyszukiwania i przypięty dane, które zasoby kompilacji na tych podstawowych możliwości, aby użytkownicy mogą łatwo zidentyfikować źródeł danych, które działają w systemie wielokrotnie.</span><span class="sxs-lookup"><span data-stu-id="500f8-160">Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources that they work with repeatedly.</span></span>
