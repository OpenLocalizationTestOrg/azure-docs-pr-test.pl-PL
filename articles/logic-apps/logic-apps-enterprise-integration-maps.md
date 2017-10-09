---
title: "aaaTransform XML przy użyciu map XSLT - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Dodaj XSLT mapy tootransform danych XML przy użyciu usługi Azure Logic Apps i hello pakiet integracyjny dla przedsiębiorstw"
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
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="6ac1a-103">Dodaj mapy dla transformacji danych XML</span><span class="sxs-lookup"><span data-stu-id="6ac1a-103">Add maps for XML data transform</span></span>

<span data-ttu-id="6ac1a-104">Używa integracji przedsiębiorstwa mapuje dane XML tootransform między formatami.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="6ac1a-105">Mapa jest dokument XML, definiujący hello dane w dokumencie, który powinien zostać przekształcone w innym formacie.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="6ac1a-106">Dlaczego warto używać mapy?</span><span class="sxs-lookup"><span data-stu-id="6ac1a-106">Why use maps?</span></span>

<span data-ttu-id="6ac1a-107">Załóżmy, że regularnie B2B zamówień lub faktur od klienta, który używa hello YYYMMDD format daty.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="6ac1a-108">Jednak w organizacji, można przechowywać daty w formacie MMDDYYY hello.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="6ac1a-109">Można użyć mapy zbyt*przekształcenie* format daty YYYMMDD hello na powitania MMDDYYY przed przekazaniem szczegółów zamówienia lub faktury hello działania bazy danych klienta.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="6ac1a-110">Jak utworzyć mapę?</span><span class="sxs-lookup"><span data-stu-id="6ac1a-110">How do I create a map?</span></span>

<span data-ttu-id="6ac1a-111">Możesz utworzyć projektów BizTalk integracji z hello [pakiet integracyjny dla przedsiębiorstw](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw hello") dla programu Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="6ac1a-112">Następnie można utworzyć pliku Mapa integracji programu, który pozwala wizualnie mapy elementów między dwoma plikami schematu XML.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="6ac1a-113">Po utworzeniu tego projektu należy dokument XSLT.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="6ac1a-114">Jak dodać mapy?</span><span class="sxs-lookup"><span data-stu-id="6ac1a-114">How do I add a map?</span></span>

1. <span data-ttu-id="6ac1a-115">Hello portalu Azure, wybierz **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="6ac1a-116">W polu wyszukiwania filtr hello, wprowadź **integracji**, a następnie wybierz pozycję **konta integracji** z listy wyników hello.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="6ac1a-117">Wybierz konto integracji hello miejscu tooadd hello mapy.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="6ac1a-118">Wybierz hello **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="6ac1a-119">Po otwarciu bloku mapy hello wybierz **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="6ac1a-120">Wprowadź **nazwa** mapy.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="6ac1a-121">Mapa hello tooupload plików, wybierz ikonę folderu powitania po prawej stronie powitania hello **mapy** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="6ac1a-122">Po zakończeniu procesu przekazywania hello wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="6ac1a-123">Po Azure dodaje hello mapy tooyour integracji konta, zostanie wyświetlony komunikat na ekranie, który pokazuje, czy plik mapy dodano lub nie.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="6ac1a-124">Po ten komunikat zostanie wyświetlony, wybierz hello **mapy** Kafelek, aby wyświetlić hello nowo dodany mapy.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="6ac1a-125">Jak edytować mapy?</span><span class="sxs-lookup"><span data-stu-id="6ac1a-125">How do I edit a map?</span></span>

<span data-ttu-id="6ac1a-126">Musisz przekazać nowy plik mapy z hello żądanych zmian.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="6ac1a-127">Można najpierw pobrać hello mapy do edycji.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="6ac1a-128">tooupload nowej mapy, który zastępuje hello istniejącej mapy, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="6ac1a-129">Wybierz hello **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="6ac1a-130">Po otwarciu bloku mapy hello wybierz hello mapy, które mają tooedit.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="6ac1a-131">Na powitania **mapy** bloku, wybierz **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="6ac1a-132">Selektor plików hello, wybierz plik mapy hello czy tooupload, a następnie wybierz **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="6ac1a-133">Jak toodelete mapy?</span><span class="sxs-lookup"><span data-stu-id="6ac1a-133">How toodelete a map?</span></span>

1. <span data-ttu-id="6ac1a-134">Wybierz hello **mapy** kafelka.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="6ac1a-135">Po otwarciu bloku mapy hello Wybierz mapę hello ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="6ac1a-136">Wybierz **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="6ac1a-137">Upewnij się, że chcesz toodelete hello mapy.</span><span class="sxs-lookup"><span data-stu-id="6ac1a-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="6ac1a-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ac1a-138">Next Steps</span></span>
* [<span data-ttu-id="6ac1a-139">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="6ac1a-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [<span data-ttu-id="6ac1a-140">Dowiedz się więcej na temat umów</span><span class="sxs-lookup"><span data-stu-id="6ac1a-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "więcej informacji na temat umowy integracji dla przedsiębiorstw")  
* [<span data-ttu-id="6ac1a-141">Dowiedz się więcej o transformacji</span><span class="sxs-lookup"><span data-stu-id="6ac1a-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Dowiedz się więcej o przedsiębiorstwie transformacje integracji")  

