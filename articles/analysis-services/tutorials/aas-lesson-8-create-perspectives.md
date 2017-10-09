---
title: AAA "Azure Analysis Services lekcji samouczka 8 Tworzenie perspektyw | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak perspektywy toocreate hello projekt samouczka usług Azure Analysis Services."
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
ms.openlocfilehash: 25391813e1969ecb22af4d6f9c1ccd8358d812fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="lesson-8-create-perspectives"></a><span data-ttu-id="7f54c-103">Lekcja 8. Tworzenie perspektyw</span><span class="sxs-lookup"><span data-stu-id="7f54c-103">Lesson 8: Create perspectives</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="7f54c-104">W tej lekcji utworzysz perspektywę sprzedaży internetowej.</span><span class="sxs-lookup"><span data-stu-id="7f54c-104">In this lesson, you create an Internet Sales perspective.</span></span> <span data-ttu-id="7f54c-105">Perspektywa definiuje możliwy do wyświetlenia podzbiór modelu, który uwzględnia ukierunkowane punkty widzenia specyficzne dla firmy lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f54c-105">A perspective defines a viewable subset of a model that provides focused, business-specific, or application-specific viewpoints.</span></span> <span data-ttu-id="7f54c-106">Gdy użytkownik łączy tooa modelu za pomocą perspektywy, zostanie wyświetlona tylko obiekty modelu (tabel, kolumn, miar, hierarchie i wskaźników KPI) jako pola zdefiniowane w tym perspektywy.</span><span class="sxs-lookup"><span data-stu-id="7f54c-106">When a user connects tooa model by using a perspective, they see only those model objects (tables, columns, measures, hierarchies, and KPIs) as fields defined in that perspective.</span></span> <span data-ttu-id="7f54c-107">toolearn więcej, zobacz [perspektywy](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span><span class="sxs-lookup"><span data-stu-id="7f54c-107">toolearn more, see [Perspectives](https://docs.microsoft.com/sql/analysis-services/tabular-models/perspectives-ssas-tabular).</span></span>
  
<span data-ttu-id="7f54c-108">Witaj perspektywy sprzedaży internetowej, utworzone w tej lekcji wyklucza hello DimCustomer tabeli obiektów.</span><span class="sxs-lookup"><span data-stu-id="7f54c-108">hello Internet Sales perspective you create in this lesson excludes hello DimCustomer table object.</span></span> <span data-ttu-id="7f54c-109">Po utworzeniu perspektywę, która wyklucza niektórych obiektów z widoku obiektu nadal istnieje w modelu hello.</span><span class="sxs-lookup"><span data-stu-id="7f54c-109">When you create a perspective that excludes certain objects from view, that object still exists in hello model.</span></span> <span data-ttu-id="7f54c-110">Nie są one jednak widoczne na liście pól raportu klienta.</span><span class="sxs-lookup"><span data-stu-id="7f54c-110">However, it is not visible in a reporting client field list.</span></span> <span data-ttu-id="7f54c-111">Niezależnie od tego, czy kolumny obliczeniowe i miary zostały uwzględnione w perspektywie, czy też nie, odpowiadające im wartości są nadal obliczane na podstawie danych z wykluczonych obiektów.</span><span class="sxs-lookup"><span data-stu-id="7f54c-111">Calculated columns and measures either included in a perspective or not can still calculate from object data that is excluded.</span></span>  
  
<span data-ttu-id="7f54c-112">Celem tej lekcji Hello jest toodescribe jak perspektywy toocreate i zapoznać się z modelu tabelarycznego hello narzędzia do tworzenia.</span><span class="sxs-lookup"><span data-stu-id="7f54c-112">hello purpose of this lesson is toodescribe how toocreate perspectives and become familiar with hello tabular model authoring tools.</span></span> <span data-ttu-id="7f54c-113">Jeśli później rozszerzyć ten model tooinclude dodatkowe tabele, możesz utworzyć dodatkowe perspektywy toodefine inny punkt widzenia hello modelu, na przykład, spisu i sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="7f54c-113">If you later expand this model tooinclude additional tables, you can create additional perspectives toodefine different viewpoints of hello model, for example, Inventory and Sales.</span></span>  
  
<span data-ttu-id="7f54c-114">Szacowany czas toocomplete tej lekcji: **pięć minut**</span><span class="sxs-lookup"><span data-stu-id="7f54c-114">Estimated time toocomplete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="7f54c-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7f54c-115">Prerequisites</span></span>  
<span data-ttu-id="7f54c-116">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="7f54c-116">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="7f54c-117">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [7 lekcji: tworzenie kluczowych wskaźników wydajności](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span><span class="sxs-lookup"><span data-stu-id="7f54c-117">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 7: Create Key Performance Indicators](../tutorials/aas-lesson-7-create-key-performance-indicators.md).</span></span>  
  
## <a name="create-perspectives"></a><span data-ttu-id="7f54c-118">Tworzenie perspektyw</span><span class="sxs-lookup"><span data-stu-id="7f54c-118">Create perspectives</span></span>  
  
#### <a name="toocreate-an-internet-sales-perspective"></a><span data-ttu-id="7f54c-119">toocreate perspektywy sprzedaży internetowej</span><span class="sxs-lookup"><span data-stu-id="7f54c-119">toocreate an Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="7f54c-120">Kliknij przycisk hello **modelu** menu > **perspektywy** > **Utwórz i Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="7f54c-120">Click hello **Model** menu > **Perspectives** > **Create and Manage**.</span></span>  
  
2.  <span data-ttu-id="7f54c-121">W hello **perspektywy** okno dialogowe, kliknij przycisk **nowej perspektywy**.</span><span class="sxs-lookup"><span data-stu-id="7f54c-121">In hello **Perspectives** dialog box, click **New Perspective**.</span></span>  
  
3.  <span data-ttu-id="7f54c-122">Kliknij dwukrotnie hello **nowej perspektywy** nagłówek kolumny, a następnie zmień nazwę **sprzedaży Internet**.</span><span class="sxs-lookup"><span data-stu-id="7f54c-122">Double-click hello **New Perspective** column heading, and then rename **Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="7f54c-123">Wybierz hello wszystkie tabele hello *z wyjątkiem* **DimCustomer**.</span><span class="sxs-lookup"><span data-stu-id="7f54c-123">Select hello all hello tables *except* **DimCustomer**.</span></span>  
  
    ![aas-lesson8-perspectives](../tutorials/media/aas-lesson8-perspectives.png)
  
    <span data-ttu-id="7f54c-125">W następnej lekcji Użyj hello analizowanie w tootest funkcji programu Excel ta perspektywa.</span><span class="sxs-lookup"><span data-stu-id="7f54c-125">In a later lesson, you use hello Analyze in Excel feature tootest this perspective.</span></span> <span data-ttu-id="7f54c-126">Witaj listy pól tabeli przestawnej programu Excel zawiera każdej tabeli, z wyjątkiem hello DimCustomer tabeli.</span><span class="sxs-lookup"><span data-stu-id="7f54c-126">hello Excel PivotTable Fields List includes each table except hello DimCustomer table.</span></span>  

## <a name="whats-next"></a><span data-ttu-id="7f54c-127">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="7f54c-127">What's next?</span></span>
<span data-ttu-id="7f54c-128">[Lekcja 9. Tworzenie hierarchii](../tutorials/aas-lesson-9-create-hierarchies.md).</span><span class="sxs-lookup"><span data-stu-id="7f54c-128">[Lesson 9: Create hierarchies](../tutorials/aas-lesson-9-create-hierarchies.md).</span></span>
  
  
  
  
