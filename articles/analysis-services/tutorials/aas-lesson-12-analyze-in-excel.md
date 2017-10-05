---
title: "Samouczek Azure Analysis Services: lekcja 12 — analiza w programie Excel | Microsoft Docs"
description: "Opisuje sposób użycia funkcji analizy w programie Excel w projekcie samouczka usług Azure Analysis Services."
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
ms.openlocfilehash: 6f47de43ff8d94de22f8b7c12fa0707a8d7ffbbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="lesson-12-analyze-in-excel"></a><span data-ttu-id="ae1be-103">Lekcja 12. Analiza w programie Excel</span><span class="sxs-lookup"><span data-stu-id="ae1be-103">Lesson 12: Analyze in Excel</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="ae1be-104">W tej lekcji użyjesz funkcji analizy w programie Excel, aby otworzyć program Microsoft Excel, automatycznie utworzyć połączenie z obszarem roboczym modelu oraz automatycznie dodać tabelę przestawną do arkusza.</span><span class="sxs-lookup"><span data-stu-id="ae1be-104">In this lesson, you use the Analyze in Excel feature to open Microsoft Excel, automatically create a connection to the model workspace, and automatically add a PivotTable to the worksheet.</span></span> <span data-ttu-id="ae1be-105">Funkcja analizy w programie Excel to szybki i łatwy sposób na sprawdzenie wydajności projektu modelu przed jego wdrożeniem.</span><span class="sxs-lookup"><span data-stu-id="ae1be-105">The Analyze in Excel feature is meant to provide a quick and easy way to test the efficacy of your model design prior to deploying your model.</span></span> <span data-ttu-id="ae1be-106">Podczas tej lekcji nie wykonasz żadnej analizy danych.</span><span class="sxs-lookup"><span data-stu-id="ae1be-106">You do not perform any data analysis in this lesson.</span></span> <span data-ttu-id="ae1be-107">Ta lekcja ma umożliwić Tobie jako autorowi modelu zapoznanie się z narzędziami, których możesz użyć do testowania projektu modelu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-107">The purpose of this lesson is to familiarize you, the model author, with the tools you can use to test your model design.</span></span>   
  
<span data-ttu-id="ae1be-108">Aby ukończyć tę lekcję, musisz dysponować programem Excel zainstalowanym na tym samym komputerze, co program SSDT.</span><span class="sxs-lookup"><span data-stu-id="ae1be-108">To complete this lesson, Excel must be installed on the same computer as SSDT.</span></span>
  
<span data-ttu-id="ae1be-109">Szacowany czas trwania lekcji: **5 minut**</span><span class="sxs-lookup"><span data-stu-id="ae1be-109">Estimated time to complete this lesson: **Five minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ae1be-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ae1be-110">Prerequisites</span></span>  
<span data-ttu-id="ae1be-111">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="ae1be-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="ae1be-112">Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 11. Tworzenie ról](../tutorials/aas-lesson-11-create-roles.md).</span><span class="sxs-lookup"><span data-stu-id="ae1be-112">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 11: Create roles](../tutorials/aas-lesson-11-create-roles.md).</span></span>  
  
## <a name="browse-using-the-default-and-internet-sales-perspectives"></a><span data-ttu-id="ae1be-113">Przeglądanie przy użyciu perspektywy domyślnej i perspektywy sprzedaży internetowej</span><span class="sxs-lookup"><span data-stu-id="ae1be-113">Browse using the Default and Internet Sales perspectives</span></span>  
<span data-ttu-id="ae1be-114">W pierwszych zadaniach przejrzysz swój model przy użyciu zarówno perspektywy domyślnej, która zawiera wszystkie obiekty modelu, jak i utworzonej wcześniej perspektywy sprzedaży internetowej.</span><span class="sxs-lookup"><span data-stu-id="ae1be-114">In these first tasks, you browse your model by using both the default perspective, which includes all model objects, and also by using the Internet Sales perspective you earlier.</span></span> <span data-ttu-id="ae1be-115">Perspektywa sprzedaży internetowej nie zawiera obiektu tabeli Klient.</span><span class="sxs-lookup"><span data-stu-id="ae1be-115">The Internet Sales perspective excludes the Customer table object.</span></span>  
  
#### <a name="to-browse-by-using-the-default-perspective"></a><span data-ttu-id="ae1be-116">Przeglądanie przy użyciu perspektywy domyślnej</span><span class="sxs-lookup"><span data-stu-id="ae1be-116">To browse by using the Default perspective</span></span>  
  
1.  <span data-ttu-id="ae1be-117">Kliknij menu **Model** > **Analizuj w programie Excel**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-117">Click the **Model** menu > **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ae1be-118">W oknie dialogowym **Analiza w programie Excel** kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-118">In the **Analyze in Excel** dialog box, click **OK**.</span></span>  
  
    <span data-ttu-id="ae1be-119">Zostanie otwarty nowy skoroszyt w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="ae1be-119">Excel opens with a new workbook.</span></span> <span data-ttu-id="ae1be-120">Zostanie utworzone połączenie ze źródłem danych przy użyciu bieżącego konta użytkownika. Do zdefiniowania pól możliwych do wyświetlenia zostanie użyta perspektywa domyślna.</span><span class="sxs-lookup"><span data-stu-id="ae1be-120">A data source connection is created using the current user account and the Default perspective is used to define viewable fields.</span></span> <span data-ttu-id="ae1be-121">Do arkusza zostanie automatycznie dodana tabela przestawna.</span><span class="sxs-lookup"><span data-stu-id="ae1be-121">A PivotTable is automatically added to the worksheet.</span></span>  
  
3.  <span data-ttu-id="ae1be-122">W programie Excel zwróć uwagę na grupy miar **DimDate** i **FactInternetSales** wyświetlane w obszarze **Lista pól tabeli przestawnej**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-122">In Excel, in the **PivotTable Field List**, notice the **DimDate** and **FactInternetSales** measure groups appear.</span></span> <span data-ttu-id="ae1be-123">Widoczne będą także tabele **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory** i **FactInternetSales** wraz z odpowiednimi kolumnami.</span><span class="sxs-lookup"><span data-stu-id="ae1be-123">The **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, and **FactInternetSales** tables with their respective columns also appear.</span></span>  
  
4.  <span data-ttu-id="ae1be-124">Zamknij program Excel bez zapisywania skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-124">Close Excel without saving the workbook.</span></span>  
  
#### <a name="to-browse-by-using-the-internet-sales-perspective"></a><span data-ttu-id="ae1be-125">Przeglądanie przy użyciu perspektywy sprzedaży internetowej</span><span class="sxs-lookup"><span data-stu-id="ae1be-125">To browse by using the Internet Sales perspective</span></span>  
  
1.  <span data-ttu-id="ae1be-126">Kliknij menu **Model**, a następnie kliknij pozycję **Analizuj w programie Excel**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-126">Click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ae1be-127">W oknie dialogowym **Analiza w programie Excel** pozostaw pole **Bieżący użytkownik systemu Windows** zaznaczone, a następnie wybierz z listy rozwijanej **Perspektywa** pozycję **Internet Sales** (Sprzedaż internetowa) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-127">In the **Analyze in Excel** dialog box, leave **Current Windows User** selected, then in the **Perspective** drop-down listbox, select **Internet Sales**, and then click **OK**.</span></span> 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  <span data-ttu-id="ae1be-129">W programie Excel zwróć uwagę na to, że **Lista pól tabeli przestawnej** nie zawiera tabeli DimCustomer.</span><span class="sxs-lookup"><span data-stu-id="ae1be-129">In Excel, in **PivotTable Fields**, notice the DimCustomer table is excluded from the field list.</span></span>  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  <span data-ttu-id="ae1be-131">Zamknij program Excel bez zapisywania skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-131">Close Excel without saving the workbook.</span></span>  
  
## <a name="browse-by-using-roles"></a><span data-ttu-id="ae1be-132">Przeglądanie przy użyciu ról</span><span class="sxs-lookup"><span data-stu-id="ae1be-132">Browse by using roles</span></span>  
<span data-ttu-id="ae1be-133">Role są ważnym elementem każdego modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="ae1be-133">Roles are an important part of any tabular model.</span></span> <span data-ttu-id="ae1be-134">Bez co najmniej jednej roli, do której użytkownicy są dodawani jako elementy członkowskie, nie mogą oni uzyskać dostępu do danych ani analizować ich przy użyciu modelu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-134">Without at least one role to which users are added as members, users cannot access and analyze data using your model.</span></span> <span data-ttu-id="ae1be-135">Funkcja analizy w programie Excel umożliwia testowanie zdefiniowanych ról.</span><span class="sxs-lookup"><span data-stu-id="ae1be-135">The Analyze in Excel feature provides a way for you to test the roles you have defined.</span></span>  
  
#### <a name="to-browse-by-using-the-sales-manager-user-role"></a><span data-ttu-id="ae1be-136">Przeglądanie przy użyciu roli użytkownika Sales Manager</span><span class="sxs-lookup"><span data-stu-id="ae1be-136">To browse by using the Sales Manager user role</span></span>  
  
1.  <span data-ttu-id="ae1be-137">W programie SSDT kliknij menu **Model**, a następnie kliknij opcję **Analizuj w programie Excel**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-137">In SSDT, click the **Model** menu, and then click **Analyze in Excel**.</span></span>  
  
2.  <span data-ttu-id="ae1be-138">W obszarze **Określ nazwę lub rolę użytkownika, która będzie używana do nawiązywania połączenia z modelem** wybierz opcję **Rola**, a następnie z listy rozwijanej wybierz pozycję **Sales Manager** (Menedżer sprzedaży) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae1be-138">In **Specify the user name or role to use to connect to the model**, select **Role**, and then in the drop-down listbox, select **Sales Manager**, and then click **OK**.</span></span>  
  
    <span data-ttu-id="ae1be-139">Zostanie otwarty nowy skoroszyt w programie Excel.</span><span class="sxs-lookup"><span data-stu-id="ae1be-139">Excel opens with a new workbook.</span></span> <span data-ttu-id="ae1be-140">Automatycznie utworzona zostanie tabela przestawna.</span><span class="sxs-lookup"><span data-stu-id="ae1be-140">A PivotTable is automatically created.</span></span> <span data-ttu-id="ae1be-141">Lista pól tabeli przestawnej zawiera wszystkie pola danych dostępne w nowym modelu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-141">The Pivot Table Field List includes all the data fields available in your new model.</span></span>  
      
3.  <span data-ttu-id="ae1be-142">Zamknij program Excel bez zapisywania skoroszytu.</span><span class="sxs-lookup"><span data-stu-id="ae1be-142">Close Excel without saving the workbook.</span></span>  
  
## <a name="whats-next"></a><span data-ttu-id="ae1be-143">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="ae1be-143">What's next?</span></span>
<span data-ttu-id="ae1be-144">Przejdź do następnej lekcji: [Lekcja 13. Wdrażanie](../tutorials/aas-lesson-13-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ae1be-144">Go to the next lesson: [Lesson 13: Deploy](../tutorials/aas-lesson-13-deploy.md).</span></span>

  
  
  
