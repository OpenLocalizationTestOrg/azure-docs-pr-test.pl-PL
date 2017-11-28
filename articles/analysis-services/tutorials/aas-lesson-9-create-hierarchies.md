---
title: "Samouczek Azure Analysis Services: lekcja 9 — tworzenie hierarchii | Microsoft Docs"
description: 
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
ms.openlocfilehash: d628dc621335acf231342a6d9186079de16e85f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="f4f7c-102">Lekcja 9. Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="f4f7c-102">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="f4f7c-103">W tej lekcji utworzysz hierarchie.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-103">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="f4f7c-104">Hierarchie to grupy kolumn uporządkowane według poziomów. Na przykład hierarchia Geografia może zawierać poziomy podrzędne Kraj, Województwo, Powiat i Miasto.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-104">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="f4f7c-105">Na liście pól aplikacji raportujących klienta hierarchie mogą występować niezależnie od innych kolumn, co ułatwia nawigację i dołączanie do raportów.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-105">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users to navigate and include in a report.</span></span> <span data-ttu-id="f4f7c-106">Aby dowiedzieć się więcej, zobacz temat [Hierarchie](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-106">To learn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="f4f7c-107">Aby utworzyć hierarchie, należy użyć projektanta modeli w *widoku diagramu*.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-107">To create hierarchies, use the model designer in *Diagram View*.</span></span> <span data-ttu-id="f4f7c-108">Tworzenie hierarchii i zarządzanie nimi nie jest obsługiwane w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-108">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="f4f7c-109">Szacowany czas trwania lekcji: **20 minut**</span><span class="sxs-lookup"><span data-stu-id="f4f7c-109">Estimated time to complete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="f4f7c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4f7c-110">Prerequisites</span></span>  
<span data-ttu-id="f4f7c-111">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="f4f7c-112">Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 8: Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="f4f7c-113">Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="f4f7c-113">Create hierarchies</span></span>  
  
#### <a name="to-create-a-category-hierarchy-in-the-dimproduct-table"></a><span data-ttu-id="f4f7c-114">Tworzenie hierarchii kategorii w tabeli DimProduct</span><span class="sxs-lookup"><span data-stu-id="f4f7c-114">To create a Category hierarchy in the DimProduct table</span></span>  
  
1.  <span data-ttu-id="f4f7c-115">W projektancie modeli (w widoku diagramu) kliknij prawym przyciskiem myszy tabelę **DimProduct**, a następnie pozycję **Utwórz hierarchię**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-115">In the model designer (diagram view), right-click the **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="f4f7c-116">Nowa hierarchia pojawi się w dolnej części okna tabeli.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-116">A new hierarchy appears at the bottom of the table window.</span></span> <span data-ttu-id="f4f7c-117">Zmień nazwę hierarchii na **Category** (Kategoria).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-117">Rename the hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="f4f7c-118">Kliknij i przeciągnij kolumnę **ProductCategoryName** do nowej hierarchii **Category**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-118">Click and drag the **ProductCategoryName** column to the new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="f4f7c-119">W hierarchii **Category** kliknij prawym przyciskiem myszy pozycje **ProductCategoryName** > **Zmień nazwę**, a następnie wpisz nazwę **Category**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-119">In the **Category** hierarchy, right-click the **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="f4f7c-120">Zmiana nazwy kolumny w hierarchii nie powoduje zmiany nazwy tej kolumny w tabeli.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-120">Renaming a column in a hierarchy does not rename that column in the table.</span></span> <span data-ttu-id="f4f7c-121">Kolumna w hierarchii jest jedynie reprezentacją kolumny w tabeli.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-121">A column in a hierarchy is just a representation of the column in the table.</span></span>  
  
4.  <span data-ttu-id="f4f7c-122">Kliknij i przeciągnij kolumnę **ProductSubcategoryName** do nowej hierarchii **Category**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-122">Click and drag the **ProductSubcategoryName** column to the **Category** hierarchy.</span></span> <span data-ttu-id="f4f7c-123">Zmień jej nazwę na **Subcategory** (Podkategoria).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-123">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="f4f7c-124">Kliknij prawym przyciskiem myszy kolumnę **ModelName** > **Dodaj do hierarchii**, a następnie wybierz pozycję **Category**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-124">Right-click the **ModelName** column > **Add to hierarchy**, and then select **Category**.</span></span> <span data-ttu-id="f4f7c-125">Zmień jej nazwę na **Model**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-125">Rename it **Model**.</span></span>

6.  <span data-ttu-id="f4f7c-126">Na zakończenie dodaj kolumnę **EnglishProductName** do hierarchii Category.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-126">Finally, add **EnglishProductName** to the Category hierarchy.</span></span> <span data-ttu-id="f4f7c-127">Zmień jej nazwę na **Product** (Produkt).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-127">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="to-create-hierarchies-in-the-dimdate-table"></a><span data-ttu-id="f4f7c-129">Tworzenie hierarchii w tabeli DimDate</span><span class="sxs-lookup"><span data-stu-id="f4f7c-129">To create hierarchies in the DimDate table</span></span>  
  
1.  <span data-ttu-id="f4f7c-130">W tabeli **DimDate** utwórz hierarchię o nazwie **Calendar** (Kalendarz).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-130">In the **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="f4f7c-131">Dodaj następujące kolumny w podanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="f4f7c-131">Add the following columns in-order:</span></span>

    *  <span data-ttu-id="f4f7c-132">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="f4f7c-132">CalendarYear</span></span>
    *  <span data-ttu-id="f4f7c-133">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="f4f7c-133">CalendarSemester</span></span>
    *  <span data-ttu-id="f4f7c-134">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="f4f7c-134">CalendarQuarter</span></span>
    *  <span data-ttu-id="f4f7c-135">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="f4f7c-135">MonthCalendar</span></span>
    *  <span data-ttu-id="f4f7c-136">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="f4f7c-136">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="f4f7c-137">W tabeli **DimDate** utwórz hierarchię o nazwie **Fiscal** (Fiskalne).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-137">In the **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="f4f7c-138">Dodaj następujące kolumny w podanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="f4f7c-138">Include the following columns in-order:</span></span>  
  
    *  <span data-ttu-id="f4f7c-139">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="f4f7c-139">FiscalYear</span></span>
    *  <span data-ttu-id="f4f7c-140">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="f4f7c-140">FiscalSemester</span></span>
    *  <span data-ttu-id="f4f7c-141">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="f4f7c-141">FiscalQuarter</span></span>
    *  <span data-ttu-id="f4f7c-142">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="f4f7c-142">MonthCalendar</span></span>
    *  <span data-ttu-id="f4f7c-143">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="f4f7c-143">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="f4f7c-144">Na koniec w tabeli **DimDate** utwórz hierarchię **ProductionCalendar**.</span><span class="sxs-lookup"><span data-stu-id="f4f7c-144">Finally, in the **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="f4f7c-145">Dodaj następujące kolumny w podanej kolejności:</span><span class="sxs-lookup"><span data-stu-id="f4f7c-145">Include the following columns in-order:</span></span>  
    *  <span data-ttu-id="f4f7c-146">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="f4f7c-146">CalendarYear</span></span>
    *  <span data-ttu-id="f4f7c-147">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="f4f7c-147">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="f4f7c-148">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="f4f7c-148">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="f4f7c-149">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="f4f7c-149">What's next?</span></span>
<span data-ttu-id="f4f7c-150">[Lekcja 10. Tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="f4f7c-150">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
