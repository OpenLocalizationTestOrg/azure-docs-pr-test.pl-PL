---
title: "aaaConvert danych XML przy użyciu transformacji - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz transformacje lub mapps danych XML tooconvert między formatami w aplikacjach logiki przy użyciu hello SDK integracji przedsiębiorstwa"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: b56ec1072c5058d3aefc7f88ac9b2748ebe56456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="e340e-103">Integracja przedsiębiorstwa z transformacji XML</span><span class="sxs-lookup"><span data-stu-id="e340e-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="e340e-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="e340e-104">Overview</span></span>
<span data-ttu-id="e340e-105">Łącznik przekształcenia integracji przedsiębiorstwa Hello konwertuje dane z jednego formatu tooanother format.</span><span class="sxs-lookup"><span data-stu-id="e340e-105">hello Enterprise integration Transform connector converts data from one format tooanother format.</span></span> <span data-ttu-id="e340e-106">Na przykład masz zawierający bieżącą datę w formacie YearMonthDay hello hello wiadomości przychodzącej.</span><span class="sxs-lookup"><span data-stu-id="e340e-106">For example, you may have an incoming message that contains hello current date in hello YearMonthDay format.</span></span> <span data-ttu-id="e340e-107">Przekształcanie tooreformat hello Data toobe można użyć w formacie MonthDayYear hello.</span><span class="sxs-lookup"><span data-stu-id="e340e-107">You can use a transform tooreformat hello date toobe in hello MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="e340e-108">Do czego służy transformacji?</span><span class="sxs-lookup"><span data-stu-id="e340e-108">What does a transform do?</span></span>
<span data-ttu-id="e340e-109">Przekształcenia, która jest także znana jako mapy, składa się z schematu XML źródła (hello danych wejściowych) i schemat XML docelowego (hello dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="e340e-109">A Transform, which is also known as a map, consists of a Source XML schema (hello input) and a Target XML schema (hello output).</span></span> <span data-ttu-id="e340e-110">Różne funkcje wbudowane toohelp manipulować i kontroli danych hello służy tym działań na ciągach, warunkowego przypisania, wyrażeniach arytmetycznych elementy formatujące czasu Data oraz nawet zapętlenia konstrukcje.</span><span class="sxs-lookup"><span data-stu-id="e340e-110">You can use different built-in functions toohelp manipulate or control hello data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-toocreate-a-transform"></a><span data-ttu-id="e340e-111">Jak toocreate transformacji?</span><span class="sxs-lookup"><span data-stu-id="e340e-111">How toocreate a transform?</span></span>
<span data-ttu-id="e340e-112">Przekształcanie/map można utworzyć za pomocą programu Visual Studio hello [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="e340e-112">You can create a transform/map by using hello Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="e340e-113">Po zakończeniu tworzenia i testowania hello przekształcania, możesz przekazać przekształcenia hello na koncie integracji.</span><span class="sxs-lookup"><span data-stu-id="e340e-113">When you are finished creating and testing hello transform, you upload hello transform into your integration account.</span></span> 

## <a name="how-toouse-a-transform"></a><span data-ttu-id="e340e-114">Jak toouse transformacji</span><span class="sxs-lookup"><span data-stu-id="e340e-114">How toouse a transform</span></span>
<span data-ttu-id="e340e-115">Po przekazaniu hello przekształcenie/map na koncie integracji, można użyć toocreate aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e340e-115">After you upload hello transform/map into your integration account, you can use it toocreate a Logic app.</span></span> <span data-ttu-id="e340e-116">aplikacji logiki Hello uruchamia przekształcenia użytkownika za każdym razem wyzwoleniu aplikacji logiki hello (i Brak zawartości wejściowej wymagające toobe przekształcone).</span><span class="sxs-lookup"><span data-stu-id="e340e-116">hello Logic app runs your transformations whenever hello Logic app is triggered (and there is input content that needs toobe transformed).</span></span>

<span data-ttu-id="e340e-117">**Poniżej przedstawiono toouse kroki hello transformacji**:</span><span class="sxs-lookup"><span data-stu-id="e340e-117">**Here are hello steps toouse a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e340e-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e340e-118">Prerequisites</span></span>

* <span data-ttu-id="e340e-119">Tworzenie konta usługi integracji i Dodaj tooit mapy</span><span class="sxs-lookup"><span data-stu-id="e340e-119">Create an integration account and add a map tooit</span></span>  

<span data-ttu-id="e340e-120">Teraz, że zostały wykonane szczególną uwagę hello wymagań wstępnych, jest toocreate czasu aplikację logiki:</span><span class="sxs-lookup"><span data-stu-id="e340e-120">Now that you've taken care of hello prerequisites, it's time toocreate your Logic app:</span></span>  

1. <span data-ttu-id="e340e-121">Tworzenie aplikacji logiki i [link jej konta integracji tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się toolink aplikacji logiki tooa konta integracji") zawierający hello mapy.</span><span class="sxs-lookup"><span data-stu-id="e340e-121">Create a Logic app and [link it tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that contains hello map.</span></span>
2. <span data-ttu-id="e340e-122">Dodaj **żądania** aplikacji logiki tooyour wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="e340e-122">Add a **Request** trigger tooyour Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="e340e-123">Dodaj hello **transformacji XML** akcji, wybierając najpierw **Dodaj akcję** </span><span class="sxs-lookup"><span data-stu-id="e340e-123">Add hello **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="e340e-124">Wprowadź słowa hello *przekształcenie* w toofilter pole wyszukiwania hello hello wszystkie akcje toohello, jednego, które mają toouse</span><span class="sxs-lookup"><span data-stu-id="e340e-124">Enter hello word *transform* in hello search box toofilter all hello actions toohello one that you want toouse</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="e340e-125">Wybierz hello **transformacji XML** akcji</span><span class="sxs-lookup"><span data-stu-id="e340e-125">Select hello **Transform XML** action</span></span>   
6. <span data-ttu-id="e340e-126">Dodaj hello XML **zawartości** który transformacji.</span><span class="sxs-lookup"><span data-stu-id="e340e-126">Add hello XML **CONTENT** that you transform.</span></span> <span data-ttu-id="e340e-127">Można używać danych XML pojawi się w żądaniu hello HTTP jako hello **zawartości**.</span><span class="sxs-lookup"><span data-stu-id="e340e-127">You can use any XML data you receive in hello HTTP request as hello **CONTENT**.</span></span> <span data-ttu-id="e340e-128">W tym przykładzie wybierz treści hello hello żądania HTTP, która wyzwoliła hello aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e340e-128">In this example, select hello body of hello HTTP request that triggered hello Logic app.</span></span>
7. <span data-ttu-id="e340e-129">Wybierz hello nazwę hello **mapy** , które mają toouse tooperform hello transformacji.</span><span class="sxs-lookup"><span data-stu-id="e340e-129">Select hello name of hello **MAP** that you want toouse tooperform hello transformation.</span></span> <span data-ttu-id="e340e-130">Mapa Hello musi być już na koncie integracji.</span><span class="sxs-lookup"><span data-stu-id="e340e-130">hello map must already be in your integration account.</span></span> <span data-ttu-id="e340e-131">W poprzednim kroku już udzielił logiki aplikacji dostępu tooyour integracji konta zawierającego mapy.</span><span class="sxs-lookup"><span data-stu-id="e340e-131">In an earlier step, you already gave your Logic app access tooyour integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="e340e-132">Zapisz swoją pracę</span><span class="sxs-lookup"><span data-stu-id="e340e-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="e340e-133">W tym momencie po zakończeniu konfigurowania mapy.</span><span class="sxs-lookup"><span data-stu-id="e340e-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="e340e-134">W przypadku aplikacji rzeczywistych można toostore hello przekształcone dane w aplikacji biznesowych, takich jak SalesForce.</span><span class="sxs-lookup"><span data-stu-id="e340e-134">In a real world application, you may want toostore hello transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="e340e-135">Można łatwo jako akcja toosend hello dane wyjściowe hello przekształcać tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="e340e-135">You can easily as an action toosend hello output of hello transform tooSalesforce.</span></span> 

<span data-ttu-id="e340e-136">Teraz możesz przetestować użytkownika przekształcenia przez punkt końcowy HTTP toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="e340e-136">You can now test your transform by making a request toohello HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="e340e-137">Funkcje i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="e340e-137">Features and use cases</span></span>
* <span data-ttu-id="e340e-138">Transformacja Hello utworzone na mapie może być prosty, takich jak kopiowanie nazwy i adresu z jednego tooanother dokumentu.</span><span class="sxs-lookup"><span data-stu-id="e340e-138">hello transformation created in a map can be simple, such as copying a name and address from one document tooanother.</span></span> <span data-ttu-id="e340e-139">Alternatywnie można tworzyć bardziej złożone przekształcenia przy użyciu operacji poza pole mapy hello.</span><span class="sxs-lookup"><span data-stu-id="e340e-139">Or, you can create more complex transformations using hello out-of-the-box map operations.</span></span>  
* <span data-ttu-id="e340e-140">Wiele operacji mapy lub funkcje są łatwo dostępne, w tym ciągów, dat funkcje związane z czasem i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="e340e-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="e340e-141">Możesz to zrobić kopię danych bezpośrednio między hello schematów.</span><span class="sxs-lookup"><span data-stu-id="e340e-141">You can do a direct data copy between hello schemas.</span></span> <span data-ttu-id="e340e-142">W hello mapowania uwzględnione w hello zestawu SDK jest tak proste, jak rysowania linii łączącego hello elementy w schemacie źródła hello z ich odpowiedniki w schemacie docelowego hello.</span><span class="sxs-lookup"><span data-stu-id="e340e-142">In hello Mapper included in hello SDK, this is as simple as drawing a line that connects hello elements in hello source schema with their counterparts in hello destination schema.</span></span>  
* <span data-ttu-id="e340e-143">Podczas tworzenia mapy, możesz wyświetlić graficzną reprezentację hello mapa, która zawiera wszystkie relacje hello i tworzysz łącza.</span><span class="sxs-lookup"><span data-stu-id="e340e-143">When creating a map, you view a graphical representation of hello map, which shows all hello relationships and links you create.</span></span>
* <span data-ttu-id="e340e-144">Użyj hello mapy testu funkcji tooadd przykładowy komunikat XML.</span><span class="sxs-lookup"><span data-stu-id="e340e-144">Use hello Test Map feature tooadd a sample XML message.</span></span> <span data-ttu-id="e340e-145">Pojedynczym kliknięciem można przetestować mapy hello utworzone i wyświetlić hello wygenerowane dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e340e-145">With a simple click, you can test hello map you created, and see hello generated output.</span></span>  
* <span data-ttu-id="e340e-146">Przekazywanie istniejącej mapy</span><span class="sxs-lookup"><span data-stu-id="e340e-146">Upload existing maps</span></span>  
* <span data-ttu-id="e340e-147">Obsługuje hello XML format.</span><span class="sxs-lookup"><span data-stu-id="e340e-147">Includes support for hello XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="e340e-148">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="e340e-148">Learn more</span></span>
* [<span data-ttu-id="e340e-149">Dowiedz się więcej o hello pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="e340e-149">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [<span data-ttu-id="e340e-150">Dowiedz się więcej o mapy</span><span class="sxs-lookup"><span data-stu-id="e340e-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")  

