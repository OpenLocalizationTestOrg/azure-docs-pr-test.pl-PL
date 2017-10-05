---
title: 'Portalu Azure: maskowania danych dynamicznych bazy danych SQL | Dokumentacja firmy Microsoft'
description: "Jak rozpocząć pracę z bazy danych SQL maskowania danych dynamicznych w portalu Azure"
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
ms.openlocfilehash: 15184e14d4e1e23b56126bbf9f972c1619dcba80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-the-azure-portal"></a><span data-ttu-id="f2d5c-103">Rozpoczynanie pracy z danymi dynamicznymi bazy danych SQL, maskowanie przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f2d5c-103">Get started with SQL Database dynamic data masking with the Azure Portal</span></span>

<span data-ttu-id="f2d5c-104">W tym temacie przedstawiono sposób wykonania [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md) z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-104">This topic shows you how to implement [dynamic data masking](sql-database-dynamic-data-masking-get-started.md) with the Azure portal.</span></span> <span data-ttu-id="f2d5c-105">Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d5c-105">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>


## <a name="set-up-dynamic-data-masking-for-your-database-using-the-azure-portal"></a><span data-ttu-id="f2d5c-106">Konfigurowanie maskowania danych dynamicznych dla bazy danych przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f2d5c-106">Set up dynamic data masking for your database using the Azure Portal</span></span>
1. <span data-ttu-id="f2d5c-107">Uruchamianie portalu Azure pod adresem [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2d5c-107">Launch the Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f2d5c-108">Przejdź do bloku ustawienia bazy danych, która zawiera dane poufne, które do zamaskowania.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-108">Navigate to the settings blade of the database that includes the sensitive data you want to mask.</span></span>
3. <span data-ttu-id="f2d5c-109">Kliknij przycisk **dynamicznego maskowania danych** Kafelek, co spowoduje uruchomienie **dynamicznego maskowania danych** blok konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-109">Click the **Dynamic Data Masking** tile which launches the **Dynamic Data Masking** configuration blade.</span></span>
   
   * <span data-ttu-id="f2d5c-110">Alternatywnie można przewijać w dół do **operacji** sekcji, a następnie kliknij przycisk **dynamicznego maskowania danych**.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-110">Alternatively, you can scroll down to the **Operations** section and click **Dynamic Data Masking**.</span></span>
     
     ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. <span data-ttu-id="f2d5c-112">W **dynamicznego maskowania danych** blok konfiguracji może zostać wyświetlony niektóre kolumny bazy danych, które aparat zalecenia ma flagę maskowania.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-112">In the **Dynamic Data Masking** configuration blade you may see some database columns that the recommendations engine has flagged for masking.</span></span> <span data-ttu-id="f2d5c-113">Aby zaakceptować zalecenia, kliknij **Dodaj maskę** do jednej lub kilku kolumn i maski zostanie utworzony na podstawie na domyślny typ dla tej kolumny.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-113">In order to accept the recommendations, just click **Add Mask** for one or more columns and a mask will be created based on the default type for this column.</span></span> <span data-ttu-id="f2d5c-114">Funkcji maskowania można zmienić, klikając reguła maskowania i edytowanie maskowania format pola w innym formacie wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-114">You can change the masking function by clicking on the masking rule and editing the masking field format to a different format of your choice.</span></span> <span data-ttu-id="f2d5c-115">Należy kliknąć przycisk **zapisać** Aby zapisać ustawienia.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-115">Be sure to click **Save** to save your settings.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. <span data-ttu-id="f2d5c-117">Aby dodać maski dla każdej kolumny w bazie danych, w górnej części **dynamicznego maskowania danych** konfiguracji bloku, kliknij przycisk **Dodaj maskę** otworzyć **Dodaj regułę maskowania** blok konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f2d5c-117">To add a mask for any column in your database, at the top of the **Dynamic Data Masking** configuration blade click **Add Mask** to open the **Add Masking Rule** configuration blade</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. <span data-ttu-id="f2d5c-119">Wybierz **schematu**, **tabeli** i **kolumny** do zdefiniuj wyznaczone pola, które maskowania.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-119">Select the **Schema**, **Table** and **Column** to define the designated field that will be masked.</span></span>
7. <span data-ttu-id="f2d5c-120">Wybierz **Format maskowania pola** z listy Kategorie maskowanie danych poufnych.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-120">Choose a **Masking Field Format** from the list of sensitive data masking categories.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. <span data-ttu-id="f2d5c-122">Kliknij przycisk **zapisać** danych maskowania bloku reguły, aby zaktualizować zestaw maskowania reguły w dynamiczne maskowanie zasad danych.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-122">Click **Save** in the data masking rule blade to update the set of masking rules in the dynamic data masking policy.</span></span>
9. <span data-ttu-id="f2d5c-123">Wpisz użytkowników SQL lub tożsamości usługi AAD, które powinny być wykluczeni z maskowania i mają dostęp do danych poufnych pozbawiony maskowania.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-123">Type the SQL users or AAD identities that should be excluded from masking, and have access to the unmasked sensitive data.</span></span> <span data-ttu-id="f2d5c-124">Powinno to być rozdzielana średnikami lista użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-124">This should be a semicolon-separated list of users.</span></span> <span data-ttu-id="f2d5c-125">Należy pamiętać, że użytkownicy z uprawnieniami administratora zawsze miały dostęp do oryginalnych danych pozbawiony maskowania.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-125">Note that users with administrator privileges always have access to the original unmasked data.</span></span>
   
    ![Okienko nawigacji](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > <span data-ttu-id="f2d5c-127">Aby uniemożliwić warstwy aplikacji mogą wyświetlać dane poufne dla użytkowników aplikacji uprzywilejowane, Dodaj użytkownika SQL lub tożsamości usługi AAD aplikacji nawiązywał w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-127">To make it so the application layer can display sensitive data for application privileged users, add the SQL user or AAD identity the application uses to query the database.</span></span> <span data-ttu-id="f2d5c-128">Zdecydowanie zaleca się, że ta lista zawiera minimalnej liczbie uprzywilejowani użytkownicy, aby zminimalizować narażenie poufnych danych.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-128">It is highly recommended that this list contain a minimal number of privileged users to minimize exposure of the sensitive data.</span></span>
   > 
   > 
10. <span data-ttu-id="f2d5c-129">Kliknij przycisk **zapisać** danych maskowania bloku konfiguracji, aby zapisać nowe lub zaktualizowane maskowania zasad.</span><span class="sxs-lookup"><span data-stu-id="f2d5c-129">Click **Save** in the data masking configuration blade to save the new or updated masking policy.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f2d5c-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2d5c-130">Next steps</span></span>

* <span data-ttu-id="f2d5c-131">Omówienie maskowania danych dynamicznych, zobacz [maskowania danych dynamicznych](sql-database-dynamic-data-masking-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2d5c-131">For an overview of dynamic data masking, see [dynamic data masking](sql-database-dynamic-data-masking-get-started.md).</span></span>
* <span data-ttu-id="f2d5c-132">Można też wdrożyć przy użyciu maskowania danych dynamicznych [poleceń cmdlet usługi Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx) lub [interfejsu API REST](https://msdn.microsoft.com/library/dn505719.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2d5c-132">You can also implement dynamic data masking using [Azure SQL Database cmdlets](https://msdn.microsoft.com/library/azure/mt574084.aspx) or the [REST API](https://msdn.microsoft.com/library/dn505719.aspx).</span></span>