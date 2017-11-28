---
<span data-ttu-id="55653-101">title: aaa "lekcji samouczka usług Azure Analysis Services 7: tworzenie kluczowych wskaźników wydajności | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate kluczowych wskaźników wydajności w hello projekt samouczka usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="55653-101">title: aaa"Azure Analysis Services tutorial lesson 7: Create Key Performance Indicators | Microsoft Docs" description: Describes how toocreate Key Performance Indicators in hello Azure Analysis Services tutorial project.</span></span> <span data-ttu-id="55653-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="55653-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="55653-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="55653-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="lesson-7-create-key-performance-indicators"></a><span data-ttu-id="55653-104">Lekcja 7. Tworzenie kluczowych wskaźników wydajności</span><span class="sxs-lookup"><span data-stu-id="55653-104">Lesson 7: Create Key Performance Indicators</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="55653-105">W tej lekcji utworzysz kluczowe wskaźniki wydajności (KPI).</span><span class="sxs-lookup"><span data-stu-id="55653-105">In this lesson, you create Key Performance Indicators (KPIs).</span></span> <span data-ttu-id="55653-106">Kluczowe wskaźniki wydajności są używane toogauge wydajności z wartości zdefiniowanych przez *Base* miary, przed *docelowej* wartość również zdefiniowane przez miarę, lub wartość bezwzględna.</span><span class="sxs-lookup"><span data-stu-id="55653-106">KPIs are used toogauge performance of a value defined by a *Base* measure, against a *Target* value also defined by a measure, or by an absolute value.</span></span> <span data-ttu-id="55653-107">W raportach aplikacji klienckich, wskaźników KPI może zapewnić specjaliści toounderstand szybkie i proste podsumowanie trendów powodzenie lub tooidentify biznesowych.</span><span class="sxs-lookup"><span data-stu-id="55653-107">In reporting client applications, KPIs can provide business professionals a quick and easy way toounderstand a summary of business success or tooidentify trends.</span></span> <span data-ttu-id="55653-108">toolearn więcej, zobacz [wskaźników KPI](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span><span class="sxs-lookup"><span data-stu-id="55653-108">toolearn more, see [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)</span></span>
  
<span data-ttu-id="55653-109">Szacowany czas toocomplete tej lekcji: **15 minut**</span><span class="sxs-lookup"><span data-stu-id="55653-109">Estimated time toocomplete this lesson: **15 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="55653-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="55653-110">Prerequisites</span></span>  
<span data-ttu-id="55653-111">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="55653-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="55653-112">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [Lekcja 6: tworzenie miar](../tutorials/aas-lesson-6-create-measures.md).</span><span class="sxs-lookup"><span data-stu-id="55653-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 6: Create measures](../tutorials/aas-lesson-6-create-measures.md).</span></span>   
  
## <a name="create-key-performance-indicators"></a><span data-ttu-id="55653-113">Tworzenie kluczowych wskaźników wydajności</span><span class="sxs-lookup"><span data-stu-id="55653-113">Create Key Performance Indicators</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a><span data-ttu-id="55653-114">toocreate InternetCurrentQuarterSalesPerformance kluczowy wskaźnik wydajności</span><span class="sxs-lookup"><span data-stu-id="55653-114">toocreate an InternetCurrentQuarterSalesPerformance KPI</span></span>  
  
1.  <span data-ttu-id="55653-115">W Konstruktorze modelu powitania kliknij hello **FactInternetSales** tabeli.</span><span class="sxs-lookup"><span data-stu-id="55653-115">In hello model designer, click hello **FactInternetSales** table.</span></span>  
  
2.  <span data-ttu-id="55653-116">W siatce miar hello kliknij przycisk pustej komórki.</span><span class="sxs-lookup"><span data-stu-id="55653-116">In hello measure grid, click an empty cell.</span></span>  
  
3.  <span data-ttu-id="55653-117">Na pasku formuły hello, powyżej tabeli hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="55653-117">In hello formula bar, above hello table, type hello following formula:</span></span> 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    <span data-ttu-id="55653-118">To jest miara służy jako hello miara podstawowa dla hello kluczowego wskaźnika wydajności.</span><span class="sxs-lookup"><span data-stu-id="55653-118">This measure serves as hello Base measure for hello KPI.</span></span>  
  
4.  <span data-ttu-id="55653-119">Kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterSalesPerformance** > **Utwórz wskaźnik KPI**.</span><span class="sxs-lookup"><span data-stu-id="55653-119">Right-click **InternetCurrentQuarterSalesPerformance** > **Create KPI**.</span></span>   
  
5.  <span data-ttu-id="55653-120">W hello kluczowego wskaźnika wydajności (KPI) — okno dialogowe w **docelowej** wybierz **wartość bezwzględna**, a następnie wpisz **1.1**.</span><span class="sxs-lookup"><span data-stu-id="55653-120">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.1**.</span></span>  
  
7.  <span data-ttu-id="55653-121">W polu po lewej stronie suwaka (niski) hello wpisz **1**, a następnie w hello suwak w prawo (wysoka) wpisz **1.07**.</span><span class="sxs-lookup"><span data-stu-id="55653-121">In hello left (low) slider field, type **1**, and then in hello right (high) slider field, type **1.07**.</span></span>  
  
8.  <span data-ttu-id="55653-122">W **wybierz styl ikony**wybierz hello romb (czerwony), trójkąt (żółty), koło typ ikony (zielony).</span><span class="sxs-lookup"><span data-stu-id="55653-122">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type.</span></span>
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > <span data-ttu-id="55653-124">Powiadomienie hello rozwijania **opisy** etykiety poniżej hello ikona dostępne style.</span><span class="sxs-lookup"><span data-stu-id="55653-124">Notice hello expandable **Descriptions** label below hello available icon styles.</span></span> <span data-ttu-id="55653-125">Użyj opisy dla hello różnych toomake elementów KPI ich więcej zidentyfikować w aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="55653-125">Use descriptions for hello various KPI elements toomake them more identifiable in client applications.</span></span>  
  
9. <span data-ttu-id="55653-126">Kliknij przycisk **OK** toocomplete hello kluczowego wskaźnika wydajności.</span><span class="sxs-lookup"><span data-stu-id="55653-126">Click **OK** toocomplete hello KPI.</span></span>  
  
    <span data-ttu-id="55653-127">W siatce miar hello, zwróć uwagę hello ikona dalej toohello **InternetCurrentQuarterSalesPerformance** miary.</span><span class="sxs-lookup"><span data-stu-id="55653-127">In hello measure grid, notice hello icon next toohello **InternetCurrentQuarterSalesPerformance** measure.</span></span> <span data-ttu-id="55653-128">Ta ikona wskazuje, że dana miara służy jako wartość podstawowa dla kluczowego wskaźnika wydajności.</span><span class="sxs-lookup"><span data-stu-id="55653-128">This icon indicates that this measure serves as a Base value for a KPI.</span></span>  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a><span data-ttu-id="55653-129">toocreate InternetCurrentQuarterMarginPerformance kluczowy wskaźnik wydajności</span><span class="sxs-lookup"><span data-stu-id="55653-129">toocreate an InternetCurrentQuarterMarginPerformance KPI</span></span>  
  
1.  <span data-ttu-id="55653-130">W siatce miar hello hello **FactInternetSales** tabeli, kliknij przycisk pustej komórki.</span><span class="sxs-lookup"><span data-stu-id="55653-130">In hello measure grid for hello **FactInternetSales** table, click an empty cell.</span></span>  
  
2.  <span data-ttu-id="55653-131">Na pasku formuły hello, powyżej tabeli hello wpisz hello następującej formuły:</span><span class="sxs-lookup"><span data-stu-id="55653-131">In hello formula bar, above hello table, type hello following formula:</span></span>  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  <span data-ttu-id="55653-132">Kliknij prawym przyciskiem myszy pozycje **InternetCurrentQuarterMarginPerformance** > **Utwórz wskaźnik KPI**.</span><span class="sxs-lookup"><span data-stu-id="55653-132">Right-click **InternetCurrentQuarterMarginPerformance** > **Create KPI**.</span></span>  
  
4.  <span data-ttu-id="55653-133">W hello kluczowego wskaźnika wydajności (KPI) — okno dialogowe w **docelowej** wybierz **wartość bezwzględna**, a następnie wpisz **1,25**.</span><span class="sxs-lookup"><span data-stu-id="55653-133">In hello Key Performance Indicator (KPI) dialog box, in **Target** select **Absolute Value**, and then type **1.25**.</span></span>   
  
5.  <span data-ttu-id="55653-134">Hello suwaka (niski) po lewej stronie pola, Przesuń do momentu wyświetlenia pola hello **0,8**, a następnie hello slajdów prawym przyciskiem myszy pole suwaka (wysoka) do momentu wyświetlenia pola hello **1,03**.</span><span class="sxs-lookup"><span data-stu-id="55653-134">In hello left (low) slider field, slide until hello field displays **0.8**, and then slide hello right (high) slider field, until hello field displays **1.03**.</span></span>  
  
6.  <span data-ttu-id="55653-135">W **wybierz styl ikony**Wybierz romb hello (czerwony), trójkąt (żółty), typ ikony koła (zielony), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="55653-135">In **Select Icon Style**, select hello diamond (red), triangle (yellow), circle (green) icon type, and then click **OK**.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="55653-136">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="55653-136">What's next?</span></span>
<span data-ttu-id="55653-137">[Lekcja 8. Tworzenie perspektyw](../tutorials/aas-lesson-8-create-perspectives.md).</span><span class="sxs-lookup"><span data-stu-id="55653-137">[Lesson 8: Create perspectives](../tutorials/aas-lesson-8-create-perspectives.md).</span></span>
  
  
