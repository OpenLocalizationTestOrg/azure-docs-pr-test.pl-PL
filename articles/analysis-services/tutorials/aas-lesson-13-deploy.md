---
title: "Samouczek Azure Analysis Services: lekcja 13 — wdrażanie | Microsoft Docs"
description: "W tym artykule opisano, jak wdrożyć projekt samouczka do usług Azure Analysis Services."
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
ms.date: 07/17/2017
ms.author: owend
ms.openlocfilehash: 70dbf5786262f75199270aa8009e03b9b48b8559
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="dfff4-103">Lekcja 13. Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="dfff4-103">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="dfff4-104">W tej lekcji skonfigurujemy właściwości wdrożenia, określając docelowy serwer usług Azure Analysis Services dla wdrożenia oraz nazwę modelu.</span><span class="sxs-lookup"><span data-stu-id="dfff4-104">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server to deploy to and a name for the model.</span></span> <span data-ttu-id="dfff4-105">Następnie wdrożymy model dla tego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="dfff4-105">You then deploy the model to that instance.</span></span> <span data-ttu-id="dfff4-106">Po wdrożeniu modelu użytkownicy mogą łączyć się z nim przy użyciu aplikacji klienckiej do raportowania.</span><span class="sxs-lookup"><span data-stu-id="dfff4-106">After your model is deployed, users can connect to it by using a reporting client application.</span></span> <span data-ttu-id="dfff4-107">Aby dowiedzieć się więcej, zobacz artykuł [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) (Wdrażanie w usługach Azure Analysis Services).</span><span class="sxs-lookup"><span data-stu-id="dfff4-107">To learn more, see [Deploy to Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="dfff4-108">Szacowany czas trwania lekcji: **5 minut**</span><span class="sxs-lookup"><span data-stu-id="dfff4-108">Estimated time to complete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="dfff4-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dfff4-109">Prerequisites</span></span>  
<span data-ttu-id="dfff4-110">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="dfff4-110">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="dfff4-111">Przed przystąpieniem do wykonywania zadań w tej lekcji należy ukończyć lekcję poprzednią: [Lekcja 12: Analiza w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="dfff4-111">Before performing the tasks in this lesson, you should have completed the previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="dfff4-112">Wdrożenie na zdalnym serwerze usług Analysis Services wymaga [uprawnień administratora](../analysis-services-server-admins.md).</span><span class="sxs-lookup"><span data-stu-id="dfff4-112">You must have [Administrator permissions](../analysis-services-server-admins.md) on the remote Analysis Services server in-order to deploy to it.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="dfff4-113">Jeśli przykładowa baza danych AdventureWorksDW2014 została zainstalowana na lokalnym serwerze SQL i model jest wdrażany na serwerze usług Azure Analysis Services, wymagana jest [lokalna brama danych](../analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="dfff4-113">If you installed the AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model to an Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-the-model"></a><span data-ttu-id="dfff4-114">Wdrażanie modelu</span><span class="sxs-lookup"><span data-stu-id="dfff4-114">Deploy the model</span></span>  
  
#### <a name="to-configure-deployment-properties"></a><span data-ttu-id="dfff4-115">Aby skonfigurować właściwości wdrożenia</span><span class="sxs-lookup"><span data-stu-id="dfff4-115">To configure deployment properties</span></span>  

  
1.  <span data-ttu-id="dfff4-116">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy projekt **AW Internet Sales**, a następnie kliknij **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-116">In **Solution Explorer**, right-click the **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="dfff4-117">W oknie dialogowym **Strony właściwości projektu AW Internet Sales** wprowadź we właściwości **Serwer** w obszarze **Serwer wdrażania** pełną nazwę serwera.</span><span class="sxs-lookup"><span data-stu-id="dfff4-117">In the **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in the **Server** property, enter the full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="dfff4-119">We właściwości **Baza danych** wpisz **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-119">In the **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="dfff4-120">We właściwości **Nazwa modelu** wpisz **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-120">In the **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="dfff4-121">Sprawdź wybrane opcje, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-121">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a><span data-ttu-id="dfff4-122">Aby wdrożyć projekt Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="dfff4-122">To deploy the Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="dfff4-123">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy projekt **AW Internet Sales** > **Kompiluj**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-123">In **Solution Explorer**, right-click the **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="dfff4-124">Kliknij prawym przyciskiem myszy projekt **AW Internet Sales** > **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-124">Right-click the **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="dfff4-125">Podczas wdrażania usług Azure Analysis Services może zostać wyświetlona prośba o wprowadzenie konta.</span><span class="sxs-lookup"><span data-stu-id="dfff4-125">When deploying to Azure Analysis Services, you may be prompted to enter your account.</span></span> <span data-ttu-id="dfff4-126">Wprowadź swoje konto organizacyjne i hasło, na przykład nancy@adventureworks.com. To konto musi być wpisane należeć do grupy Administratorzy na serwerze.</span><span class="sxs-lookup"><span data-stu-id="dfff4-126">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on the server.</span></span>
  
    <span data-ttu-id="dfff4-127">Zostanie wyświetlone okno dialogowe Wdrażanie pokazujące stan wdrożenia metadanych i każdej tabeli zawartej w modelu.</span><span class="sxs-lookup"><span data-stu-id="dfff4-127">The Deploy dialog box appears and displays the deployment status of the metadata and each table included in the model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="dfff4-129">Po pomyślnym zakończeniu wdrażania kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="dfff4-129">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="dfff4-130">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="dfff4-130">Conclusion</span></span>  
<span data-ttu-id="dfff4-131">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="dfff4-131">Congratulations!</span></span> <span data-ttu-id="dfff4-132">Tworzenie i wdrażanie pierwszego modelu tabelarycznego usług Analysis Services zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="dfff4-132">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="dfff4-133">Ten samouczek pomógł przy wykonywaniu typowych zadań związanych z tworzeniem modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="dfff4-133">This tutorial has helped guide you through completing the most common tasks in creating a tabular model.</span></span> <span data-ttu-id="dfff4-134">Skoro model Adventure Works Internet Sales został wdrożony, można użyć programu SQL Server Management Studio do zarządzania modelem, a także utworzyć skrypty procesu i plan tworzenia kopii zapasowych.</span><span class="sxs-lookup"><span data-stu-id="dfff4-134">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio to manage the model; create process scripts and a backup plan.</span></span> <span data-ttu-id="dfff4-135">Użytkownicy mogą teraz również łączyć się z modelem, używając aplikacji klienckiej do raportowania (np. Microsoft Excel lub Power BI).</span><span class="sxs-lookup"><span data-stu-id="dfff4-135">Users can also now connect to the model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="dfff4-137">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="dfff4-137">What's next?</span></span>
<span data-ttu-id="dfff4-138">[Łączenie z programem Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="dfff4-138">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="dfff4-139">[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="dfff4-139">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="dfff4-140">[Lekcja uzupełniająca — wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="dfff4-140">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="dfff4-141">Lekcja uzupełniająca — niewyrównane hierarchie</span><span class="sxs-lookup"><span data-stu-id="dfff4-141">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
