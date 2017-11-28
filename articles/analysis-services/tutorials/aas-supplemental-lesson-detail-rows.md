---
<span data-ttu-id="88da6-101">title: aaa "samouczek lekcji dodatkowych usług Azure Analysis Services: wiersze szczegółów | Opis elementu Microsoft Docs": w tym artykule opisano, jak toocreate, a wyrażenie wiersze szczegółów w hello Samouczek usług Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="88da6-101">title: aaa"Azure Analysis Services tutorial supplemental lesson: Detail Rows | Microsoft Docs" description: Describes how toocreate a Detail Rows Expression in hello Azure Analysis Services tutorial.</span></span>
<span data-ttu-id="88da6-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="88da6-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="88da6-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="88da6-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 05/26/2017 ms.author: owend</span></span>
---
# <a name="supplemental-lesson---detail-rows"></a><span data-ttu-id="88da6-104">Lekcja uzupełniająca — wiersze szczegółów</span><span class="sxs-lookup"><span data-stu-id="88da6-104">Supplemental lesson - Detail Rows</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="88da6-105">W tej lekcji uzupełniające służą hello toodefine edytora języka DAX wyrażenia niestandardowego wiersze szczegółów.</span><span class="sxs-lookup"><span data-stu-id="88da6-105">In this supplemental lesson, you use hello DAX Editor toodefine a custom Detail Rows Expression.</span></span> <span data-ttu-id="88da6-106">Wyrażenie wiersze szczegółów jest właściwością w miarę, zapewniając użytkownikom końcowym więcej informacji na temat wyników hello agregować miary.</span><span class="sxs-lookup"><span data-stu-id="88da6-106">A Detail Rows Expression is a property on a measure, providing end-users more information about hello aggregated results of a measure.</span></span> 
  
<span data-ttu-id="88da6-107">Szacowany czas toocomplete tej lekcji: **10 minut**</span><span class="sxs-lookup"><span data-stu-id="88da6-107">Estimated time toocomplete this lesson: **10 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="88da6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="88da6-108">Prerequisites</span></span>  
<span data-ttu-id="88da6-109">Ta lekcja uzupełniająca stanowi część samouczka modelowania tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="88da6-109">This supplemental lesson topic is part of a tabular modeling tutorial.</span></span> <span data-ttu-id="88da6-110">Przed wykonaniem zadania hello w tym uzupełniające lekcji, powinno mieć ukończone wszystkie poprzednie — lekcje lub zakończonych projektu modelu przykładowej firmy Adventure Works Internet sprzedaży.</span><span class="sxs-lookup"><span data-stu-id="88da6-110">Before performing hello tasks in this supplemental lesson, you should have completed all previous lessons or have a completed Adventure Works Internet Sales sample model project.</span></span>  
  
## <a name="what-do-we-need-toosolve"></a><span data-ttu-id="88da6-111">Co zrobić, potrzebujemy toosolve?</span><span class="sxs-lookup"><span data-stu-id="88da6-111">What do we need toosolve?</span></span>
<span data-ttu-id="88da6-112">Przyjrzyjmy się hello szczegóły naszych miary InternetTotalSales przed dodaniem wyrażenia do szczegółów wierszy.</span><span class="sxs-lookup"><span data-stu-id="88da6-112">Let's look at hello details of our InternetTotalSales measure, before adding a Detail Rows Expression.</span></span>

1.  <span data-ttu-id="88da6-113">Programu SSDT, kliknij przycisk hello **modelu** menu > **analizy w programie Excel** tooopen programu Excel i Utwórz pustą tabelę przestawną.</span><span class="sxs-lookup"><span data-stu-id="88da6-113">In SSDT, click hello **Model** menu > **Analyze in Excel** tooopen Excel and create a blank PivotTable.</span></span>
  
2.  <span data-ttu-id="88da6-114">W **pól tabeli przestawnej**, Dodaj hello **InternetTotalSales** miarę Tabela FactInternetSales hello zbyt**wartości**, **CalendarYear**z hello DimDate tabeli zbyt**kolumn**, i **EnglishCountryRegionName** za**wierszy**.</span><span class="sxs-lookup"><span data-stu-id="88da6-114">In **PivotTable Fields**, add hello **InternetTotalSales** measure from hello FactInternetSales table too**Values**, **CalendarYear** from hello DimDate table too**Columns**, and **EnglishCountryRegionName** too**Rows**.</span></span> <span data-ttu-id="88da6-115">Nasze tabeli przestawnej teraz daje wyników zagregowany z miary InternetTotalSales hello regiony i roku.</span><span class="sxs-lookup"><span data-stu-id="88da6-115">Our PivotTable now gives us aggregated results from hello InternetTotalSales measure by regions and year.</span></span> 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. <span data-ttu-id="88da6-117">W tabeli przestawnej hello kliknij dwukrotnie wartość zagregowana roku i nazwę regionu.</span><span class="sxs-lookup"><span data-stu-id="88da6-117">In hello PivotTable, double-click an aggregated value for a year and a region name.</span></span> <span data-ttu-id="88da6-118">W tym miejscu możemy podwójnie hello wartość dla klientów w Australii i hello 2014 roku.</span><span class="sxs-lookup"><span data-stu-id="88da6-118">Here we double-clicked hello value for Australia and hello year 2014.</span></span> <span data-ttu-id="88da6-119">Otwarty został nowy arkusz zawierający dane, które jednak nie są użyteczne.</span><span class="sxs-lookup"><span data-stu-id="88da6-119">A new sheet opens containing data, but not useful data.</span></span>

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
<span data-ttu-id="88da6-121">Co mamy ma tutaj toosee to tabela zawierająca kolumn i wierszy współtworzenia toohello agregowana wynik naszych InternetTotalSales miary.</span><span class="sxs-lookup"><span data-stu-id="88da6-121">What we would like toosee here is a table containing columns and rows of data that contribute toohello aggregated result of our InternetTotalSales measure.</span></span> <span data-ttu-id="88da6-122">toodo, że wyrażenie wiersze szczegółów można dodać jako właściwość hello miary.</span><span class="sxs-lookup"><span data-stu-id="88da6-122">toodo that, we can add a Detail Rows Expression as a property of hello measure.</span></span>

## <a name="add-a-detail-rows-expression"></a><span data-ttu-id="88da6-123">Dodawanie wyrażenia wierszy szczegółów</span><span class="sxs-lookup"><span data-stu-id="88da6-123">Add a Detail Rows Expression</span></span>

#### <a name="toocreate-a-detail-rows-expression"></a><span data-ttu-id="88da6-124">toocreate wyrażenie wiersze szczegółów</span><span class="sxs-lookup"><span data-stu-id="88da6-124">toocreate a Detail Rows Expression</span></span> 
  
1. <span data-ttu-id="88da6-125">Programu SSDT, w siatce miar Tabela FactInternetSales hello, kliknij przycisk hello **InternetTotalSales** miary.</span><span class="sxs-lookup"><span data-stu-id="88da6-125">In SSDT, in hello FactInternetSales table's measure grid, click hello **InternetTotalSales** measure.</span></span> 

2. <span data-ttu-id="88da6-126">W **właściwości** > **wyrażenie wiersze szczegółów**, kliknij przycisk hello Edytor przycisk tooopen hello edytora języka DAX.</span><span class="sxs-lookup"><span data-stu-id="88da6-126">In **Properties** > **Detail Rows Expression**, click hello editor button tooopen hello DAX Editor.</span></span>

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. <span data-ttu-id="88da6-128">W edytorze języka DAX wprowadź powitania po wyrażeniu:</span><span class="sxs-lookup"><span data-stu-id="88da6-128">In DAX Editor, enter hello following expression:</span></span>

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    <span data-ttu-id="88da6-129">To wyrażenie określa nazwy kolumny i miary z powiązanych tabel i tabela FactInternetSales hello są zwracane, gdy użytkownik kliknie dwukrotnie wyników zagregowany w tabeli przestawnej lub raportu.</span><span class="sxs-lookup"><span data-stu-id="88da6-129">This expression specifies names, columns, and measure results from hello FactInternetSales table and related tables are returned when a user double-clicks an aggregated result in a PivotTable or report.</span></span>

4. <span data-ttu-id="88da6-130">W programie Excel Usuń arkusz hello utworzony w kroku 3, a następnie kliknij dwukrotnie wartość zagregowana.</span><span class="sxs-lookup"><span data-stu-id="88da6-130">Back in Excel, delete hello sheet created in Step 3, then double-click an aggregated value.</span></span> <span data-ttu-id="88da6-131">Tym razem z właściwością wyrażenie wiersze szczegółów zdefiniowane dla miary hello, nowy arkusz zostanie otwarty zawierający przydatne znacznie więcej danych.</span><span class="sxs-lookup"><span data-stu-id="88da6-131">This time, with a Detail Rows Expression property defined for hello measure, a new sheet opens containing a lot more useful data.</span></span>

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. <span data-ttu-id="88da6-133">Wykonaj ponowne wdrożenie modelu.</span><span class="sxs-lookup"><span data-stu-id="88da6-133">Redeploy your model.</span></span>

  
## <a name="see-also"></a><span data-ttu-id="88da6-134">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="88da6-134">See Also</span></span>  
<span data-ttu-id="88da6-135">[Funkcja SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span><span class="sxs-lookup"><span data-stu-id="88da6-135">[SELECTCOLUMNS Function (DAX)](https://msdn.microsoft.com/library/mt761759.aspx) </span></span>  
[<span data-ttu-id="88da6-136">Lekcja uzupełniająca — zabezpieczenia dynamiczne</span><span class="sxs-lookup"><span data-stu-id="88da6-136">Supplemental Lesson - Dynamic security</span></span>](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[<span data-ttu-id="88da6-137">Lekcja uzupełniająca — niewyrównane hierarchie</span><span class="sxs-lookup"><span data-stu-id="88da6-137">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
