---
<span data-ttu-id="05193-101">title: aaa "lekcji samouczka usług Azure Analysis Services 13: Wdrażanie | Opis elementu Microsoft Docs": w tym artykule opisano, jak samouczek hello toodeploy projektu tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="05193-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="05193-102">usługi: documentationcenter usług analysis services: "Autor: minewiskan Menedżera: Edytor erikre:" tagów: "</span><span class="sxs-lookup"><span data-stu-id="05193-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="05193-103">MS.AssetID: ms.service: ms.devlang usług analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: ms.author 2017-07/17: owend</span><span class="sxs-lookup"><span data-stu-id="05193-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="05193-104">Lekcja 13. Wdrażanie</span><span class="sxs-lookup"><span data-stu-id="05193-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="05193-105">W tej lekcji można skonfigurować właściwości wdrożenia; Określanie tooand toodeploy nazwę modelu hello Azure Analysis Services serwera.</span><span class="sxs-lookup"><span data-stu-id="05193-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="05193-106">Następnie możesz wdrożyć hello modelu toothat wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="05193-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="05193-107">Po wdrożeniu modelu, użytkownicy mogą łączyć tooit przy użyciu raportowania aplikacji klienckiej.</span><span class="sxs-lookup"><span data-stu-id="05193-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="05193-108">toolearn więcej, zobacz [wdrażanie usług Analysis Services tooAzure](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="05193-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="05193-109">Szacowany czas toocomplete tej lekcji: **5 minut**</span><span class="sxs-lookup"><span data-stu-id="05193-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="05193-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="05193-110">Prerequisites</span></span>  
<span data-ttu-id="05193-111">Ten temat stanowi część samouczka modelowania tabelarycznego, który należy wykonać w podanej kolejności.</span><span class="sxs-lookup"><span data-stu-id="05193-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="05193-112">Przed wykonaniem zadania hello w tej lekcji, powinno mieć ukończone poprzedniej lekcji hello: [lekcji 12: analizować w programie Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="05193-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="05193-113">Musi mieć [uprawnienia administratora](../analysis-services-server-admins.md) na powitania zdalnego usług Analysis Services serwera w kolejności toodeploy tooit.</span><span class="sxs-lookup"><span data-stu-id="05193-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="05193-114">Jeśli hello AdventureWorksDW2014 przykładowa baza danych jest zainstalowana na lokalnym serwerze SQL i jest instalowany serwer usług Azure Analysis Services modelu tooan [bramy danych lokalnych](../analysis-services-gateway.md) jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="05193-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="05193-115">Wdróż hello model</span><span class="sxs-lookup"><span data-stu-id="05193-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="05193-116">Właściwości wdrożenia tooconfigure</span><span class="sxs-lookup"><span data-stu-id="05193-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="05193-117">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="05193-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="05193-118">W hello **strony właściwości sprzedaży Internet AW** okna dialogowego, w obszarze **serwera wdrażania**, w hello **serwera** właściwości, wprowadź hello całego serwera.</span><span class="sxs-lookup"><span data-stu-id="05193-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="05193-120">W hello **bazy danych** właściwości, typ **Adventure Works Internet sprzedaży**.</span><span class="sxs-lookup"><span data-stu-id="05193-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="05193-121">W hello **Nazwa modelu** właściwości, typ **Adventure Works Internet sprzedaży modelu**.</span><span class="sxs-lookup"><span data-stu-id="05193-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="05193-122">Sprawdź wybrane opcje, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="05193-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="05193-123">Witaj toodeploy sprzedaży Internet Adventure Works</span><span class="sxs-lookup"><span data-stu-id="05193-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="05193-124">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu > **kompilacji**.</span><span class="sxs-lookup"><span data-stu-id="05193-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="05193-125">Kliknij prawym przyciskiem myszy hello **sprzedaży Internet AW** projektu > **Wdróż**.</span><span class="sxs-lookup"><span data-stu-id="05193-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="05193-126">W przypadku wdrażania tooAzure Analysis Services, może być zostanie wyświetlony monit o tooenter Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="05193-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="05193-127">Wprowadź swoje konto organizacyjne i hasło, na przykład nancy@adventureworks.com. To konto musi być w Administratorzy na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="05193-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="05193-128">okno dialogowe wdrażanie Hello pojawia się i wyświetla stan wdrożenia hello hello metadanych i każdej tabeli objęte hello modelu.</span><span class="sxs-lookup"><span data-stu-id="05193-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="05193-130">Po pomyślnym zakończeniu wdrażania kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="05193-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="05193-131">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="05193-131">Conclusion</span></span>  
<span data-ttu-id="05193-132">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="05193-132">Congratulations!</span></span> <span data-ttu-id="05193-133">Tworzenie i wdrażanie pierwszego modelu tabelarycznego usług Analysis Services zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="05193-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="05193-134">W tym samouczku pomogła informacje pomocne przy zakończeniu hello najbardziej typowych zadań tworzenia modelu tabelarycznego.</span><span class="sxs-lookup"><span data-stu-id="05193-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="05193-135">Teraz, gdy jest wdrażana modelu sprzedaży Internet Adventure Works, można użyć programu SQL Server Management Studio toomanage hello modelu; Tworzenie planu tworzenia kopii zapasowych i skrypty procesu.</span><span class="sxs-lookup"><span data-stu-id="05193-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="05193-136">Użytkownicy mogą teraz również łączyć modelu toohello raportowania aplikacji klienckiej, takich jak program Microsoft Excel lub Power BI.</span><span class="sxs-lookup"><span data-stu-id="05193-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="05193-138">Co dalej?</span><span class="sxs-lookup"><span data-stu-id="05193-138">What's next?</span></span>
<span data-ttu-id="05193-139">[Łączenie z programem Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="05193-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="05193-140">[Lekcja uzupełniająca — zabezpieczenia dynamiczne](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="05193-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="05193-141">[Lekcja uzupełniająca — wiersze szczegółów](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="05193-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="05193-142">Lekcja uzupełniająca — niewyrównane hierarchie</span><span class="sxs-lookup"><span data-stu-id="05193-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
