---
<span data-ttu-id="4c012-101">title: aaa "lekcji samouczka usług Azure Analysis Services 9: tworzenie hierarchii | Opis Microsoft Docs": usługi: documentationcenter usług analysis services:" Autor: minewiskan Menedżera: Edytor erikre: "tagów:"</span><span class="sxs-lookup"><span data-stu-id="4c012-101">title: aaa"Azure Analysis Services tutorial lesson 9: Create hierarchies | Microsoft Docs" description: services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="4c012-102">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="4c012-102">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-9-create-hierarchies"></a><span data-ttu-id="4c012-103">Lekcja 9. Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="4c012-103">Lesson 9: Create hierarchies</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="4c012-104">W tej lekcji utworzysz hierarchie.</span><span class="sxs-lookup"><span data-stu-id="4c012-104">In this lesson, you create hierarchies.</span></span> <span data-ttu-id="4c012-105">Hierarchie to grupy kolumn uporządkowane według poziomów. Na przykład hierarchia Geografia może zawierać poziomy podrzędne Kraj, Województwo, Powiat i Miasto.</span><span class="sxs-lookup"><span data-stu-id="4c012-105">Hierarchies are groups of columns arranged in levels; for example, a Geography hierarchy might have sublevels for Country, State, County, and City.</span></span> <span data-ttu-id="4c012-106">Hierarchie można pojawiają się niezależnie od innych kolumn w raportowania listy pól aplikacji klienta, dzięki czemu łatwiej klienta toonavigate użytkowników i zawarte w raporcie.</span><span class="sxs-lookup"><span data-stu-id="4c012-106">Hierarchies can appear separate from other columns in a reporting client application field list, making them easier for client users toonavigate and include in a report.</span></span> <span data-ttu-id="4c012-107">toolearn więcej, zobacz [hierarchii](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="4c012-107">toolearn more, see [Hierarchies](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)</span></span>
  
<span data-ttu-id="4c012-108">hierarchie toocreate za pomocą projektanta modelu hello w *widoku diagramu*.</span><span class="sxs-lookup"><span data-stu-id="4c012-108">toocreate hierarchies, use hello model designer in *Diagram View*.</span></span> <span data-ttu-id="4c012-109">Tworzenie hierarchii i zarządzanie nimi nie jest obsługiwane w widoku danych.</span><span class="sxs-lookup"><span data-stu-id="4c012-109">Creating and managing hierarchies is not supported in Data View.</span></span>  
  
<span data-ttu-id="4c012-110">Szacowany czas toocomplete tej lekcji: **20 minut**</span><span class="sxs-lookup"><span data-stu-id="4c012-110">Estimated time toocomplete this lesson: **20 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="4c012-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4c012-111">Prerequisites</span></span>  
<span data-ttu-id="4c012-112">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="4c012-112">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="4c012-113">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 8: Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="4c012-113">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>  
  
## <a name="create-hierarchies"></a><span data-ttu-id="4c012-114">Tworzenie hierarchii</span><span class="sxs-lookup"><span data-stu-id="4c012-114">Create hierarchies</span></span>  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a><span data-ttu-id="4c012-115">Hierarchia kategorii w tabeli DimProduct hello toocreate</span><span class="sxs-lookup"><span data-stu-id="4c012-115">toocreate a Category hierarchy in hello DimProduct table</span></span>  
  
1.  <span data-ttu-id="4c012-116">W Projektancie modeli hello (widoku diagramu), kliknij prawym przyciskiem myszy hello **DimProduct** tabeli > **tworzenie hierarchii**.</span><span class="sxs-lookup"><span data-stu-id="4c012-116">In hello model designer (diagram view), right-click hello **DimProduct** table > **Create Hierarchy**.</span></span> <span data-ttu-id="4c012-117">Nowej hierarchii pojawi się u dołu okna tabeli hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c012-117">A new hierarchy appears at hello bottom of hello table window.</span></span> <span data-ttu-id="4c012-118">Zmień nazwę hierarchii hello **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="4c012-118">Rename hello hierarchy **Category**.</span></span>  
  
2.  <span data-ttu-id="4c012-119">Kliknij i przeciągnij hello **ProductCategoryName** toohello kolumny nowy **kategorii** hierarchii.</span><span class="sxs-lookup"><span data-stu-id="4c012-119">Click and drag hello **ProductCategoryName** column toohello new **Category** hierarchy.</span></span>  
  
3.  <span data-ttu-id="4c012-120">W hello **kategorii** hierarchii, kliknij prawym przyciskiem myszy hello **ProductCategoryName** > **zmienić**, a następnie wpisz **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="4c012-120">In hello **Category** hierarchy, right-click hello **ProductCategoryName** > **Rename**, and then type **Category**.</span></span>  
  
    > [!NOTE]  
    > <span data-ttu-id="4c012-121">Zmiana nazwy kolumny w hierarchii nie powoduje zmiany nazwy tej kolumny w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4c012-121">Renaming a column in a hierarchy does not rename that column in hello table.</span></span> <span data-ttu-id="4c012-122">Kolumna w hierarchii jest po prostu reprezentację hello kolumny w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="4c012-122">A column in a hierarchy is just a representation of hello column in hello table.</span></span>  
  
4.  <span data-ttu-id="4c012-123">Kliknij i przeciągnij hello **ProductSubcategoryName** toohello kolumny **kategorii** hierarchii.</span><span class="sxs-lookup"><span data-stu-id="4c012-123">Click and drag hello **ProductSubcategoryName** column toohello **Category** hierarchy.</span></span> <span data-ttu-id="4c012-124">Zmień jej nazwę na **Subcategory** (Podkategoria).</span><span class="sxs-lookup"><span data-stu-id="4c012-124">Rename it **Subcategory**.</span></span> 
  
5.  <span data-ttu-id="4c012-125">Powitania kliknij prawym przyciskiem myszy **ModelName** kolumny > **dodać toohierarchy**, a następnie wybierz **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="4c012-125">Right-click hello **ModelName** column > **Add toohierarchy**, and then select **Category**.</span></span> <span data-ttu-id="4c012-126">Zmień jej nazwę na **Model**.</span><span class="sxs-lookup"><span data-stu-id="4c012-126">Rename it **Model**.</span></span>

6.  <span data-ttu-id="4c012-127">Na koniec należy dodać **EnglishProductName** toohello hierarchia kategorii.</span><span class="sxs-lookup"><span data-stu-id="4c012-127">Finally, add **EnglishProductName** toohello Category hierarchy.</span></span> <span data-ttu-id="4c012-128">Zmień jej nazwę na **Product** (Produkt).</span><span class="sxs-lookup"><span data-stu-id="4c012-128">Rename it **Product**.</span></span>  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a><span data-ttu-id="4c012-130">hierarchie toocreate hello DimDate tabeli</span><span class="sxs-lookup"><span data-stu-id="4c012-130">toocreate hierarchies in hello DimDate table</span></span>  
  
1.  <span data-ttu-id="4c012-131">W hello **DimDate** tabeli, należy utworzyć hierarchię o nazwie **kalendarza**.</span><span class="sxs-lookup"><span data-stu-id="4c012-131">In hello **DimDate** table, create a hierarchy named **Calendar**.</span></span>  
  
3.  <span data-ttu-id="4c012-132">Dodaj hello następujących kolumn w kolejności:</span><span class="sxs-lookup"><span data-stu-id="4c012-132">Add hello following columns in-order:</span></span>

    *  <span data-ttu-id="4c012-133">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="4c012-133">CalendarYear</span></span>
    *  <span data-ttu-id="4c012-134">CalendarSemester</span><span class="sxs-lookup"><span data-stu-id="4c012-134">CalendarSemester</span></span>
    *  <span data-ttu-id="4c012-135">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="4c012-135">CalendarQuarter</span></span>
    *  <span data-ttu-id="4c012-136">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="4c012-136">MonthCalendar</span></span>
    *  <span data-ttu-id="4c012-137">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="4c012-137">DayNumberOfMonth</span></span>
    
4.  <span data-ttu-id="4c012-138">W hello **DimDate** tabeli, należy utworzyć **obrachunkowym** hierarchii.</span><span class="sxs-lookup"><span data-stu-id="4c012-138">In hello **DimDate** table, create a **Fiscal** hierarchy.</span></span> <span data-ttu-id="4c012-139">Dołącz hello następujących kolumn w kolejności:</span><span class="sxs-lookup"><span data-stu-id="4c012-139">Include hello following columns in-order:</span></span>  
  
    *  <span data-ttu-id="4c012-140">FiscalYear</span><span class="sxs-lookup"><span data-stu-id="4c012-140">FiscalYear</span></span>
    *  <span data-ttu-id="4c012-141">FiscalSemester</span><span class="sxs-lookup"><span data-stu-id="4c012-141">FiscalSemester</span></span>
    *  <span data-ttu-id="4c012-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="4c012-142">FiscalQuarter</span></span>
    *  <span data-ttu-id="4c012-143">MonthCalendar</span><span class="sxs-lookup"><span data-stu-id="4c012-143">MonthCalendar</span></span>
    *  <span data-ttu-id="4c012-144">DayNumberOfMonth</span><span class="sxs-lookup"><span data-stu-id="4c012-144">DayNumberOfMonth</span></span>
  
5.  <span data-ttu-id="4c012-145">Ponadto w hello **DimDate** tabeli, należy utworzyć **ProductionCalendar** hierarchii.</span><span class="sxs-lookup"><span data-stu-id="4c012-145">Finally, in hello **DimDate** table, create a **ProductionCalendar** hierarchy.</span></span> <span data-ttu-id="4c012-146">Dołącz hello następujących kolumn w kolejności:</span><span class="sxs-lookup"><span data-stu-id="4c012-146">Include hello following columns in-order:</span></span>  
    *  <span data-ttu-id="4c012-147">CalendarYear</span><span class="sxs-lookup"><span data-stu-id="4c012-147">CalendarYear</span></span>
    *  <span data-ttu-id="4c012-148">WeekNumberOfYear</span><span class="sxs-lookup"><span data-stu-id="4c012-148">WeekNumberOfYear</span></span>
    *  <span data-ttu-id="4c012-149">DayNumberOfWeek</span><span class="sxs-lookup"><span data-stu-id="4c012-149">DayNumberOfWeek</span></span>
  
 ## <a name="whats-next"></a><span data-ttu-id="4c012-150">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="4c012-150">What's next?</span></span>
<span data-ttu-id="4c012-151">[Lekcja 10. Tworzenie partycji](../tutorials/aas-lesson-10-create-partitions.md).</span><span class="sxs-lookup"><span data-stu-id="4c012-151">[Lesson 10: Create partitions](../tutorials/aas-lesson-10-create-partitions.md).</span></span> 
  
  
