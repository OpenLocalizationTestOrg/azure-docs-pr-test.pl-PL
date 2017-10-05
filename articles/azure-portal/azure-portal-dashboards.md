---
title: "Tworzyć i udostępniać pulpity nawigacyjne portalu Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tworzyć i edytować pulpitów nawigacyjnych w portalu Azure."
services: azure-portal
documentationcenter: 
author: sewatson
manager: timlt
editor: tysonn
ms.assetid: ff422f36-47d2-409b-8a19-02e24b03ffe7
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 09/06/2016
ms.author: sewatson
ms.openlocfilehash: 5429e68723448ff5db6ef0ed8da1b927e97e6dd9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-share-dashboards-in-the-azure-portal"></a><span data-ttu-id="c31da-103">Tworzenie i udostępnianie pulpitów nawigacyjnych w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c31da-103">Create and share dashboards in the Azure portal</span></span>
<span data-ttu-id="c31da-104">Można tworzyć wiele pulpitów nawigacyjnych i udostępniać je innym użytkownikom, którzy mają dostęp do Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c31da-104">You can create multiple dashboards and share them with others who have access to your Azure subscriptions.</span></span>  <span data-ttu-id="c31da-105">W tym artykule przechodzi przez podstawy tworzenia, edytowania, publikowanie i zarządzanie dostępem do pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c31da-105">This article goes through the basics of creating, editing, publishing, and managing access to dashboards.</span></span>

## <a name="create-a-dashboard"></a><span data-ttu-id="c31da-106">Utwórz pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="c31da-106">Create a dashboard</span></span>
<span data-ttu-id="c31da-107">Aby utworzyć pulpit nawigacyjny, wybierz **nowego pulpitu nawigacyjnego** przycisk Dalej, aby nazwa bieżącego pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31da-107">To create a dashboard, select the **New dashboard** button next to the current dashboard's name.</span></span>  

![Utwórz pulpit nawigacyjny](./media/azure-portal-dashboards/new-dashboard.png)

<span data-ttu-id="c31da-109">Ta akcja tworzy nowy, pusty, prywatne pulpitu nawigacyjnego i umieszcza Tryb dostosowywania, w którym można nazwa pulpitu nawigacyjnego i dodać lub zmienić Kafelki.</span><span class="sxs-lookup"><span data-stu-id="c31da-109">This action creates a new, empty, private dashboard and puts you into customization mode where you can name your dashboard and add or rearrange tiles.</span></span>  <span data-ttu-id="c31da-110">W tym trybie galerii zwijanej kafelka przejmuje menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="c31da-110">When in this mode, the collapsible tile gallery takes over the left navigation menu.</span></span>  <span data-ttu-id="c31da-111">Galeria kafelka pozwala znaleźć kafelków dla zasobów platformy Azure na różne sposoby: można przeglądać [grupy zasobów](../azure-resource-manager/resource-group-overview.md#resource-groups), przez przez typ zasobu [tag](../azure-resource-manager/resource-group-using-tags.md), lub przez wyszukiwanie według nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="c31da-111">The tile gallery lets you find tiles for your Azure resources in various ways: you can browse by [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups), by resource type, by [tag](../azure-resource-manager/resource-group-using-tags.md), or by searching for your resource by name.</span></span>  

![Dostosowanie pulpitu nawigacyjnego](./media/azure-portal-dashboards/customize-dashboard.png)

<span data-ttu-id="c31da-113">Dodaj Kafelki przez przeciąganie i upuszczanie je na powierzchnię pulpitu nawigacyjnego wszędzie tam, gdzie ma.</span><span class="sxs-lookup"><span data-stu-id="c31da-113">Add tiles by dragging and dropping them onto the dashboard surface wherever you want.</span></span>

<span data-ttu-id="c31da-114">Brak nową kategorię o nazwie **ogólne** dla kafelków, które nie są skojarzone z określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="c31da-114">There's a new category called **General** for tiles that are not associated with a particular resource.</span></span>  <span data-ttu-id="c31da-115">W tym przykładzie mamy przypinanie kafelka Markdown.</span><span class="sxs-lookup"><span data-stu-id="c31da-115">In this example, we pin the Markdown tile.</span></span>  <span data-ttu-id="c31da-116">Ten Kafelek umożliwia dodawanie niestandardowej zawartości do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31da-116">You use this tile to add custom content to your dashboard.</span></span>  <span data-ttu-id="c31da-117">Kafelek obsługuje zwykłego tekstu, [składni języka Markdown](https://daringfireball.net/projects/markdown/syntax)oraz ograniczony zestaw HTML.</span><span class="sxs-lookup"><span data-stu-id="c31da-117">The tile supports plain text, [Markdown syntax](https://daringfireball.net/projects/markdown/syntax), and a limited set of HTML.</span></span>  <span data-ttu-id="c31da-118">(Dla bezpieczeństwa, nie może wykonać czynności, takie jak wstrzyknąć `<script>` znaczniki lub używać niektórych elementu Style CSS, która może kolidować z portalu.)</span><span class="sxs-lookup"><span data-stu-id="c31da-118">(For safety, you can't do things like inject `<script>` tags or use certain styling element of CSS that might interfere with the portal.)</span></span> 

![Dodawanie znaczników markdown](./media/azure-portal-dashboards/add-markdown.png)

## <a name="edit-a-dashboard"></a><span data-ttu-id="c31da-120">Edytuj pulpit nawigacyjny</span><span class="sxs-lookup"><span data-stu-id="c31da-120">Edit a dashboard</span></span>
<span data-ttu-id="c31da-121">Po utworzeniu pulpitu nawigacyjnego, można przypiąć Kafelki z galerii kafelka lub reprezentacja kafelka bloków.</span><span class="sxs-lookup"><span data-stu-id="c31da-121">After creating your dashboard, you can pin tiles from the tile gallery or the tile representation of blades.</span></span> <span data-ttu-id="c31da-122">Załóżmy przypiąć reprezentację naszej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c31da-122">Let's pin the representation of our resource group.</span></span> <span data-ttu-id="c31da-123">Można albo numeru pin podczas przeglądania elementu, lub z bloku grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c31da-123">You can either pin when browsing the item, or from the resource group blade.</span></span> <span data-ttu-id="c31da-124">W obu przypadkach efekt spowodować przypinanie kafelka reprezentację grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c31da-124">Both approaches result in pinning the tile representation of the resource group.</span></span>

![Przypnij do pulpitu nawigacyjnego](./media/azure-portal-dashboards/pin-to-dashboard.png)

<span data-ttu-id="c31da-126">Po przypięciu elementu, wygląda na to, na pulpicie nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="c31da-126">After pinning the item, it appears on your dashboard.</span></span>

![widok pulpitu nawigacyjnego](./media/azure-portal-dashboards/view-dashboard.png)

<span data-ttu-id="c31da-128">Mamy kafelków Markdown i grupy zasobów przypięty do pulpitu nawigacyjnego, firma Microsoft można zmieniać rozmiar i zmienić Kafelki na odpowiedni układ.</span><span class="sxs-lookup"><span data-stu-id="c31da-128">Now that we have a Markdown tile and a resource group pinned to the dashboard, we can resize and rearrange the tiles into a suitable layout.</span></span>

<span data-ttu-id="c31da-129">Kursora myszy i wybierając "..." lub klikając Kafelek można wyświetlić wszystkie polecenia kontekstowych dla tego kafelka.</span><span class="sxs-lookup"><span data-stu-id="c31da-129">By hovering and selecting "…" or right-clicking on a tile you can see all the contextual commands for that tile.</span></span> <span data-ttu-id="c31da-130">Domyślnie istnieją dwie pozycje:</span><span class="sxs-lookup"><span data-stu-id="c31da-130">By default, there are two items:</span></span>

1. <span data-ttu-id="c31da-131">**Odepnij z pulpitu nawigacyjnego** — usuwa kafelka pulpitu nawigacyjnego</span><span class="sxs-lookup"><span data-stu-id="c31da-131">**Unpin from dashboard** – removes the tile from the dashboard</span></span>
2. <span data-ttu-id="c31da-132">**Dostosowywanie** — wprowadza trybu dostosowania</span><span class="sxs-lookup"><span data-stu-id="c31da-132">**Customize** – enters customize mode</span></span>

![Dostosowywanie kafelka](./media/azure-portal-dashboards/customize-tile.png)

<span data-ttu-id="c31da-134">Wybierając dostosować, można zmieniać rozmiar i zmienić kolejność kafelków.</span><span class="sxs-lookup"><span data-stu-id="c31da-134">By selecting customize, you can resize and reorder tiles.</span></span> <span data-ttu-id="c31da-135">Aby zmienić rozmiar kafelka, wybierz nowy rozmiar z menu kontekstowego, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="c31da-135">To resize a tile, select the new size from the contextual menu, as shown in the following image.</span></span>

![Zmień rozmiar kafelka](./media/azure-portal-dashboards/resize-tile.png)

<span data-ttu-id="c31da-137">Lub, jeśli Kafelek obsługuje dowolnej wielkości, Zmień rozmiar można przeciągnąć prawym dolnym rogu.</span><span class="sxs-lookup"><span data-stu-id="c31da-137">Or, if the tile supports any size, you can drag the bottom right-hand corner to the desired size.</span></span>

![Zmień rozmiar kafelka](./media/azure-portal-dashboards/resize-corner.png)

<span data-ttu-id="c31da-139">Po zmianie rozmiaru kafelków, wyświetlić pulpit nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="c31da-139">After resizing tiles, view the dashboard.</span></span>

![Widok kafelków](./media/azure-portal-dashboards/view-tile.png)

<span data-ttu-id="c31da-141">Po zakończeniu dostosowanie pulpitu nawigacyjnego po prostu wybierz **gotowe dostosowywanie** aby zakończyć działanie trybu dostosowania, lub kliknij prawym przyciskiem myszy i wybierz polecenie **gotowe dostosowywanie** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="c31da-141">Once you are finished customizing a dashboard, simply select the **Done customizing** to exit customize mode or right-click and select **Done customizing** from the context menu.</span></span>

## <a name="publish-a-dashboard-and-manage-access-control"></a><span data-ttu-id="c31da-142">Publikowanie pulpitu nawigacyjnego i zarządzanie kontrolą dostępu</span><span class="sxs-lookup"><span data-stu-id="c31da-142">Publish a dashboard and manage access control</span></span>
<span data-ttu-id="c31da-143">Podczas tworzenia pulpitu nawigacyjnego jest prywatna domyślnie, co oznacza, że jesteś jedyną osobą, która to sprawdzić.</span><span class="sxs-lookup"><span data-stu-id="c31da-143">When you create a dashboard, it is private by default, which means you are the only person who can see it.</span></span>  <span data-ttu-id="c31da-144">Aby umożliwić innym osobom, użyj **udziału** przycisku, który pojawi się równolegle z innymi poleceniami pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31da-144">To make it visible to others, use the **Share** button that appears alongside the other dashboard commands.</span></span>

![Udostępnij pulpit nawigacyjny](./media/azure-portal-dashboards/share-dashboard.png)

<span data-ttu-id="c31da-146">Zostanie wyświetlona prośba o wybranie subskrypcji i grupy zasobów dla pulpitu nawigacyjnego do opublikowania dla.</span><span class="sxs-lookup"><span data-stu-id="c31da-146">You are asked to choose a subscription and resource group for your dashboard to be published to.</span></span> <span data-ttu-id="c31da-147">Aby bezproblemowo zintegrować pulpitów nawigacyjnych w ekosystemie, wdrożyliśmy udostępnionych pulpitów nawigacyjnych jako zasobów platformy Azure (tak, aby nie można udostępnić, wpisując adres e-mail).</span><span class="sxs-lookup"><span data-stu-id="c31da-147">To seamlessly integrate dashboards into the ecosystem, we've implemented shared dashboards as Azure resources (so you can't share by typing an email address).</span></span>  <span data-ttu-id="c31da-148">Dostęp do informacji wyświetlanych przez większość Kafelki w portalu są regulowane przez [kontroli dostępu opartej na roli Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c31da-148">Access to the information displayed by most of the tiles in the portal are governed by [Azure Role Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="c31da-149">Z punktu widzenia kontroli dostępu do udostępnionych pulpitów nawigacyjnych nie różnią się od maszyny wirtualnej lub konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c31da-149">From an access control perspective, shared dashboards are no different from a virtual machine or a storage account.</span></span>  

<span data-ttu-id="c31da-150">Załóżmy, że masz subskrypcję platformy Azure i członkowie zespołu są przypisane role **właściciela**, **współautora**, lub **czytnika** subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c31da-150">Let's say you have an Azure subscription and members of your team have been assigned the roles of **owner**, **contributor**, or **reader** of the subscription.</span></span>  <span data-ttu-id="c31da-151">Użytkownicy, którzy są właściciele i współautorzy mogą się na liście, wyświetlanie, tworzenie, modyfikowanie lub usuwanie pulpitów nawigacyjnych w ramach danej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c31da-151">Users who are owners or contributors are able to list, view, create, modify, or delete dashboards within that subscription.</span></span>  <span data-ttu-id="c31da-152">Użytkownicy, którzy są czytników są w stanie listy i widok pulpity nawigacyjne, ale nie można je modyfikować lub usuwać.</span><span class="sxs-lookup"><span data-stu-id="c31da-152">Users who are readers are able to list and view dashboards, but cannot modify or delete them.</span></span>  <span data-ttu-id="c31da-153">Użytkownicy z dostępem czytnika można wprowadzać zmian lokalnych do udostępnionego pulpitu nawigacyjnego, ale nie będą mogły publikować tych zmian na serwerze.</span><span class="sxs-lookup"><span data-stu-id="c31da-153">Users with reader access are able to make local edits to a shared dashboard, but are not able to publish those changes back to the server.</span></span>  <span data-ttu-id="c31da-154">Jednak mogą one ułatwić prywatnej kopii pulpitu nawigacyjnego na własny użytek.</span><span class="sxs-lookup"><span data-stu-id="c31da-154">However, they can make a private copy of the dashboard for their own use.</span></span>  <span data-ttu-id="c31da-155">Jak zawsze poszczególnych Kafelki na pulpicie nawigacyjnym wymuszanie własnych regułami kontroli dostępu na podstawie zasobów, które są zgodne.</span><span class="sxs-lookup"><span data-stu-id="c31da-155">As always, individual tiles on the dashboard enforce their own access control rules based on the resources they correspond to.</span></span>  

<span data-ttu-id="c31da-156">Dla wygody portalu do publikowania przewodniki środowisko możesz kierunku wzorzec, gdzie umieścić pulpitów nawigacyjnych w grupie zasobów o nazwie **pulpity nawigacyjne**.</span><span class="sxs-lookup"><span data-stu-id="c31da-156">For convenience, the portal's publishing experience guides you towards a pattern where you place dashboards in a resource group called **dashboards**.</span></span>  

![Publikowanie pulpitu nawigacyjnego](./media/azure-portal-dashboards/publish-dashboard.png)

<span data-ttu-id="c31da-158">Można również opublikować pulpit nawigacyjny do określonej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c31da-158">You can also choose to publish a dashboard to a particular resource group.</span></span>  <span data-ttu-id="c31da-159">Kontrola dostępu do tego pulpitu nawigacyjnego odpowiada kontroli dostępu dla grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="c31da-159">The access control for that dashboard matches the access control for the resource group.</span></span>  <span data-ttu-id="c31da-160">Użytkownicy, którzy mogą zarządzać zasobami w danej grupie zasobów mają także dostęp do pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c31da-160">Users that can manage the resources in that resource group also have access to the dashboards.</span></span>

![Publikowanie pulpitu nawigacyjnego do grupy zasobów](./media/azure-portal-dashboards/publish-to-resource-group.png)

<span data-ttu-id="c31da-162">Po opublikowaniu pulpitu nawigacyjnego **udostępniania + dostępu** Panelu sterowania zostanie odświeżania i wyświetlić informacje o pulpicie nawigacyjnym opublikowane, łącznie z łączem do zarządzania dostępem użytkowników do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="c31da-162">After your dashboard is published, the **Sharing + access** control pane will refresh and show you information about the published dashboard, including a link to manage user access to the dashboard.</span></span>  <span data-ttu-id="c31da-163">To łącze powoduje uruchomienie standardowego bloku kontroli dostępu opartej na rolach, używany do zarządzania dostępem dla wszystkich zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c31da-163">This link launches the standard Role Based Access Control blade used to manage access for any Azure resource.</span></span>  <span data-ttu-id="c31da-164">Możesz zawsze wrócić do tego widoku, wybierając **udziału**.</span><span class="sxs-lookup"><span data-stu-id="c31da-164">You can always get back to this view by selecting **Share**.</span></span>

![Zarządzanie kontrolą dostępu](./media/azure-portal-dashboards/manage-access.png)

## <a name="next-steps"></a><span data-ttu-id="c31da-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c31da-166">Next steps</span></span>
* <span data-ttu-id="c31da-167">Aby zarządzać zasobami, zobacz [zasobów Azure zarządzania za pośrednictwem portalu](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c31da-167">To manage resources, see [Manage Azure resources through portal](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="c31da-168">Aby wdrożyć zasobów, zobacz [wdrożenie zasobów z szablonami usługi Resource Manager i portalu Azure](../azure-resource-manager/resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c31da-168">To deploy resources, see [Deploy resources with Resource Manager templates and Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md).</span></span>

