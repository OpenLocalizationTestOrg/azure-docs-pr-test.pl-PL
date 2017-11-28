---
title: "Przekształcanie XML przy użyciu map XSLT - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dodaj XSLT mapy do transformacji danych XML przy użyciu usługi Azure Logic Apps i pakiet integracyjny dla przedsiębiorstw"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="b3260-103">Dodaj mapy dla transformacji danych XML</span><span class="sxs-lookup"><span data-stu-id="b3260-103">Add maps for XML data transform</span></span>

<span data-ttu-id="b3260-104">Integracji przedsiębiorstwa do transformacji danych XML między formatami wykorzystuje mapy.</span><span class="sxs-lookup"><span data-stu-id="b3260-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="b3260-105">Mapa jest dokument XML, który definiuje dane w dokumencie, który powinien zostać przekształcone w innym formacie.</span><span class="sxs-lookup"><span data-stu-id="b3260-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="b3260-106">Dlaczego warto używać mapy?</span><span class="sxs-lookup"><span data-stu-id="b3260-106">Why use maps?</span></span>

<span data-ttu-id="b3260-107">Załóżmy, że regularnie B2B zamówień lub faktur od klienta, który używa formatu YYYMMDD dla daty.</span><span class="sxs-lookup"><span data-stu-id="b3260-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="b3260-108">Jednak w organizacji, przechowywać w formacie MMDDYYY daty.</span><span class="sxs-lookup"><span data-stu-id="b3260-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="b3260-109">Możesz użyć mapy do *przekształcenie* format daty YYYMMDD do MMDDYYY przed przekazaniem szczegółów zamówienia lub faktury działania bazy danych klienta.</span><span class="sxs-lookup"><span data-stu-id="b3260-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="b3260-110">Jak utworzyć mapę?</span><span class="sxs-lookup"><span data-stu-id="b3260-110">How do I create a map?</span></span>

<span data-ttu-id="b3260-111">Można tworzyć projektów BizTalk integracji z [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw") dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="b3260-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="b3260-112">Następnie można utworzyć pliku Mapa integracji programu, który pozwala wizualnie mapy elementów między dwoma plikami schematu XML.</span><span class="sxs-lookup"><span data-stu-id="b3260-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="b3260-113">Po utworzeniu tego projektu należy dokument XSLT.</span><span class="sxs-lookup"><span data-stu-id="b3260-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="b3260-114">Jak dodać mapy?</span><span class="sxs-lookup"><span data-stu-id="b3260-114">How do I add a map?</span></span>

1. <span data-ttu-id="b3260-115">W portalu Azure wybierz **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="b3260-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="b3260-116">W polu filtru wyszukiwania wprowadź **integracji**, a następnie wybierz pozycję **konta integracji** z listy wyników.</span><span class="sxs-lookup"><span data-stu-id="b3260-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="b3260-117">Wybierz konto integracji, w której chcesz dodać mapy.</span><span class="sxs-lookup"><span data-stu-id="b3260-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="b3260-118">Wybierz **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b3260-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="b3260-119">Po otwarciu bloku mapy, wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="b3260-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="b3260-120">Wprowadź **nazwa** mapy.</span><span class="sxs-lookup"><span data-stu-id="b3260-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="b3260-121">Aby przekazać plik mapy, wybierz ikonę folderu w prawej części **mapy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="b3260-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="b3260-122">Po zakończeniu procesu przekazywania, wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3260-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="b3260-123">Po Azure dodaje mapy do swojego konta integracji, zostanie wyświetlony komunikat na ekranie, który pokazuje, czy plik mapy dodano lub nie.</span><span class="sxs-lookup"><span data-stu-id="b3260-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="b3260-124">Po ten komunikat zostanie wyświetlony, wybierz **mapy** sąsiadująco w celu wyświetlania nowo dodanych mapy.</span><span class="sxs-lookup"><span data-stu-id="b3260-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="b3260-125">Jak edytować mapy?</span><span class="sxs-lookup"><span data-stu-id="b3260-125">How do I edit a map?</span></span>

<span data-ttu-id="b3260-126">Musisz przekazać nowy plik mapy z żądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="b3260-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="b3260-127">Można najpierw pobrać mapy do edycji.</span><span class="sxs-lookup"><span data-stu-id="b3260-127">You can first download the map for editing.</span></span>

<span data-ttu-id="b3260-128">Aby przekazać nowy mapy, który zastępuje istniejące mapy, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="b3260-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="b3260-129">Wybierz **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b3260-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="b3260-130">Po otwarciu bloku mapy, wybierz mapy, który chcesz edytować.</span><span class="sxs-lookup"><span data-stu-id="b3260-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="b3260-131">Na **mapy** bloku, wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="b3260-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="b3260-132">Selektor plików wybierz plik mapy, który chcesz przekazać, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3260-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="b3260-133">Jak usunąć mapy?</span><span class="sxs-lookup"><span data-stu-id="b3260-133">How to delete a map?</span></span>

1. <span data-ttu-id="b3260-134">Wybierz **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="b3260-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="b3260-135">Po otwarciu bloku mapy, wybierz mapę, którą chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="b3260-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="b3260-136">Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="b3260-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="b3260-137">Upewnij się, że chcesz usunąć mapy.</span><span class="sxs-lookup"><span data-stu-id="b3260-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="b3260-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3260-138">Next Steps</span></span>
* [<span data-ttu-id="b3260-139">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="b3260-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [<span data-ttu-id="b3260-140">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="b3260-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  
* [<span data-ttu-id="b3260-141">Dowiedz się więcej o transformacji</span><span class="sxs-lookup"><span data-stu-id="b3260-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Dowiedz się więcej o przedsiębiorstwie transformacje integracji")  

