---
title: "toocreate aaaHow biletu pomocy technicznej dla usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Jak toocreate obsługi biletu w usłudze Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a><span data-ttu-id="a6835-103">Jak toocreate obsługi biletu usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a6835-103">How toocreate a support ticket for SQL Data Warehouse</span></span>
<span data-ttu-id="a6835-104">Jeśli masz problemy z usługą SQL Data Warehouse, utwórz bilet pomocy technicznej, aby umożliwić naszemu zespołowi inżynierów udzielenie pomocy.</span><span class="sxs-lookup"><span data-stu-id="a6835-104">If you are having any issues with your SQL Data Warehouse, please create a support ticket so that our engineering team can assist you.</span></span>

> [!NOTE] 
> <span data-ttu-id="a6835-105">Począwszy od 12 20 2016-sprawdzenie kondycji zasobów hello w portalu Azure hello jest niedokładna.</span><span class="sxs-lookup"><span data-stu-id="a6835-105">As of 12/20/2016, hello resource health check in hello Azure portal is not accurate.</span></span> <span data-ttu-id="a6835-106">Obecnie pracujemy toofix ten problem.</span><span class="sxs-lookup"><span data-stu-id="a6835-106">We are actively working toofix this issue.</span></span> 


## <a name="create-a-support-ticket"></a><span data-ttu-id="a6835-107">Tworzenie biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a6835-107">Create a support ticket</span></span>
1. <span data-ttu-id="a6835-108">Otwórz hello [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a6835-108">Open hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a6835-109">Na ekranie głównej powitania kliknij hello **Pomoc i obsługa techniczna** kafelka.</span><span class="sxs-lookup"><span data-stu-id="a6835-109">On hello Home screen, click hello **Help + support** tile.</span></span>
   
    ![Pomoc i obsługa techniczna](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. <span data-ttu-id="a6835-111">Na hello pomoc + Obsługa bloku, kliknij przycisk **Utwórz żądanie obsługi**.</span><span class="sxs-lookup"><span data-stu-id="a6835-111">On hello Help + Support blade, click **Create support request**.</span></span>
   
    ![Nowe żądanie pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. <span data-ttu-id="a6835-113">Wybierz hello **żądania typu**.</span><span class="sxs-lookup"><span data-stu-id="a6835-113">Select hello **Request Type**.</span></span>
   
    ![Typ żądania](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > <span data-ttu-id="a6835-115">Domyślnie każdy serwer SQL (np. myserver.database.windows.net) ma **limit przydziału jednostek DTU** wynoszący 45 000.</span><span class="sxs-lookup"><span data-stu-id="a6835-115">By default, each SQL server (e.g. myserver.database.windows.net) has a **DTU Quota** of 45,000.</span></span> <span data-ttu-id="a6835-116">Ten limit przydziału jest po prostu limitem bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="a6835-116">This quota is simply a safety limit.</span></span> <span data-ttu-id="a6835-117">Tworzenie biletu pomocy technicznej i wybierając można zwiększyć limitu przydziału *przydziału* jako typ żądania hello.</span><span class="sxs-lookup"><span data-stu-id="a6835-117">You can increase your quota by creating a support ticket and selecting *Quota* as hello request type.</span></span> <span data-ttu-id="a6835-118">toocalculate Twojego jednostek dtu w warstwie musi należy pomnożyć hello 7.5 przez hello całkowita [DWU] [ DWU] potrzebne.</span><span class="sxs-lookup"><span data-stu-id="a6835-118">toocalculate your DTU needs, multiply hello 7.5 by hello total [DWU][DWU] needed.</span></span> <span data-ttu-id="a6835-119">Na przykład chcesz toohost dwa DW6000s na jeden serwer SQL server, możesz zażądać limit przydziału jednostek DTU z 90,000.</span><span class="sxs-lookup"><span data-stu-id="a6835-119">For example, you would like toohost two DW6000s on one SQL server, then you should request a DTU quota of 90,000.</span></span>  <span data-ttu-id="a6835-120">Twoje bieżące użycie jednostek DTU z bloku serwera SQL hello można wyświetlić w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="a6835-120">You can view your current DTU consumption from hello SQL server blade in hello portal.</span></span> <span data-ttu-id="a6835-121">Zarówno wstrzymana i cofanie wstrzymania bazy danych są wliczane do limitu przydziału jednostek dtu w warstwie hello.</span><span class="sxs-lookup"><span data-stu-id="a6835-121">Both paused and un-paused databases count toward hello DTU quota.</span></span> 
   > 
   > 
5. <span data-ttu-id="a6835-122">Wybierz hello **subskrypcji** czy hosty hello bazy danych z problemem hello są raportowania.</span><span class="sxs-lookup"><span data-stu-id="a6835-122">Select hello **Subscription** that hosts hello database with hello problem you are reporting.</span></span>
   
    ![Subskrypcja](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. <span data-ttu-id="a6835-124">Wybierz **SQL Data Warehouse** jako hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="a6835-124">Select **SQL Data Warehouse** as hello Resource.</span></span>
   
    ![Zasób](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. <span data-ttu-id="a6835-126">Wybierz odpowiedni [Plan pomocy technicznej platformy Azure][Azure support plan].</span><span class="sxs-lookup"><span data-stu-id="a6835-126">Select your [Azure support plan][Azure support plan].</span></span>
   
   * <span data-ttu-id="a6835-127">Pomoc techniczna związana z **rozliczeniami, limitami przydziałów i zarządzaniem subskrypcjami** jest dostępna na wszystkich poziomach pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a6835-127">**Billing, quota and subscription management** support is available at all support levels.</span></span>
   * <span data-ttu-id="a6835-128">**Naprawa w razie awarii** jest oferowana w ramach pomocy technicznej na poziomach [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] i [Premium][Premier].</span><span class="sxs-lookup"><span data-stu-id="a6835-128">**Break-fix** support is provided through [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] or [Premier][Premier] support.</span></span> <span data-ttu-id="a6835-129">Naprawa w razie awarii problemów są problemów napotykanych przez klientów podczas korzystania z usługi Azure w przypadku, gdy istnieje uzasadniona możliwość hello Microsoft spowodował problem.</span><span class="sxs-lookup"><span data-stu-id="a6835-129">Break-fix issues are problems experienced by customers while using Azure where there is a reasonable expectation that Microsoft caused hello problem.</span></span>
   * <span data-ttu-id="a6835-130">**Wsparcie dla deweloperów** i **usługi doradcze** są dostępne pod adresem hello [Professional Direct] [ Professional Direct] i [Premier] [ Premier] poziomach pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="a6835-130">**Developer mentoring** and **advisory services** are available at hello [Professional Direct][Professional Direct] and [Premier][Premier] support levels.</span></span> 
     
     <span data-ttu-id="a6835-131">Jeśli masz plan pomocy technicznej Premium, możesz zgłaszać także usługi SQL Data Warehouse problemy na powitania związane z [Microsoft Premier online portalu][Microsoft Premier online portal].</span><span class="sxs-lookup"><span data-stu-id="a6835-131">If you have a Premier support plan, you can also report SQL Data Warehouse related issues on hello [Microsoft Premier online portal][Microsoft Premier online portal].</span></span>  <span data-ttu-id="a6835-132">Zobacz [plany pomocy technicznej platformy Azure] [ Azure support plan] toolearn więcej informacji na temat hello obsługuje różne plany, ich zakresach, czasach reakcji, cenach, itp.  Często zadawane pytania na temat pomocy technicznej platformy Azure można znaleźć w temacie [Pomoc techniczna platformy Azure — często zadawane pytania][Azure support FAQs].</span><span class="sxs-lookup"><span data-stu-id="a6835-132">See [Azure support plans][Azure support plan] toolearn more about hello various support plans, including scope, response times, pricing, etc.  For frequently asked questions about Azure support, see [Azure support FAQs][Azure support FAQs].</span></span>  
     
     ![Plan pomocy technicznej](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. <span data-ttu-id="a6835-134">Wybierz hello **typ problemu** i **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="a6835-134">Select hello **Problem Type** and **Category**.</span></span> <span data-ttu-id="a6835-135">W tym przykładzie Wybraliśmy "Narzędzia" jako hello typ problemu i "klient" hello kategorii.</span><span class="sxs-lookup"><span data-stu-id="a6835-135">In this example, we have chosen "Tools" as hello Problem type and "Client tools" as hello category.</span></span> 
   
    ![Typ problemu i kategoria](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. <span data-ttu-id="a6835-137">Opisz hello problem i wybierz poziom hello wpływ na prowadzoną działalność.</span><span class="sxs-lookup"><span data-stu-id="a6835-137">Describe hello problem and choose hello level of business impact.</span></span>
   
    ![Opis problemu](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. <span data-ttu-id="a6835-139">Twoje **informacje kontaktowe** dotyczące tego biletu pomocy technicznej zostaną wstępnie wypełnione.</span><span class="sxs-lookup"><span data-stu-id="a6835-139">Your **contact information** for this support ticket will be pre-filled.</span></span> <span data-ttu-id="a6835-140">Zaktualizuj je w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="a6835-140">Update this if necessary.</span></span>
    
    ![Informacje kontaktowe](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. <span data-ttu-id="a6835-142">Kliknij przycisk **Utwórz** toosubmit hello obsługi żądania.</span><span class="sxs-lookup"><span data-stu-id="a6835-142">Click **Create** toosubmit hello support request.</span></span>

## <a name="monitor-a-support-ticket"></a><span data-ttu-id="a6835-143">Monitorowanie biletu pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="a6835-143">Monitor a support ticket</span></span>
<span data-ttu-id="a6835-144">Gdy prześlesz żądanie pomocy technicznej hello hello zespołu pomocy technicznej platformy Azure skontaktuje się z Tobą.</span><span class="sxs-lookup"><span data-stu-id="a6835-144">After you have submitted hello support request, hello Azure support team will contact you.</span></span> <span data-ttu-id="a6835-145">toocheck stan żądania i uzyskać więcej informacji, kliknij przycisk **Zarządzaj żądaniami obsługi** na powitania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a6835-145">toocheck your request status and details, click **Manage support requests** on hello dashboard.</span></span>

![Sprawdzanie stanu](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a><span data-ttu-id="a6835-147">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="a6835-147">Other Resources</span></span>
<span data-ttu-id="a6835-148">Ponadto można połączyć z hello społeczności SQL Data Warehouse w [przepełnienie stosu] [ Stack Overflow] lub na powitania [forum MSDN magazynu danych SQL Azure] [ Azure SQL Data Warehouse MSDN forum].</span><span class="sxs-lookup"><span data-stu-id="a6835-148">Additionally, you can connect with hello SQL Data Warehouse community on [Stack Overflow][Stack Overflow] or on hello [Azure SQL Data Warehouse MSDN forum][Azure SQL Data Warehouse MSDN forum].</span></span>

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

