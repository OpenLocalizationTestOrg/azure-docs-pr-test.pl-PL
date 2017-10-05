---
title: "Konwertowanie danych XML przy użyciu transformacji - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Utwórz transformacje lub mapps do konwersji danych XML między formatami w aplikacjach logiki przy użyciu zestawu SDK integracji przedsiębiorstwa"
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
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="b543b-103">Integracja przedsiębiorstwa z transformacji XML</span><span class="sxs-lookup"><span data-stu-id="b543b-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="b543b-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b543b-104">Overview</span></span>
<span data-ttu-id="b543b-105">Łącznik przekształcenia integracji przedsiębiorstwa konwertuje dane z jednego formatu do innego formatu.</span><span class="sxs-lookup"><span data-stu-id="b543b-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="b543b-106">Przykładowo może istnieć wiadomości przychodzącej, która zawiera bieżącą datę w formacie YearMonthDay.</span><span class="sxs-lookup"><span data-stu-id="b543b-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="b543b-107">Transformacja służy do ponownego formatowania daty w formacie MonthDayYear.</span><span class="sxs-lookup"><span data-stu-id="b543b-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="b543b-108">Do czego służy transformacji?</span><span class="sxs-lookup"><span data-stu-id="b543b-108">What does a transform do?</span></span>
<span data-ttu-id="b543b-109">Przekształcanie, który jest także znana jako mapy, składa się z schematu XML źródła (dane wejściowe) i schematu XML docelowego (dane wyjściowe).</span><span class="sxs-lookup"><span data-stu-id="b543b-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="b543b-110">Różne funkcje wbudowane można użyć, aby manipulować i kontroli danych, tym działań na ciągach, warunkowego przypisania, wyrażeniach arytmetycznych elementy formatujące czasu daty, a nawet zapętlenia konstrukcje.</span><span class="sxs-lookup"><span data-stu-id="b543b-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="b543b-111">Jak utworzyć transformację?</span><span class="sxs-lookup"><span data-stu-id="b543b-111">How to create a transform?</span></span>
<span data-ttu-id="b543b-112">Przekształcanie/map można utworzyć za pomocą programu Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span><span class="sxs-lookup"><span data-stu-id="b543b-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="b543b-113">Po zakończeniu tworzenia i testowania transformacji możesz przekazać do konta integracji transformacji.</span><span class="sxs-lookup"><span data-stu-id="b543b-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="b543b-114">Jak używać przekształcania</span><span class="sxs-lookup"><span data-stu-id="b543b-114">How to use a transform</span></span>
<span data-ttu-id="b543b-115">Po wysłaniu przekształcenie/map na koncie integracji można służy do tworzenia aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b543b-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="b543b-116">Aplikację logiki działa z przekształcenia po każdym wyzwoleniu aplikacji logiki (i Brak zawartości wejściowej, które muszą zostać przekształcone).</span><span class="sxs-lookup"><span data-stu-id="b543b-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="b543b-117">**Poniżej przedstawiono kroki, aby użyć transformacji**:</span><span class="sxs-lookup"><span data-stu-id="b543b-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="b543b-118">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b543b-118">Prerequisites</span></span>

* <span data-ttu-id="b543b-119">Tworzenie konta usługi integracji i Dodaj mapę do niej</span><span class="sxs-lookup"><span data-stu-id="b543b-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="b543b-120">Teraz, że zostały wykonane szczególną uwagę wymagania wstępne, jest czas, aby utworzyć aplikację logiki:</span><span class="sxs-lookup"><span data-stu-id="b543b-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="b543b-121">Tworzenie aplikacji logiki i [połączyć go z kontem integracji](../logic-apps/logic-apps-enterprise-integration-accounts.md "Dowiedz się połączyć konto integracji aplikacji logiki") zawierający mapy.</span><span class="sxs-lookup"><span data-stu-id="b543b-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="b543b-122">Dodaj **żądania** do aplikacji logiki wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="b543b-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="b543b-123">Dodaj **transformacji XML** akcji, wybierając najpierw **Dodaj akcję** </span><span class="sxs-lookup"><span data-stu-id="b543b-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="b543b-124">Wprowadź słowa *przekształcenie* w polu wyszukiwania, aby filtrować wszystkie akcje do tego, który ma być używany</span><span class="sxs-lookup"><span data-stu-id="b543b-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="b543b-125">Wybierz **transformacji XML** akcji</span><span class="sxs-lookup"><span data-stu-id="b543b-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="b543b-126">Dodanie pliku XML **zawartości** który transformacji.</span><span class="sxs-lookup"><span data-stu-id="b543b-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="b543b-127">Można używać danych XML pojawi się w żądaniu HTTP jako **zawartości**.</span><span class="sxs-lookup"><span data-stu-id="b543b-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="b543b-128">W tym przykładzie wybierz treści żądania HTTP, która wyzwoliła aplikacji logiki.</span><span class="sxs-lookup"><span data-stu-id="b543b-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="b543b-129">Wybierz nazwę **mapy** chcesz używać do wykonywania transformacji.</span><span class="sxs-lookup"><span data-stu-id="b543b-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="b543b-130">Mapa musi być już na koncie integracji.</span><span class="sxs-lookup"><span data-stu-id="b543b-130">The map must already be in your integration account.</span></span> <span data-ttu-id="b543b-131">W poprzednim kroku już udzielił Ci dostęp do aplikacji logiki do swojego konta integracji zawierającego mapy.</span><span class="sxs-lookup"><span data-stu-id="b543b-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="b543b-132">Zapisz swoją pracę</span><span class="sxs-lookup"><span data-stu-id="b543b-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="b543b-133">W tym momencie po zakończeniu konfigurowania mapy.</span><span class="sxs-lookup"><span data-stu-id="b543b-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="b543b-134">W przypadku aplikacji rzeczywistych można przechowywać przekształcone dane w aplikacji biznesowych, takich jak SalesForce.</span><span class="sxs-lookup"><span data-stu-id="b543b-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="b543b-135">Możesz z łatwością jako akcja wysyłane dane wyjściowe przekształcenia Salesforce.</span><span class="sxs-lookup"><span data-stu-id="b543b-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="b543b-136">Teraz możesz przetestować z transformacji, wysyłając żądania do punktu końcowego HTTP.</span><span class="sxs-lookup"><span data-stu-id="b543b-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="b543b-137">Funkcje i przypadki użycia</span><span class="sxs-lookup"><span data-stu-id="b543b-137">Features and use cases</span></span>
* <span data-ttu-id="b543b-138">Transformacja utworzone na mapie może być prosty, takich jak kopiowanie nazwy i adresu z jednego dokumentu do innego.</span><span class="sxs-lookup"><span data-stu-id="b543b-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="b543b-139">Alternatywnie można tworzyć bardziej złożone przekształcenia przy użyciu operacji poza pole mapy.</span><span class="sxs-lookup"><span data-stu-id="b543b-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="b543b-140">Wiele operacji mapy lub funkcje są łatwo dostępne, w tym ciągów, dat funkcje związane z czasem i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b543b-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="b543b-141">Możesz to zrobić kopię danych bezpośrednio między schematów.</span><span class="sxs-lookup"><span data-stu-id="b543b-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="b543b-142">W mapowania dołączony do zestawu SDK jest tak proste, jak rysowania linii łączącej elementy w schemacie źródła z ich odpowiedniki w schemacie docelowego.</span><span class="sxs-lookup"><span data-stu-id="b543b-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="b543b-143">Podczas tworzenia mapy, możesz wyświetlić graficzną reprezentację mapa, która zawiera wszystkie relacje i tworzysz łącza.</span><span class="sxs-lookup"><span data-stu-id="b543b-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="b543b-144">Funkcja testu mapy do dodania przykładowy komunikat XML.</span><span class="sxs-lookup"><span data-stu-id="b543b-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="b543b-145">Pojedynczym kliknięciem można przetestować mapy, który został utworzony, a Zobacz wygenerowanych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b543b-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="b543b-146">Przekazywanie istniejącej mapy</span><span class="sxs-lookup"><span data-stu-id="b543b-146">Upload existing maps</span></span>  
* <span data-ttu-id="b543b-147">Obsługuje XML format.</span><span class="sxs-lookup"><span data-stu-id="b543b-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="b543b-148">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="b543b-148">Learn more</span></span>
* [<span data-ttu-id="b543b-149">Dowiedz się więcej o pakiet integracyjny dla przedsiębiorstw</span><span class="sxs-lookup"><span data-stu-id="b543b-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Dowiedz się więcej na temat pakiet integracyjny dla przedsiębiorstw")  
* [<span data-ttu-id="b543b-150">Dowiedz się więcej o mapy</span><span class="sxs-lookup"><span data-stu-id="b543b-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Dowiedz się więcej na temat map integracji przedsiębiorstwa")  

