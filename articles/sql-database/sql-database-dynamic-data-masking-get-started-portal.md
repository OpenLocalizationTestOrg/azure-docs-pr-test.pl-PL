---
title: 'Portalu Azure: maskowania danych dynamicznych bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Sposób uruchamiania tooget z danymi dynamicznymi bazy danych SQL maskowania w hello portalu Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a><span data-ttu-id="ccad3-103">Rozpoczynanie pracy z danymi dynamicznymi bazy danych SQL maskowania z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ccad3-103">Get started with SQL Database dynamic data masking with hello Azure Portal</span></span>

<span data-ttu-id="ccad3-104">W tym temacie opisano sposób tooimplement [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md) z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ccad3-104">This topic shows you how tooimplement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with hello Azure portal.</span></span> <span data-ttu-id="ccad3-105">Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub hello [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccad3-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a><span data-ttu-id="ccad3-106">Konfigurowanie maskowania danych dynamicznych dla bazy danych przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ccad3-106">Set up dynamic data masking for your database using hello Azure Portal</span></span>
1. <span data-ttu-id="ccad3-107">Uruchom hello portalu Azure pod adresem [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ccad3-107">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ccad3-108">Przejdź bloku ustawienia toohello hello bazy danych, która zawiera hello poufne dane, które mają toomask.</span><span class="sxs-lookup"><span data-stu-id="ccad3-108">Navigate toohello settings blade of hello database that includes hello sensitive data you want toomask.</span></span>
3. <span data-ttu-id="ccad3-109">Kliknij przycisk hello **dynamicznego maskowania danych** kafelka, który uruchamia hello **dynamicznego maskowania danych** blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ccad3-109">Click hello **Dynamic Data Masking** tile which launches hello **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="ccad3-110">Alternatywnie przewiń toohello **operacji** sekcji, a następnie kliknij przycisk **dynamicznego maskowania danych**.</span><span class="sxs-lookup"><span data-stu-id="ccad3-110">Alternatively, you can scroll down toohello **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="ccad3-112">W hello **dynamicznego maskowania danych** który aparat zalecenia hello blok konfiguracji może zostać wyświetlony niektóre kolumny bazy danych ma flagę maskowania.</span><span class="sxs-lookup"><span data-stu-id="ccad3-112">In hello **Dynamic Data Masking** configuration blade you may see some database columns that hello recommendations engine has flagged for masking.</span></span> <span data-ttu-id="ccad3-113">W celu tooaccept hello zalecenia, kliknij **Dodaj maskę** do co najmniej jedną kolumnę i maski zostanie utworzony na podstawie na powitania domyślny typ dla tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="ccad3-113">In order tooaccept hello recommendations, just click **Add Mask** for one or more columns and a mask will be created based on hello default type for this column.</span></span> <span data-ttu-id="ccad3-114">Możesz zmienić hello funkcji maskowania klikając hello reguła i edytowanie hello maskowania innym formacie tooa format pole wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ccad3-114">You can change hello masking function by clicking on hello masking rule and editing hello masking field format tooa different format of your choice.</span></span> <span data-ttu-id="ccad3-115">Należy się tooclick **zapisać** toosave ustawień.</span><span class="sxs-lookup"><span data-stu-id="ccad3-115">Be sure tooclick **Save** toosave your settings.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="ccad3-117">tooadd maska dla każdej kolumny w bazie danych, u góry hello hello **dynamicznego maskowania danych** konfiguracji bloku, kliknij przycisk **Dodaj maskę** tooopen hello **Dodaj regułę maskowania** Blok konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ccad3-117">tooadd a mask for any column in your database, at hello top of hello **Dynamic Data Masking** configuration blade click **Add Mask** tooopen hello **Add Masking Rule** configuration blade</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="ccad3-119">Wybierz hello **schematu**, **tabeli** i **kolumny** toodefine Witaj wyznaczone pola, które maskowania.</span><span class="sxs-lookup"><span data-stu-id="ccad3-119">Select hello **Schema**, **Table** and **Column** toodefine hello designated field that will be masked.</span></span>
7. <span data-ttu-id="ccad3-120">Wybierz **Format maskowania pola** z listy hello kategorii maskowanie danych poufnych.</span><span class="sxs-lookup"><span data-stu-id="ccad3-120">Choose a **Masking Field Format** from hello list of sensitive data masking categories.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="ccad3-122">Kliknij przycisk **zapisać** danych hello maskowania bloku tooupdate hello zestawu reguł maskowania reguły w hello dynamiczne maskowanie zasad danych.</span><span class="sxs-lookup"><span data-stu-id="ccad3-122">Click **Save** in hello data masking rule blade tooupdate hello set of masking rules in hello dynamic data masking policy.</span></span>
9. <span data-ttu-id="ccad3-123">Użytkownicy SQL hello typu lub tożsamości usługi AAD, które powinny być wykluczeni z maskowania i mają dostęp toohello pozbawione maskowania poufnych danych.</span><span class="sxs-lookup"><span data-stu-id="ccad3-123">Type hello SQL users or AAD identities that should be excluded from masking, and have access toohello unmasked sensitive data.</span></span> <span data-ttu-id="ccad3-124">Powinno to być rozdzielana średnikami lista użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ccad3-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="ccad3-125">Należy pamiętać, że użytkownicy z uprawnieniami administratora zawsze mają oryginalnych danych zamaskowana toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="ccad3-125">Note that users with administrator privileges always have access toohello original unmasked data.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="ccad3-127">toomake tak hello warstwy aplikacji można wyświetlić danymi poufnymi w przypadku użytkowników aplikacji uprzywilejowane, Dodaj hello użytkownika SQL lub aplikacji hello tożsamości usługi AAD używa tooquery hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="ccad3-127">toomake it so hello application layer can display sensitive data for application privileged users, add hello SQL user or AAD identity hello application uses tooquery hello database.</span></span> <span data-ttu-id="ccad3-128">Zdecydowanie zaleca się, że ta lista zawiera minimalnej liczbie użytkownicy o odpowiednich uprawnieniach toominimize ujawnianie danych wrażliwych hello.</span><span class="sxs-lookup"><span data-stu-id="ccad3-128">It is highly recommended that this list contain a minimal number of privileged users toominimize exposure of hello sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="ccad3-129">Kliknij przycisk **zapisać** danych hello maskowania konfiguracji bloku toosave hello maskowania nowych lub zaktualizowanych zasad.</span><span class="sxs-lookup"><span data-stu-id="ccad3-129">Click **Save** in hello data masking configuration blade toosave hello new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="ccad3-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ccad3-130">Next steps</span></span>

* <span data-ttu-id="ccad3-131">Omówienie maskowania danych dynamicznych, zobacz [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ccad3-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="ccad3-132">Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub hello [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="ccad3-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or hello [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>
