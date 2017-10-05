---
title: "Samouczek Azure Analysis Services: lekcja 8 — tworzenie perspektyw | Microsoft Docs"
description: "Opisuje sposób tworzenia perspektyw w projekcie samouczka usług Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 05/26/2017
ms.author: owend
ms.openlocfilehash: 491500909b0de0360afae45e172e85999d764fe0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="b1842-103">Lekcja 8. Tworzenie perspektyw</span><span class="sxs-lookup"><span data-stu-id="b1842-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="b1842-104">W tej lekcji utworzysz perspektywę sprzedaży internetowej.</span><span class="sxs-lookup"><span data-stu-id="b1842-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="b1842-105">Perspektywa definiuje możliwy do wyświetlenia podzbiór modelu, który uwzględnia ukierunkowane punkty widzenia specyficzne dla firmy lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b1842-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="b1842-106">Użytkownik, który połączy się z modelem przy użyciu perspektywy, zobaczy jedynie odpowiednie obiekty modelu (tabele, kolumny, miary, hierarchie i kluczowe wskaźniki wydajności) w postaci pól zdefiniowanych w danej perspektywie.</span><span class="sxs-lookup"><span data-stu-id="b1842-106">When a user connects to a model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="b1842-107">Aby dowiedzieć się więcej, zobacz temat [Perspektywy](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="b1842-107">To learn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="b1842-108">Utworzona w tej lekcji perspektywa sprzedaży internetowej nie zawiera obiektu tabeli DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="b1842-108">The Internet Sales perspective you create in this lesson excludes the DimCustomer table object.</span></span> <span data-ttu-id="b1842-109">W przypadku utworzenia perspektywy, która wyłącza określone obiekty z widoku, obiekty te nadal istnieją w modelu.</span><span class="sxs-lookup"><span data-stu-id="b1842-109">When you create a perspective that excludes certain objects from view, that object still exists in the model.</span></span> <span data-ttu-id="b1842-110">Nie są one jednak widoczne na liście pól raportu klienta.</span><span class="sxs-lookup"><span data-stu-id="b1842-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="b1842-111">Niezależnie od tego, czy kolumny obliczeniowe i miary zostały uwzględnione w perspektywie, czy też nie, odpowiadające im wartości są nadal obliczane na podstawie danych z wykluczonych obiektów.</span><span class="sxs-lookup"><span data-stu-id="b1842-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="b1842-112">Celem tej lekcji jest przedstawienie sposobu tworzenia perspektyw i zapoznanie się z narzędziami do tworzenia modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="b1842-112">The purpose of this lesson is to describe how to create perspectives and become familiar with the tabular model authoring tools.</span></span> <span data-ttu-id="b1842-113">Jeśli model zostanie później rozszerzony w celu uwzględnienia dodatkowych tabel, możesz utworzyć dodatkowe perspektywy, np. uwzględniające punkt widzenia zapasów magazynowych i sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="b1842-113">If you later expand this model to include additional tables, you can create additional perspectives to define different viewpoints of the model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="b1842-114">Szacowany czas trwania lekcji: **5 minut**</span><span class="sxs-lookup"><span data-stu-id="b1842-114">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="b1842-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b1842-115">Prerequisites</span></span>  
<span data-ttu-id="b1842-116">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="b1842-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="b1842-117">Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 7. Tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="b1842-117">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="b1842-118">Tworzenie perspektyw</span><span class="sxs-lookup"><span data-stu-id="b1842-118">Create perspectives</span></span>  
  
#### <a name="to-create-an-internet-sales-perspective"></a><span data-ttu-id="b1842-119">Tworzenie perspektywy sprzedaży internetowej</span><span class="sxs-lookup"><span data-stu-id="b1842-119">To create an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="b1842-120">W menu **Model** kliknij pozycje **Perspektywy** > **Utwórz i zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="b1842-120">Click the **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="b1842-121">W oknie dialogowym **Perspektywy** kliknij przycisk **Nowa perspektywa**.</span><span class="sxs-lookup"><span data-stu-id="b1842-121">In the **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="b1842-122">Kliknij dwukrotnie nagłówek kolumny **Nowa perspektywa**, a następnie zmień nazwę na **Internet Sales** (Sprzedaż internetowa).</span><span class="sxs-lookup"><span data-stu-id="b1842-122">Double-click the **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="b1842-123">Zaznacz wszystkie tabele *z wyjątkiem* tabeli **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="b1842-123">Select the all the tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="b1842-125">W kolejnej lekcji użyjesz funkcji Analiza w programie Excel do testowania tej perspektywy.</span><span class="sxs-lookup"><span data-stu-id="b1842-125">In a later lesson, you use the Analyze in Excel feature to test this perspective.</span></span> <span data-ttu-id="b1842-126">Lista pól tabeli przestawnej programu Excel zawiera wszystkie tabele z wyjątkiem tabeli DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="b1842-126">The Excel PivotTable Fields List includes each table except the DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="b1842-127">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="b1842-127">What's next?</span></span>
<span data-ttu-id="b1842-128">[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="b1842-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
